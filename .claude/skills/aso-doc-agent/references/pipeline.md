---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 0%

---
# Agente de Doc ASO — Pipeline

Referenciado de `SKILL.md`. Essa é a fonte da verdade para a ordem de execução; SKILL.md é
o resumo. Leia `config.yml` antes de começar — cada valor em `{braces}` abaixo é um
chave de configuração.

**Tratamento de erros (aplica-se a todas as etapas abaixo).** Uma chamada de ferramenta/API que causa erros (autenticação
falha, tempo limite, consulta malformada, esquema inesperado) nunca é a mesma coisa que um
um resultado vazio legítimo e nunca podem cair silenciosamente numa situação de
ramificação &quot;empty&quot; ou &quot;anything to do&quot; (por exemplo, etapa 1.2, &quot;Nothing to do here&quot;, etapa 3.3)
&quot;pendências épicas totalmente cobertas ou todas em andamento&quot;). Quando ocorrer um erro de chamada, pare e registre a
erro real no resumo da execução em vez de continuar como se tivesse retornado corretamente.

## Etapa 0 - Comprovação

1. `pwd` e check `guidelines.md` + `.claude/skills/aso-doc-agent/config.yml` ambos existem. Caso contrário, pare — diretório errado.
2. `gh auth status` — confirme se a conta `sandsinh_adobe` tem um token válido neste host. **Nunca executar`gh auth switch`** — ele inverte a conta `gh` ativa em todo o computador como um efeito colateral, que pode silenciosamente reter qualquer outro terminal/processo neste computador na conta errada para uma execução diária autônoma. Em vez disso, faça essa execução apenas: `export GH_TOKEN=$(gh auth token --user sandsinh_adobe)` uma vez no início, portanto, cada chamada `gh` abaixo usa esse token por meio da variável env `GH_TOKEN`, independentemente de qual conta esteja ativa globalmente.
3. `mkdir -p {state_dir}` se ausente.
4. Leia `{state_dir}/run-state.json` se ele existir (ou trate como `{"runs_completed": 0, "tracked_prs": []}`). `tracked_prs` é a lista própria deste agente de `{number, headRefName, key}` para PRs que ele abriu — usada apenas para detectar uma PR que fechou sem mesclagem (Etapa 1.5), já que `gh pr list --state open` sozinha não pode vê-la depois que ela se foi. O tempo de solicitação de mídia vive em um arquivo separado, `{state_dir}/media-requests.json` (Etapa 5) — GitHub e Jira permanecem como fonte de verdade para todo o resto (status da PR, status do tíquete).
5. `--ticket KEY` presente -> ignore a escolha automática da Etapa 3, use KEY diretamente (ainda executa as Etapas 4-7). Caso contrário, escolha automática na Etapa 3.

## Etapa 1 — reconciliar execuções anteriores

Execute isso sempre, mesmo em uma execução fechada ou vazia.

1. `gh pr list --repo {github.repo} --label {github.pr_label} --state open --json number,url,isDraft,headRefName,title,reviewDecision`
2. **Verificação de revisão — a cada PR aberta, a cada execução** (`pr.check_reviews_every_run`):
   - `gh pr view <number> --repo {github.repo} --json reviewDecision,reviews,comments`
   - `reviewDecision == "APPROVED"` -> mesclar agora: `gh pr merge <number> --repo {github.repo} --merge`. Verifique a mesclagem realmente realizada (`gh pr view <number> --json state,mergedAt` — `state == "MERGED"`) antes de tratá-la como concluída; uma rejeição de ramificação protegida ou uma verificação necessária ainda pendente pode deixar a PR aberta mesmo depois que `gh pr merge` é chamado e isso deve ser registrado como uma falha, não relatado ao Jira como mesclado (essa é uma mesclagem normal aprovada por humanos, não baseada em tempo limite). Ao confirmar a mesclagem: comente no tíquete Jira vinculado que foi mesclado, remova a PR de `tracked_prs`.
   - `reviewDecision == "CHANGES_REQUESTED"` -> **não** corrija automaticamente a PR nesta versão. Leia os comentários de revisão (`gh api repos/{github.repo}/pulls/<number>/comments` para comentários incorporados, além do corpo de revisão de nível superior no campo `reviews`) e execute **Aprender com os comentários** abaixo. Registre a PR como aguardando ação do autor no resumo de execução. Se esta PR tiver sido `CHANGES_REQUESTED` por mais de `pr.stale_after_hours` sem atualização, sinalize-a como obsoleta para a porta de cap Etapa 2 — ela permanece aberta para um humano, mas não ocupa mais um slot de cap.
   - Qualquer outra coisa (nenhuma revisão ainda, `REVIEW_REQUIRED` sem nenhuma revisão enviada) -> nada a fazer aqui.
3. **Aprenda com os comentários.** Para cada comentário ou corpo de revisão lido como uma observação *generalizável* sobre tom, estrutura ou conteúdo — não uma correção pontual específica para essa PR (compare &quot;sempre mencione a guia Ignorado para oportunidades com suporte para ignorar&quot; vs. &quot;erro de digitação na linha 12&quot;) — anexe uma entrada datada e vinculada a tíquete a `references/review-learnings.md`. Ignore o feedback puramente mecânico (erros de digitação, links quebrados, fiapos): corrija aqueles na própria PR; eles não precisam de uma lição durável. O formato de entrada exato está documentado nesse arquivo.
4. Para cada PR de **rascunho** nessa lista, extraia a chave Jira do nome da ramificação (`{github.branch_prefix}<KEY>-...`).
   - `mcp__Corp-Jira__list_attachments` + `mcp__Corp-Jira__get_jira_comments` nessa chave.
   - Procure por: um novo anexo de imagem correspondente à captura solicitada, OU um comentário contendo uma URL `video.tv.adobe.com`.
   - Se encontrada: `git fetch`/`checkout` a ramificação, adicione a imagem a `help/**/assets/` (se for um anexo de imagem, baixe via `download_attachment`) ou preencha o espaço reservado `>[!VIDEO](...)` (se for um comentário de URL de vídeo), valide em relação a `experience-league-markdown`, confirme, envie, `gh pr ready <number>`, comente na PR &quot;Mídia adicionada — pronta para revisão.&quot;, atualize a entrada `{state_dir}/media-requests.json` para `resolved`.
   - Se não for encontrado: verifique o tempo decorrido desde a solicitação em `{state_dir}/media-requests.json`. Aplique a lógica de escalonamento/desistência da Etapa 5 aqui também (um rascunho de PR deixado aberto nas execuções ainda precisa que sua mídia seja perseguida) — incluindo a chamada `gh pr ready` do caminho de desistência, portanto, um rascunho desistente ainda se torna revisável em vez de ficar preso.
5. **Detectar PRs fechadas sem mesclagem.** Comparar a lista de relações públicas desta execução (etapa 1) com `tracked_prs` de `run-state.json`. Qualquer PR rastreada ausente na lista aberta e não confirmada mesclada na etapa 2 foi fechada sem mesclagem — antes de descartá-la, obtenha seu estado final (`gh pr view <number> --repo {github.repo} --json reviews,comments`) e execute **Aprenda com os comentários** sobre ela uma última vez, portanto, o raciocínio de rejeição de um humano não será perdido. Em seguida, solte-o do rastreamento. Nenhuma ação adicional é necessária no próprio ticket: como o rótulo da declaração é aplicado somente no momento da publicação (Etapa 6.10), um ticket fechado não mesclado já não tem rótulo e as verificações da Etapa 3.2 (sem PR aberta/mesclada) o tornam naturalmente qualificado para ser escolhido novamente em uma execução futura.
6. Defina `tracked_prs` em `run-state.json` para a lista de PRs abertas atual (`number`, `headRefName` e a chave Jira analisada a partir do nome da ramificação), para que a próxima etapa 5 da execução seja diferente.

## Etapa 2 — Tampa da PR

1. Contar PRs abertas da saída `gh pr list` da Etapa 1, excluindo qualquer PR sinalizada na Etapa 1.2 como obsoleta-`CHANGES_REQUESTED` (aberta por mais de `pr.stale_after_hours` sem atualização) — elas permanecem abertas para um humano, mas não ocupam mais um slot de limite.
2. Se count >= `{pr.max_open}` (3): log `"cap reached ({count}/{pr.max_open} open) — skipping new ticket this run"`, vá para a Etapa 7.
3. Continue com a Etapa 3.

## Etapa 3 — Escolher um tíquete

Ignorar totalmente se `--ticket KEY` foi passado (use KEY).

```
JQL: "Epic Link" = {jira.epic} AND status = "{jira.open_status}"
     ORDER BY priority DESC, created ASC
```

1. Executar a pesquisa (`mcp__Corp-Jira__search_jira_issues`, `minimizeOutput: true`, campos limitados a `key,summary,priority,status,labels`).
2. Ande os resultados em ordem. Ignorar qualquer tíquete que:
   - já tem o rótulo `{jira.picked_label}`, OU
   - já tem uma ramificação existente `{github.branch_prefix}<KEY>-*` no local remoto (`git ls-remote --heads origin '{github.branch_prefix}<KEY>-*'`), OU
   - O já tem uma PR aberta ou mesclada (verificação cruzada na lista da Etapa 1 / `gh pr list --state all --search <KEY>`).
3. O primeiro ticket que passa em todas as três verificações é o pick. Se nenhum passar **porque a pesquisa realmente retornou zero tíquete qualificado**, registre `"epic backlog fully covered or all in flight"` e vá para a Etapa 7. Se a pesquisa em si falhar (erro de autenticação, tempo limite, JQL malformado), esse não é o caso — registre o erro real (consulte Tratamento de erros acima).
4. Rotule o tíquete **não** ainda — o rótulo da declaração é aplicado na Etapa 6.10, somente depois que uma ramificação e PR realmente existirem. As etapas 4 a 5 (pesquisa/rascunho/mídia) podem falhar ou travar sem deixar qualquer rastro no ticket; os únicos sinais em andamento antes da Etapa 6 são as verificações de existência de ramificação/existência de PR acima, o que é suficiente, dado que isso é executado a partir de uma única máquina sem simultaneidade real para proteção contra.

## Etapa 4 — Investigação + projeto

A pesquisa vem primeiro e tem **várias fontes** — nunca rascunho de uma única entrada (o Jira
apenas o tíquete ou apenas a leitura de documentos semelhantes). Todas as fontes abaixo confirmam ou
corrige os outros; contradições são resolvidas confiando no código fonte > documentos Wiki/PR >
Discussão do Slack > a inferência do próprio autor do documento, nessa ordem, e ser sinalizado em linha
como `<!-- CONFIRM -->` quando não puderem ser resolvidos.

0. **Lições de revisão acumuladas.** Leia `references/review-learnings.md` primeiro. Aplique qualquer coisa nele que seja relevante para o tópico deste tíquete antes do rascunho — é assim que o feedback de revisões de PR anteriores melhora rascunhos futuros em vez de repetir a mesma correção.

### Pesquisa (faça tudo o que for aplicável — não pule direto para a redação)

1. **código Source (verdade fundamental sobre como realmente funciona).** Pesquise no repositório de interface primária (`research.code_repos` em config.yml) o adaptador/manipulador do recurso (`*OpportunityAdapter.tsx`, `*SuggestionAdapter.tsx`), seu gancho de dados (`use*Data.ts`) e suas cadeias de caracteres de título/descrição `.l10n.ts`/`.I10n.ts`. Essa é a autoridade para nomes de campo, forma de dados, categoria e cópia exata do produto — prefira-a a qualquer outra coisa quando as fontes discordarem.
2. **Wiki (intenção de design, especificações, decisões).** `mcp__Adobe-Wiki__search_wiki_content` com o nome do recurso/oportunidade e a chave épica/de tíquete. Leia as páginas correspondentes (`get_wiki_content`) para: por que o recurso existe, terminologia que a equipe de produtos usa, qualquer fluxo de UX documentado ou casos de borda e qualquer captura de tela incorporada que estabeleça a aparência real da interface do usuário (informa a especificação de captura de mídia na etapa 5; não substitui uma captura de tela nova real, a menos que a página esteja atual).
3. **Slack (como a equipe realmente fala sobre isso, perguntas abertas, alterações recentes).** `mcp__Slack__slack_search_messages` com o nome do recurso/oportunidade e a chave do tíquete, irrestrito pelo canal, a menos que `research.slack_channels` o restrinja em config.yml. Procure por: mensagens de anúncio (geralmente tem o enquadramento limpo voltado para o cliente), threads de discussão de design e qualquer coisa que indique o recurso alterado recentemente de uma maneira que documentos irmãos ou comentários de código ainda não refletiriam.
4. **Histórico de PR do GitHub (lógica de implementação, capturas de tela, discussão de revisão).** `gh search prs --repo <repo> "<feature name>"` ou `gh pr list --repo <repo> --search "<ticket key OR feature name>" --state all` através de `research.code_repos`. Leia descrições de PR mescladas para obter lógica, documentos de design vinculados e capturas de tela que esclarecem o comportamento que o código por si só não explica (por exemplo, por que um tipo de correção é restrito, como um caso de borda é na interface do usuário).
5. **Análogos de tons.** Com base no resumo do tíquete, localize de 2 a 3 páginas existentes mais próximas:
   - &quot;... tíquetes de &quot;como fazer&quot; da oportunidade -> leia dois arquivos semelhantes no `help/documentation/opportunities/` (o local real de &quot;como fazer&quot; por oportunidade — `help/opportunity-types/*.md` são as páginas de aterrissagem da categoria com grades de cartão vinculadas a elas, não o conteúdo de &quot;como fazer&quot; em si).
   - Configurações/fluxo de trabalho/tíquetes de conexão -> leia 1-2 arquivos irmãos em `help/documentation/` (verifique `setup/`, `opportunities/`, `settings.md`, `basics.md` para obter a correspondência mais próxima).
     Estrutura do cabeçalho do espelho, uso da caixa de notas, comprimento da frase, nível de detalhes técnicos.
6. **Regras de formato.** Leia novamente a Referência rápida da habilidade `experience-league-markdown` antes de escrever. Cada cabeçalho/nota/imagem/link deve corresponder exatamente à sua sintaxe.

### Rascunho

7. **Decisão de arquivo de destino.** Prefira estender a seção relevante de uma página existente a criar um novo arquivo, A MENOS QUE o tíquete corresponda à granularidade das páginas independentes existentes (por exemplo, cada oportunidade recebe seu próprio arquivo em `help/documentation/opportunities/` — uma nova oportunidade segue a estrutura exata de um irmão existente). Ao estender uma página existente, toque somente em uma seção para esse ticket — não edite seções não relacionadas, mesmo que pareçam desatualizadas. Se for uma nova página autônoma, adicione também seu cartão à página de aterrissagem `help/opportunity-types/*.md` relevante (lista de comentários de origem + bloco HTML gerado, correspondendo ao padrão exato dos cartões existentes) e registre-o em `help/main-toc/TOC.md`.
8. **Rascunho v1.** Grave o conteúdo agora (em memória/scratch, ainda não no arquivo do repositório — isso acontece na Etapa 6 após a decisão de mídia, de modo que um documento com mídia pendente e um documento resolvido passam pelo mesmo caminho de gravação). Sintetize todas as etapas de 1 a 6 — não reitere apenas a descrição do tíquete Jira.
9. **Iterar.** Reler o rascunho da v1 contra cada descoberta de pesquisa das etapas 1-4: o rascunho perdeu algo que o Slack ou o Wiki descobriram? Isso contradiz o que o código-fonte realmente faz? Corresponde ao tom irmão o mais próximo possível? Revise antes de seguir em frente — isso é uma segunda passagem real, não uma formalidade. Qualquer coisa realmente não confirmada após essa aprovação (não encontrada em nenhuma das quatro fontes) recebe um comentário incorporado `<!-- CONFIRM -->` em vez de uma suposição.
10. **Decisão de mídia.** Decida `mediaNeeded: true|false`.
    - `true` se o recurso for um fluxo de trabalho de interface de usuário de várias etapas, no qual uma descrição textual sozinha seria materialmente mais difícil de seguir (corresponde à expressão &quot;usada criteriosamente... quando uma descrição textual é insuficiente&quot; de `guidelines.md`).
    - Se `true`, produzir: `mediaType` (`screenshot` ou `video`), `captureSteps` (etapas exatas para reproduzir o estado a ser capturado), `urls` (URL(s) de aplicativo voltado para o cliente e/ou URL(s) de página interna necessárias para alcançar esse estado — obter URLs reais da descrição/comentários do tíquete Jira, Wiki ou convenções de `open-aso-devmode-url`, se referenciadas lá; nunca criar uma URL).
    - Se `false`, ignore a Etapa 5 para este tíquete.

## Etapa 5 — Portão de mídia

Somente é executado quando a Etapa 4 define `mediaNeeded: true`. Todos os carimbos de data e hora em
`{state_dir}/media-requests.json` são UTC ISO-8601 (`date -u +%Y-%m-%dT%H:%M:%SZ`) —
sempre escreva e compare neste formato para que a matemática do tempo decorrido abaixo seja inequívoca
entre execuções.

1. Verifique `{state_dir}/media-requests.json` se há uma entrada existente para esta chave de tíquete. Se não houver, será uma nova solicitação.
2. **Nova solicitação:**
   - `mcp__Slack__slack_lookup_user` em `media.contacts_in_order[0].email` (sandinh) para obter a ID de usuário do Slack.
   - `mcp__Slack__slack_send_dm` com uma mensagem contendo: a chave + link do tíquete Jira, exatamente o que capturar (`captureSteps`), os URL(s) a serem usados e onde a resposta deve ir (&quot;responder no tíquete Jira — anexar a captura de tela diretamente ou, para vídeo, carregar por meio do formulário de vídeo normal do Experience League e colar o link `video.tv.adobe.com` resultante como comentário&quot;).
   - Gravar `{state_dir}/media-requests.json[KEY] = {requestedTo: "sandsinh", requestedAt: <UTC ISO-8601 now>, escalated: false}`.
3. **Solicitação existente:** ambos os limites abaixo são medidos a partir do `requestedAt` original — o escalonamento não redefine o relógio:
   - `now - requestedAt` &lt; `media.escalate_after_hours` -> não fazer nada nessa execução, prosseguir para a publicação com mídia ainda pendente (rascunho de PR).
   - `now - requestedAt` >= `media.escalate_after_hours` e ainda não escalonado -> DM `media.contacts_in_order[1]` (kanishka), a sandinh das anotações da mensagem já foi solicitada há N horas sem resposta. Atualizar entrada: `escalated: true, escalatedAt: <UTC ISO-8601 now>`.
   - `now - requestedAt` >= `media.give_up_after_hours` (independentemente do estado de escalonamento) -> defina `mediaNeeded: false` para fins de publicação, insira uma nota no rascunho: `>[!TIP]\n>\n>A screenshot for this step is being added in a follow-up update.` Se uma PR já existir para este tíquete e ainda for um rascunho (alcançado aqui pela Etapa 1.4, não uma nova Etapa 6 de publicação), `git fetch`/faça check-out da ramificação, aplique a nota, confirme, envie por push e chame `gh pr ready <number>` — um rascunho fornecido ainda deve se tornar revisável, não permanecer preso indefinidamente. Marcar entrada `gaveUp: true`.

## Etapa 6 — Publicação

Ignorar se o tíquete foi totalmente ignorado na Etapa 3 (nada para publicar).

1. `git fetch origin` e `git checkout -B {github.branch_prefix}<KEY>-<short-slug> origin/main` — `-B` (não `-b`), portanto, uma ramificação local restante de uma execução anterior com falha é redefinida em vez de bloquear o check-out; ramificação diretamente de `origin/main` também descarta qualquer estado local sujo de uma falha anterior em vez de falhar nela.
2. Grave o rascunho da Etapa 4 no arquivo de destino decidido na Etapa 4.3. Verifique novamente a lista de verificação &quot;Antes de confirmar as alterações do Markdown&quot; de `experience-league-markdown` linha por linha.
3. Se uma linha de marcação estiver configurada (`markdownlint_custom.json` na raiz do repositório) e `markdownlint-cli`/`npx markdownlint` estiver disponível, execute-a com os arquivos alterados e corrija as violações antes de confirmar.
4. Confirmação: `docs(aso): <ticket summary, lowercase, no trailing period>\n\nSITES-XXXXX`.
5. `git push -u origin <branch>`.
6. Seleção do revisor: `gh pr list --repo {github.repo} --label {github.pr_label} --state open --json reviewRequests` — conte quantos revisores estão atualmente listados; atribua o que tiver menos (vínculo -> `sandsinh_adobe`).
7. Corpo da PR:

   ```
   ## Summary
   [1-2 sentence description of the feature now documented]
   
   ## Source
   Closes documentation gap tracked in [SITES-XXXXX](https://jira.corp.adobe.com/browse/SITES-XXXXX)
   
   ## Media
   [either "No media needed for this update." OR "Screenshot/video requested from {contact} on {date} — PR opened as draft until resolved." OR "Media follow-up pending — shipped without it; see inline note."]
   
   > 🤖 Drafted by aso-doc-agent
   ```
8. `gh pr create --repo {github.repo} --title "<ticket summary>" --body "<above>" --label {github.pr_label} --reviewer <chosen-github-handle> --draft` se a mídia ainda estiver pendente, caso contrário, omita `--draft`.
9. `gh pr edit <number> --add-label {github.pr_label}` se o sinalizador de rótulo não foi usado (correia e suspensórios, corresponde ao padrão usado em outro lugar nas ferramentas desta organização).
10. Jira: `add_jira_comment` vinculando a URL da PR, e agora — pela primeira vez nesta execução — adicione `{jira.picked_label}` (`update_jira_issue`, mesclar com rótulos existentes). Essa é a afirmação, deliberadamente aplicada apenas quando uma filial e PR existem: uma falha em qualquer lugar nas Etapas 3-5 deixa o bilhete completamente sem rótulo e seguramente selecionável novamente, em vez de permanentemente preso. Não fazer transição do status do tíquete — deixe isso para a triagem da própria equipe de documentos; `{jira.picked_label}` é o único sinal de status que este agente grava.

## Etapa 7 — Resumo da execução

1. Atualização `{state_dir}/run-state.json`: `runs_completed += 1`, carimbo de data/hora, tíquete escolhido (ou &quot;nenhum&quot; + motivo), PR aberta/atualizada (ou &quot;nenhum&quot; + motivo), status de limite.
2. Imprima um resumo curto em formato legível por humanos (tíquete, ação tomada, link de RP, status da mídia).
