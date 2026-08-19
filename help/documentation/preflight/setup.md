---
title: Configurações de simulação
description: Saiba como configurar a Comprovação no AEM Sites Optimizer.
TQID: https://experienceleague.adobe.com/GfLmEEBoSP2481ZZUjRyyfMjExGgI0l9yMAqTF8ObcY
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
source-git-commit: 9edf940bffa7407ca58ea9f504ea8afe4bdd7a50
workflow-type: tm+mt
source-wordcount: 896
ht-degree: 47%

---

# Configurações de simulação

A execução da comprovação exige a sua configuração no ambiente de criação. Você pode configurar a Comprovação para o Editor universal, Criação baseada em documento, Editor de páginas do AEM Sites ou Adobe Managed Services, de modo que possa executar auditorias de Comprovação em suas páginas antes que elas sejam publicadas.

## Habilitar acesso do usuário

Para usar a Comprovação, verifique se o usuário está atribuído a pelo menos um dos seguintes perfis de produto do AEM Sites Optimizer no [Adobe Admin Console](https://adminconsole.adobe.com):

* AEM Sites Optimizer: sugerir usuário automaticamente
* AEM Sites Optimizer: otimizar usuário automaticamente

## Ativar simulação

>[!BEGINTABS]

>[!TAB Universal Editor]

Para configurar a simulação no Universal Editor, siga estas etapas:

1. Abra o **Extension Manager** em:
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. Localizar a extensão de **Simulação do AEM Sites Optimizer**.
1. O administrador de sistema da organização precisará habilitar essa extensão.
1. Após habilitar a extensão, abra uma página no **Universal Editor**, como, por exemplo:
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. A **Extensão do Preflight** aparece no **painel lateral**.
1. Selecione a **Extensão de simulação** no painel lateral para abrir a simulação para a página atual.

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

1. Abra o URL de visualização (`*.aem.page`) da página que deseja auditar.
1. No **Sidekick**, clique no botão **Comprovação** para abrir a Comprovação da página atual.

>[!TAB Editor de páginas do AEM Sites]

Se o ambiente do autor estiver executando o [AEM 2026.7.0 (versão 27083)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/maintenance/2026/2026-7-0#release-27083) ou posterior, a Comprovação será incorporada ao Editor de páginas do AEM Sites e nenhum bookmarklet será necessário. Siga estas etapas:

1. Abra a página que deseja auditar no **editor de páginas do AEM Sites**.
1. Na barra de ferramentas do editor, selecione o ícone **Comprovação** (o botão Reproduzir, destacado abaixo) para abrir o painel Comprovação da página atual.

   ![O ícone de Comprovação na barra de ferramentas do Editor de Páginas do AEM Sites](./assets/setup/toolbar-preflight-button.png){align="center"}

>[!NOTE]
>
>Não vê o ícone **Comprovação** na barra de ferramentas? Verifique o seguinte:
>
>* **Versão com suporte** — o botão integrado requer o AEM 2026.7.0 (versão 27083) ou posterior. Em versões anteriores, use o método bookmarklet abaixo.
>* **Implantação** — o botão integrado está sendo habilitado para organizações em estágios, portanto, talvez ele ainda não tenha chegado à sua organização, mesmo em uma versão com suporte. Até que isso aconteça, use o método de bookmarklet abaixo ou entre em contato com a Adobe ou com o administrador.
>* **Acesso à página** — o botão aparece somente quando você tem acesso de edição à página.
>* **Acesso do usuário** — Confirme se o **AEM Sites Optimizer - Usuário de Sugestão Automática** ou o **AEM Sites Optimizer - Perfil de Usuário de Otimização Automática** foi atribuído ao seu usuário. Consulte [Habilitar acesso de usuário](#enable-user-access).

Para usar a opção Comprovação no Editor de páginas do AEM Sites em versões anteriores do AEM, você pode criar um bookmarklet no navegador da Web. Siga estas etapas:

1. Exiba a **Barra de marcadores** do seu navegador da web:

   * Pressione **Ctrl+Shift+B** (Windows) ou **Cmd+Shift+B** (Mac).

1. Crie um novo marcador no seu navegador:

   * Clique com o botão direito do mouse na barra de marcadores e selecione **Nova página** ou **Adicionar marcador**.
   * No campo **Endereço (URL)**, cole o seguinte código:

   ```javascript
   javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
   ```

1. Nomeie o marcador **Simulação** (ou qualquer nome que preferir).
1. Abra o URL de visualização (`*.aem.page`) da página que você deseja auditar no **Editor de páginas do AEM Sites**.
1. Clique no marcador **Comprovação** na Barra de marcadores para abrir a Comprovação da página atual.

>[!TAB Adobe Managed Services]

>[!IMPORTANT]
>
>Somente os ambientes do Adobe Managed Services (AMS) que usam o Provedor de identidade (IMS) da Adobe para autenticação no AEM Author são compatíveis. O Preflight não funcionará se sua organização usar qualquer outro provedor de identidade para autenticação AMS.

Quando a Comprovação é criada na barra de ferramentas do Editor de páginas do AEM Sites, nenhum bookmarklet é necessário. Entre em contato com a Adobe para instalá-la em sua organização. Após a instalação, siga estas etapas:

1. Abra a página que deseja auditar no **editor de páginas do AEM Sites**.
1. Na barra de ferramentas do editor, selecione o ícone **Comprovação** (o botão Reproduzir, destacado abaixo) para abrir o painel Comprovação da página atual.

   ![O ícone de Comprovação na barra de ferramentas do Editor de Páginas do AEM Sites](./assets/setup/toolbar-preflight-button.png){align="center"}

>[!NOTE]
>
>Não vê o ícone **Comprovação** na barra de ferramentas? O botão integrado pode ainda não estar instalado para a sua organização. Entre em contato com o Adobe para instalá-lo ou use o método de bookmarklet abaixo.

Para usar a comprovação no Editor de páginas do AEM Sites em um ambiente AMS sem o ícone da barra de ferramentas, crie um bookmarklet no navegador da Web, seguindo estas etapas:

1. Exiba a **Barra de marcadores** do seu navegador da web:

   * Pressione **Ctrl+Shift+B** (Windows) ou **Cmd+Shift+B** (Mac).

1. Crie um novo marcador no seu navegador:

   * Clique com o botão direito do mouse na barra de marcadores e selecione **Nova página** ou **Adicionar marcador**.
   * No campo **Endereço (URL)**, cole o seguinte código:

   ```javascript
   javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=ams';document.head.appendChild(script);})();
   ```

1. Nomeie o marcador **Simulação** (ou qualquer nome que preferir).
1. Abra a página que deseja auditar no **editor de páginas do AEM Sites**.
1. Clique no marcador **Comprovação** na Barra de marcadores para abrir a Comprovação da página atual.

>[!ENDTABS]

## Práticas recomendadas

Ao executar auditorias de simulação, lembre-se das seguintes diretrizes:

* Sempre execute auditorias em **páginas de preparo ou pré-visualização** antes de publicar na produção.
* Priorize a resolução de **problemas de alto impacto**, como links corrompidos, tags H1 ausentes ou links inseguros.
* Certifique-se de que **a autenticação esteja ativada** nos ambientes de teste protegidos antes de executar auditorias.
* Revise e aplique as **recomendações de metatags** para melhorar o desempenho da SEO.
