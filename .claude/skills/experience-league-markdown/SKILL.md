---
name: experience-league-markdown
description: Use ao gravar ou editar arquivos do Markdown em um repositório da Adobe Experience League / Adobe-Enterprise-Docs (help/**/*.md) — governa o primeiro plano, cabeçalhos, notas (NOTE/TIP/IMPORTANT/WARNING/etc.), guias (BEGINTABS/TAB/ENDTABS), incorporações de vídeo, selos, imagens, links/referências cruzadas, tabelas, listas, blocos de código e o incluo na lista de permissões de tag restrito do HTML que o pipeline de validação da Experience League impõe.
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---


# Experience League Markdown

## Visão geral

Os documentos do Experience League usam o Markdown com sabor de GitHub, além de um conjunto de extensões personalizadas (códigos de atalho, selos, guias, incorporações de vídeo baseados em blockquote). O pipeline de criação **valida** esses arquivos — o uso de sintaxe sem suporte (marcas `<video>` brutas, `<hr>`, listas de tarefas, caracteres de marcadores mistos, níveis de cabeçalho ignorados, imagens superdimensionadas) causa um erro de compilação/validação, não apenas uma unidade de estilo.

Source da verdade: https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax (procure esta página se o reference.md local parecer obsoleto — a data da &quot;Última atualização&quot; está no topo).

Referência de sintaxe completa com cada código curto e regra: [reference.md](reference.md). Leia antes de escrever qualquer coisa não trivial (guias, vídeo, selos, tabelas com o HTML).

## Referência rápida

| Elemento | Sintaxe | Notas |
|---|---|---|
| Frontmatter | `---\ntitle: ...\ndescription: ...\n---` | Linha em branco, depois `# Title` deve vir |
| Níveis de cabeçalho | `#`, `##`, `###` | `#` = título (corresponde ao frontmatter `title`), `##` = entradas de miniTOC. Nunca pule um nível. Linha em branco antes/depois. Máximo de 69 caracteres (EN) |
| ID do cabeçalho | `## Heading text {#custom-id}` | Obrigatório se o cabeçalho começar com/contiver um numeral, por exemplo: `## 2026 release notes {#2026-release-notes}` |
| Nota/Dica/etc. | `>[!NOTE]` então `>` então `>Text` (cada um em sua própria linha) | Tipos: NOTA, DICA, IMPORTANTE, AVISO, CUIDADO, ADMINISTRADOR, DISPONIBILIDADE, PRÉ-REQUISITOS, INFORMAÇÕES, ERRO, SUCESSO |
| Guias | `>[!BEGINTABS]` / `>[!TAB Title]` / `>[!ENDTABS]` | Não é possível aninhar conjuntos de guias; não é possível aninhar dentro de listas |
| Vídeo | `>[!VIDEO](https://video.tv.adobe.com/v/ID/?learn=on&enablevpops)` | Deve ser hospedado em video.tv.adobe.com — nenhum link bruto `<video>`/arquivo |
| Imagem | `![alt text](assets/img.png "hover text"){width="300" align="center"}` | `align` é somente `center` ou `right` (não `left`, não `valign`) |
| Link (relativo) | `[Text](../folder/file.md)` | Conta para a localização do arquivo de origem |
| Link (raiz) | `[Text](/help/guide/file.md)` | Funciona em qualquer lugar no repositório; necessário para URLs com selo do TOC.md |
| Deep link | `[Text](file.md#heading-id)` | O cabeçalho de destino precisa de um `{#heading-id}` explícito |
| Link externo (URL vazio) | `<https://example.com>` | URLs vazios NÃO são vinculados automaticamente — envolva `< >` ou use `[text](url)` |
| Lista de marcadores | `* item` (escolha um de `*`/`-`/`+`, mantenha a consistência) | Linha em branco antes/depois da lista; misturando marcadores = erro de validação |
| Lista numerada | `1. item` (repetir `1.` a cada linha) | O GitHub renderiza os números reais |
| Código (em linha) | `` `code` `` | Para nomes de arquivo, comandos, valores, exemplos de URLs não validados |
| Código (cercado) | ` `&#x200B;``language ` ... ` ``&#x200B;` ` | Sempre especifique um idioma; linha em branco antes/depois; `{line-numbers="true" start-line="n" highlight="n-m"}` opcional |
| Medalha (em linha) | `[!BADGE Beta]{type=Informative url="..." tooltip="..."}` | `type`: Informativo/Positivo/Negativo/Neutro/Cuidado |
| Recolhível | `+++Summary` ... `+++` | Não há recolhíveis aninhados; linhas em branco em torno de listas internas/código |
| Hack de linha em branco | `<br>&nbsp;` em sua própria linha | Linhas em branco extras sem formatação recolhidas/ignoradas pelo renderizador |
| Comentar | `<!-- text -->` | Nunca `<!--> text <-->` — visível para qualquer um que visualize o arquivo raw no GitHub, então sem segredos |

## Erros comuns

- **Erro de validação bruto `<video>`, `<iframe>`, ou outro HTML** → não relacionado ao. O incluo na lista de permissões HTML é: `table tbody td tfoot thead th tr col colgroup p ul ol li br b caption i strong u s span sub sup a img div em pre code codeblock`. Qualquer outra coisa (incluindo `<video>`/`<source>`) foi rejeitada — use o código de atalho `>[!VIDEO]`, que requer que o vídeo já esteja hospedado em video.tv.adobe.com.
- **`<hr>`/ `***` regras horizontais, códigos de atalho emoji (`:bowtie:`), listas de tarefas (`- [x]`)** — não há suporte; não use-as mesmo se uma visualização local as renderizar.
- **Combinação de marcadores** (`*` e `-` na mesma lista) — erro de validação. Escolha um por artigo.
- **Ignorando níveis de cabeçalho** (`##` diretamente para `####`) — não permitido.
- **Um cabeçalho com numeral à esquerda sem uma ID explícita** (por exemplo, `## 2026 release notes`) — deve adicionar `{#some-id}` ou a espaçador automática pode colidir/quebrar.
- **URLs vazias em prosa** (`Visit https://example.com for more`) — não serão renderizadas como um link. Quebrar linha em `< >` ou usar `[text](url)`.
- **Linhas em branco adicionais para o espaçamento visual** — recolhidas pelo renderizador. Use `<br>&nbsp;` em vez de `<br>` puro ou novas linhas repetidas.
- **Imagens com mais de ~5 MB** — aviso de validação em 5 MB, erro em 20 MB. Mais de 100 imagens em um artigo interrompem a renderização (limite EDS).
- **Mais de duas medalhas em metadados de front-end** — não permitido por padrão.
- **Problemas de escape**: a barra invertida-escape funciona somente para `` # { } [ ] * + - . ! ``. Para `<` `>` em itens como `<filename>` espaços reservados, use um bloco de código incorporado ou entidades HTML (`&lt;filename&gt;`), não uma barra invertida.

## Antes de confirmar as alterações do Markdown

1. O Frontmatter está presente, `# Title` segue imediatamente (após a linha em branco).
2. Cada cabeçalho tem uma linha em branco antes e depois; nenhum nível ignorado.
3. Qualquer vídeo é `>[!VIDEO](https://video.tv.adobe.com/...)`, não uma tag `<video>` bruta.
4. Qualquer código curto personalizado (`>[!NOTE]`, `>[!BEGINTABS]`, `>[!BADGE ...]`) corresponde à sintaxe exata em [reference.md](reference.md) — incluindo a linha `>` em branco dentro de blocos de várias linhas.
5. As listas usam um estilo consistente de marcador/número, com linhas em branco ao redor de toda a lista.
6. Links: links relativos resolvem da pasta do arquivo de *origem*; links entre repositórios ou sumários/selos usam o formulário relativo à raiz (`/help/...`).
7. Nenhuma tag do HTML fora do incluo na lista de permissões na seção Erros comuns acima.
