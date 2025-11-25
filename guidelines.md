---
source-git-commit: 2f4ef1c6f44d602bfe365a52eb692fe7faa7f05f
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 77%

---
# Diretrizes para colaboração na documentação do Adobe Experience Manager

## Filosofia da documentação

Os usuários do Adobe Experience Manager trabalham em ambientes extremamente competitivos, esforçando-se para criar experiências digitais para se destacar de seus concorrentes. Portanto, quando a Adobe fornece ferramentas avançadas no AEM, essas ferramentas são complementadas com documentação clara e precisa. Ela permite que os clientes aproveitem imediatamente seu investimento no AEM e maximizem o retorno do investimento.

O objetivo é disponibilizar a documentação do AEM aos usuários o quanto antes. Portanto, a Adobe prioriza uma documentação precisa e utilizável, e busca atualizá-la e aprimorá-la continuamente.

## Contribuições à documentação

Para melhorar continuamente a documentação do AEM, toda a comunidade de usuários do AEM é bem-vinda para contribuir em sua elaboração. Seja por meio de pull requests ou problemas, as melhorias na documentação podem ser correções, esclarecimentos, expansões e exemplos adicionais.

## Padrões de documentação

Embora a Adobe aceite contribuições para a documentação do AEM, sejam na forma de solicitações de pull ou tópicos, elas precisam estar em conformidade com os padrões de contribuição e documentação.

As contribuições que não cumprirem esses padrões poderão ser rejeitadas.

### Os casos de uso padrão estão documentados no Adobe

A documentação do AEM abrange casos de uso padrão. Casos de uso que não se enquadrarem no escopo de instalação e de uso padrão do produto não farão parte da documentação do AEM.

### O Adobe geralmente não documenta bugs e suas soluções

A documentação do AEM abrange casos de uso padrão. Por esse motivo, os bugs, seus efeitos e soluções alternativas não são documentados,

As exceções a essa regra aplicam-se às notas de versão, nas quais problemas conhecidos podem ser listados com possíveis soluções aprovadas pelo Gerenciamento de produtos.

### As contribuições à documentação não se destinam a responder perguntas técnicas.

Quaisquer ideias para melhorar a documentação do AEM são bem-vindas como contribuições. No entanto, comentários, tópicos e solicitações de pull devem ser realizados apenas como *contribuições*. Eles não devem envolver perguntas sobre como usar o AEM, implementar o projeto do AEM ou resolver problemas técnicos.

Você pode relatar qualquer dúvida sobre o uso do AEM ou erros técnicos. Use o processo normal de suporte por meio do [Portal de suporte corporativo da Experience Cloud](https://experienceleague.adobe.com/pt-br?support-solution=General#support) ou o processo discutido na [comunidade do Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=pt).

***As contribuições à documentação do AEM não substituem o Suporte ao cliente da Adobe***. Logo, qualquer contribuição que buscar respostas a perguntas relacionadas a suporte será rejeitada.

### As contribuições devem mencionar claramente as páginas pertinentes à documentação.

Se você criar um problema para sugerir melhorias na documentação, deverá incluir links para as páginas afetadas. Caso crie um tópico por meio de um link **Editar esta página** na documentação, o tópico será criado automaticamente com um link para a página.

Esse processo não se aplica a solicitações de pull, uma vez que, por sua natureza, fazem referência às páginas afetadas.

## Diretrizes de documentação

Quaisquer contribuições à documentação do AEM devem seguir determinadas diretrizes de estilo.

Seguir essas diretrizes facilita a revisão de sua contribuição, o que agiliza a integração à documentação do AEM.

### Idioma e estilo

#### Idioma

* A documentação do AEM foi criada e mantida em inglês americano.
* Mantenha as sentenças o mais simples possível.
* Use linguagem clara e concisa.

Lembre-se de que os leitores da documentação do AEM estão espalhados ao redor do mundo, e não espera-se que sejam falantes nativos ou fluentes em inglês. Evite linguagem coloquial e utilize um vocabulário claro e simples.

#### Siga o Manual de Estilo da Microsoft®

[O Manual de Estilo da Microsoft®](https://learn.microsoft.com/pt-br/style-guide/welcome/) é um guia de estilo gratuito que se concentra na documentação de softwares, e a documentação do AEM o segue sempre que possível.

### Formatação

| Item | Estilo |
|---|---|
| Elemento ou opção da interface do usuário | **negrito** |
| Nome do arquivo, caminho, entrada do usuário, valores de parâmetro | `monospaced` |
| Código, linha de comando | ```Code Block``` |

### Capturas de tela

As capturas de tela devem ser utilizadas com critério e somente quando uma descrição textual for insuficiente.

Não use marcadores ou outras anotações em capturas de tela (como quadros vermelhos, setas ou texto). Dessa forma, as capturas de tela são mais facilmente reutilizadas ou replicadas em versões localizadas da documentação.

### Referências específicas à versão

Evite referências diretas a uma versão específica em todo o conteúdo da documentação, sempre que possível. Esta recomendação torna a documentação mais flexível e extensível para versões futuras.

### Uso do Day, AEM, CQ, CRX

Em um artigo, sempre use o nome completo do produto **Adobe Experience Manager** na primeira vez em que for utilizado. Posteriormente, pode ser referido como **AEM**.

Não use Day, Day Software, CQ e CRX, exceto quando inevitável, como em nomes de classe ou em referência ao histórico do AEM.
