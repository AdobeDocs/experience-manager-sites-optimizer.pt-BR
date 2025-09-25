---
title: Configuração de comprovação
description: Saiba como configurar a extensão Comprovação para o AEM Sites Optimizer.
source-git-commit: 6e177ef6b9d121ac7484ae118037c7e542f981d8
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Configuração de comprovação

A identificação da oportunidade de Comprovação do AEM Sites Optimizer exige a configuração da extensão de Comprovação no Universal Editor, na Visualização baseada em documentos ou no AEM Cloud Service para executar auditorias de Comprovação em suas páginas antes que elas sejam publicadas.

## Habilitar acesso do usuário

Para usar a extensão Comprovação, verifique se o usuário está atribuído a pelo menos um dos seguintes perfis de produto do AEM Sites Optimizer no [Adobe Admin Console](https://adminconsole.adobe.com):

* AEM Sites Optimizer - Sugestão automática de usuário
* AEM Sites Optimizer - Otimizar usuário automaticamente

## Ativar a extensão Comprovação

>[!BEGINTABS]

>[!TAB Editor Universal]

Para configurar a Comprovação no Universal Editor, siga estas etapas:

1. Abra o **Extension Manager** em:
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. Localize a **Extensão de Comprovação do AEM Sites Optimizer** e envie uma solicitação para habilitá-la.
1. A **equipe do Adobe AEM** revisará e habilitará a extensão para sua organização.
1. Após habilitar a extensão, abra uma página no **Editor Universal**, por exemplo:
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. A **Extensão de Comprovação** aparecerá no **painel lateral**.
1. Selecione a **Extensão de Comprovação** no painel lateral para iniciar uma **Auditoria de Comprovação** da página atual.

>[!TAB Criação baseada em documentos]

Para configurar a Comprovação para a criação baseada em documentos, siga estas etapas:

1. Adicione a seguinte configuração a `/tools/sidekick/config.json` no repositório GitHub do projeto do Edge Delivery Services:

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

1. Atualize a função `loadLazy()` em `/scripts/scripts.js` para importar o script de Comprovação para URLs de visualização:

   ```javascript
   if (window.location.href.includes('.aem.page')) {
      import('../tools/sidekick/aem-sites-optimizer-preflight.js');
   }
   ```

1. Abra a URL de visualização (`*.aem.page`) da página que deseja auditar.
1. No **Sidekick**, clique no botão **Comprovação** para iniciar a auditoria da página atual.

>[!TAB Editor de páginas do AEM Sites]

Para usar a comprovação no Editor de páginas do AEM Sites, você pode criar um bookmarklet no navegador da Web. Siga estas etapas:

1. Mostre sua **Barra de Indicadores** em seu navegador da Web:

   * Pressione **Ctrl+Shift+B** (Windows) ou **Cmd+Shift+B** (Mac).

!. Crie um novo marcador no navegador:

* Clique com o botão direito do mouse na Barra de marcadores e selecione **Nova página** ou **Adicionar marcador**.
* No campo **Endereço (URL)**, cole o seguinte código:

```javascript
javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
```

1. Nomeie o marcador **Comprovação** (ou qualquer nome que desejar).
1. Abra a URL de visualização (`*.aem.page`) da página que você deseja auditar no **Editor de Páginas do AEM Sites**.
1. Clique no marcador **Comprovação** na Barra de marcadores para iniciar a auditoria da página atual.

>[!ENDTABS]

## Práticas recomendadas

Ao executar auditorias de comprovação, lembre-se das seguintes diretrizes:

* Sempre execute auditorias em **páginas de preparo ou visualização** antes de publicar na produção.
* Priorize a resolução de **problemas de alto impacto**, como links com falha, tags H1 ausentes ou links inseguros.
* Verifique se a **autenticação está habilitada** para ambientes de preparo protegidos antes de executar auditorias.
* Revise e aplique as **recomendações de metatags** para melhorar o desempenho da SEO.
