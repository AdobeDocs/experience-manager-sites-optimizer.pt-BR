---
solution: Experience Manager
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
usetq: true
product: adobe experience manager
landing-page-name: experience-manager
landing-page-breadcrumb-title: AEM
type: Documentation
description: Documentação do AEM Sites Optimizer.
index: true
git-repo: https://github.com/AdobeDocs/experience-manager-sites-optimizer.pt-BR
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: b6745249d9a773ce875f421dd16947a1a4d0a245
workflow-type: tm+mt
source-wordcount: 85
ht-degree: 2%

---


# Metadados para uso interno

O sistema de criação do GitHub organiza os metadados hierarquicamente, usando os seguintes níveis crescentes de precedentes.

1. metadata.md
1. ToC
1. Artigo

Os metadados definidos no arquivo metadata.md se aplicam a todo o repositório, mas podem ser substituídos nos níveis de índice e artigo. Qualquer substituição dos metadados deve ser feita no nível mais baixo possível.

Os metadados no repositório `experience-manager-cloud-service.en` são o mínimo necessário.

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

Artigo

* `title`
* `description`
* `contentOwner` (somente no conteúdo do ativo principal em `/help/assets`)

