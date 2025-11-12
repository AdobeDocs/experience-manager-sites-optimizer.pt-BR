---
title: Configurações de simulação
description: Saiba como configurar a extensão do Preflight para o AEM Sites Optimizer.
source-git-commit: 210acc5337796707ced10f2b84d473503fc06088
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 100%

---


# Configurações de simulação

A identificação da oportunidade de simulação do AEM Sites Optimizer exige a configuração da extensão de simulação no Universal Editor, na visualização baseada em documentos ou no AEM Cloud Service para executar auditorias de simulação das suas páginas antes que elas sejam publicadas.

## Habilitar acesso do usuário

Para usar a extensão de simulação, certifique-se de que o usuário tenha sido atribuído a pelo menos um dos seguintes perfis de produtos do AEM Sites Optimizer no [Adobe Admin Console](https://adminconsole.adobe.com):

* AEM Sites Optimizer: sugerir usuário automaticamente
* AEM Sites Optimizer: otimizar usuário automaticamente

## Habilitar a extensão de simulação

>[!BEGINTABS]

>[!TAB Universal Editor]

Para configurar a simulação no Universal Editor, siga estas etapas:

1. Abra o **Extension Manager** em:
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. Localize a **Extensão de simulação do AEM Sites Optimizer** e envie uma solicitação para habilitá-la.
1. A **equipe do Adobe AEM** analisará e habilitará a extensão para a sua organização.
1. Após habilitar a extensão, abra uma página no **Universal Editor**, como, por exemplo:
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. A **Extensão de simulação** aparecerá no **painel lateral**.
1. Selecione a **Extensão de simulação** no painel lateral para iniciar a **Auditoria de simulação** da página atual.

>[!TAB Criação baseada em documentos]

Para configurar a simulação para criação baseada em documentos, siga estas etapas:

1. Adicione a seguinte configuração a `/tools/sidekick/config.json` no repositório do GitHub do seu projeto do Edge Delivery Services:

   ```json
   {
     "plugins": [
       {
         "id": "preflight",
         "titleI18n": {
           "en": "Preflight"
         },
         "environments": ["preview"],
         "event": "preflight"
       }
     ]
   }
   ```

1. Crie um novo arquivo `/tools/sidekick/aem-sites-optimizer-preflight.js` e adicione o seguinte conteúdo:

   ```javascript
   (function () {
     let isAEMSitesOptimizerPreflightAppLoaded = false;
     function loadAEMSitesOptimizerPreflightApp() {
       const script = document.createElement('script');
       script.src = 'https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=plugin';
       script.onload = function () {
         isAEMSitesOptimizerPreflightAppLoaded = true;
       };
       script.onerror = function () {
         console.error('Error loading AEMSitesOptimizerPreflightApp.');
       };
       document.head.appendChild(script);
     }
   
     function handlePluginButtonClick() {
       if (!isAEMSitesOptimizerPreflightAppLoaded) {
         loadAEMSitesOptimizerPreflightApp();
       }
     }
   
     // Sidekick V1 extension support
     const sidekick = document.querySelector('helix-sidekick');
     if (sidekick) {
       sidekick.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('helix-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   
     // Sidekick V2 extension support
     const sidekickV2 = document.querySelector('aem-sidekick');
     if (sidekickV2) {
       sidekickV2.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('aem-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   }());
   ```

1. Atualize a função `loadLazy()` em `/scripts/scripts.js` para importar o script de simulação para URLs de pré-visualização:

   ```javascript
   if (window.location.href.includes('.aem.page')) {
      import('../tools/sidekick/aem-sites-optimizer-preflight.js');
   }
   ```

1. Abra o URL de pré-visualização (`*.aem.page`) da página que deseja auditar.
1. No **Sidekick**, clique no botão **Simulação** para iniciar a auditoria da página atual.

>[!TAB Editor de páginas do AEM Sites]

Para usar a simulação no editor de páginas do AEM Sites, você pode criar um marcador no seu navegador da web. Siga estas etapas:

1. Exiba a **Barra de marcadores** do seu navegador da web:

   * Pressione **Ctrl+Shift+B** (Windows) ou **Cmd+Shift+B** (Mac).

1. Crie um novo marcador no seu navegador:

   * Clique com o botão direito do mouse na barra de marcadores e selecione **Nova página** ou **Adicionar marcador**.
   * No campo **Endereço (URL)**, cole o seguinte código:

   ```javascript
   javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
   ```

1. Nomeie o marcador **Simulação** (ou qualquer nome que preferir).
1. Abra o URL de pré-visualização (`*.aem.page`) da página que deseja auditar no **Editor de páginas do AEM Sites**.
1. Clique no marcador **Simulação**, na barra de marcadores, para iniciar a auditoria da página atual.

>[!ENDTABS]

## Práticas recomendadas

Ao executar auditorias de simulação, lembre-se das seguintes diretrizes:

* Sempre execute auditorias em **páginas de preparo ou pré-visualização** antes de publicar na produção.
* Priorize a resolução de **problemas de alto impacto**, como links corrompidos, tags H1 ausentes ou links inseguros.
* Verifique se a **autenticação está habilitada** para ambientes de preparo protegidos antes de executar auditorias.
* Revise e aplique as **recomendações de metatags** para melhorar o desempenho da SEO.
