---
title: Executar auditorias no Preflight
description: Saiba como iniciar uma auditoria com o Preflight na sua página.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: ae16300fdfd525dc5efead2f165d5a238b5ea6e1
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 17%
---

# Auditorias no Preflight

O Preflight audita a página para identificar oportunidades para aprimorar o conteúdo antes da publicação. Diferentemente de uma verificação automática, você escolhe quando executar as auditorias para analisar uma página quando estiver pronto.

![A tela de aterrissagem de Comprovação com o botão Analisar página](./assets/audits/hero.png){align="center"}

Para executar auditorias com o Preflight em uma página:

1. Abra a página que deseja auditar em seu [ambiente de criação](./access-preflight.md) (Editor universal, Criação baseada em documento ou Editor de páginas do AEM Sites).
1. Abra o [painel do Preflight](./access-preflight.md). A simulação abre na tela de aterrissagem **Executar auditoria de preparação de desempenho**.
1. Se necessário, abra **Configurações** (o ícone de engrenagem) para incluir links de navegação do site na auditoria de Links internos. Essa configuração está desativada por padrão e não está disponível no Editor universal. Dependendo do seu ambiente, as **Configurações** aparecem no cabeçalho ou em **Mais ações** (**...**). Consulte [Incluir links de navegação do site](./opportunities/seo/internal-links.md#include-site-navigation-links).
1. Selecione **Analisar página**. A simulação executa todas as suas auditorias na página atual e abre o painel de preparação, onde exibe a porcentagem de auditorias aprovadas e as oportunidades encontradas, agrupadas por categoria.

Para entender os resultados de visualização e identificar oportunidades de otimização, consulte [Resultados de auditoria em Comprovação](./audit-results.md).

## Usar o botão de comprovação integrado

Se o ambiente do autor estiver executando o [AEM 2026.7.0 (versão 27083)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/maintenance/2026/2026-7-0#release-27083) ou posterior, a Comprovação será incorporada na barra de ferramentas do Editor de páginas do AEM Sites. Selecione o ícone **Comprovação** (o botão Reproduzir) para abrir o painel da página atual e selecione **Analisar página** para executar as auditorias.

>[!VIDEO](https://video.tv.adobe.com/v/3496629?learn=on&enablevpops)

## Continuar uma sessão anterior

A comprovação lembra da execução mais recente, de modo que não é necessário executar novamente as auditorias se você sair e voltar.

* Se você reabrir o painel Comprovação na **mesma guia do navegador**, inclusive depois de uma atualização, a Comprovação carregará os resultados da última execução automática.
* Se você retornar **em uma nova guia ou depois de fechar o navegador**, a tela de aterrissagem mostrará um botão **Continuar última sessão** ao lado de **Analisar página**. Selecione **Continuar última sessão** para recarregar os resultados mais recentes ou selecione **Analisar página** para iniciar uma nova execução.

A comprovação rastreia a execução mais recente separadamente para cada página, portanto, o **Continuar última sessão** sempre recarregará a última execução para a página em que você está.

Quando você recarregar uma execução anterior, o cabeçalho mostrará há quanto tempo essa execução foi executada (por exemplo, *2 minutos atrás* ou *ontem*) para que você possa ter uma ideia geral da atualidade dos resultados. O rótulo é atualizado conforme o tempo passa e permanece visível à medida que você se move entre o painel de preparação e as páginas de detalhes de auditoria.

Quando as auditorias terminarem e os resultados forem exibidos, selecione **Reanalisar** na barra de ferramentas para descartar os resultados e executar cada auditoria novamente. Consulte [Resultados de auditoria em Comprovação](./audit-results.md#toolbar).
