---
title: Documentação de oportunidade de vulnerabilidades do site
description: Saiba mais sobre a oportunidade de vulnerabilidades do site e como usá-la para aumentar a segurança do em seu site.
badgeSecurityPosture: label="Postura de segurança" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Postura de segurança"
source-git-commit: ab2d75b1d986d83e3303e29a25d2babd1598394a
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 1%

---


# Oportunidade de vulnerabilidades do site

![Oportunidade de vulnerabilidades do site](./assets/website-vulnerabilities/hero.png){align="center"}

A oportunidade de vulnerabilidades do site identifica vulnerabilidades de segurança nas bibliotecas de terceiros usadas pelo seu código de aplicativo. Essas vulnerabilidades podem ser exploradas por um invasor mal-intencionado, aumentando o risco e diminuindo a postura de segurança do seu site.

A oportunidade de vulnerabilidades do site exibe um resumo na parte superior da página, incluindo o seguinte:

* **Problemas encontrados** - O número de vulnerabilidades encontradas, categorizadas pelo risco de segurança que representam (baixo, médio, alto).
* **Risco de segurança agregado** - O risco de segurança geral para o site com base nas vulnerabilidades encontradas pela oportunidade.

## Identificação automática

![Identificar automaticamente vulnerabilidades do site](./assets/website-vulnerabilities/auto-identify.png){align="center"}

O recurso **Oportunidade de Vulnerabilidades do Site** identifica e lista automaticamente as vulnerabilidades encontradas em bibliotecas de terceiros usadas pelo seu código de aplicativo. Ele fornece os seguintes detalhes:

* **Biblioteca** - A biblioteca de terceiros que contém a vulnerabilidade. Uma única biblioteca pode ter várias vulnerabilidades.
* **Versão Atual** - A versão da biblioteca em uso no momento.
* **Versão Recomendada** - A versão sugerida que resolve a vulnerabilidade.
* **Pontuação** - A classificação de gravidade da vulnerabilidade, também resumida na parte superior da página.
* **Vulnerabilidade** - O identificador de vulnerabilidade, uma breve descrição e um link para o Banco de Dados Nacional de Vulnerabilidades (NVD) para obter mais detalhes. Acesse o link NVD clicando no identificador ou no link ao lado da descrição.

## Sugestão automática

![Sugerir vulnerabilidades de site automaticamente](./assets/website-vulnerabilities/auto-suggest.png){align="center"}

A sugestão automática fornece sugestões geradas por IA para a **Versão recomendada** da biblioteca vulnerável para a qual você deve atualizar. Cada entrada tem uma **Pontuação** indicando sua gravidade geral, ajudando a priorizar as vulnerabilidades mais críticas.

>[!BEGINTABS]

>[!TAB Detalhes da vulnerabilidade]

Cada vulnerabilidade contém um link para as informações detalhadas no [Banco de Dados Nacional de Vulnerabilidades (NVD)](https://nvd.nist.gov/). Ao clicar no identificador de vulnerabilidade ou no item de link à direita da descrição, você será direcionado para a página NVD dessa vulnerabilidade.

>[!TAB Ignorar entradas]

Você pode optar por ignorar as entradas da lista de vulnerabilidades. Selecionar o **ícone de ignorar** remove a entrada da lista. As entradas ignoradas podem ser engajadas novamente na guia **Ignoradas**, na parte superior da página de oportunidade.<!---right now it does not seem to be implemented, but the page description mentions this functionality-->

>[!ENDTABS]


## Otimizar automaticamente o [!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![Otimizar vulnerabilidades do site automaticamente](./assets/website-vulnerabilities/auto-optimize.png){align="center"}

O Sites Optimizer Ultimate adiciona a capacidade de implantar a otimização automática para as vulnerabilidades encontradas.

>[!BEGINTABS]

>[!TAB Implantar otimização]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Solicitar aprovação]

{{auto-optimize-request-approval}}

>[!ENDTABS]