---
title: Auditoria de comprovação do Lorem Ipsum
description: Saiba mais sobre a auditoria Lorem ipsum em Comprovação para AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 587aec4eb905a2b1ced746590ca25b8ed97b16c1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%
---
# Auditoria Lorem ipsum

A auditoria **Lorem ipsum** detecta um texto de espaço reservado que foi deixado no conteúdo da página.

## Por que é importante

Ao publicar uma página com texto de espaço reservado, ela fica inacabada para os leitores. Os mecanismos de pesquisa podem indexar o texto do espaço reservado e mostrá-lo nos resultados de pesquisa, e as plataformas sociais podem mostrá-lo nas visualizações de link. O texto para espaço reservado geralmente fica oculto da exibição, por exemplo, em texto alternativo de imagem ou rótulos de acessibilidade. Quando estiver, as pessoas que usam leitores de tela ou outras tecnologias assistivas ainda poderão ouvi-lo, mesmo que ele não apareça na página.

## O que a auditoria verifica

A auditoria relata cada local na página em que o texto do espaço reservado é exibido. Ele verifica o texto da página visível, além de vários locais onde pode não ser visível imediatamente ou de forma alguma:

* texto alt da imagem
* rótulos e descrições de acessibilidade
* espaços reservados no campo de formulário
* dicas de ferramentas
* o título da página
* metadados, como a meta descrição e as tags de compartilhamento em redes sociais

O código que não é apresentado aos usuários, como scripts e estilos, não é verificado.

## Como o texto é correspondente

A auditoria procura a frase &quot;lorem ipsum&quot; em qualquer combinação de letras maiúsculas e minúsculas. Ela também encontra a frase quando as palavras são divididas em linhas ou elementos, ou não têm espaço entre elas. Se a frase aparecer mais de uma vez no mesmo elemento ou atributo, esse local será relatado uma vez.

## Limitações conhecidas

* **Somente &quot;lorem ipsum&quot;:** outro texto de espaço reservado, como &quot;TBD&quot; ou outras palavras de preenchimento latinas sem &quot;lorem ipsum&quot;, não foi detectado.
* **Destaque na página:** não está disponível para o título ou os metadados da página, pois eles não aparecem na página. Use o texto mostrado na oportunidade para encontrá-los.

## Como resolver

Quando a auditoria encontra oportunidades, cada uma identifica onde o texto do espaço reservado aparece. Onde estiver disponível, use **Realçar na página** para ir para o texto em seu conteúdo. Substitua o espaço reservado por conteúdo real ou remova-o. Para rótulos de texto alternativo e acessibilidade, escreva uma descrição da imagem ou do controle. Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
