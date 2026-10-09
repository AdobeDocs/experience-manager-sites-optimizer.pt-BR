---
title: Auditoria de Links Externos de Comprovação
description: Saiba mais sobre a auditoria de Links externos em Comprovação para AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 9fd898e905bf843b4d39891c5875497a01569791
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%
---
# Auditoria de Links Externos

A auditoria de **Links Externos** analisa os links na sua página que apontam para outros sites. A auditoria verifica cada link externo da página que você está editando e sinaliza os que estão corrompidos, inseguros ou que não puderam ser verificados automaticamente.

## Por que é importante

Um link externo quebrado é um beco sem saída para o leitor e um sinal para os mecanismos de pesquisa de que a página não é bem mantida. Os links externos também são aqueles sobre os quais você tem menos controle: o outro site pode mover, renomear ou remover uma página a qualquer momento e seu link para de funcionar silenciosamente. Marcá-los antes de publicar captura os links que ficaram obsoletos desde que foram adicionados pela primeira vez.

## O que a auditoria verifica

A auditoria relata uma oportunidade para cada link externo que tenha um dos seguintes problemas:

* **Link corrompido:** o link não pode ser acessado ou retorna um erro como `Status 404`, `Status 410` ou um erro de servidor `5xx`. Um link que atinge o erro após um redirecionamento é relatado da mesma forma. Um link cujo site não responde de forma alguma, por exemplo, porque o domínio não existe mais, também é relatado como interrompido.
* **Link não seguro:** o link usa `http://` e o site não o redireciona para `https://`. Um link que começa como `http://`, mas é redirecionado para uma página `https://` segura, não está sinalizado. Atualize o link para usar `https://`.
* **Link não verificado:** o site respondeu, mas recusou a verificação automatizada, por exemplo, porque requer entrada (`Status 401` ou `Status 403`), limita solicitações automatizadas (`Status 429`) ou bloqueia bots, como fazem algumas redes sociais. Um link que é redirecionado muitas vezes para ser seguido também é relatado dessa maneira. Esses links provavelmente funcionam em um navegador, portanto, a Comprovação não os relata como corrompidos. Em vez disso, ele solicita que você abra o link e confirme-o, além de relatá-lo com baixo impacto.

Um link pode ser inseguro e quebrado, ou inseguro e não verificado, caso em que ambas as oportunidades são relatadas. Um link que é resolvido com sucesso não é sinalizado, mesmo quando tem redirecionamentos no caminho.

## Como os links são verificados

Um link externo é qualquer link cujo host seja diferente da página que você está editando. O host é o nome de domínio mais qualquer porta não padrão, como `:8443`. Os subdomínios contam como hosts diferentes, portanto, `blog.example.com` e `example.com` são ambos externos a `www.example.com`. Não importa se o link usa `http://` ou `https://`. Os links para o mesmo host, incluindo os links do `http://` para o seu próprio site, são cobertos pela auditoria de [Links Internos](./internal-links.md). Links como `mailto:`, `tel:` e `javascript:` são ignorados.

O navegador não consegue ler o status de um link em outro site, portanto, a Comprovação verifica os links externos nos servidores da Adobe em vez de verificar na sessão de criação. Cada link é verificado uma vez, mesmo que apareça várias vezes na página ou com âncoras diferentes, como `#pricing` e `#features`. A oportunidade destaca o primeiro lugar em que o link é exibido.

Os links que o verificador de links do AEM já marcou como inválidos são incluídos na auditoria, mesmo que o editor remova o link clicável da página. Eles são então verificados novamente, em vez de considerados confiáveis, para que um link que tenha começado a funcionar desde então não seja relatado.

## Limitações conhecidas

* **Número de links:** até 50 links externos distintos são verificados por página. Os links além desse limite não são verificados.
* **Limite de tempo:** cada link tem um tempo limite de 10 segundos, e toda a verificação tem um limite de tempo para que a Simulação permaneça responsiva. Um site que não responde dentro do tempo limite é relatado como interrompido. Em páginas com muitos sites lentos, alguns links podem não ser verificados em uma determinada execução.
* **Endereços privados:** os links que são resolvidos para endereços de rede privados ou internos, como um site de intranet, não são verificados e não são relatados.
* **Modo de exibição do lado do servidor**: como os links são verificados nos servidores da Adobe, um site que se comporta de forma diferente com base no local, na entrada ou na detecção de bot pode retornar um resultado diferente daquele que você vê no navegador. Esses links geralmente são relatados como **Link não verificado** em vez de corrompidos.

## Como resolver

Quando a auditoria encontra oportunidades, cada uma descreve o problema e a alteração recomendada e identifica o link envolvido. Use o **Destaque na página** para ir até o link em seu conteúdo e abrir a URL em uma nova guia para confirmar o problema para si mesmo. Para um link quebrado, atualize-o para o novo local da página ou remova-o. Para um link não verificado, confirme se ele é aberto corretamente no navegador. Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
