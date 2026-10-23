---
title: Auditoria de links internos de comprovação
description: Saiba mais sobre a auditoria de Links internos em Comprovação para AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 59c097682899889aa2a5d76333f80cc58e28ff1e
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 0%
---
# Auditoria de Links internos

A auditoria de **Links internos** analisa os links na sua página que apontam para o seu próprio site. A auditoria verifica cada link interno da página que você está editando e sinaliza aqueles que estão quebrados, inseguros ou apontados para algum lugar que um visitante não pode seguir.

## Por que é importante

Um link interno quebrado é um beco sem saída para o leitor e um rastreo desperdiçado para um mecanismo de busca, que não passa nenhum valor para a página que deveria alcançar. Links internos também são o tipo mais fácil de quebrar por acidente: uma página é movida ou renomeada, e cada link para ela silenciosamente para de funcionar. Como os links estão todos no seu próprio site, eles também são aqueles que você pode corrigir a si mesmo.

## O que a auditoria verifica

A auditoria relata uma oportunidade para cada link interno que tem um dos seguintes problemas:

* **Link corrompido:** o link retorna um erro, como `Status 403` ou `Status 404`, ou ainda retorna `Status 500` ou `Status 501` depois que a simulação tenta novamente. Um link que atinge o erro após um redirecionamento é relatado da mesma forma.
* **Link não seguro:** o link usa `http://` em vez de `https://`. Quando a versão segura do mesmo URL funcionar, a Comprovação oferecerá como sugestão.
* **URL do Editor:** o link aponta para uma URL do editor do AEM em vez da página de conteúdo. O link funciona durante a criação, que é o que facilita a perda, mas cada visitante acessa a interface de criação do. A comprovação sugere o URL do conteúdo.
* **Fragmento ausente:** o link aponta para uma âncora, como `#pricing`, que a página de destino não tem. A página ainda abre, mas o leitor chega no topo dela em vez da seção desejada, portanto, é menos sério do que um link quebrado. Se a página tiver a mesma âncora com maiúsculas diferentes, a opção Comprovação sugerirá a âncora corrigida. Se a própria página de destino estiver corrompida, ela será relatada como **Link interrompido**.
* **Link não verificado:** a verificação atingiu o tempo limite ou encontrou um erro de rede, ou o link continuou retornando `Status 429` (muitas solicitações) ou um erro de servidor diferente de `Status 500` ou `Status 501`, como `Status 503`. A comprovação não pode informar se o link funciona, portanto, ela solicita que você verifique o link sozinho em vez de relatá-lo como corrompido.

Um link que é resolvido com sucesso não é sinalizado, mesmo quando tem vários redirecionamentos no caminho. Nenhum é um link que redireciona para um site diferente, porque não é mais um link interno.

## Como os links são verificados

A auditoria verifica os links da sua sessão de criação, para que eles sejam exibidos da maneira que você está conectado. Uma página que existe somente na instância do autor é resolvida corretamente em vez de parecer corrompida. Como o site está em execução e você está conectado, um erro como `Status 403` ou `Status 500` aponta para um problema com a página vinculada.

Os links que o verificador de links do AEM já marcou como inválidos são incluídos na auditoria, mesmo que o editor remova o link clicável da página. Eles são então verificados novamente, em vez de considerados confiáveis, para que um link que tenha começado a funcionar desde então não seja relatado.

Quando o tempo limite de uma verificação é atingido, ocorre um erro de rede, retorna `Status 429` ou um erro de servidor, a simulação repete o link mais duas vezes. Um link que funciona em uma tentativa não é relatado.

Uma oportunidade é relatada para cada local em que um link é exibido, portanto, um link incorreto usado em três pontos fornece três instâncias para correção, cada uma destacando seu próprio ponto na página. Quando um desses pontos tiver mais de um problema, o comando Comprovação os mostrará juntos em uma única placa.

## Incluir links de navegação do site

Por padrão, a auditoria de Links internos ignora os links de navegação do site. Esses links não estão verificados nem são relatados. Um link no corpo da página ainda será verificado, mesmo se o mesmo URL também aparecer em um menu.

Um link conta como navegação se o próprio link ou qualquer ancestral for um elemento `<nav>` ou tiver um atributo `role="navigation"`.

Para incluir links de navegação na próxima execução de auditoria:

1. Antes de iniciar uma auditoria ou depois que uma execução terminar, abra **Configurações** (o ícone de engrenagem) no cabeçalho Comprovação. Se o ícone de engrenagem não estiver visível, abra **Mais ações** (**...**) e selecione **Configurações**.
1. Selecione **Mostrar links de navegação do site**.
1. Selecione **Analisar página** para iniciar uma execução ou **Reanalisar** se os resultados já estiverem exibidos.

![O menu Configurações de Comprovação com a opção Mostrar links de navegação do site](./assets/internal-links/settings-menu.png){align="center"}

**Mostrar links de navegação do site** controla quais links são verificados pela auditoria, e não apenas quais resultados são exibidos.

A alteração da configuração não inicia uma auditoria nem altera os resultados já exibidos na tela. Quando esses resultados usarem uma configuração diferente, um ponto aparecerá em **Reanalyze**, com o rótulo **Reanalyze para aplicar as novas configurações**. Execute as auditorias novamente para aplicar a alteração ou restaure a configuração anterior para limpar o ponto.

A comprovação salva a configuração no navegador e a retém depois que você sai. Guias no mesmo site compartilham a configuração. Para ignorar os links de navegação novamente, desmarque **Mostrar links de navegação do site** antes da próxima execução.

A configuração não está disponível durante a execução de auditorias.

## Filtrar os resultados

Na página de detalhes, use o filtro ao lado do cabeçalho **Instâncias** para mostrar apenas algumas das oportunidades:

| Filtro | Oportunidades mostradas |
|---|---|
| **Todos** (padrão) | Todas as oportunidades |
| **Quebrado** | Links quebrados e URLs do editor |
| **Precisa de verificação** | Links inseguros, fragmentos ausentes e links não verificados |

Um link `http://` inseguro cuja versão `https://` está quebrada tem duas oportunidades no mesmo cartão. **Quebrado** mostra somente a oportunidade de link quebrado, e **Precisa de verificação** mostra somente a oportunidade de link inseguro. Para obter mais informações, consulte [Instâncias de filtro](../../audit-results.md#filter-instances).

## Limitações conhecidas

A auditoria é executada no Editor de páginas do AEM Sites, no Adobe Managed Services (AMS) e na criação baseada em documentos por meio da Sidekick. No momento, ela não está disponível no Editor universal.

## Como resolver

Quando a auditoria encontra oportunidades, cada uma descreve o problema e a alteração recomendada e identifica o link envolvido. Use o **Destaque na página** para ir para o link em seu conteúdo e use a seção **URL Atual** para copiar a URL ou abri-la em uma nova guia, para que você possa confirmar o problema. Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
