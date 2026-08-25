---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---
# Agente de Doc ASO — Uso

O que é isso, como funciona e o que fazer quando precisa de você.

## O que faz

Todos os dias, esse agente escolhe o único recurso ASO não documentado de maior prioridade de
[SITES-49539](https://jira.corp.adobe.com/browse/SITES-49539) lista de pendências (39 tíquetes, por exemplo,
&quot;Como fazer oportunidade canônica&quot;, &quot;notificações do Slack&quot;), escreve uma parte da documentação
no estilo da casa deste repositório, e abre uma PR — atribuindo qualquer uma das duas
os revisores configurados (`sandsinh_adobe` / `kanishka_adobe`) atualmente têm menos aberturas
revisar solicitações deste agente. Se o recurso precisar de uma captura de tela ou vídeo, ele solicitará
um sobre o Slack antes de terminar a PR.

Cada execução também verifica o status de revisão em cada PR aberta: as PRs aprovadas são mescladas
imediatamente, e o feedback solicitado por alterações é lido e, quando é generalizável
lição (não um erro de digitação único), registrada para que os rascunhos futuros não repitam o mesmo erro.

Uma execução = um recurso = no máximo uma PR. Ele nunca toca em mais de um tíquete por execução,
e nunca abre mais de 3 PRs de uma só vez (aguarda que as existentes sejam mescladas/fechadas primeiro).

## Onde tudo vive

| O que | Caminho |
|---|---|
| Como ele decide o que fazer | `.claude/skills/aso-doc-agent/SKILL.md` |
| O passo a passo exato | `.claude/skills/aso-doc-agent/references/pipeline.md` |
| Configurações específicas da equipe (edite para alterar revisores, limite, tempo de escalonamento) | `.claude/skills/aso-doc-agent/config.yml` |
| Lições aprendidas com o feedback de revisão da PR (rastreado no Git, lido antes de cada rascunho) | `.claude/skills/aso-doc-agent/references/review-learnings.md` |
| Estado de execução local (gitigado — seguro para excluir, ele será reconstruído) | `.claude/skills/aso-doc-agent/state/` |
| Instalador de agendamento diário | `.claude/scripts/aso-doc-agent-setup.sh` |
| Incluo na lista de permissões de permissões para execuções headless | `.claude/settings.local.json` (gestionado, máquina-local) |

## Executando

- **Manualmente, em uma sessão normal:** `/aso-doc-agent` (ou `/aso-doc-agent --ticket SITES-XXXXX`)
- **Headless, one-off:** `claude -p "/aso-doc-agent"` da raiz do repositório
- **Diariamente, sem supervisão:** já instalado via `launchctl` (veja abaixo) — é executado às 07:53 hora local todos os dias; nenhuma ação necessária

### Instalação/alteração do agendamento diário

```bash
bash .claude/scripts/aso-doc-agent-setup.sh
```

Instala um trabalho `launchd` (`~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist`) que
executa `claude -p "/aso-doc-agent"` deste repositório diariamente. Execute o script novamente sempre que
editar o cronograma dentro dele (padrão: 07:53 local). Isso só funciona enquanto o computador estiver
ativado e ativado nesse momento — iniciado não executa tarefas perdidas retroativamente, mas será executado
o próximo horário agendado normalmente.

```bash
launchctl list | grep com.sandsinh.aso-doc-agent   # confirm it's loaded
launchctl start com.sandsinh.aso-doc-agent         # trigger a run right now, don't wait for 07:53
launchctl unload ~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist  # stop it
```

Os logs de cada execução programada chegam ao `.claude/skills/aso-doc-agent/state/launchd.out.log`
e `launchd.err.log`.

## O que você será solicitado a fazer

- **Um DM do Slack do agente** (enviado como você, para você — sandsinh primeiro, kanishka em
escalonamento) solicitando uma captura de tela ou vídeo, com etapas de captura exatas e os URL(s) para
usar. **Responda no tíquete Jira vinculado, não no Slack**: anexe a captura de tela diretamente,
ou para vídeo, carregue-o por meio do formulário normal de vídeo do Experience League
(`experience-league-video-upload` habilidade) e cole o resultado `video.tv.adobe.com`
link como um comentário Jira. A próxima execução o pega automaticamente.
- Se ninguém responder dentro de **5 dias**, a solicitação será escalonada de sandinh para kanishka
automaticamente. Após **10 dias** sem resposta de nenhum dos dois, o agente envia o documento
sem mídia e adiciona uma nota em linha. Não há mesclagem automática baseada em tempo limite — a PR
ainda espera por uma revisão humana real, por mais tempo que leve.
- **Uma PR a ser revisada** — atribuída a qualquer um de vocês que tiver menos PRs abertas por agente
aguardando revisão. Rascunhos de PRs significam que a mídia ainda está pendente; eles mudam para
pronto para revisão automaticamente quando o ativo for exibido. Aprovar e o agente se mescla
na próxima execução — não é necessária nenhuma etapa de mesclagem separada.
- **Se você solicitar alterações**, o agente lerá seus comentários sobre a próxima execução. Generalizável
o feedback (não é uma correção de erro de digitação/link) é gravado em `references/review-learnings.md`, portanto,
a mesma correção não precisa ser repetida em uma PR futura.

## Ajustar o comportamento

Editar `.claude/skills/aso-doc-agent/config.yml` (rastreado no Git) — as alterações afetam cada
execução futura, nesta máquina ou em qualquer outra pessoa que clone o repositório):

- `pr.max_open` — quantas PRs abertas antes do agente pausar de escolher novos tíquetes (padrão 3)
- `pr.stale_after_hours` — por quanto tempo uma PR de `CHANGES_REQUESTED` pode permanecer aberta antes de parar de contar em direção a `pr.max_open` (padrão 336 = 14 dias); ela permanece aberta, isso apenas desbloqueia novas escolhas
- `github.reviewers` — quem é atribuído e em qual saldo
- `media.contacts_in_order` / `escalate_after_hours` (padrão 120 = 5 dias) / `give_up_after_hours` (padrão 240 = 10 dias) — quem é perguntado, em que ordem e com que paciência; ambos são medidos a partir da solicitação original, portanto, o escalonamento não anula a data de desistência
- `pr.check_reviews_every_run` — desativar a etapa de verificação de revisão (não recomendado; é assim que ocorrem as mesclagens e os aprendizados)

## Se parar em um prompt de permissão

As execuções headless (`claude -p`, inicializadas) não têm terminal para solicitar — uma chamada de ferramenta não listada
vão simplesmente falhar em vez de se enforcar. Se o log de uma execução mostrar uma negação de permissão para um comando
o pipeline realmente precisa, adicione-o à lista `permissions.allow` em
`.claude/settings.local.json` (não rastreado no Git — machine-local; cada desenvolvedor em execução
este agente precisa de sua própria cópia com seu próprio incluo na lista de permissões de escopo).

## Se ele parar de fazer progresso inteiramente

Marque, em ordem:
1. `gh pr list --repo Adobe-Enterprise-Docs/experience-manager-sites-optimizer.en --label aso-doc-agent --state open` — se isso mostrar 3, ele está aguardando revisões, não travado.
2. Jira: há um tíquete `New` qualificado restante em SITES-49539 que ainda não seja `aso-doc-agent-picked`? O rótulo só é aplicado depois que uma ramificação+PR existe (pipeline.md Etapa 6.10), portanto, uma execução com falha não deve deixar um tíquete rotulado, mas não publicado. Se você ainda encontrar um (por exemplo, um rótulo adicionado manualmente), remova-o manualmente para tornar o tíquete elegível novamente.
3. `.claude/skills/aso-doc-agent/state/launchd.err.log` para o erro da execução mais recente.
4. Se o resumo de uma execução mostrar &quot;backlog épico totalmente coberto&quot; ou &quot;nada a fazer aqui&quot;, mas você sabe que deve haver trabalho elegível, trate isso como suspeito — essas mensagens são reservadas para resultados genuinamente vazios. Um erro real de Jira/GitHub/Slack é registrado separadamente e deve ser exibido como sua própria linha em `launchd.err.log`, em vez de se ocultar atrás de uma dessas mensagens.
