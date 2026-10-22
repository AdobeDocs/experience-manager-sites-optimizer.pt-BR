---
title: Resultados de auditoria na simulação
description: Saiba como interpretar os resultados da auditoria de Comprovação, o medidor de disponibilidade e as categorias de auditoria, e navegar até oportunidades na visualização.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: ae16300fdfd525dc5efead2f165d5a238b5ea6e1
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 2%
---

# Resultados de auditoria na simulação

Quando as auditorias forem concluídas, a Comprovação exibirá os resultados no painel de preparação. O painel mostra um medidor de disponibilidade geral e as oportunidades encontradas, agrupadas por categoria de auditoria. Em cada categoria, as auditorias individuais identificam itens específicos a serem revisados ou corrigidos.

## Barra de ferramentas

A barra de ferramentas na parte superior do painel de preparação fornece ações para a execução atual:

* **Reanalisar** - Inicie uma auditoria totalmente nova na página atual. A opção Reanalisar sempre descarta os resultados exibidos e executa cada auditoria novamente, portanto, use-a sempre que desejar novos resultados — por exemplo, após editar a página. Selecione **Reanalisar** na barra de ferramentas.
* **Exportar** - Baixe a execução atual como um arquivo **CSV** (compatível com planilha) ou **PDF** (um documento formatado). Dependendo do seu ambiente, selecione **Exportar** na barra de ferramentas ou em **Mais ações** (**...**) menu.
* **Configurações** - Use **Mostrar links de navegação do site** para incluir links de navegação do site (atualmente apenas Links Internos). Selecione o ícone de engrenagem ou abra **Mais ações** (**...**) e selecione **Configurações**. As configurações estão disponíveis antes ou depois de uma execução, mas não enquanto auditorias estão em execução ou no Editor universal. Consulte [Incluir links de navegação do site](./opportunities/seo/internal-links.md#include-site-navigation-links).

Se você alterar uma configuração após uma execução, um ponto em **Reanalisar** e o rótulo **Reanalisar para aplicar novas configurações** indicarão que os resultados exibidos usaram uma configuração diferente. Selecione **Reanalisar** para aplicar a configuração salva a uma nova execução.

Ao exportar, você também pode escolher o que incluir:

* **Incluir tabela de metadados** - Adicione uma tabela de detalhes de execução, como o host, o caminho de conteúdo e os detalhes de geração.
* **Incluir auditorias aprovadas** - Inclua as auditorias aprovadas que não tiveram oportunidades, não apenas as oportunidades encontradas.

>[!NOTE]
>
>As exportações do PDF são sempre geradas em inglês, independentemente do idioma da interface. As exportações de CSV seguem o idioma da interface o mais próximo possível.

## Medidor de disponibilidade

Na parte superior do painel, o medidor de prontidão reflete os resultados gerais de auditoria. Ela mostra a porcentagem de auditorias que terminaram sem oportunidades, rotuladas como **% aprovadas**, juntamente com o número total de oportunidades encontradas em todas as auditorias. Por exemplo, **85% aprovado** significa que 85% das auditorias concluídas não encontraram oportunidades. Essa porcentagem descreve os resultados da auditoria, não o progresso da execução.

![O medidor de preparação e as categorias de auditoria no painel de Comprovação](./assets/overview/hero.png){align="center"}

Quando você está visualizando uma execução que foi recarregada de uma sessão anterior, o cabeçalho mostra há quanto tempo ela foi executada — por exemplo, *ontem*. Para obter mais informações, consulte [Continuar uma sessão anterior](./audits.md#continue-a-previous-session).

Enquanto as auditorias ainda estão em execução, o painel mostra a **página Análise**, com um status curto abaixo dela. Uma barra de progresso é exibida inicialmente, antes da chegada das categorias de auditoria nomeadas. Quando as categorias forem exibidas, seus indicadores de processamento individuais mostrarão quais categorias ainda têm trabalho em andamento. Quando todas as auditorias forem concluídas, o medidor exibirá a porcentagem final aprovada e a contagem de oportunidades.

## Categorias de auditoria

Comprove auditorias relacionadas a grupos em categorias, como **SEO** e **Acessibilidade**. Cada categoria aparece como um cartão que mostra o número de oportunidades encontradas ou indica que todas as auditorias foram aprovadas sem oportunidades.

Expanda uma categoria para ver suas auditorias individuais. Cada auditoria mostra se passou ou encontrou oportunidades, uma breve descrição e uma contagem das oportunidades encontradas. Selecione uma auditoria que encontrou oportunidades para abrir sua página de detalhes.

Uma categoria pode mostrar resultados enquanto algumas de suas auditorias ainda estão em execução. Seu ícone mostra um indicador de processamento e seu status informa, por exemplo, **3/3 auditorias passadas até agora**. Essa contagem inclui apenas as auditorias que retornaram resultados, portanto, pode ser alterada à medida que mais resultados chegam. Expanda a categoria para ver auditorias individuais que ainda estão sendo processadas. Uma categoria sem oportunidades mostra a marca de seleção totalmente limpa somente após a conclusão do trabalho pendente.

Para obter a lista completa das categorias de auditoria e das auditorias em cada uma, consulte [Categorias de auditoria de comprovação](./overview.md#preflight-audit-categories).

## Detalhes da oportunidade

A página de detalhes mostra as oportunidades que a auditoria selecionada encontrou. Quando o mesmo problema ocorre em mais de um local, cada ocorrência é chamada de instância. Use o navegador (**Instância anterior** e **Próxima instância**) para percorrê-las; ele mostra sua posição, por exemplo *1 de 5 instâncias encontradas*. Para retornar ao painel de preparação, selecione a seta para trás ao lado do título de auditoria; o painel é reaberto com a categoria da auditoria expandida.

Para auditorias que identificam uma URL específica na página, a seção **Elemento** aparece na parte superior do cartão para introduzir o item, e o restante da oportunidade segue abaixo dele em sua própria seção.

Quando mais de uma oportunidade afeta o mesmo item (por exemplo, vários problemas com o mesmo link), a Comprovação os mostra juntos em um cartão, cada um em sua própria seção intitulada com seu número de instância, como **Instância 3**. O navegador mostra um intervalo em vez de uma única posição, por exemplo *3-5 de 12 instâncias encontradas*.

![A página de detalhes da auditoria de Links Internos, mostrando uma oportunidade e a seção URL Atual](./assets/audit-results/audit-detail.png){align="center"}

Cada oportunidade inclui:

* Um selo de gravidade ou impacto que indica a importância da oportunidade.
* Detalhes sobre a oportunidade, como uma descrição do problema, uma recomendação e, para acessibilidade, a regra WCAG relacionada e o nível de conformidade.
* Uma seção **Elemento** que identifica o elemento afetado na página, com um botão **Realce na página**. Quando o elemento tem texto legível, a seção é denominada **Elemento: Texto** e mostra esse texto; caso contrário, ela é denominada **Elemento: Seletor** e mostra o seletor de CSS do elemento. Para oportunidades de **Links Internos** e **Canônico**, uma seção **URL Atual** também mostra a URL envolvida. Selecione **Copiar URL** para copiá-la para a área de transferência ou **Abrir em nova guia** para abri-la.
* Uma seção **Sugestão** com uma correção recomendada. Quando a sugestão é gerada pela IA, ela é marcada como uma sugestão gerada pela IA e pode incluir um breve raciocínio explicando a correção sugerida.

## Realçar na página

Após a conclusão das auditorias, é possível localizar e entender rapidamente uma oportunidade, destacando-a diretamente na página.

A comprovação destaca o elemento afetado no contexto, conectando o resultado no painel ao local exato no seu conteúdo. Isso facilita a análise e a resolução de oportunidades sem pesquisar manualmente pela página.

1. Abra o painel Comprovação no contexto da página para auditar e selecione **Analisar página** para executar as auditorias.
1. Selecione uma auditoria no painel de preparação e, em seguida, selecione uma oportunidade para revisar.
1. Selecione **Destaque na página**. A visualização rola automaticamente para a área relevante e realça o elemento correspondente, para que você possa identificar e otimizar facilmente a oportunidade no contexto.

O realce não é possível para todas as oportunidades — por exemplo, quando uma oportunidade não está vinculada a um elemento específico, o elemento é oculto ou não está mais na página. Nesses casos, o botão **Realçar na página** está esmaecido; passe o mouse sobre ele para ver o motivo.

No Editor Universal, o realce ainda não é suportado para as oportunidades de **Acessibilidade**; o botão **Realçar na página** fica esmaecido e você pode passar o mouse sobre ele para ver o motivo.

No Editor universal, a simulação só pode realçar o conteúdo editável. Se o elemento afetado não fizer parte do conteúdo editável, o botão **Realçar na página** ficará esmaecido; passe o mouse sobre ele para ver o motivo. Se o elemento em si não for diretamente editável, mas o bloco editável mais próximo for, o Preflight realçará esse bloco e adicionará uma nota explicando o porquê.

No Editor de páginas do AEM Sites e no Adobe Managed Services (AMS), o realce também requer o **modo de Edição**. No **Modo de visualização**, a Comprovação mostra um aviso de **Problemas de destaque não disponíveis**; alterne para o **Modo de edição** para destacar elementos na página.

## ID da tarefa

Cada execução de comprovação tem uma ID de tarefa exclusiva, mostrada na parte inferior do painel. É útil principalmente quando um administrador está solucionando problemas em uma execução específica. Passe o mouse sobre a ID e selecione o ícone de cópia que aparece à direita; a ID é copiada para a área de transferência e uma mensagem de confirmação é exibida. Inclua essa ID ao relatar um problema.

Quando você usa a opção Comprovação fora do Editor universal (por exemplo, por meio do Sidekick ou de um bookmarklet), o rodapé do painel também mostra o nome da organização acima da ID da tarefa. No Editor universal, sua organização aparece no cabeçalho do AEM.
