---
name: experience-league-video-upload
description: Use quando um usuário quiser enviar/carregar um vídeo no Experience League (video.tv.adobe.com / envio de vídeo KT) para incorporação via >[!VIDEO] na marcação deste repositório — abrange o preenchimento do formulário de envio com automação do navegador, os padrões deste repositório e o que nunca deve ser automatizado.
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# Carregamento de vídeo do Experience League

## Visão geral

Os vídeos do Experience League não são hospedados neste repositório — um `.mp4` local é carregado por meio de um formulário de envio separado, que retorna uma URL `video.tv.adobe.com` inserida com `>[!VIDEO](...)` (consulte [[experience-league-markdown]]). Essa habilidade preenche o formulário por meio da automação do navegador, até (não incluindo) anexar o arquivo e enviar.

Formulário: https://81368-exlmpcvideoupload.adobeio-static.net/#/

## Recomendação de arquivo de vídeo

Antes de o usuário gravar ou selecionar um clipe, recomende uma **proporção de 16:9** em uma **resolução máxima de 1920 x 1080 pixels** — este é o requisito declarado do formulário, não apenas uma preferência de estilo. Mencione-o proativamente (por exemplo, quando um usuário disser que está prestes a capturar uma gravação de tela para isso), não apenas se solicitado.

## Regra rígida: nunca anexar o arquivo ou enviar

O envio cria um tíquete KT Jira real e faz o upload para a plataforma de vídeo de produção — uma ação voltada para fora e difícil de reverter. **Sempre** pare quando todos os outros campos forem preenchidos e retorne ao usuário para o arquivo de vídeo e o clique final no envio, mesmo que ele não repita a instrução na próxima vez. Este é o padrão para essa habilidade, não algo que precise ser confirmado novamente por solicitação — ignore esta parada somente se o usuário disser explicitamente para se submeter a ele na mesma solicitação.

## Pré-requisitos

Precisa do servidor MCP `chrome-devtools`, que é **não** confirmado neste repositório (um MCP de automação de navegador não deve ser forçado em todos os colaboradores). Se não estiver carregado:

1. Criar `.mcp.json` na raiz do repositório:

   ```json
   {
     "mcpServers": {
       "chrome-devtools": {
         "command": "npx",
         "args": ["-y", "chrome-devtools-mcp@latest", "--accept-insecure-certs", "--no-usage-statistics"]
       }
     }
   }
   ```
2. Adicionar `.mcp.json` a `.gitignore` (ferramentas pessoais, não compartilhadas).
3. Em `.claude/settings.local.json`, adicione `"enableAllProjectMcpServers": true` e `"enabledMcpjsonServers": ["chrome-devtools"]`.
4. Instrua o usuário a reiniciar o Claude Code (ou executar `/mcp`) — os servidores MCP somente são carregados na inicialização; isso não pode ser feito no meio da sessão.

## Padrões deste repositório

A menos que o usuário diga o contrário, use:

| Texto | Padrão | Por que |
|---|---|---|
| Nuvem | `Experience Cloud` | — |
| Produto | `AEM` | Padrão especificado pelo usuário para este repositório (o formulário também lista `AEM as a Cloud Service` — não o substitua, a menos que solicitado) |
| Subproduto | `AEM Sites` | Correspondência mais próxima; o formulário não tem entrada &quot;Sites Optimizer&quot; |
| Funções | `User` | O conteúdo de comprovação/Sites Optimizer é destinado a autores/profissionais de marketing, não a administradores/desenvolvedores, a menos que o vídeo seja claramente destinado a um público-alvo técnico |
| Níveis de habilidade | `Beginner` | A menos que o fluxo de trabalho mostrado tenha pré-requisitos reais |
| Gênero da voz(s) do vídeo | `No voices` | Somente para gravações em tela silenciosa — pergunte se o clipe tem narração |
| Tipo de vídeo | Perguntar ou inferir a partir do conteúdo | As opções ativas são `Event` / `Feature` / `Technical` / `Value` — uma apresentação da interface do usuário geralmente é `Feature` |
| Email | o que for preenchido | O formulário preenche automaticamente o email Adobe do usuário conectado; não o substitua |

## Etapas

1. `mcp__chrome-devtools__new_page` para a URL do formulário.
2. `mcp__chrome-devtools__take_snapshot` e aguarde (`mcp__chrome-devtools__wait_for` em `"Title"`) até que os dados do formulário terminem de ser carregados — ele começa em um &quot;Carregando dados de formulário...&quot; girador.
3. Preenchimento de **Título** e **Descrição** — A descrição é uma caixa de rich text editável de conteúdo, não uma `<textarea>` simples. `fill`/`fill_form` nele silenciosamente sem operações (o valor não funciona e o erro &quot;obrigatório&quot; permanece). Em vez disso: `click` focalize e `mcp__chrome-devtools__type_text` com o texto.
4. Os menus suspensos (**Tipo de vídeo**, **Gênero do(s) vídeo(s)**, **Nuvem**, **Produto**, **Subproduto**, **Nome do evento**) são botões de caixa de listagem personalizados, não nativos `<select>`. Para cada: `click` o botão para abri-lo, leia as opções reais do instantâneo (elas são carregadas por API — não suponha que a ortografia de opção exata da tabela de padrões ainda esteja atual) e `click` a `option` correspondente.
5. O **Produto** e o **Subproduto** estarão desabilitados até que o campo pai seja definido (Produto precisa da Nuvem; Subproduto precisa do Produto) — preencha-os nessa ordem.
6. **Funções** e **Níveis de habilidade** são grupos de caixas de seleção — `fill_form` com `"value": "true"` na caixa de seleção `uid`s funciona bem aqui (diferente do campo de descrição).
7. Pare. Faça uma captura de tela, resuma o que foi definido e por quê (especialmente qualquer padrão que tenha sido substituído, como Produto/Subproduto), e diga ao usuário para anexar o vídeo e enviar a si mesmo.
8. Depois que o usuário informar que enviou, solicite a URL de vídeo MPC do Adobe resultante (mostrada no formulário após o carregamento, por exemplo, `https://video.tv.adobe.com/v/3496629?learn=on`). Use-o para preencher o código curto `>[!VIDEO](...)` onde quer que este vídeo deva ir — não invente ou adivinhe o URL/ID sozinho.

## Validação de um URL de vídeo retornado

Sempre que um usuário entrega um URL de vídeo para incorporar (etapa 8 acima ou qualquer outro momento):

- **Rejeitar qualquer item que não esteja em `video.tv.adobe.com`.** Os vídeos devem ser hospedados nesse local de acordo com [[experience-league-markdown]] — um link para o YouTube, um host de arquivos ou qualquer outro domínio não é um destino `>[!VIDEO]` válido. Informe ao usuário que ele precisa passar pelo fluxo de upload deste repositório primeiro; não o incorpore.
- **Se estiver faltando `&enablevpops` numa URL `video.tv.adobe.com` válida, adicione-a** antes de incorporar (corresponde à convenção já usada por todos os outros `>[!VIDEO]` neste repositório — consulte `help/home.md`, `help/documentation/trial.md` etc.). Acrescentar `&enablevpops` se já houver um `?`, caso contrário `?enablevpops`.

## Erros comuns

- Experimentando `fill`/`fill_form` no campo Descrição e avançando quando o banner de erro ainda mostrar &quot;É necessária uma descrição.&quot; — verifique a lista de erros após cada etapa, não apenas no final.
- Adivinhando o texto de opção da lista suspensa da memória em vez de abrir a lista suspensa — os valores reais (por exemplo, `No voices` para gênero de voz, `Feature`/`Technical`/`Value` para tipo de vídeo, a divisão AEM/AEM-as-a-Cloud-Service em Produto) não são adivinháveis e podem ser alterados independentemente deste documento.
- Clicar em **Carregar vídeo** / anexar um arquivo &quot;para salvar uma etapa para o usuário.&quot; Não — consulte Regra rígida acima.
