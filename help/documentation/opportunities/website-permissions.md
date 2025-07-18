---
title: Documentação de oportunidade de permissões do site
description: Saiba mais sobre a oportunidade de permissões de site e como usá-la para aumentar a segurança em seu site.
badgeSecurityPosture: label="Postura de segurança" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Postura de segurança"
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 79%

---


# Oportunidade de permissões de site

![Oportunidade de permissões de site](./assets/website-permissions/hero.png){align="center"}

A oportunidade de permissões de site otimiza as permissões do site, essenciais para manter um ambiente seguro e gerenciável do AEM. Esta oportunidade permite que você refine os controles de acesso removendo permissões muito amplas, como `jcr:all` em caminhos genéricos como `/` ou `/content`, e alinhando o acesso do usuário com o princípio do privilégio mínimo. Ao simplificar as permissões e eliminar redundâncias, você pode reduzir os riscos de segurança, melhorar a capacidade de manutenção e evitar futuras configurações incorretas. Revise e atualize permissões no console Permissões de segurança do AEM ou no repositório de códigos. Isso garante que os usuários de serviço tenham somente o acesso de que realmente precisam.

## Identificação automática

![Identificar permissões de site automaticamente](./assets/website-permissions/auto-identify.png){align="center"}

O recurso **Oportunidade de permissões de site** identifica e lista automaticamente

* **Usuário**: a conta de usuário com a permissão suspeita.
* **Caminho** - Use as guias na parte superior para organizar e filtrar oportunidades por status.
* **Permissão** - A permissão suspeita.
* **Problema**: indica o tipo de problema que afeta a permissão.

## Sugestão automática

![Sugerir vulnerabilidades do site automaticamente](./assets/website-permissions/auto-suggest.png){align="center"}

A sugestão automática fornece recomendações geradas por IA no campo **Permissões sugeridas**, permitindo que você substitua as permissões sinalizadas por alternativas seguras.

## Otimizar automaticamente

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![Otimizar permissões de site automaticamente](./assets/website-permissions/auto-optimize.png){align="center"}

O Sites Optimizer Ultimate adiciona a capacidade de implantar a otimização automática para as vulnerabilidades encontradas.

>[!BEGINTABS]

>[!TAB Implantar otimização]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Solicitar aprovação]

{{auto-optimize-request-approval}}

>[!ENDTABS]
