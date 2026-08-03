---
title: Notas de versão
description: Saiba mais sobre os novos recursos, melhorias e correções de erros mais recentes no Adobe Experience Manager Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: c3279d62d56503108a6c28389cfbf14b95cd5a1a
workflow-type: tm+mt
source-wordcount: 1803
ht-degree: 0%

---


# Notas de versão

Esta página documenta as atualizações mais recentes, os novos recursos e as melhorias no Adobe Experience Manager Sites Optimizer.

Os recursos marcados como **(Acesso antecipado)** estão disponíveis mediante solicitação — entre em contato com a equipe de sua conta ou o Engenheiro de sucesso do cliente para habilitá-los para sua organização.

## 1-19 de julho de 2026

### Novos recursos

- **Gerenciamento de Permissões** — Os usuários com o recurso Gerenciar usuários agora podem controlar o acesso ao site a partir de uma nova guia Permissões — pesquisar pessoas por nome ou email e conceder ou revogar recursos específicos. As ações que um usuário não tem permissão para executar aparecem desabilitadas com uma dica de ferramenta que explica como solicitar acesso.
- **Emblemas de Status de Implantação** — As correções marcadas como implantadas manualmente agora exibem um emblema distinto &quot;Marcado como implantado&quot; na exibição Implantado, facilitando a diferenciação entre atualizações manuais e implantações automáticas.

### Aprimoramentos

- **Correção automática para GitHub (Cloud Manager)** — A correção automática de código para oportunidades como Core Web Vitals, Segurança e Acessibilidade de formulário agora pode gerar solicitações de pull no Cloud Manager, trazer repositórios Git próprios hospedados no GitHub, correspondendo ao suporte existente para GitLab, Bitbucket e Azure DevOps. A nova opção Configurações permite controlar a confirmação da configuração única do site.
- **Correção automática por ramificação (Cloud Manager Standard)** — A correção automática por ramificação agora está disponível para repositórios padrão do Cloud Manager quando habilitada para seu site.
- **Modo de Exibição Implantado: Executado por** — O modo de exibição Implantado agora mostra quem marcou cada correção como implantada e quando seu status foi atualizado pela última vez, por meio das novas colunas &quot;Executado por&quot; e &quot;Status atualizado pela última vez&quot;.
- **Feedback de Desconexão do Google Ads** — A desconexão de uma conta do Google Ads em Configurações agora mostra um status &quot;Desconectando...&quot;, com uma mensagem de erro invisível se a desconexão falhar, para que você possa tentar novamente.

### Correções de erros

- A oportunidade Corrigir rótulos ARIA agora mostra o URL da página correto na caixa de diálogo Detalhes quando uma correção abrange várias páginas.
- A mensagem de informações da caixa de diálogo Ignorar agora é exibida corretamente, com texto alinhado corretamente, em coreano, chinês simplificado e chinês tradicional.
- As caixas de diálogo de páginas relacionadas para Texto alternativo e Metadados inválidos ou ausentes agora são carregadas de forma confiável, e a exibição Implantada de Metadados inválidos ou ausentes e as correções de metatags agora funcionam corretamente com o formato de sugestão mais recente.

## 11-22 de maio de 2026

### Novos recursos

- **Relatório de Alertas do Site (Acesso Antecipado)** — Um novo Relatório de Alertas do Site de 90 dias fornece uma visão trimestral da integridade do site, usando blocos diários codificados por cores para destacar períodos de alertas elevados, de modo que você possa identificar e investigar rapidamente tendências ao longo do tempo.
- **Integração de Telemetria Operacional** — Os sites que ainda não conectaram dados de telemetria operacional agora recebem um banner persistente na página inicial e uma caixa de diálogo de integração guiada para concluir a configuração, garantindo que você obtenha visibilidade total do desempenho real do usuário.
- **Texto Alternativo: Reconhecimento do Gerenciador de Vários Sites** — Ao gerar correções de Texto Alternativo para sites que usam o Gerenciador de Vários Sites do AEM ou a Cópia de Idioma, a Sites Optimizer agora verifica se as correções podem ser aplicadas com segurança a cada variante de idioma antes de sugerir essas correções.

### Aprimoramentos

- **Precisão do Texto Alternativo** — As sugestões de Texto Alternativo agora são extraídas do sinal de auditoria mais recente, e problemas redetectados são exibidos nas guias Problemas Atuais e Implantados para obter uma imagem completa.

### Correções de erros

- O estado do botão Implantar agora reflete corretamente se uma correção pode realmente ser implantada.
- O tema escuro agora é aplicado corretamente na atualização da página.
- Os relatórios mostram datas na localidade do usuário.
- As preferências regionais para idioma e formato de número/data agora podem ser configuradas independentemente.
- O texto alternativo de imagem corrompido agora pode ser acessado por leitores de tela.

## 21 de abril-10 de maio de 2026

### Novos recursos

- **Nenhum Estado Integrado do Site** — Os clientes que ainda não adicionaram um site agora veem um prompt claro e acionável na home page para começar rapidamente.
- **Documentação na Central de ajuda** — a documentação do AEM Sites Optimizer no Experience League agora pode ser acessada diretamente da central de ajuda no aplicativo, sem sair do produto.

### Correções de erros

- Os sites sem sugestões ativas agora exibem corretamente uma caixa de diálogo Ação necessária.
- As sugestões ignoradas agora aparecem na guia Ignorado, conforme esperado.
- Os menus suspensos do Seletor de tráfego pago não truncam mais o texto traduzido.
- O seletor de página do mapa do site agora está dimensionado corretamente.

## 13 de março a 20 de abril de 2026

### Novos recursos

- **Integração de avaliações** — novos usuários de avaliação agora passam por um fluxo de configuração guiado: insira seu domínio, aguarde a análise e, em seguida, explore suas primeiras oportunidades — nenhuma configuração é necessária para começar.
- **Página de Oportunidades de Avaliação** — Os usuários de avaliação podem pesquisar, classificar e filtrar oportunidades, com três sugestões desbloqueadas e sugestões restantes exibidas em uma visualização bloqueada com um prompt de atualização.
- **Progresso Mensal da Otimização** — Uma barra de progresso na página inicial rastreia quantas ações de otimização você executou este mês, ajudando você a se manter atualizado em relação às metas de integridade do site.
- **URLs de Destino de Auditoria (Acesso Antecipado)** — Em Configurações, você pode especificar até 100 URLs personalizados para garantir que essas páginas sejam sempre incluídas nas auditorias.
- **Configuração do tipo de entrega** — As configurações agora permitem que você especifique o tipo de entrega do seu site (Edge Delivery Services, AEM Cloud Service ou AEM Managed Services) e conecte seu provedor de conteúdo.
- **Redesign do Core Web Vitals** — A oportunidade do Core Web Vitals foi reprojetada com links Jira, download de CSV e suporte a várias seleções para ações em lote.
- **Tabela Unificada de Backlinks Quebrados** — Backlinks quebrados de todas as origens agora são mostrados em uma única tabela unificada, com a capacidade de exportar regras de redirecionamento CDN diretamente.
- **Nenhum CTA acima da dobra: implantar para autor** — correções para a oportunidade Nenhum CTA acima da dobra agora podem ser implantadas diretamente para o autor do AEM.
- **Implantação de correção automática do Forms** — As correções de oportunidades do Forms agora podem ser implantadas diretamente no AEM Author.
- **Suporte ao Gerenciador de Vários Sites da AEM** — As oportunidades que afetam várias cópias de idioma de um site agora indicam em qual site raiz a correção foi aplicada, usando uma coluna &quot;Corrigido em&quot;.
- **Ignorar correções com falha** — Agora você pode ignorar correções individuais que falharam na implantação, mantendo seu fluxo de trabalho desbloqueado.
- **Abrir no AEM Editor** — as sugestões de oportunidade agora incluem um link direto para abrir a página afetada no editor visual do AEM para edições rápidas em linha.

## 28 de fevereiro a 13 de março de 2026

### Novos recursos

- **Oportunidade de Incompatibilidade de Intenção de Anúncio** — Um novo tipo de oportunidade identifica páginas de aterrissagem de tráfego pago que não estão sendo convertidas, apresentando a taxa de rejeição, o custo por clique e as métricas de tráfego para ajudá-lo a priorizar melhorias na página de aterrissagem.
- **Nenhum CTA acima da dobra** — esta oportunidade agora é um tipo dedicado de primeira classe com sua própria página de detalhes e filtragem, facilitando o rastreamento e a priorização de melhorias de conversão.
- **Sugestões de URL do Mapa do Site** — A oportunidade do Mapa do Site agora sugere URLs de substituição para páginas que retornam erros 404, facilitando a correção de entradas quebradas do mapa do site.
- **Backlinks Desfeitos Novamente** — A página de detalhes Backlinks Desfeitos foi reprojetada para maior clareza e usabilidade.

### Aprimoramentos

- **Principais páginas de pesquisa orgânica V2** — Os dados de tráfego orgânico agora são obtidos de um conjunto de dados Ahrefs de 30 dias, fornecendo insights de desempenho de pesquisa mais abrangentes e acionáveis.
- **Vulnerabilidades de Segurança: Árvore de Dependência** — Os detalhes da vulnerabilidade de segurança agora incluem uma visualização de árvore de dependência para que você possa entender todo o impacto de uma vulnerabilidade em seu projeto.

## 14-27 de fevereiro de 2026

### Novos recursos

- **Principais páginas de pesquisa orgânica** — O Monitor de Integridade do Site agora inclui uma guia dedicada que mostra as principais páginas de tráfego orgânico do site, oferecendo visibilidade sobre qual conteúdo direciona mais tráfego de pesquisa.
- **Correção de Texto Alternativo V2** — Antes de implantar uma correção de Texto Alternativo, você pode executar uma avaliação de pré-teste &quot;Verificar Correção&quot; para verificar se a correção pode ser aplicada com êxito ao seu conteúdo.
- **Modo de Exibição Implantado para Texto Alternativo** — As correções de Texto Alternativo agora aparecem em uma guia Implantado, fornecendo um histórico completo de melhorias de acessibilidade junto com os problemas pendentes atuais.
- **Portão de Implantação de Organização Externa** — Ao implantar correções em um site gerenciado externamente, uma etapa de confirmação explícita agora é necessária para evitar alterações acidentais.

### Aprimoramentos

- **Isenções de URL de Marcas do Meta** — URLs específicas agora podem ser excluídas da validação de Marcas do Meta por meio de configuração, reduzindo falsos positivos para títulos intencionalmente curtos ou não padrão.
- **Filtragem avançada de URL** — As listas de oportunidades agora oferecem suporte à correspondência de prefixos de sub-rotas ao filtrar por URL, facilitando o foco em seções específicas do site.
- **Gráficos de tendências aprimorados** — Os gráficos de tendências de tráfego agora tratam corretamente os dados de ano para ano, eliminando declínios enganosos nos limites do ano.

## 6-13 de fevereiro de 2026

### Novos recursos

- **Modo de manutenção** — o Sites Optimizer agora lida com janelas de manutenção planejadas normalmente, exibindo uma mensagem de status clara em vez de dados incompletos ou enganosos durante o tempo de inatividade.
- **Modo de Exibição Implantado de Backlinks Quebrados** — Os backlinks fixos agora são rastreados em uma guia Implantado, agrupados por data para que você possa ver seu histórico de correções rapidamente.
- **Nenhuma CTA Acima da Oportunidade de Dobra** — Um novo tipo de oportunidade exibe páginas em que nenhuma call-to-action clara está visível acima da dobra, ajudando você a identificar e melhorar páginas com baixo potencial de conversão.
- **Integração do Jira para Acessibilidade e Contraste de Cores (Acesso Antecipado)** — As oportunidades de acessibilidade do Forms e do Contraste de Cores agora podem ser vinculadas diretamente aos tíquetes do Jira para um rastreamento simplificado de problemas no seu fluxo de trabalho existente.

### Aprimoramentos

- **Exibições Implantadas para Tags e Segurança do Meta** — As oportunidades de Tags e Segurança do Meta agora incluem guias Implantadas agrupadas por data, consistentes com outros tipos de oportunidade.
- **Rastreamento de Implantação de Texto Alt** — &quot;Marcar como Implantado&quot; agora está disponível para correções de Texto Alt, e o texto alternativo editado manualmente é preservado em execuções de reanálise.

## 26 de janeiro a 6 de fevereiro de 2026

### Novos recursos

- **Exibição Implantada para Canonical &amp; Hreflang** — As alterações nas oportunidades Canonical e Hreflang agora são agrupadas por data de implantação em uma guia Implantada, fornecendo um histórico claro do que foi corrigido e quando.
- **Exportação para CSV** — Agora você pode exportar dados de oportunidade para oportunidades de High Organic Low CTR e Forms para CSV para análise e relatórios offline.
- **Oportunidades favoritas** — Inicie qualquer oportunidade a partir de seu cabeçalho para adicioná-la aos seus favoritos, tornando mais rápido navegar de volta para as oportunidades em que você está trabalhando ativamente.
- **Exibição Implantada para Cadeias de Redirecionamento** — As correções da Cadeia de Redirecionamento agora podem ser marcadas como Implantadas diretamente da página de detalhes.

### Aprimoramentos

- **Estimativas de custo do banner de cookie aprimoradas** — Os cálculos de custo para a oportunidade de Banner de cookie foram refinados para maior precisão.

## 16-23 de janeiro de 2026

### Novos recursos

- **Monitor de Integridade do Site (Disponibilidade Geral)** — O Monitor de Integridade do Site agora está disponível para todos os clientes, fornecendo uma exibição contínua da integridade do desempenho do site. Novos sites são configurados automaticamente após a integração.
- **Suporte a Site de Subcaminho** — Os sites com escopo para subcaminhos de URL específicos agora têm suporte total no Monitor de Integridade do Site.

### Aprimoramentos

- **Avisos de Suficiência de Dados Acionáveis** — Oportunidades de Tráfego Pago com menos de 1.000 visualizações de página agora exibem um aviso de suficiência de dados, ajudando você a concentrar esforços de otimização nos casos em que os dados de tráfego são estatisticamente significativos.
- **Validação flexível de título do Meta** — o requisito mínimo de caracteres para metatítulos foi reduzido, oferecendo mais flexibilidade na criação de títulos de página concisos.
- **Caixa de Diálogo Novidades Localizada** — A caixa de diálogo de anúncios do recurso no aplicativo agora é exibida no seu idioma preferido.
- **Medalha publicada** — As variações na oportunidade Alta de baixa CTR orgânica que foram implantadas agora mostram uma medalha &quot;Publicada&quot;, facilitando a distinção entre alterações ativas e pendentes.
- **Links de Solicitação de Pull em Acessibilidade** — A guia Implantado da oportunidade de Acessibilidade agora mostra a URL de solicitação de pull associada para cada correção, facilitando o rastreamento de alterações de volta ao histórico de controle de origem.
