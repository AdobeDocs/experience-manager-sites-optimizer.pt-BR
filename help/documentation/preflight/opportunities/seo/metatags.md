---
title: Auditoria de metatags de comprovação
description: Saiba mais sobre a auditoria de Metatags em Comprovação para AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 913fd85808a08eb8f6ba7de8207d53ee7b68409e
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 1%
---
# Auditoria de metatags

A auditoria **Metatags** revisa o título da página, a meta descrição e o cabeçalho principal (H1). Ele sinaliza qualquer um deles que está ausente, vazio ou fora do comprimento recomendado e sinaliza páginas com mais de um cabeçalho H1.

## Por que é importante

O título da página e a metadescrição geralmente são o que as pessoas veem para a sua página nos resultados da pesquisa: o título como o título clicável e a descrição como o resumo abaixo dele. Um título ou uma descrição ausente ou mal dimensionada pode ser cortada ou substituída por um texto que o mecanismo de pesquisa escolhe na página. O cabeçalho H1 informa aos leitores e mecanismos de pesquisa sobre o que a página é principalmente, portanto, uma página deve ter um H1 claro.

## O que a auditoria verifica

A auditoria relata uma oportunidade para cada um dos seguintes problemas:

* **Título da página:** ausente, vazio, muito curto ou mais longo que o comprimento ideal.
* **Descrição do Meta:** ausente, vazio, muito curto ou mais longo que o comprimento ideal.
* Cabeçalho **H1:** ausente, vazio, maior que o comprimento ideal ou mais de um H1 na página.

Um valor com alguns caracteres acima do comprimento ideal é relatado como **acima do comprimento ideal**, e um ultrapassou o máximo da auditoria como **muito longo**. A comprovação não tem um limite muito longo para títulos de página.

| Tag | Comprimento ideal | Acima do comprimento ideal | Muito longo |
|---|---|---|---|
| Título da página | 40 a 60 caracteres | Mais de 60 caracteres | - |
| Descrição do Meta | 140 a 160 caracteres | 161 a 175 caracteres | Mais de 175 caracteres |
| Título H1 | Até 70 caracteres | 71 a 75 caracteres | Mais de 75 caracteres |

Esses intervalos são diretrizes recomendadas, não requisitos do mecanismo de pesquisa. A comprovação os usa para decidir quando relatar uma oportunidade.

Cada oportunidade é relatada em um dos três níveis de impacto:

* **Alta:** uma marca ausente ou vazia.
* **Moderado:** um título de página ou uma metadescrição muito curta, uma metadescrição ou H1 muito longa ou uma página com mais de um H1.
* **Baixo:** um valor acima do comprimento ideal, mas não muito longo, incluindo qualquer título de página com mais de 60 caracteres.

## Como os valores são lidos

A auditoria lê a página que você está editando: o texto do elemento `<title>`, o conteúdo da marca `<meta name="description">` e o texto visível do primeiro elemento `<h1>`, incluindo qualquer texto em negrito ou itálico dentro dele.

Uma marca está **ausente** quando a página não a possui e **vazia** quando ela está lá, mas não tem texto visível. Os comprimentos contam todos os caracteres, incluindo espaços e pontuação. Somente o primeiro H1 é verificado em relação ao comprimento. Quando uma página tem mais de um H1, cada um é listado como uma instância separada, para que você possa localizar e alterar os cabeçalhos extras.

## Sugestões

Cada oportunidade inclui uma recomendação, como o comprimento ideal para a tag ou um H1 em uma página.

O título da página, a meta descrição e as oportunidades H1 também podem incluir uma sugestão gerada por IA, escrita a partir do conteúdo da própria página. Uma sugestão é mostrada somente se se ajustar ao comprimento ideal. Revise e edite cada sugestão antes de usá-la.

Quando uma oportunidade H1 não tem sugestão de IA, sua sugestão é um conselho fixo, como encurtar o cabeçalho ou alterar cabeçalhos H1 extras para H2. Quando um título de página ou uma oportunidade de meta descrição não tem nenhuma sugestão de IA, a Comprovação mostra que nenhuma sugestão está disponível.

## Se um valor sinalizado parecer correto para você

Nas páginas do Edge Delivery Services, um título de página ou uma meta descrição que você não definiu é preenchida automaticamente a partir do primeiro cabeçalho e do primeiro parágrafo da página. Geralmente, esses são menores do que o comprimento ideal, portanto, a página é sinalizada. Configurar seu próprio título e descrição nos metadados da página resolve isso.

## Limitações conhecidas

* **Outras marcas de cabeçalho não estão marcadas**, como as marcas Open Graph para compartilhamento em redes sociais ou a marca de robôs.
* **O comprimento é contado em caracteres:** os mecanismos de pesquisa reduzem os títulos e descrições com base no espaço ocupado na tela; portanto, um valor dentro do comprimento ideal ainda pode ser reduzido nos resultados da pesquisa.
* **Idiomas sem espaços entre palavras:** em páginas de idiomas como chinês, japonês ou coreano, um valor que seja bem lido ainda pode ser sinalizado, e as sugestões de IA podem estar fora do comprimento ideal.

## Como resolver

Cada oportunidade descreve o problema e a alteração recomendada, e mostra o valor atual do título da página ou da meta descrição.

* **Título da página e meta descrição:** atualize-os onde seu site os define, por exemplo, nas propriedades de página no AEM Sites ou nos metadados de página no Edge Delivery Services. Estas marcas estão no cabeçalho da página, portanto, o **Destaque na página** não está disponível para elas.
* Cabeçalho **H1:** use **Realçar na página** para localizar o cabeçalho no seu conteúdo. No Edge Delivery Services, no Editor de páginas do AEM Sites e no Adobe Managed Services (AMS), a Comprovação rola até o cabeçalho e o contorna; o Editor de páginas e o AMS exigem o **modo de Edição**. No Editor universal, a Comprovação seleciona o cabeçalho ou o bloco editável mais próximo que o contém. Um cabeçalho na navegação ou um rodapé é exibido, mas não pode ser selecionado. Para obter mais informações, consulte [Destaque na página](../../audit-results.md#highlight-on-page).

Para saber como revisar e resolver oportunidades, consulte [Resultados de auditoria em Comprovação](../../audit-results.md).
