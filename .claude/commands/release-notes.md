---
description: Converta as notas de versão internas do ASO sprint no formato do Experience League voltado para o cliente e anexe à página de notas de versão.
source-git-commit: d17008c39f231c45a9ba41ca7f0aa96b9878f674
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---


# Conversor de notas de versão

Converte as notas de versão internas do Sprint (do canal `#aem-sites-optimizer-announcements` do Slack ou da saída do Cursor `.cursor/commands/release-notes`) em uma entrada voltada para o cliente e as anexa a `help/documentation/release-notes.md`.

## Uso

Chame essa habilidade e cole o conteúdo das notas de versão internas quando solicitado. A habilidade irá:

1. Aplique as diretrizes abaixo para filtragem e regras de tom.
2. Analise as notas de versão internas (seções categorizadas por emoji: ✨ Recursos, 🚀 Aprimoramentos, 🤖 AI-First, 🔧 Correções, 🏢 BackOffice).
3. Filtrar todas as categorias excluídas por diretrizes (ferramentas de IA, BackOffice, material de localização, testes E2E, itens somente SitesInternal).
4. Reescreva os itens restantes no tom voltado para o cliente usando os exemplos de tom abaixo como referência.
5. Agrupar itens relacionados por área de recurso (não por equipe ou acordo de recompra).
6. Formate como uma nova entrada de versão seguindo o modelo de estrutura de página abaixo.
7. Preceda a nova entrada a `help/documentation/release-notes.md` (acima da entrada mais recente anterior, abaixo do parágrafo de introdução da página).
8. Imprima uma tabela de resumo mostrando: itens mantidos, itens regravados, itens descartados (com o motivo para cada item descartado).

## Diretrizes

### Princípios básicos

1. **Benefício para o cliente em primeiro lugar.** Cada entrada deve responder &quot;o que posso fazer agora que não poderia antes, ou fazer melhor?&quot; — não &quot;o que nós enviamos?&quot; Comece com o valor, não com a implementação.

2. **Tom de liderança.** Escreva para um tomador de decisão: resultados e recursos, não mecânica técnica. Um VP de Experiência Digital deve entender imediatamente por que uma atualização é importante.

3. **Nenhum jargão interno.** Substitua toda a taquigrafia interna do grupo:
   - &quot;PLG&quot; → &quot;usuários de avaliação&quot; ou &quot;novos clientes&quot;
   - &quot;BackOffice&quot; → omitir completamente (alteração somente na infraestrutura)
   - &quot;MSM&quot; → &quot;AEM Multi-Site Manager&quot;
   - &quot;SHM&quot; → &quot;Monitor de integridade do site&quot;
   - &quot;OrcaFix&quot;, &quot;Comandos do cursor&quot;, &quot;AGENTS.md&quot; → omitir completamente
   - &quot;EDS&quot; → &quot;Edge Delivery Services&quot;

4. **Entradas curtas.** Uma frase de *o que*, uma frase de *por que é importante*. Se ambos se encaixarem em uma frase, faça isso.

5. **Escopo preciso.** Inclua somente as alterações que um cliente verá na interface do usuário do produto ou na experiência em seus fluxos de trabalho. As alterações na infraestrutura, nas ferramentas e na experiência do desenvolvedor são excluídas.

### Modelo de estrutura de página

Cada entrada de versão segue esta estrutura:

```markdown
## [Month Start]–[Day End], [Year]

### New Features

- **[Feature Name]** — [One-sentence benefit statement. One sentence of business context if needed.]

### Enhancements

- **[Enhancement Name]** — [One-sentence improvement statement.]

### Bug Fixes

- [Short description of what was fixed and why it matters to users.]
```

**Regras:**
- Formato de intervalo de datas: `May 11–22, 2026` (traço, mês abreviado, ano de quatro dígitos).
- Ordem cronológica inversa: versão mais recente na parte superior da página.
- Incluir somente seções que tenham conteúdo. Omita &quot;Melhorias&quot; ou &quot;Correções de erros&quot; se estiverem vazios.
- As entradas de Correções de erros não usam nomes de recursos em negrito; elas são marcadores simples.
- Inclua Correções de erros somente se houver 3 ou mais correções visíveis pelo usuário que valham a pena serem observadas.

### O que incluir vs. excluir

**Incluir:**

| Categoria | Exemplos |
|---|---|
| Novos tipos de oportunidade | Incompatibilidade de intenção de anúncio, nenhum CTA acima da dobra |
| Novas exibições ou fluxos de trabalho | Guia Implantado, exportação de CSV, vinculação de Jira |
| Melhorias de avaliação/integração | Fluxo de configuração guiado, estado integrado sem site |
| Melhorias nas configurações | URLs de destino de auditoria, configuração de tipo de entrega |
| Correções significativas de UX | Contagens incorretas, navegação corrompida, problemas de exibição que afetam as decisões |
| Novos dados/integrações | Dados do Ahrefs na Pesquisa orgânica, árvore de dependência na Segurança |
| Recursos de implantação para criação | Novos tipos de oportunidade que oferecem suporte à implantação direta |

**Excluir:**

| Categoria | Por que |
|---|---|
| Ferramentas de IA (OrcaFix, comandos do cursor, AGENTS.md, regras do Claude Code) | Ferramentas internas de desenvolvedor, não visíveis para os clientes |
| Linter de localização / ganchos de pré-confirmação | Processo de engenharia, não é um recurso do produto |
| BackOffice / alterações na infraestrutura | Não visível na interface do usuário, a menos que altere o comportamento do usuário final |
| Atualizações de versão do React Spectrum | Dependência interna, não visível ao usuário |
| Melhorias no teste E2E | Qualidade de engenharia, não é um recurso do produto |
| Liberar automação do pipeline | Processo interno |
| Recursos apenas do SitesInternal | Não disponível para clientes |

### Exemplos de tons

| Frase interna | Frase voltada para o cliente |
|---|---|
| &quot;Estado REJEITADO introduzido para fluxo de trabalho de validação manual&quot; | &quot;Agora você pode marcar sugestões como rejeitadas para indicar que elas não se aplicam ao seu site, mantendo sua lista de oportunidades focada em itens acionáveis.&quot; |
| &quot;Exibição Implantada para oportunidades Canônicas e Hreflang (agrupadas por data)&quot; | &quot;As alterações nas oportunidades Canônicas e Hreflang agora são agrupadas por data de implantação em uma guia Implantado, fornecendo um histórico claro do que foi corrigido e quando.&quot; |
| &quot;Autofix V2 de Texto Alternativo — Avaliação antes do voo &#39;Verificar capacidade de correção&#39;&quot; | &quot;Antes de implantar uma correção de Texto Alternativo, você pode executar uma verificação antes do voo para verificar se a correção pode ser aplicada com êxito ao conteúdo.&quot; |
| &quot;96% de otimização de armazenamento para métricas de SHM&quot; | omitir — somente infraestrutura |
| &quot;AGENTS.md com funções de agente formais e medidas de proteção de segurança&quot; | omitir — ferramentas internas de IA |
| &quot;Otimizações de desempenho de teste E2E (~6min → ~5min)&quot; | omitir — processo de engenharia |

### Regras de agrupamento

- **Agrupar por área de recurso**, não por equipe ou repositório. Por exemplo, todas as melhorias de Texto alternativo (recursos, aprimoramentos e correções) pertencem à mesma área — não as distribua entre seções.
- **Consolidar correções estreitamente relacionadas** em um único marcador, em vez de listar cada uma separadamente (por exemplo, &quot;Várias melhorias de exibição e layout nas oportunidades de Tráfego pago, Acessibilidade e Segurança&quot;).
- **Seção Limite para Correções de Erros**: incluir esta seção somente quando houver 3 ou mais correções visíveis pelo usuário que valha a pena chamar. As correções triviais ou puramente cosméticas abaixo desse limite devem ser omitidas.

## Etapas

1. Aplique as diretrizes neste arquivo — internalize todos os princípios, inclua/exclua regras, exemplos de tons e regras de agrupamento.
2. Solicite ao usuário o intervalo de datas coberto (por exemplo, &quot;11-22 de maio de 2026&quot;) se ainda não tiver sido fornecido.
3. Peça ao usuário para colar o conteúdo das notas de versão internas (ou aceitar um caminho de arquivo).
4. Processe o conteúdo:
   - **Analisar** cada seção (✨/🚀/🤖/🔧/🏢) e seus marcadores.
   - **Filtro** de acordo com a tabela Excluir acima. Marque cada item eliminado com um motivo.
   - **Reescrever** itens mantidos no tom do cliente: benefício-primeiro, sem jargão, entradas curtas.
   - **Agrupar** por área de recurso onde vários itens estão relacionados.
   - **Verificação de limite**: incluir apenas uma seção &quot;Correções de erros&quot; se houver mais de 3 correções visíveis pelo usuário.
5. Formate a nova entrada usando o modelo de estrutura de página acima.
6. Ler o conteúdo atual de `help/documentation/release-notes.md`.
7. Insira a nova entrada imediatamente após o parágrafo de introdução da página (antes do cabeçalho de data `##` mais recente anterior).
8. Grave o arquivo atualizado.
9. Imprimir a tabela de resumo.

## Formato de entrada

A habilidade aceita as notas de versão internas no formato padrão da equipe:

```
*ASO UI Release Notes — [Date Range]*
Collaborators: [teams]

✨ *Features*
• [Feature description]

🚀 *Enhancements*
• [Enhancement description]

🤖 *AI-First Development*
• [AI tooling items — will be dropped]

🔧 *Fixes & UX Improvements*
• [Fix description]

🏢 *BackOffice*
• [BackOffice items — will be dropped]
```

## Saída

Os resultados da habilidade:

1. A entrada formatada voltada para o cliente (para revisão antes da gravação).
2. Um prompt de confirmação antes de modificar `release-notes.md`.
3. Após a gravação: uma tabela de resumo de itens mantidos/reescritos/soltos.
