---
title: Preparando a documentação de correções de código
description: Saiba como o AEM Sites Optimizer prepara patches de código para correções do Core Web Vitals e como rastreá-los posteriormente.
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: a86d83ee226055e6401b13fd421b40d449b96fa8
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 2%

---

# Preparação da documentação de patches de código

<!--![Preparing code patches](./assets/preparing-code-patches/hero.png){align="center"}-->

Para a [oportunidade de vitais para a Web principais](/help/documentation/opportunities/core-web-vitals.md), o AEM Sites Optimizer gera correções de nível de código para problemas de desempenho identificados. Você revisa e prepara essas correções como patches de código, em vez de implantá-las diretamente.

## Preparar patches de código

Selecione um ou mais problemas na lista do Core Web Vitals e clique em **Preparar patch de código** para preparar sua seleção ou **Preparar todos os patches de código** para preparar todos os patches disponíveis de uma só vez. O AEM Sites Optimizer cria um problema do GitHub rotulado para cada correção e abre automaticamente uma solicitação de pull vinculada com a alteração do código, pronta para que sua equipe revise, teste e mescle.

Essa ação é desativada quando você não tem permissão para preparar patches de código ou quando o site não está totalmente configurado para ele, por exemplo, quando nenhum repositório de código está conectado ou a geração de patch ainda está em andamento. Em cada caso, o Sites Optimizer explica por que ao lado do botão desativado.

## Rastrear patches de código preparados

Depois de preparar os patches de código, você pode gerenciá-los e seguir as próximas etapas da guia **Implantado** na página de detalhes do Core Web Vitals, ao lado das guias **Atual** e **Ignorado**. O status de um patch reflete se sua solicitação de pull foi mesclada, não apenas gerada — um problema só é movido para **Implantado** depois que a correção é realmente mesclada na sua base de código.

## Consulte também

* [Oportunidade dos sinais vitais principais da Web](/help/documentation/opportunities/core-web-vitals.md#auto-optimize)
* [Implantação da documentação do autor](/help/documentation/opportunities/deploying-to-author.md)
