---
title: Auditoria de Links Externos de Comprovação
description: Saiba mais sobre a auditoria de Links externos em Comprovação para AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 12279cd1468a3442709cb73a8691922598a33dab
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%
---
# Auditoria de Links Externos

A auditoria de **Links Externos** analisa os links na sua página que apontam para outros sites. A auditoria verifica cada link externo da página que você está editando e sinaliza os que estão corrompidos, inseguros ou que não puderam ser verificados automaticamente.

## Por que é importante

Um link externo quebrado é um beco sem saída para o leitor e um sinal para os mecanismos de pesquisa de que a página não é bem mantida. Os links externos também são aqueles sobre os quais você tem menos controle: o outro site pode mover, renomear ou remover uma página a qualquer momento e seu link para de funcionar silenciosamente. Marcá-los antes de publicar captura os links que ficaram obsoletos desde que foram adicionados pela primeira vez.

## O que a auditoria verifica

A auditoria classifica os problemas em três grupos:

* **Quebrado:** o link falha para cada visitante neste momento e não é esperado que se recupere.
* **Não verificado:** o link falha para alguns visitantes, pode falhar apenas temporariamente ou não pôde ser verificado.
* **Prática recomendada:** o link funciona, mas não deve ser criado dessa forma, como um link `http://` inseguro.

A auditoria relata uma oportunidade para cada link externo que tenha um dos seguintes problemas:

* **Link quebrado:** o link não funciona para ninguém que o abra. A comprovação relata que um link foi interrompido quando:
  * seu site não pode ser acessado, por exemplo, porque o domínio não existe mais.
  * retorna `Status 404` ou `Status 410`.
  * retorna `Status 405`, o que significa que o site rejeita solicitações de página normais.
  * ele é redirecionado em um loop por mais de 20 vezes. Os navegadores usam o mesmo limite e mostram um erro de &quot;muitos redirecionamentos&quot;.

  Um link que atinge um desses erros após um redirecionamento é relatado da mesma forma.
* **Link não seguro:** o link usa `http://` e a Comprovação não o viu redirecionar para `https://`, inclusive quando o site não respondeu. Um link que começa como `http://`, mas é redirecionado para uma página `https://` segura, não está sinalizado. Atualize o link para usar `https://`.
* **Link não verificado:** A simulação não pôde confirmar se o link funciona, portanto, ela solicita que você abra o link e verifique você mesmo. A oportunidade explica qual caso se aplica:
  * **Exige entrada:** o link retorna `Status 401`. Os visitantes sem uma conta do não podem abri-la, portanto, confirme se isso é intencional.
  * **Bloqueia verificações automatizadas:** o link retorna `Status 403` ou `Status 429`, ou o site bloqueia solicitações automatizadas de outra forma, como faz o LinkedIn. Confirme se o link abre em um navegador.
  * **Sites com murais de entrada e redes sociais:** o LinkedIn, Instagram, Facebook, X (Twitter), TikTok e Threads retornam erros enganosos a solicitações anônimas; portanto, um loop de `Status 404`, `Status 410`, `Status 405` ou redirecionamento desses sites é relatado como não verificado, em vez de corrompido.
  * **Erro de servidor:** o link retorna um erro de servidor (`Status 5xx`) que persiste quando a Comprovação o verifica novamente. Tentativas de comprovação uma vez antes de relatá-lo. O erro pode ser temporário, portanto, confirme se o link funciona antes de publicar.
  * **Indisponível por motivos legais:** o link retorna `Status 451` na região de onde as verificações de Comprovação são feitas. Confirme se isso funciona para o seu público-alvo.
  * **Nenhuma resposta a tempo:** o site não respondeu a tempo, mesmo depois que a simulação foi repetida uma vez. O site pode estar lento ou temporariamente inativo.

Um link pode ser inseguro e quebrado, ou inseguro e não verificado, caso em que ambas as oportunidades são relatadas. Uma cadeia de redirecionamento sozinha não será sinalizada se atingir uma página de trabalho em 20 redirecionamentos.

## Quais links são verificados

Todos os links externos na página são verificados. Um link externo é qualquer link cujo host seja diferente da página que você está editando. O host é o nome de domínio mais qualquer porta não padrão, como `:8443`. Os subdomínios contam como hosts diferentes, portanto, `blog.example.com` e `example.com` são ambos externos a `www.example.com`. Os links para o mesmo host, incluindo os links do `http://` para o seu próprio site, são cobertos pela auditoria de [Links Internos](./internal-links.md). Os links na navegação do site são sempre incluídos, porque a configuração **Mostrar links de navegação do site** se aplica somente à auditoria de Links Internos. Links como `mailto:`, `tel:` e `javascript:` são ignorados.

Cada link é relatado uma vez, mesmo que apareça várias vezes na página ou com âncoras diferentes, como `#pricing` e `#features`. A oportunidade destaca o primeiro lugar em que o link é exibido.

Os links que o verificador de links do AEM já marcou como inválidos são incluídos na auditoria, mesmo que o editor remova o link clicável da página. Elas são verificadas novamente, em vez de assumidas como confiáveis, para que um link que começou a funcionar desde então não seja relatado.

## Filtrar os resultados

Na página de detalhes, use o filtro ao lado do cabeçalho **Instâncias** para mostrar apenas algumas das oportunidades:

| Filtro | Oportunidades mostradas |
|---|---|
| **Todos** (padrão) | Todas as oportunidades |
| **Quebrado** | Links quebrados |
| **Precisa de verificação** | Links não verificados e links inseguros |

Se um link tiver mais de uma oportunidade, como um link inseguro que também foi desfeito, cada oportunidade será exibida em seu próprio filtro. Para obter mais informações, consulte [Instâncias de filtro](../../audit-results.md#filter-instances).

## Limitações conhecidas

* **Endereços privados:** links para endereços de rede privados ou internos, como um site de intranet, não são verificados e não são relatados.
* **Limites de tempo:** cada link tem seu próprio limite de tempo, portanto, um site lento não impede que outros links sejam verificados. Cada link na página obtém um resultado. Um link que não responde a tempo, mesmo após uma nova tentativa, é relatado como **Link não verificado** em vez de interrompido.
* **Domínios excluídos:** a configuração do site pode excluir domínios específicos da verificação. Os links para um domínio excluído ou para qualquer um de seus subdomínios não são verificados e não são relatados.
* **Modo de exibição do lado do servidor:** A comprovação verifica os links externos dos servidores da Adobe em vez de verificar no navegador. Um site que se comporta de forma diferente com base na localização, logon ou detecção de bot pode retornar um resultado diferente do que você vê no navegador. Esses links geralmente são relatados como **Link não verificado** em vez de corrompidos.

## Como resolver

Quando a auditoria encontra oportunidades, cada uma descreve o problema e a alteração recomendada e identifica o link envolvido. Use o **Destaque na página** para ir até o link em seu conteúdo e abrir a URL em uma nova guia para confirmar o problema para si mesmo. Em seguida, aproveite a oportunidade:

* **Link quebrado:** atualize o link para o novo local da página, ou substitua-o ou remova-o. Para um loop de redirecionamento, entre em contato com o proprietário do outro site ou vincule a uma origem diferente.
* **Link não seguro:** altere o link para usar `https://`, depois de confirmar que a versão segura funciona.
* **Link não verificado:** abra o link em seu navegador e confirme se ele mostra a página esperada. Para um link que requer logon, confirme se os leitores devem ter uma conta. Para um erro de servidor, verifique o link novamente antes de publicar. Se o link não funcionar, considere-o como corrompido.

Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
