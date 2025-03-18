---
title: Documentação de oportunidade da configuração do CORS
description: Saiba mais sobre a oportunidade de configuração do CORS e para identificar e corrigir vulnerabilidades de segurança do site.
badgeSecurityPosture: label="Postura de segurança" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Postura de segurança"
source-git-commit: ab2d75b1d986d83e3303e29a25d2babd1598394a
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---


# Oportunidade de configuração do CORS

![Oportunidade de configuração do CORS](./assets/cors-configuration/hero.png){align="center"}

A configuração correta do CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens) é essencial para proteger aplicativos da Web contra o acesso não autorizado aos dados. Quando o cabeçalho `Access-Control-Allow-Origin` é definido como `*`, qualquer domínio pode solicitar e receber respostas, potencialmente expondo informações confidenciais a invasores. Isso oferece uma oportunidade de fortalecer a segurança implementando uma lista de permissões controlada de domínios confiáveis ou desabilitando o CORS onde não é necessário. Garantir uma configuração segura do CORS ajuda a proteger o conteúdo privado, mantendo o acesso ininterrupto para usuários autorizados.

## Identificação automática

![Oportunidade de configuração CORS de identificação automática](./assets/cors-configuration/auto-identify.png){align="center"}

A identificação automática verifica o site em busca de erros de configuração do CORS e detecta URLs susceptíveis a acesso não autorizado. Esses URLs são listados na tabela superior, juntamente com os seguintes detalhes:

* **Prefixo de página** - O prefixo de caminho de URL vulnerável à configuração incorreta do CORS.
* **Exemplo de página** - Um exemplo de URL que é susceptível a acesso não autorizado.

## Sugestão automática

![Oportunidade de configuração de Sugestão Automática do CORS](./assets/cors-configuration/auto-suggest.png){align="center"}

Sugestão automática de **arquivos de código do aplicativo** e suas **Linhas** para revisão que podem estar definindo políticas CORS frouxas.


## Otimizar automaticamente o [!BADGE Ultimate]{type=Positive tooltip="Ultimate"}



>[!BEGINTABS]

>[!TAB Implantar otimização]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Solicitar aprovação]

{{auto-optimize-request-approval}}

>[!ENDTABS]
