---
title: Auditoria de Tamanho de Corpo de Comprovação
description: Saiba mais sobre a auditoria de tamanho de corpo em Comprovação para AEM Sites Optimizer.
source-git-commit: c85cfb84b315b64ab5fcddfaa192ce78dd8d1a67
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%
---
# Auditoria de tamanho do corpo

A auditoria **Tamanho do corpo** revisa a quantidade de conteúdo do corpo na sua página. Páginas com pouco conteúdo podem ser menos úteis para os leitores e podem ser mal classificadas nos resultados de pesquisa. As páginas de sinalizadores de auditoria parecem ter muito pouco texto.

## Por que é importante

Os mecanismos de pesquisa e os assistentes de IA dependem do texto de uma página para entender sobre o que se trata. Uma página com pouco ou nenhum texto geralmente é tratada como de baixo valor, o que pode prejudicar sua classificação e se é exibida nas respostas de IA.

## O que a auditoria verifica

A auditoria mede a quantidade de texto criado na página e relata duas situações:

* **Nenhum conteúdo de texto:** a página foi lida com êxito, mas não tem nenhum corpo de texto. Por exemplo, uma página que é apenas uma imagem.
* **Conteúdo fino:** a página tem texto, mas menos do que o mínimo recomendado.

Uma página com texto suficiente passa e não é sinalizada.

## Como o conteúdo é medido

A auditoria mede o texto na área de conteúdo principal da página, não a página inteira. Os elementos compartilhados, como navegação, cabeçalhos, rodapés e navegação estrutural, são repetidos em cada página e a auditoria os exclui onde podem ser reconhecidos para que esse cromo compartilhado não mascare um conteúdo genuinamente fino. A forma como ele pode separar completamente o conteúdo desse cromo depende da marcação da página, conforme descrito abaixo.

Para encontrar o conteúdo, a auditoria usa a primeira destas opções que se aplicam:

1. **`<main>`elementos (ou `role="main"`).** Essa é tratada como a área de conteúdo definitivo e somente o texto dentro dela é medido (se uma página tiver mais de um desses elementos, seu texto será combinado). É a opção mais confiável.
1. **O corpo da página, com o cromo removido.** Se não houver `<main>` e nenhum `role="main"`, a auditoria mede o `<body>` após a remoção do cromo de página reconhecido: navegação e o cabeçalho e rodapé em nível de página, sejam eles marcados com tags padrão do HTML, funções de marcos ARIA ou os componentes padrão de cabeçalho, rodapé, navegação estrutural e navegação do AEM. Um cabeçalho ou rodapé que pertence a uma seção de conteúdo, como o título ou o byline de um artigo, é mantido.
1. **O corpo inteiro da página.** Se não houver um ponto de referência de conteúdo e nenhum chrome reconhecido, o `<body>` inteiro será medido.

Algumas observações sobre o que conta. As imagens não contribuem com nenhum texto (o texto `alt` não é medido), portanto, uma página que é principalmente imagens ainda pode ser sinalizada. O texto dentro das tags `<script>` e `<style>` nunca é contado, portanto, a análise ou os scripts de camada de dados não inflam a medida. No entanto, o texto do link comum é contado como qualquer outro texto no seu conteúdo.

## Se uma página sinalizada parecer correta para você

Se uma página for sinalizada como fina, mas você estiver confiante de que tem conteúdo suficiente, a auditoria pode não ter separado claramente o conteúdo do cromo ao redor, como navegação, cabeçalhos e rodapés.

Se você quiser que a auditoria meça sua página com mais precisão, as seguintes opções de marcação a ajudarão:

* A opção mais confiável é envolver o conteúdo criado em um elemento `<main>` (ou adicionar `role="main"`). Isso remove qualquer ambiguidade, para que somente seu conteúdo seja medido.
* Se não for possível adicionar um `<main>`, a marcação padrão de cabeçalho e rodapé (`<header>`, `<footer>`) ou as variações padrão de Fragmento de experiência de cabeçalho e rodapé do AEM ajudam a auditoria a reconhecer e excluir o cromo da página.
* Marcar os cabeçalhos e rodapés de nível de seção dentro de `<article>`, `<section>` ou `<aside>` impede que o conteúdo desses cabeçalhos e rodapés seja descartado.

## Limitações conhecidas

A auditoria depende da marcação da página para distinguir o conteúdo do chrome. Em uma página que tenha **não `<main>`, nenhuma marcação de ponto de referência padrão e componentes de cabeçalho/rodapé nomeados de forma diferente das convenções da plataforma**, alguns textos do cromo podem ser incluídos na medição, ou, ocasionalmente, os textos criados podem ser excluídos. Adicionar um elemento `<main>` ao redor do seu conteúdo resolve cada caso. A auditoria não tenta adivinhar a região de conteúdo a partir da densidade do texto ou do layout visual; ela depende de sinais de marcação para que os resultados sejam previsíveis e repetíveis.

## Como resolver

Quando a auditoria encontra oportunidades, cada uma descreve o problema e a alteração recomendada. Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
