---
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---
# Experience League Markdown — Referência de sintaxe completa

Condensado de https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax (última confirmação em relação à página &quot;Última atualização: 17 de junho de 2026&quot;). Busque novamente a página ao vivo se algo parecer desatualizado.

## Frontmatter e título

```markdown
---
title: Title for search optimization
description: This is the article description used for search optimization.
---
# Article title
```

A linha imediatamente após o fechamento de `---` (e uma linha em branco) deve ser `# Title` — e deve corresponder a `title:` no primeiro plano.

## Formatação básica de texto

- Negrito: `**bold**`
- Itálico: `*italic*`
- Negrito+itálico: `***both***`
- Evitar um caractere de formatação: `\*not italic\*`
- Os parágrafos não precisam de sintaxe especial — apenas uma linha em branco entre eles.

## Cabeçalhos

```markdown
# This is level 1 (article title)
## This is level 2 (mini-TOC entry)
### This is level 3
```

- `#` (H1) = título do artigo, deve corresponder ao frontmatter `title`.
- `##` (H2) = aparece no miniTOC por padrão (`mini-toc-levels: 3` no primeiro plano para mostrar mais níveis).
- Nunca saltar um nível (`##` → `####` é inválido).
- Linha em branco necessária antes de **e** após cada cabeçalho.
- Comprimento máximo do cabeçalho: 69 caracteres (EN), 120 (localizado).
- ID de cabeçalho/âncora: `## Creating processing rules {#processing-rules}` — minúsculas, hifenizadas. Obrigatório se o texto do cabeçalho começar com um número (por exemplo, ano). Sem uma ID explícita, a âncora padrão é o texto de cabeçalho autovalidado.

## Observações / admoestações

Tipos padrão: `NOTE`, `TIP`, `IMPORTANT`, `WARNING`. Tipos somente EXL mais recentes: `ADMIN`, `AVAILABILITY`, `PREREQUISITES`, `INFO`, `ERROR`, `SUCCESS`.

```markdown
>[!NOTE]
>
>This is a standard NOTE block.
>
>It can include multiple paragraphs.
```

Cada linha do bloco começa com `>`. Inclua uma linha `>` vazia logo após o marcador de tipo.

## Guias

```markdown
>[!BEGINTABS]

>[!TAB iOS]

Content for the iOS tab.

>[!TAB Android]

Content for the Android tab.

>[!ENDTABS]
```

- Não é possível aninhar conjuntos de guias em conjuntos de guias, ou conjuntos de guias em listas.
- Os títulos das tabulações são renderizados textualmente — sem formatação de markdown em `>[!TAB ...]`.
- Vários conjuntos de guias estão prontos para uma página.

## Vídeo

```markdown
>[!VIDEO](https://video.tv.adobe.com/v/27069/?learn=on&enablevpops)
```

- O vídeo já deve estar hospedado em `video.tv.adobe.com` (Adobe TV/MPC) — não há suporte para links de arquivos de vídeo brutos ou marcas `<video>`.
- Parâmetros de consulta recomendados: `?learn=on&enablevpops` (a forma canônica usada por cada incorporação neste repositório). Adicionar `&autoplay=true` à reprodução automática.
- Transcrições: adicione `{transcript=true}` ao código curto ou defina `auto-video-transcripts: true` em `TOC.md`/`metadata.md` para todo o guia/repositório.

## Selos

Selo em linha (renderiza onde colocado):

```markdown
[!BADGE Beta]{type=Informative url="https://www.example.com" tooltip="Go to example.com"}
```

Selo de metadados (renderiza acima do H1) — na frente:

```yaml
badgePremium: label="Premium" type="Positive" url="https://www.premium-product.com" tooltip="Download Premium"
```

- `type` (não diferencia maiúsculas de minúsculas): `Informative` (padrão/azul), `Positive` (verde), `Negative` (vermelho), `Neutral` (cinza escuro), `Caution` (amarelo).
- Somente o rótulo é necessário; `type`/`url`/`tooltip` opcional.
- Máximo de **dois** selos de metadados por artigo (configurável, mas &quot;pergunte&quot; antes de depender de uma exceção).
- Os valores do selo de metadados devem ser citados. O selo embutido `url`/`tooltip` deve estar entre aspas.
- As URLs de selo usadas de `TOC.md` devem ser relativas à raiz (`/help/guide/article.md`), não relativas — as entradas do índice se aplicam às pastas.
- `before-title="false"` move um selo de metadados abaixo de H1.
- Adicione `newtab=true` para abrir a URL do selo em uma nova guia.

## Imagens

```markdown
![alt text](assets/logo.png "Hover text"){width="300" align="center"}
```

- `align`: `center` ou `right` somente — não `left`, não `valign`.
- `width`: pixels (`"300"`) ou porcentagem da área de exibição (`"50%"`).
- `zoomable="yes"` faz a imagem clicar para ampliar (não combine com uma imagem que também seja um link — o link ganha).
- Caminho relativo de raiz para imagens compartilhadas: `/help/assets/imagename.png`.
- Limites: limite rígido de 100 MB (GitHub), 5 MB antes de começar a carregar, 20 MB acionam um erro de validação. Máximo de 100 imagens por artigo (limite de renderização do EDS).

## Links e referências cruzadas

- Externo: `[Adobe](https://www.adobe.com)`
- URL vazio como um link: `<https://www.adobe.com>` — um URL vazio não encapsulado faz **não** um vínculo automático.
- Referência cruzada relativa: `[Overview](collaborative-doc-instructions/overview.md)` — resolver a partir do local do arquivo de *origem*; suporta `./`, `../`, `../../`.
- Referência cruzada relativa a raiz: `[Overview](/help/using/docile-rules/introduction.md)` — funciona a partir de qualquer arquivo no repositório, independentemente do local de origem.
- Deep link para um cabeçalho: o destino precisa de `{#heading-id}`; link com `[Text](file.md#heading-id)` (ou apenas `#heading-id` para mesma página).
- Abra em uma nova guia: `[See What's new](whats-new.md){target="_blank"}`.

## Listas

```markdown
1. This is step 1.
1. This is the next step.
   1. Sub-step (indent 3 spaces for numbered lists)
   1. Sub-step
```

```markdown
* First item.
* Second item.
```

- Listas numeradas: sempre gravar `1.` (ou sempre `1)`) — o GitHub renderiza a sequência real. Escolha um estilo (`.` vs `)`) e mantenha a consistência no artigo.
- Listas de marcadores: escolha um dos `*`, `-`, `+` e mantenha-se consistente — misturá-los no mesmo artigo é um erro de validação. Convenção na maioria dos repositórios: `*`.
- Linha em branco necessária antes e depois de qualquer lista.
- O conteúdo entre itens de lista (imagens, tabelas, notas) deve ser recuado até o início do texto (3 espaços para listas numeradas, 2 para listas de marcadores) ou quebra a lista. O recuo excessivo (6 espaços) o transforma em um bloco de código.

## Blocos de código

Inline: `` `code` `` — ou envolva em backticks triplos inline se você precisar de um backtick literal.

Cercado:

````markdown
```javascript
var x = 1;
```
````

- Sempre especifique um idioma para o realce da sintaxe + o botão Copiar.
- Linha em branco necessária acima e abaixo do bloco cercado.
- Números de linha: `` ```html {line-numbers="true"} ``
- Iniciar numeração em outro lugar: `` ```html {line-numbers="true" start-line="7"} ``
- Linhas de destaque: `` ```html {line-numbers="true" start-line="7" highlight="11-13, 16"} ``
- O conteúdo do bloco de código nunca é localizado (exceto `!UICONTROL`/`!DNL` tags, que são removidas no momento da publicação).
- Nenhuma formatação de markdown/HTML (como `<i>`) funciona dentro de blocos de código — use colchetes angulares ou texto sem formatação para espaços reservados.

## Tabelas

- Tabelas de tubulação GFM padrão funcionam para casos simples.
- As tabelas do HTML são permitidas para casos especiais (por exemplo, uma tabela sem linha de cabeçalho). Caso contrário, prefira o Markdown.
- O HTML limitado é permitido dentro de células da tabela de markdown: `<p>`, `<br>`, `<ul>`, `<ol>`.
- As tabelas podem ser definidas como renderização automática ou fixa — consulte o artigo &quot;Tabelas&quot; vinculado do guia de sintaxe se precisar desse nível de controle.

## Seções flexíveis

```markdown
+++See details

This is text inside a collapsible section.

* Bullet one
* Bullet two

+++
```

- Não aninhe seções que podem ser recolhidas — elas não serão renderizadas corretamente (e não falharão na validação, portanto, o erro é enviado silenciosamente).
- Linhas em branco em torno de listas internas/blocos de código dentro da seção são necessárias, assim como em qualquer outro lugar.

## Realce do texto

```markdown
This sentence is normal. <span class="preview">This text is highlighted.</span>
```

Use `<span class="preview">` para realce de parágrafo/incorporado, `<div class="preview">` para vários parágrafos/componentes.

## Trechos e inclusões

- Âncoras H2 compartilhadas de um repositório `help/snippets.md`: referência com `{{anchor-id}}`.
- Arquivos de inclusão compartilhados de `help/_includes/*.md`: referência com `{{$include /help/_includes/filename.md}}`.

## Comentários

```markdown
<!-- standard comment code -->
```

- Nunca usar `<!--> bad comment syntax <-->` (traços ausentes) — ele é renderizado visivelmente em vez de ocultar o texto.
- Os comentários são invisíveis nos documentos renderizados, mas **são visíveis para qualquer pessoa que visualize o arquivo .md bruto no GitHub** — sem segredos ou informações confidenciais.
- Evite comentários dentro de listas de itens (pode quebrar a renderização da lista). Em `TOC.md`, comente apenas as linhas no final do arquivo, nunca no meio da lista.

## Solução alternativa em branco

Linhas em branco adicionais na origem são recolhidas pelo renderizador. Para forçar o espaço vertical visível, coloque `<br>&nbsp;` em sua própria linha onde deseja o espaço.

## Caracteres de escape

- Caracteres escapáveis com barra invertida: `` # { } [ ] * + - . ! `` — ex.: `\# not a heading`.
- Para colchetes (`<placeholder>`), a barra invertida não funciona — use um bloco de código incorporado (`` `<placeholder>` ``) ou entidades HTML (`&lt;placeholder&gt;`).
- As entidades HTML dentro dos blocos de código **não** são convertidas de volta ao caractere — `&gt;` permanece como texto literal lá.
- Os metadados (YAML frontmatter) têm suas próprias regras de escape - se um valor começar com um caractere especial como `:` ou `[`, cite o valor inteiro: `title: "Processing rules: A new beginning"`.

## Incluo na lista de permissões HTML restrito

Somente essas tags da HTML são permitidas em qualquer lugar no Markdown; qualquer outro item é um erro de validação:

```
table  tbody  td  tfoot  thead  th  tr  col  colgroup
p  ul  ol  li  br
b  i  strong  u  s  em  sub  sup  span
caption  a  img  div
pre  code  codeblock
```

Prefira a sintaxe de marcação em vez do HTML sempre que o Markdown puder fazer o trabalho — na verdade, o HTML é apenas para casos de borda, como uma tabela sem cabeçalho.

## Explicitamente incompatível (não use mesmo se uma visualização local as renderizar)

- Regras horizontais (`***`, `<hr>`)
- Códigos de atalho Emoji (`:bowtie:`)
- Listas de tarefas (`- [x] done`)
- Aspas de bloco *componentes* além dos códigos de atalho de observação/guia/vídeo (as aspas de bloco `>` simples são renderizadas como aspas, não como um componente estilizado)
- Sintaxe da lista de definições do Markdown (use a formatação manual em negrito + traço: `**Frog** - An amphibious green creature.`)
- `valign` em imagens

## Vale a pena conhecer os limites de tamanho de arquivo/contagem

| Coisa | Limite |
|---|---|
| Tamanho do arquivo de imagem/download | Aviso de validação em 5 MB, erro em 20 MB, limite rígido do GitHub de 100 MB |
| Imagens por artigo | 100 (limite de renderização do EDS) |
| Selos de metadados por artigo | 2 (padrão) |
