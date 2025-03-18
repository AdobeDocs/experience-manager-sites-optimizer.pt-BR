---
title: Documentação de oportunidade de problemas do mapa do site
description: Saiba mais sobre a oportunidade de problemas do mapa de site e como usá-lo para melhorar a aquisição de tráfego.
badgeTrafficAcquisition: label="Aquisição de tráfego" type="Caution" url="../../opportunity-types/traffic-acquisition.md" tooltip="Aquisição de tráfego"
source-git-commit: d812a49e4b49d329717586b9f3c7a235aff3e69a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---


# Oportunidade de problemas do mapa do site

![Oportunidade de problemas do mapa do site](./assets/sitemap-issues/hero.png){align="center"}

Um mapa de site completo e preciso ajuda os mecanismos de pesquisa a rastrear e indexar páginas do site com eficiência, garantindo melhor visibilidade dos resultados da pesquisa. A oportunidade do mapa de site identifica possíveis problemas com seu mapa de site. A correção desses problemas pode melhorar muito a indexação do mecanismo de pesquisa e a descoberta de conteúdo no site.

Um resumo é exibido na parte superior da página, incluindo um resumo do problema e seu impacto no site e na empresa.

* **Tráfego projetado perdido** - A perda de tráfego estimada devido a problemas de mapa de site.
* **Valor de tráfego projetado** - O valor estimado do tráfego perdido.

## Identificação automática

Os problemas do mapa do site podem ser filtrados usando os seguintes critérios:

* **Mapa do site com problemas** - A URL do mapa de site analisada que contém problemas em potencial.
* **Tipo de problema** - O tipo de problema identificado no mapa de site:
   * **Erros de cliente** - Entradas que não retornam uma resposta `200 Success`.
   * **Redirecionamentos** - Redirecionamentos com falha ou configurados incorretamente.

>[!BEGINTABS]

>[!TAB Erros de cliente]

![Identificar automaticamente erros de cliente do mapa de site](./assets/sitemap-issues/auto-identify-client-errors.png){align="center"}

Se os URLs no mapa de site retornarem esses dados, os mecanismos de pesquisa poderão supor que o mapa de site esteja desatualizado ou que as páginas foram removidas por engano. O cliente indica que a solicitação do cliente (navegador ou rastreador) era inválida. As comuns incluem:

* **404 Não encontrado** - A página solicitada não existe.
* **403 Proibido** - O servidor nega acesso à página solicitada.
* **410 Sumiu** - A página foi intencionalmente removida e não retornará.
* **401 Não autorizado** - A autenticação é necessária, mas não foi fornecida.

Esses erros podem prejudicar o SEO, especialmente se páginas importantes retornarem **404 ou 410**, já que os mecanismos de pesquisa podem desindexá-los.

Cada problema é exibido em uma tabela, com a coluna **Página** identificando a entrada do mapa de site afetada:

* **Página** - A URL da entrada do mapa de site com um problema.

>[!TAB Redirecionamentos]

![Identificar automaticamente erros de cliente do mapa de site](./assets/sitemap-issues/auto-identify-redirects.png){align="center"}

Os mapas do site devem incluir apenas URLs de destino final, não aqueles que redirecionam. Redirecionamentos são destinados a orientar usuários e crawlers para o local correto, mas podem causar problemas se configurado incorretamente:

* **302 Encontrado (Redirecionamento Temporário)** - Pode causar problemas de SEO se for usado por engano em vez de um **301**.
* **307 Redirecionamento temporário** - Semelhante a 302, mas preserva o método HTTP.
* **Loops de Redirecionamento** - Quando uma página redireciona para si mesma ou cria um loop infinito.
* **Redirecionamentos interrompidos** - Quando um redirecionamento resulta em uma página 4xx ou inexistente.

Cada problema é exibido em uma tabela, com a coluna **Página** identificando a entrada do mapa de site afetada:

* **Página** - A URL da entrada do mapa de site com um problema.

>[!ENDTABS]

## Sugestão automática

Cada problema de mapa de site [que atende aos critérios de filtro](#auto-identify) está listado em uma tabela com as seguintes colunas:

* **Página** - A URL da entrada do mapa de site com um problema.
* **Sugestão** - A correção recomendada para o problema.

As sugestões normalmente incluem um caminho atualizado do site para corrigir a entrada do mapa de site. Em alguns casos, eles também podem fornecer instruções mais detalhadas, como especificar o público alvo de redirecionamento correto.

## Otimizar automaticamente o [!BADGE Ultimate]{type=Positive tooltip="Ultimate"}


![Otimizar automaticamente problemas do mapa de site](./assets/sitemap-issues/auto-optimize.png){align="center"}

O Sites Optimizer Ultimate adiciona a capacidade de implantar otimizações automáticas de mapas de site.

>[!BEGINTABS]

>[!TAB Implantar otimização]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Solicitar aprovação]

{{auto-optimize-request-approval}}

>[!ENDTABS]
