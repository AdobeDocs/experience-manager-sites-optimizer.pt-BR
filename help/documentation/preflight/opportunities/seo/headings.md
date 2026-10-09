---
title: Auditoria de Cabeçalhos de Comprovação
description: Saiba mais sobre a auditoria de títulos em Comprovação para AEM Sites Optimizer.
source-git-commit: af80dbb47a25b10cdbe55965fb7c4ce496448871
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%
---
# Auditoria de títulos

A auditoria **Títulos** revisa os subtítulos na sua página (H2 a H6). Ela sinaliza cabeçalhos que não têm texto e cabeçalhos que ignoram um nível, como um H2 seguido diretamente por um H4.

## Por que é importante

Os cabeçalhos dão a uma página seu contorno. Os leitores os examinam para encontrar o que precisam, os usuários de leitores de tela se movem por uma página por seus cabeçalhos e os mecanismos de pesquisa os usam para entender como o conteúdo é organizado. Um cabeçalho vazio adiciona uma interrupção nesse outline sem nada nele, e um nível ignorado torna a estrutura mais difícil de seguir.

## O que a auditoria verifica

A auditoria relata uma oportunidade para cada um dos seguintes problemas:

* **Cabeçalho vazio:** um H2, H3, H4, H5 ou H6 que não tem texto. Um cabeçalho que contenha apenas espaços ou apenas uma imagem é contado como vazio.
* **Nível de cabeçalho ignorado:** um cabeçalho com mais de um nível a mais do que o cabeçalho imediatamente antes dele, por exemplo, um H2 seguido de um H4 ou um H1 seguido de um H3. A oportunidade é relatada no cabeçalho mais profundo.

Ambos são relatados com impacto moderado.

Os cabeçalhos H1 são revisados pela auditoria [Metatags](./metatags.md), que verifica se há H1 ausente, vazio ou muito longo e mais de um H1 em uma página.

## Como os cabeçalhos são lidos

A auditoria lê a página que você está editando e verifica cada cabeçalho na ordem em que ele aparece:

* Todos os cabeçalhos são contados, incluindo os do cabeçalho da página, navegação e rodapé, e os que estão ocultos na tela.
* Somente a etapa de um cabeçalho para o próximo é marcada. Uma página cujo primeiro cabeçalho é um H3 não é sinalizada para isso.
* Os títulos podem voltar qualquer número de níveis, por exemplo, de uma H4 para uma H2.

## Sugestões

Cada oportunidade inclui uma recomendação e um aviso fixo para a alteração ser feita. A auditoria de Títulos não gera sugestões de IA.

## Se um cabeçalho sinalizado parecer correto para você

Se uma oportunidade não corresponder ao que você espera, um dos motivos a seguir geralmente é:

* **O cabeçalho faz parte do seu modelo de página.** Os títulos no cabeçalho, navegação ou rodapé são verificados junto com o conteúdo, de modo que um cabeçalho de rodapé com vários níveis mais profundos do que o último cabeçalho do conteúdo pode ser sinalizado como um nível ignorado. Corrigi-lo no modelo o resolve em todas as páginas que usam o modelo.
* **O cabeçalho contém apenas uma imagem ou um ícone.** Um cabeçalho sem texto é reportado como vazio mesmo quando mostra uma imagem. Adicione texto ao cabeçalho ou use um elemento que não seja de cabeçalho para a imagem.

## Limitações conhecidas

* **Visibilidade não considerada:** os cabeçalhos ocultos na tela ainda estão marcados.
* **Páginas muito grandes:** páginas com mais de 500 cabeçalhos não são verificadas.

## Como resolver

Quando a auditoria encontra oportunidades, cada uma descreve o problema e a alteração recomendada.

* **Cabeçalho vazio:** adicione texto descritivo ao cabeçalho ou remova-o se não for necessário.
* **Nível do cabeçalho ignorado:** altere o cabeçalho para o próximo nível abaixo do cabeçalho antes dele (por exemplo, uma H4 depois que uma H2 se tornar uma H3) ou adicione o nível ausente entre eles.

Use **Realçar na página** para localizar o cabeçalho no seu conteúdo. A forma como o cabeçalho é realçado depende de onde você executa a Comprovação:

* **Edge Delivery Services:** A simulação rola até o cabeçalho e o contorna.
* **Editor de páginas do AEM Sites e Adobe Managed Services (AMS):** A simulação rola até o cabeçalho e o contorna. O realce requer **Modo de edição**.
* **Editor Universal:** A simulação seleciona o próprio cabeçalho ou o bloco editável mais próximo que o contém. Para um cabeçalho no conteúdo que o editor não gerencia, como navegação ou rodapé, a Comprovação o exibe, mas não pode selecionar o próprio cabeçalho.

Para obter mais informações, consulte [Destaque na página](../../audit-results.md#highlight-on-page).

Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
