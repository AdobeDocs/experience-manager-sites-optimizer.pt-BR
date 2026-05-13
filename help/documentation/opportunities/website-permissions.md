---
title: Documentação de oportunidade de permissões do site
description: Saiba mais sobre a oportunidade de permissões de site e como usá-la para aumentar a segurança em seu site.
badgeSecurityPosture: label="Postura de segurança" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Postura de segurança"
TQID: https://experienceleague.adobe.com/9nGa4iRd0cBuWSUZxLvbXXo1Rx84ZqMLnD8lF8XkayU
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 252f5292d6dc62711b4ebeb8ce5a2707857fd674
workflow-type: tm+mt
source-wordcount: 227
ht-degree: 100%

---

# Oportunidade de permissões de site

![Oportunidade de permissões de site](./assets/website-permissions/hero.png){align="center"}

A oportunidade de permissões de site otimiza as permissões do site, essenciais para manter um ambiente seguro e gerenciável do AEM. Esta oportunidade permite que você refine os controles de acesso removendo permissões muito amplas, como `jcr:all` em caminhos genéricos como `/` ou `/content`, e alinhando o acesso do usuário com o princípio do privilégio mínimo. Ao simplificar as permissões e eliminar redundâncias, você pode reduzir os riscos de segurança, melhorar a capacidade de manutenção e evitar futuras configurações incorretas. Revise e atualize as permissões no console de permissões de segurança do AEM ou no seu repositório de código. Isso garante que os usuários de serviços contem somente com o acesso de que realmente precisam.

## Identificação automática

![Identificar permissões de site automaticamente](./assets/website-permissions/auto-identify.png){align="center"}

O recurso **Oportunidade de permissões de site** identifica e lista automaticamente

* **Usuário**: a conta de usuário com a permissão suspeita.
* **Caminho**: use as guias localizadas na parte superior para organizar e filtrar as oportunidades por status.
* **Permissão**: a permissão suspeita.
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
