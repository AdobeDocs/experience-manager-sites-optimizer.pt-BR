---
title: AEM Sites Optimizer - Guia de integração de comprovação
description: Saiba mais sobre as oportunidades de simulação e como configurar a análise de simulação no AEM Sites Optimizer.
source-git-commit: 0a6ddcdfd369253500067b31617facfb7f38b656
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 6%

---


# Oportunidades de comprovação

![Oportunidades de simulação](./assets/preflight/hero.png){align="center"}

<span class="preview">A Comprovação do AEM Sites Optimizer analisa os dados técnicos e de desempenho da sua página e antecipa e detecta oportunidades antes de publicá-las. Ele usa IA gerativa para sugerir otimizações.</span>

## Oportunidades

<!-- CARDS

* ../documentation/opportunities/invalid-or-missing-metadata.md
  {title=Canonical}
  {image=../assets/common/card-link.png}
* ../documentation/opportunities/broken-internal-links.md
  {title=Broken Internal Links}
  {image=../assets/common/card-link.png}
* ../documentation/opportunities/invalid-or-missing-metadata.md
  {title=Metatags}
  {image=../assets/common/card-code.png}
* ../documentation/opportunities/invalid-or-missing-metadata.md
  {title=H1 count}
  {image=../assets/common/card-code.png}
* ../documentation/opportunities/accessibility-issues.md
  {title=Accessibility}
  {image=../assets/common/card-puzzle.png}

-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Canonical">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/invalid-or-missing-metadata.md" title="Canônico" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-link.png" alt="Canônico"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" title="Canônico">Canônico</a>
                    </p>
                    <p class="is-size-6">Saiba mais sobre a oportunidade canônica e como usá-la para melhorar o SEO e evitar problemas de conteúdo duplicado.</p>
                </div>
                <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Broken Internal Links">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/broken-internal-links.md" title="Links internos corrompidos" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-link.png" alt="Links internos corrompidos"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/broken-internal-links.md" target="_blank" rel="referrer" title="Links internos corrompidos">Links Internos Desfeitos</a>
                    </p>
                    <p class="is-size-6">Saiba mais sobre a oportunidade de links internos corrompidos e como usá-la para identificar e corrigir links corrompidos ou problemáticos em seu site.</p>
                </div>
                <a href="../documentation/opportunities/broken-internal-links.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Metatags">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/invalid-or-missing-metadata.md" title="Metatags" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-code.png" alt="Metatags"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" title="Metatags">Metatags</a>
                    </p>
                    <p class="is-size-6">Saiba mais sobre a oportunidade de metatags e como usá-la para otimizar os metadados da página, a fim de melhorar o desempenho do SEO.</p>
                </div>
                <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="H1 count">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/invalid-or-missing-metadata.md" title="Contagem H1" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-code.png" alt="Contagem H1"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" title="Contagem H1">Contagem H1</a>
                    </p>
                    <p class="is-size-6">Saiba mais sobre a oportunidade de contagem H1 e como usá-la para garantir a estrutura de cabeçalho adequada e a otimização de SEO.</p>
                </div>
                <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Accessibility">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/accessibility-issues.md" title="Acessibilidade" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-puzzle.png" alt="Acessibilidade"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/accessibility-issues.md" target="_blank" rel="referrer" title="Acessibilidade">Acessibilidade</a>
                    </p>
                    <p class="is-size-6">Saiba mais sobre a oportunidade de acessibilidade e como usá-la para garantir que seu site seja acessível a todos os usuários.</p>
                </div>
                <a href="../documentation/opportunities/accessibility-issues.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>

</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Como configurar

### Configuração do editor universal

1. Acesse o Extension Manager pelo URL: https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor
2. Selecione a extensão e a solicitação do AEM Sites Optimizer Preflight para ativar o
3. A equipe da AEM habilitará a extensão para sua organização
4. Depois disso, abra uma página no Universal Editor, como: https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/site/subscription.html
5. A extensão Comprovação estará visível no painel lateral
6. Clicar na extensão Comprovação no painel lateral iniciará a Auditoria de comprovação da página atual

### Configuração de Visualização Baseada em Documento

#### Etapa 1: ativar o Sidekick com o botão de comprovação

Adicione a seguinte configuração a `/tools/sidekick/config.json` em seu repositório GitHub:

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

#### Etapa 2: criar o script de integração do Sidekick

Criar `/tools/sidekick/aem-sites-optimizer-preflight.js` com o seguinte conteúdo:

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

#### Etapa 3: Atualizar Arquivo de Scripts

Adicione a seguinte instrução de importação à função `loadLazy()` em `/scripts/scripts.js` para URLs de visualização, conforme mostrado abaixo:

```javascript
if (window.location.href.includes('.aem.page')) {
   import('../tools/sidekick/aem-sites-optimizer-preflight.js');
}
```

Agora, o botão Comprovação deve estar visível no Sidekick.

#### Etapa 4: Execução da auditoria

Abra o URL de visualização (*.aem.page) da página auditada. Clique no botão Comprovação no Sidekick.

### Configuração do AEM Cloud Service

Você pode usar a opção de bookmarklet para testar a Comprovação em editores de página e ambientes de sandbox do AEM Cloud Service.

<!-- Drag the button below to your Bookmarks Bar to get started. -->

Pressione **Ctrl+Shift+B** (Windows) ou **Cmd+Shift+B** (Mac) para mostrar a Barra de Marcadores. Clique com o botão direito do mouse na barra de favoritos e selecione &quot;Nova página&quot; ou &quot;Adicionar favorito&quot;. No campo de endereço, copie o código abaixo.

<!-- **Drag this link to your Bookmarks Bar:**

<a href="javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();">Preflight</a> -->

**Copiar este código e criar um novo indicador:**

```
javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
```

Depois que o Bookmarklet for adicionado, abra o URL de visualização (*.aem.page) da página auditada. Clique no marcador Comprovação para iniciar a Auditoria de comprovação.

## Práticas recomendadas

Ao usar a comprovação, esteja ciente do seguinte:

* Execute auditorias de Comprovação em todas as páginas de preparo/visualização antes de publicar.
* Resolva os problemas de alto impacto primeiro (links quebrados, tags H1 ausentes, links inseguros).
* Ativar autenticação para ambientes de preparo protegidos.
* Revise e implemente sugestões de meta tags para melhorar o desempenho da SEO.
