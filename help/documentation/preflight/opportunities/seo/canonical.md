---
title: Comprovação de auditoria canônica
description: Saiba mais sobre a auditoria canônica em Comprovação para AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 5c97431c2029e117339877219c2d6e4e30902a70
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%
---
# Auditoria canônica

A auditoria **Canônica** revisa o link canônico na sua página. O link canônico é uma tag `<link rel="canonical">` no `<head>` da página que nomeia a URL preferencial para o conteúdo da página. A auditoria sinaliza links canônicos que estão ausentes, configurados incorretamente ou que apontam para outro lugar que não a própria página.

## Por que é importante

O mesmo conteúdo geralmente pode ser acessado em mais de um URL, por exemplo, com e sem uma barra à direita, com parâmetros de rastreamento ou com maiúsculas e minúsculas diferentes. Os mecanismos de pesquisa tratam cada URL como uma página separada, a menos que informado de outra forma. O link canônico informa o URL preferido; isso os ajuda a agrupar as duplicatas, combinar sinais de classificação, como links de entrada em um URL, e mostrar esse URL nos resultados da pesquisa.

Um link canônico que está errado pode ser pior do que nenhum. Os mecanismos de pesquisa podem ignorar um link canônico no qual não podem confiar, como um sem URL, um colocado fora da `<head>` ou uma das várias marcas em que discordam. Um link canônico que aponta para uma página diferente solicita que os mecanismos de pesquisa mostrem essa página no lugar da sua, o que pode manter a página fora dos resultados da pesquisa.

## O que a auditoria verifica

A auditoria verifica a existência de problemas em três domínios:

* **Se a página tem um link canônico:** o link canônico está ausente ou a página tem mais de um. Vários links canônicos que apontam para URLs diferentes são relatados separadamente, porque os mecanismos de pesquisa podem ignorar todos eles.
* **Se a marca está configurada corretamente:** a marca está fora de `<head>`, não tem atributo `href` ou vazio, ou carrega um atributo como `hreflang`, `media` ou `type` que pode fazer com que os mecanismos de pesquisa a ignorem.
* **Se a URL está correta:** a URL canônica é relativa em vez de absoluta, contém letras maiúsculas no caminho ou na cadeia de caracteres de consulta, usa um protocolo diferente (`http://` ou `https://`) da página ou aponta para uma página diferente daquela que você está editando.

## Como o URL canônico é comparado

A simulação é executada nas páginas de visualização, cujo host geralmente é diferente do site de produção. Para evitar a sinalização de cada página de visualização, a auditoria não compara o host do URL canônico com o host da página. Ao verificar se o link canônico aponta para a própria página, ele compara somente o caminho da URL, de modo que `https://www.example.com/products/shoes` corresponde à página de visualização `/products/shoes`. Uma barra à direita e uma letra maiúscula no caminho não contam como diferenças nesta verificação.

## Limitações conhecidas

* **Domínio diferente:** uma URL canônica que aponta para um site diferente não é sinalizada pela Comprovação, pois os hosts de visualização sempre diferem do site de produção. Confirme se o domínio no URL canônico é o que você espera.
* **Cabeçalho `Link` HTTP:** A simulação verifica somente a marca canônica, não o cabeçalho `Link` HTTP. Uma página que define seu URL canônico somente no cabeçalho é relatada como ausente no link canônico.

## Como resolver

Quando a auditoria encontra oportunidades, cada uma descreve o problema e a alteração recomendada. Na maioria dos casos, a página deve ter exatamente um link canônico, no `<head>`, com uma URL absoluta com um caminho em minúsculas que aponte para a própria página. Se a página apontar intencionalmente para outra página como sua versão canônica, por exemplo, uma cópia duplicada ou amigável para impressora, você pode deixá-la como está. A auditoria continuará a informá-lo. Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
