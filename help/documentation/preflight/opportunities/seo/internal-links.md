---
title: Auditoria de links internos de comprovação
description: Saiba mais sobre a auditoria de Links internos em Comprovação para AEM Sites Optimizer.
source-git-commit: d87b607248efdeecf1ba29ede03bf1628d1dff30
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%
---
# Auditoria de Links internos

A auditoria de **Links internos** analisa os links na sua página que apontam para o seu próprio site. A auditoria verifica cada link interno da página que você está editando e sinaliza aqueles que estão quebrados, inseguros ou apontados para algum lugar que um visitante não pode seguir.

## Por que é importante

Um link interno quebrado é um beco sem saída para o leitor e um rastreo desperdiçado para um mecanismo de busca, que não passa nenhum valor para a página que deveria alcançar. Links internos também são o tipo mais fácil de quebrar por acidente: uma página é movida ou renomeada, e cada link para ela silenciosamente para de funcionar. Como os links estão todos no seu próprio site, eles também são aqueles que você pode corrigir a si mesmo.

## O que a auditoria verifica

A auditoria relata uma oportunidade para cada link interno que tem um dos seguintes problemas:

* **Link quebrado:** o link retorna um erro, como `Status 404` ou `Status 500`. Um link que atinge o erro após um redirecionamento é relatado da mesma forma.
* **Link não seguro:** o link usa `http://` em vez de `https://`. Quando a versão segura do mesmo URL funcionar, a Comprovação oferecerá como sugestão.
* **URL do Editor:** o link aponta para uma URL do editor do AEM em vez da página de conteúdo. O link funciona durante a criação, que é o que facilita a perda, mas cada visitante acessa a interface de criação do. A comprovação sugere o URL do conteúdo.
* **Fragmento ausente:** o link aponta para uma âncora, como `#pricing`, que a página de destino não tem. A página ainda abre, mas o leitor chega no topo dela em vez da seção desejada, portanto, isso é relatado com um impacto menor do que um link quebrado. Se a página tiver a mesma âncora com maiúsculas diferentes, a opção Comprovação sugerirá a âncora corrigida. Se a própria página de destino estiver corrompida, ela será relatada como **Link interrompido**.
* **Link não verificado:** a verificação atingiu o tempo limite ou encontrou um erro de rede. A comprovação não pode informar se o link funciona, portanto, ela solicita que você verifique o link sozinho em vez de relatá-lo como corrompido.

Um link que é resolvido com sucesso não é sinalizado, mesmo quando tem vários redirecionamentos no caminho. Nenhum é um link que redireciona para um site diferente, porque não é mais um link interno.

## Como os links são verificados

A auditoria verifica os links da sua sessão de criação, para que eles sejam exibidos da maneira que você está conectado. Uma página que existe somente na instância do autor é resolvida corretamente em vez de parecer corrompida.

Os links que o verificador de links do AEM já marcou como inválidos são incluídos na auditoria, mesmo que o editor remova o link clicável da página. Eles são então verificados novamente, em vez de considerados confiáveis, para que um link que tenha começado a funcionar desde então não seja relatado.

Uma oportunidade é relatada para cada local em que um link é exibido, portanto, um link incorreto usado em três pontos fornece três instâncias para correção, cada uma destacando seu próprio ponto na página. Quando um desses pontos tiver mais de um problema, o comando Comprovação os mostrará juntos em uma única placa.

## Limitações conhecidas

A auditoria é executada no Editor de páginas do AEM Sites, no Adobe Managed Services (AMS) e na criação baseada em documentos por meio da Sidekick. No momento, ela não está disponível no Editor universal.

## Como resolver

Quando a auditoria encontra oportunidades, cada uma descreve o problema e a alteração recomendada e identifica o link envolvido. Use o **Destaque na página** para ir para o link em seu conteúdo e use a seção **URL Atual** para copiar a URL ou abri-la em uma nova guia, para que você possa confirmar o problema. Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
