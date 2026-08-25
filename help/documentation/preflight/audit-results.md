---
title: Resultados de auditoria na simulação
description: Saiba como interpretar os resultados da auditoria de Comprovação, o medidor de disponibilidade e as categorias de auditoria, e navegar até oportunidades na visualização.
source-git-commit: 56a56991a262d9f19a228dc9ca6ec440acdc2999
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 3%

---


# Resultados de auditoria na simulação

Quando as auditorias forem concluídas, a Comprovação exibirá os resultados no painel de preparação. O painel mostra um medidor de disponibilidade geral e as oportunidades encontradas, agrupadas por categoria de auditoria. Em cada categoria, as auditorias individuais identificam itens específicos a serem revisados ou corrigidos.

## Barra de ferramentas

A barra de ferramentas na parte superior do painel de preparação fornece ações para a execução atual:

* **Reanalisar** - Inicie uma auditoria totalmente nova na página atual. A opção Reanalisar sempre descarta os resultados exibidos e executa cada auditoria novamente, portanto, use-a sempre que desejar novos resultados — por exemplo, após editar a página. A reanálise está em **Mais ações** (**...**) menu.
* **Exportar** - Baixe a execução atual como um arquivo **CSV** (compatível com planilha) ou **PDF** (um documento formatado). Dependendo do seu ambiente, selecione **Exportar** na barra de ferramentas ou em **Mais ações** (**...**) menu.

Ao exportar, você também pode escolher o que incluir:

* **Incluir tabela de metadados** - Adicione uma tabela de detalhes de execução, como o host, o caminho de conteúdo e os detalhes de geração.
* **Incluir auditorias aprovadas** - Inclua as auditorias aprovadas que não tiveram oportunidades, não apenas as oportunidades encontradas.

>[!NOTE]
>
>As exportações do PDF são sempre geradas em inglês, independentemente do idioma da interface. As exportações de CSV seguem o idioma da interface o mais próximo possível.

## Medidor de disponibilidade

Na parte superior do painel, o medidor de prontidão reflete os resultados gerais de auditoria. Ela mostra uma pontuação de prontidão como uma porcentagem, com base na proporção de auditorias que terminaram sem oportunidades, juntamente com o número total de oportunidades encontradas em todas as auditorias. O medidor de disponibilidade ajuda a medir a integridade geral da página rapidamente.

![O medidor de preparação e as categorias de auditoria no painel de Comprovação](./assets/overview/hero.png){align="center"}

Quando você está visualizando uma execução que foi recarregada de uma sessão anterior, o cabeçalho mostra há quanto tempo ela foi executada — por exemplo, *ontem*. Para obter mais informações, consulte [Continuar uma sessão anterior](./audits.md#continue-a-previous-session).

Enquanto as auditorias ainda estão em execução, o medidor de prontidão mostra uma barra de progresso com um status curto abaixo dela que mostra a etapa atual. Quando as auditorias forem concluídas, o medidor exibirá a porcentagem final de prontidão e a contagem de oportunidades.

## Categorias de auditoria

Comprove auditorias relacionadas a grupos em categorias, como **SEO** e **Acessibilidade**. Cada categoria aparece como um cartão que mostra o número de oportunidades encontradas ou indica que todas as auditorias foram aprovadas sem oportunidades.

Expanda uma categoria para ver suas auditorias individuais. Cada auditoria mostra se passou ou encontrou oportunidades, uma breve descrição e uma contagem das oportunidades encontradas. Selecione uma auditoria que encontrou oportunidades para abrir sua página de detalhes.

Para obter a lista completa das categorias de auditoria e das auditorias em cada uma, consulte [Categorias de auditoria de comprovação](./overview.md#preflight-audit-categories).

## Detalhes da oportunidade

A página de detalhes mostra as oportunidades que a auditoria selecionada encontrou. Quando o mesmo problema ocorre em mais de um local, cada ocorrência é chamada de instância. Use o navegador (**Instância anterior** e **Próxima instância**) para percorrê-las; ele mostra sua posição, por exemplo *1 de 5 instâncias encontradas*. Para retornar ao painel de preparação, selecione a seta para trás ao lado do título de auditoria; o painel é reaberto com a categoria da auditoria expandida.

![A página de detalhes de uma auditoria, mostrando uma oportunidade e sua sugestão](./assets/audit-results/audit-detail.png){align="center"}

Cada oportunidade inclui:

* Um selo de gravidade ou impacto que indica a importância da oportunidade.
* Detalhes sobre a oportunidade, como uma descrição do problema, uma recomendação e, para acessibilidade, a regra WCAG relacionada e o nível de conformidade.
* Uma seção **Elemento** que identifica o elemento afetado na página, com um botão **Realce na página**. Quando o elemento tem texto legível, a seção é denominada **Elemento: Texto** e mostra esse texto; caso contrário, ela é denominada **Elemento: Seletor** e mostra o seletor de CSS do elemento. Para oportunidades de **Links** e **Canônicos**, uma seção **URL Atual** também mostra a URL envolvida, que você pode abrir em uma nova guia, se possível.
* Uma seção **Sugestão** com uma correção recomendada. Quando a sugestão é gerada pela IA, ela é marcada como uma sugestão gerada pela IA e pode incluir um breve raciocínio explicando a correção sugerida.

## Realçar na página

Após a conclusão das auditorias, é possível localizar e entender rapidamente uma oportunidade, destacando-a diretamente na página.

A comprovação destaca o elemento afetado no contexto, conectando o resultado no painel ao local exato no seu conteúdo. Isso facilita a análise e a resolução de oportunidades sem pesquisar manualmente pela página.

1. Abra o painel Comprovação no contexto da página para auditar e selecione **Analisar página** para executar as auditorias.
1. Selecione uma auditoria no painel de preparação e, em seguida, selecione uma oportunidade para revisar.
1. Selecione **Destaque na página**. A visualização rola automaticamente para a área relevante e realça o elemento correspondente, para que você possa identificar e otimizar facilmente a oportunidade no contexto.

O realce não é possível para todas as oportunidades — por exemplo, quando uma oportunidade não está vinculada a um elemento específico, o elemento é oculto ou não está mais na página. Nesses casos, o botão **Realçar na página** está esmaecido; passe o mouse sobre ele para ver o motivo.

No Editor Universal, o realce ainda não é suportado para as oportunidades de **Acessibilidade**; o botão **Realçar na página** fica esmaecido e você pode passar o mouse sobre ele para ver o motivo.

No Editor de páginas do AEM Sites e no Adobe Managed Services (AMS), o realce também requer o **modo de Edição**. No **Modo de visualização**, a Comprovação mostra um aviso de **Problemas de destaque não disponíveis**; alterne para o **Modo de edição** para destacar elementos na página.

## ID da tarefa

Cada execução de comprovação tem uma ID de tarefa exclusiva, mostrada na parte inferior do painel. É útil principalmente quando um administrador está solucionando problemas em uma execução específica. Passe o mouse sobre a ID e selecione o ícone de cópia que aparece à direita; a ID é copiada para a área de transferência e uma mensagem de confirmação é exibida. Inclua essa ID ao relatar um problema.

Quando você usa a opção Comprovação fora do Editor universal (por exemplo, por meio do Sidekick ou de um bookmarklet), o rodapé do painel também mostra o nome da organização acima da ID da tarefa. No Editor universal, sua organização aparece no cabeçalho do AEM.
