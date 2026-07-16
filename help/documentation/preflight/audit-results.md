---
title: Resultados de auditoria na simulação
description: Saiba como interpretar os resultados da auditoria de Comprovação, o medidor de disponibilidade e as categorias de auditoria, e navegar até oportunidades na visualização.
source-git-commit: f19dd2eec5cef95f406111d2250ff1101a4fd430
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 5%

---


# Resultados de auditoria na simulação

Quando as auditorias forem concluídas, a Comprovação exibirá os resultados no painel de preparação. O painel mostra um medidor de disponibilidade geral e as oportunidades encontradas, agrupadas por categoria de auditoria. Em cada categoria, as auditorias individuais identificam itens específicos a serem revisados ou corrigidos.

## Medidor de disponibilidade

Na parte superior do painel, o medidor de prontidão reflete os resultados gerais de auditoria. Ela mostra uma pontuação de prontidão como uma porcentagem, com base na proporção de auditorias que terminaram sem oportunidades, juntamente com o número total de oportunidades encontradas em todas as auditorias. O medidor de disponibilidade ajuda a medir a integridade geral da página rapidamente.

![O medidor de preparação e as categorias de auditoria no painel de Comprovação](./assets/overview/hero.png){align="center"}

Enquanto as auditorias ainda estão em execução, o medidor de disponibilidade mostra uma barra de progresso com um status como **Executando auditorias** ou o número de auditorias ainda em execução. Quando as auditorias forem concluídas, o medidor exibirá a porcentagem final de prontidão e a contagem de oportunidades.

## Categorias de auditoria

Comprove auditorias relacionadas a grupos em categorias, como **SEO** e **Acessibilidade**. Cada categoria aparece como um cartão que mostra o número de oportunidades encontradas ou indica que todas as auditorias foram aprovadas sem oportunidades.

Expanda uma categoria para ver suas auditorias individuais. Cada auditoria mostra se passou ou encontrou oportunidades, uma breve descrição e uma contagem das oportunidades encontradas. Selecione uma auditoria que encontrou oportunidades para abrir sua página de detalhes.

Para obter a lista completa das categorias de auditoria e das auditorias em cada uma, consulte [Categorias de auditoria de comprovação](./overview.md#preflight-audit-categories).

## Detalhes da oportunidade

A página de detalhes mostra as oportunidades que a auditoria selecionada encontrou. Quando o mesmo problema ocorre em mais de um local, cada ocorrência é chamada de instância. Use o navegador (**Instância anterior** e **Próxima instância**) para percorrê-las; ele mostra sua posição, por exemplo *1 de 5 instâncias encontradas*.

![A página de detalhes de uma auditoria, mostrando uma oportunidade e sua sugestão](./assets/audit-results/audit-detail.png){align="center"}

Cada oportunidade inclui:

* Um selo de gravidade ou impacto que indica a importância da oportunidade.
* Detalhes sobre a oportunidade, como uma descrição do problema, uma recomendação e, para acessibilidade, a regra WCAG relacionada e o nível de conformidade.
* Uma seção **Elemento** que mostra o elemento afetado na página, com um botão **Realce na página**.
* Uma seção **Sugestão** com uma correção recomendada. Quando a sugestão é gerada pela IA, ela é marcada como uma sugestão gerada pela IA e pode incluir um breve raciocínio explicando a correção sugerida.

## Realçar na página

Após a conclusão das auditorias, é possível localizar e entender rapidamente uma oportunidade, destacando-a diretamente na página.

A comprovação destaca o elemento afetado no contexto, conectando o resultado no painel ao local exato no seu conteúdo. Isso facilita a análise e a resolução de oportunidades sem pesquisar manualmente pela página.

1. Abra o painel Comprovação no contexto da página para auditar e selecione **Analisar página** para executar as auditorias.
1. Selecione uma auditoria no painel de preparação e, em seguida, selecione uma oportunidade para revisar.
1. Selecione **Destaque na página**. A visualização rola automaticamente para a área relevante e realça o elemento correspondente, para que você possa identificar e otimizar facilmente a oportunidade no contexto.

## ID da tarefa

Cada execução de comprovação tem uma ID de tarefa exclusiva, mostrada na parte inferior do painel. É útil principalmente quando um administrador está solucionando problemas em uma execução específica. Passe o mouse sobre a ID e selecione o ícone de cópia que aparece à direita; a ID é copiada para a área de transferência e uma mensagem de confirmação é exibida. Inclua essa ID ao relatar um problema.
