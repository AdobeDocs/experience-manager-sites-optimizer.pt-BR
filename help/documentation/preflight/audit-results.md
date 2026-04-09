---
title: Resultados da auditoria na Comprovação
description: Saiba como interpretar os resultados da auditoria de Comprovação e a barra de Progresso do usuário, navegar até problemas na visualização e aplicar sugestões geradas por IA.
source-git-commit: 10534d1fabdd88b11f45895d39bc1afd0d664ff1
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Resultados da auditoria na Comprovação

Quando a auditoria é concluída, a Comprovação exibe os resultados da auditoria como oportunidades. Cada oportunidade é organizada por tipo e inclui recomendações para ajudá-lo a aprimorar e otimizar a página. Em uma oportunidade, problemas individuais identificam itens específicos a serem revisados ou corrigidos.

Na parte superior da caixa de diálogo Comprovação do AEM há uma barra de Progresso do usuário que reflete os resultados gerais da auditoria. Ela mostra a porcentagem de oportunidades que passaram sem problemas e o número total de problemas encontrados em todas as oportunidades. A barra de progresso do usuário ajuda os autores a medir a integridade geral da página rapidamente.

![Barra de progresso do usuário e oportunidades de auditoria na caixa de diálogo Comprovação do AEM](./assets/overview/hero.png){align="center"}

A barra é codificada por cores:

* Vermelho para **menos de 1/3** de oportunidades concluídas
* Laranja para **1/3 a 2/3 concluído**
* Verde para **mais de 2/3 concluídos**
* Azul enquanto as auditorias **ainda estão em execução**

Consulte a [lista completa de tipos de oportunidade disponíveis e como resolvê-los](./overview.md#preflight-opportunities).

## Navegar até os problemas e aplicar sugestões

Depois que a auditoria for concluída, você poderá ir rapidamente para os problemas identificados e aplicar as sugestões geradas pela IA diretamente na pré-visualização.

![Realce da visualização de comprovação e painel de sugestão de IA](./assets/audit-results/highlight-issue.png){align="center"}

### Navegar para um problema

1. Selecione um problema na lista de problemas do painel &#39;Comprovação&#39;.
1. A visualização rola automaticamente para e realça o local correspondente na página, para que você possa revisar o problema no contexto sem pesquisá-lo manualmente.

### Aplicar sugestões geradas por IA

Para problemas que incluem recomendações geradas por IA, você pode aplicar as otimizações sugeridas diretamente do painel de sugestões.

#### Aplicar uma otimização

1. Revise a sugestão gerada pela IA.
1. Selecione **Aplicar Otimização**.

O conteúdo recomendado é aplicado diretamente ao conteúdo.

#### Editar antes de aplicar

Se forem necessários ajustes:

1. Modifique a sugestão gerada pela IA no painel de sugestões.
1. Selecione **Aplicar Otimização**.

Sua versão editada é aplicada à visualização.
