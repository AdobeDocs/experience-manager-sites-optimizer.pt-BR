---
title: Documentação de oportunidade da configuração do CORS
description: Saiba mais sobre a oportunidade de configuração do CORS e de identificar e corrigir vulnerabilidades de segurança do site.
badgeSecurityPosture: label="Postura de segurança" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Postura de segurança"
TQID: https://experienceleague.adobe.com/z-8fvRSLN71AnJ4Y6n9TnHGHoOEAAjt8AbVJY9RG-C0
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 252f5292d6dc62711b4ebeb8ce5a2707857fd674
workflow-type: tm+mt
source-wordcount: 199
ht-degree: 100%

---

# Oportunidade de configuração do CORS

![Oportunidade de configuração do CORS](./assets/cors-configuration/hero.png){align="center"}

A configuração correta do CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens) é essencial para proteger aplicativos da Web contra o acesso não autorizado aos dados. Quando o cabeçalho `Access-Control-Allow-Origin` é definido como `*`, qualquer domínio pode solicitar e receber respostas, potencialmente expondo informações confidenciais a invasores. Essa funcionalidade oferece uma oportunidade de fortalecer a segurança, implementando-se uma lista de permissões controlada de domínios confiáveis ou desabilitando-se o CORS quando desnecessário. Garantir uma configuração segura do CORS ajuda a proteger o conteúdo privado, mantendo o acesso ininterrupto para usuários autorizados.

## Identificação automática

![Identificar automaticamente oportunidade de configuração do CORS](./assets/cors-configuration/auto-identify.png){align="center"}

A identificação automática verifica o site em busca de erros de configuração do CORS e detecta URLs suscetíveis a acesso não autorizado. Esses URLs são listados na tabela superior, juntamente com os seguintes detalhes:

* **Prefixo de página**: o prefixo de caminho de URL vulnerável à configuração incorreta do CORS.
* **Exemplo de página**: um exemplo de URL que é suscetível a acesso não autorizado.

## Sugestão automática

![Sugerir automaticamente oportunidade de configuração do CORS](./assets/cors-configuration/auto-suggest.png){align="center"}

A sugestão automática fornece **Arquivos de código de aplicativo** e suas **Linhas** a serem revisadas, o que pode estar definindo políticas de CORS inadequadas.


## Otimizar automaticamente

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

>[!BEGINTABS]

>[!TAB Implantar otimização]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Solicitar aprovação]

{{auto-optimize-request-approval}}

>[!ENDTABS]
