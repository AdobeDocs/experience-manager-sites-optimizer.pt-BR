---
title: Implantação da documentação do autor
description: Saiba como o AEM Sites Optimizer implanta otimizações selecionadas no ambiente de criação e como rastreá-las posteriormente.
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 1d55c607aab6c820d014b9a57bfae20b8170c672
workflow-type: tm+mt
source-wordcount: 245
ht-degree: 6%

---

# Implantação da documentação do autor

<!--![Deploying to author](./assets/deploying-to-author/hero.png){align="center"}-->

Depois que a AEM Sites Optimizer identificar uma oportunidade e sugerir otimizações, você poderá revisar e implantar as otimizações selecionadas para executar outras ações.

## Implantar no criador

Selecione uma ou mais sugestões da lista de uma oportunidade e clique em **Implantar no Autor** para implantar sua seleção ou **Implantar tudo no autor** para implantar todas as sugestões disponíveis de uma só vez. O AEM Sites Optimizer aplica as otimizações selecionadas somente ao ambiente de criação — não publica as alterações no site ativo. O autor do AEM pode então revisar e publicar as alterações do Sistema de gerenciamento de conteúdo (CMS), de forma consistente com o fluxo de trabalho de [Otimização automática](/help/documentation/opportunities/missing-alt-text.md#auto-optimize) de cada oportunidade.

Essa ação é desativada quando você não tem permissão para implantar ou quando o site não está totalmente configurado para implantação (por exemplo, um repositório de código ainda não foi conectado). Em ambos os casos, o Sites Optimizer explica por que ao lado do botão desativado.

## Rastrear otimizações implantadas

<!--![Deployed tab](./assets/deploying-to-author/deployed-tab.png){align="center"}-->

Depois de implantar as otimizações selecionadas, você poderá gerenciá-las e executar as próximas etapas a partir da guia **Implantado** na página de detalhes da oportunidade, ao lado das guias **Atual** e **Ignorado**.

A mecânica de implantação específica — incluindo como as atualizações são aplicadas ao Edge Delivery Services, AEM as a Cloud Service ou Digital Asset Management — varia de acordo com o tipo de oportunidade. Consulte a seção **Otimização automática** dessa oportunidade para obter detalhes.

## Consulte também

* [Oportunidade de texto alternativo ausente](/help/documentation/opportunities/missing-alt-text.md#auto-optimize)
* [Oportunidade dos sinais vitais principais da Web](/help/documentation/opportunities/core-web-vitals.md#auto-optimize)
* [Oportunidade de backlinks corrompidos](/help/documentation/opportunities/broken-backlinks.md#auto-optimize)
