---
title: Auditoria de Links Externos de Comprovação
description: Saiba mais sobre a auditoria de Links externos em Comprovação para AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 13bc34bf4c3d31e730dbe597b84fd6d594df6fea
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%
---
# Auditoria de Links Externos

A auditoria de **Links Externos** analisa os links na sua página que apontam para outros sites. A auditoria verifica cada link externo da página que você está editando e sinaliza os que estão corrompidos, inseguros ou que não puderam ser verificados automaticamente.

## Por que é importante

Um link externo quebrado é um beco sem saída para o leitor e um sinal para os mecanismos de pesquisa de que a página não é bem mantida. Os links externos também são aqueles sobre os quais você tem menos controle: o outro site pode mover, renomear ou remover uma página a qualquer momento e seu link para de funcionar silenciosamente. Marcá-los antes de publicar captura os links que ficaram obsoletos desde que foram adicionados pela primeira vez.

## O que a auditoria verifica

A auditoria relata uma oportunidade para cada link externo que tenha um dos seguintes problemas:

* **Link corrompido:** o link retorna `Status 404` ou `Status 410`, ou seu site não pode ser acessado, por exemplo, porque o domínio não existe mais. Um link que atinge o erro após um redirecionamento é relatado da mesma forma.
* **Link não seguro:** o link usa `http://` e o site não o redireciona para `https://`. Um link que começa como `http://`, mas é redirecionado para uma página `https://` segura, não está sinalizado. Atualize o link para usar `https://`.
* **Link não verificado:** A comprovação não pôde confirmar se o link funciona, por exemplo, porque o site requer entrada, bloqueia verificações automatizadas, continua retornando um erro de servidor, não responde a tempo ou redireciona muitas vezes. Algumas redes sociais, como LinkedIn e Instagram, relatam páginas que existem como ausentes para cheques automatizados, de modo que os erros de página ausente desses sites também são relatados como não verificados. Esses links provavelmente funcionam em um navegador, portanto, a Comprovação não os relata como corrompidos. Em vez disso, ele solicita que você abra o link e confirme-o, além de relatá-lo com baixo impacto.

Um link pode ser inseguro e quebrado, ou inseguro e não verificado, caso em que ambas as oportunidades são relatadas. Um link que é resolvido com sucesso não é sinalizado, mesmo quando tem redirecionamentos no caminho.

## Quais links são verificados

Todos os links externos na página são verificados. Um link externo é qualquer link cujo host seja diferente da página que você está editando. O host é o nome de domínio mais qualquer porta não padrão, como `:8443`. Os subdomínios contam como hosts diferentes, portanto, `blog.example.com` e `example.com` são ambos externos a `www.example.com`. Os links para o mesmo host, incluindo os links do `http://` para o seu próprio site, são cobertos pela auditoria de [Links Internos](./internal-links.md). Os links na navegação do site são sempre incluídos, porque a configuração **Mostrar links de navegação do site** se aplica somente à auditoria de Links Internos. Links como `mailto:`, `tel:` e `javascript:` são ignorados.

Cada link é relatado uma vez, mesmo que apareça várias vezes na página ou com âncoras diferentes, como `#pricing` e `#features`. A oportunidade destaca o primeiro lugar em que o link é exibido.

Os links que o verificador de links do AEM já marcou como inválidos são incluídos na auditoria, mesmo que o editor remova o link clicável da página. Elas são verificadas novamente, em vez de assumidas como confiáveis, para que um link que começou a funcionar desde então não seja relatado.

## Limitações conhecidas

* **Endereços privados:** links para endereços de rede privados ou internos, como um site de intranet, não são verificados e não são relatados.
* **Modo de exibição do lado do servidor:** A comprovação verifica os links externos dos servidores da Adobe em vez de verificar no navegador. Um site que se comporta de forma diferente com base na localização, logon ou detecção de bot pode retornar um resultado diferente do que você vê no navegador. Esses links geralmente são relatados como **Link não verificado** em vez de corrompidos.

## Como resolver

Quando a auditoria encontra oportunidades, cada uma descreve o problema e a alteração recomendada e identifica o link envolvido. Use o **Destaque na página** para ir até o link em seu conteúdo e abrir a URL em uma nova guia para confirmar o problema para si mesmo. Para um link quebrado, atualize-o para o novo local da página ou remova-o. Para um link não verificado, confirme se ele é aberto corretamente no navegador. Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
