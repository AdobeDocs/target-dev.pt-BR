---
keywords: implementação, biblioteca javascript, js, atjs, decisão no dispositivo, decisão no dispositivo, at.js, no dispositivo, implementação0
description: Saiba como executar [!UICONTROL decisão no dispositivo] com a biblioteca at.js do
title: Como a Decisão no dispositivo funciona com a biblioteca JavaScript at.js?
feature: at.js
exl-id: bd0e062f-c259-46f3-adba-e380af058ac8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '3689'
ht-degree: 14%

---

# [!UICONTROL Decisão no dispositivo] para at.js

A partir da versão 2.5.0, as ofertas da at.js [!UICONTROL decisão no dispositivo]. [!UICONTROL Decisão no dispositivo] permite armazenar seus [Teste A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) e [Direcionamento de experiência](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) no navegador para executar decisões na memória sem uma solicitação de bloqueio de rede para o [!DNL Adobe Target] Rede de borda.

>[!NOTE]
>
>[!UICONTROL Decisão no dispositivo] O está disponível para implementações do lado do cliente e do lado do servidor. Este artigo descreve [!UICONTROL decisão no dispositivo] para o lado do cliente. Para obter informações sobre [!UICONTROL decisão no dispositivo] para o lado do servidor, consulte a documentação de implementação do lado do servidor [aqui](../../../server-side/sdk-guides/on-device-decisioning/overview.md).

[!DNL Target] O também oferece a flexibilidade de fornecer a experiência mais relevante e atualizada de suas atividades de experimentação e personalização orientada por aprendizado de máquina (orientado por aprendizado de máquina) por meio de uma chamada de servidor em tempo real. Em outras palavras, quando o desempenho é mais importante, você pode optar por usar [!UICONTROL decisão no dispositivo]. No entanto, quando a experiência mais relevante, atualizada e orientada por aprendizado de máquina for necessária, uma chamada de servidor poderá ser feita.

## Quais são os benefícios do [!UICONTROL decisão no dispositivo]?

Os benefícios da [!UICONTROL decisão no dispositivo] incluem:

* **Proporcione decisões e experiências extremamente rápidas.** O particionamento e a decisão são executados na memória e no navegador para evitar o bloqueio de solicitações de rede.
* **Melhorar o desempenho dos aplicativos.** Execute experimentos e forneça personalização aos seus clientes e usuários sem comprometer as experiências do usuário final.
* **Melhore A Pontuação De Qualidade Do Site Do Google.** Com as decisões sendo tomadas na memória, melhore a pontuação da Qualidade do site do Google em seu negócio online para torná-lo mais detectável pelos consumidores.
* **Aprenda com a análise em tempo real.** Obtenha insights do desempenho da sua atividade em tempo real via [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T). O A4T permite que você mude sua estratégia em momentos críticos.

## Recursos compatíveis

A variável [!DNL Adobe Target] O JS SDK oferece aos clientes a flexibilidade para escolher entre o desempenho e a atualização dos dados para as decisões. Em outras palavras, se o fornecimento do conteúdo personalizado mais relevante e envolvente por meio do aprendizado de máquina for mais importante para você, uma chamada de servidor em tempo real deverá ser feita. Mas quando o desempenho é mais crítico, uma decisão no dispositivo e na memória deve ser tomada. Para [!UICONTROL decisão no dispositivo] para funcionar, consulte a lista de recursos compatíveis:

* Tipos de atividades 
* Direcionamento de público
* Método de alocação

Para obter mais informações, consulte [Recursos compatíveis com o [!UICONTROL decisão no dispositivo]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

## Como o [!UICONTROL decisão no dispositivo] trabalhar?

Ao implantar e inicializar o at.js com o [!UICONTROL decisão no dispositivo] habilitado, uma [artefato de regra](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) que inclui seu [!UICONTROL decisão no dispositivo] para atividades A/B e XT, públicos-alvo e ativos, o é baixado do Akamai CDN mais próximo ao visitante e armazenado em cache localmente no navegador do visitante. Quando uma solicitação é feita pela at.js para recuperar uma experiência, a decisão sobre qual experiência retornar é tomada na memória, com base nos metadados codificados no artefato de regra em cache.

## Método de decisão

Com [!UICONTROL decisão no dispositivo], [!DNL Target] O introduz uma nova configuração chamada Método de decisão. A configuração Método de decisão determina como a at.js fornece suas experiências. O Método de decisão tem três valores:

* Somente no lado do servidor
* Somente no dispositivo
* Híbrido

### Somente no lado do servidor

Somente no lado do servidor é o método de decisão padrão definido imediatamente quando a at.js 2.5.0+ é implementada e implantada em suas propriedades da Web.

Usar somente no lado do servidor como configuração padrão significa que todas as decisões são tomadas na rede de borda do [!DNL Target], o que envolve uma chamada de servidor de bloqueio. Essa abordagem pode apresentar latência incremental, mas também oferece benefícios significativos, como a capacidade de aplicar [!DNL Target]Os recursos de aprendizado de máquina do que incluem [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) e [Direcionamento automático](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) atividades.

Além disso, aprimorar suas experiências personalizadas usando [!DNL Target]O perfil de usuário do, que é mantido em sessões e canais, pode fornecer resultados significativos para sua empresa.

Por fim, somente no lado do servidor permite usar a Adobe Experience Cloud e refinar públicos-alvo que podem ser direcionados por meio de segmentos do Audience Manager e do Adobe Analytics.

O diagrama a seguir ilustra a interação entre seu visitante, o navegador, o at.js 2.5.0+ e o [!DNL Adobe Target] Rede de borda. Este diagrama de fluxo captura novos visitantes e visitantes recorrentes.

(Clique na imagem para expandir até a largura total.)

![Diagrama de fluxo somente do lado do servidor](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/server-side-only.png "Diagrama de fluxo somente do lado do servidor"){zoom=&quot;yes&quot;}

A lista a seguir corresponde aos números no diagrama:

| Etapa | Descrição |
| --- | --- |
| 1 | A ID de visitante do Experience Cloud é recuperada do [Serviço de identidade da Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html?). |
| 2 | A biblioteca at.js é carregada de modo síncrono e oculta o corpo do documento.<br />   A biblioteca at.js também pode ser carregada de forma assíncrona com uma opção que oculta previamente o trecho implementado na página. |
| 3 | A biblioteca at.js oculta o corpo para evitar cintilação. |
| 4 | É feita uma solicitação de carregamento de página que inclui todos os parâmetros configurados, como (ECID, ID do cliente, Parâmetros personalizados, Perfil do usuário e assim por diante). |
| 5 | Os scripts de perfil executam e, em seguida, fazem o feed na Loja do perfil.<br />A Loja de perfis solicita públicos qualificados da Biblioteca de públicos-alvo (por exemplo, públicos-alvo compartilhados da Adobe Analytics, da Adobe Audience Manager e assim por diante).<br />Os atributos do cliente são enviados à Loja de perfis em um processo em lote. |
| 6 | A Loja de perfis é usada para qualificação de público-alvo e classificação para filtrar atividades. |
| 7 | O conteúdo resultante é selecionado depois que a experiência é determinada a partir do estado ativo [!DNL Target] atividades. |
| 8 | A biblioteca at.js oculta os elementos correspondentes na página que estão associados à experiência que deve ser renderizada. |
| 9 | A biblioteca at.js exibe o corpo da página para que o restante da página possa ser carregado para que o visitante a visualize. |
| 10 | A biblioteca at.js manipula o DOM para renderizar a experiência do [!DNL Target] Rede de borda. |
| 11 | A experiência é renderizada para o visitante. |
| 12 | A página da Web inteira é carregada. |
| 13 | Os dados do Analytics são enviados ao servidores de Coleção de dados. |
| 14 | Os dados direcionados correspondem aos dados do Analytics por meio da SDID e são processados no armazenamento de relatórios do Analytics. Em seguida, os dados do Analytics podem ser visualizados no Analytics e no [!DNL Target] pelos relatórios do [!UICONTROL Analytics for Target] (A4T). |

### Somente no dispositivo

Somente no dispositivo é o método de decisão que deve ser definido na at.js 2.5.0+ quando [!UICONTROL decisão no dispositivo] O deve ser usado somente em suas páginas da Web.

[!UICONTROL Decisão no dispositivo] O pode fornecer suas experiências e atividades de personalização em uma velocidade extremamente rápida, pois as decisões são tomadas a partir de um artefato de regras em cache que contém todas as suas atividades qualificadas para [!UICONTROL decisão no dispositivo].

Para saber mais sobre quais atividades se qualificam para [!UICONTROL decisão no dispositivo], consulte [Recursos compatíveis com o [!UICONTROL decisão no dispositivo]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

Esse método de decisão deve ser usado somente se o desempenho for altamente crítico em todas as páginas que exigem decisões do Target. Além disso, lembre-se de que, quando esse método de decisão é selecionado, as atividades do [!DNL Target] que não se qualificam para a tomada de decisão no dispositivo não são entregues ou executadas.  A biblioteca at.js 2.5.0+ está configurada para procurar somente pelo artefato de regras em cache para tomar decisões.

O diagrama a seguir ilustra a interação entre seu visitante, o navegador, a at.js 2.5.0+ e o Akamai CDN. O Akamai CDN armazena em cache o artefato de regras da primeira visita. Para a primeira visita de página de um novo visitante, o artefato de regras JSON deve ser baixado do Akamai CDN para ser armazenado em cache localmente no navegador do visitante. Após o download do artefato de regras JSON, a decisão é tomada imediatamente, sem uma chamada de rede de bloqueio. O diagrama de fluxo a seguir captura novos visitantes.

(Clique na imagem para expandir até a largura total.)

![Diagrama de fluxo somente no dispositivo](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only.png "Diagrama de fluxo somente no dispositivo"){zoom=&quot;yes&quot;}

A lista a seguir corresponde aos números no diagrama:

>[!NOTE]
>
>[!DNL Adobe Target] Os servidores de administração qualificam todas as suas atividades qualificadas para [!UICONTROL decisão no dispositivo], gere o artefato de regras JSON e o propague para o Akamai CDN. Suas atividades são continuamente monitoradas em busca de atualizações para produzir um novo artefato de regras JSON que será propagado para o Akamai CDN.

| Etapa | Descrição |
| --- | --- |
| 1 | A ID de visitante do Experience Cloud é recuperada do [Serviço de identidade da Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | A biblioteca at.js é carregada de modo síncrono e oculta o corpo do documento.<br />A biblioteca at.js também pode ser carregada de forma assíncrona com uma opção que oculta previamente o trecho implementado na página. |
| 3 | A biblioteca at.js oculta o corpo para evitar cintilação. |
| 4 | A biblioteca at.js faz uma solicitação para recuperar o artefato de regra JSON do CDN Akamai mais próximo para o visitante. |
| 5 | O Akamai CDN responde com o artefato de regra JSON. |
| 6 | O artefato da regra JSON é armazenado em cache localmente no navegador do visitante. |
| 7 | A biblioteca at.js interpreta o artefato da regra JSON e executa a decisão de recuperar a experiência e oculta os elementos testados. |
| 8 | A biblioteca at.js exibe o corpo da página para que o restante da página possa ser carregado para que o visitante a visualize. |
| 9 | A biblioteca at.js manipula o DOM para renderizar a experiência do artefato de regra JSON em cache. |
| 10 | A experiência é renderizada para o visitante. |
| 11 | A página da Web inteira é carregada. |
| 12 | Os dados do Analytics são enviados ao servidores de Coleção de dados. Os dados direcionados correspondem aos dados do Analytics por meio da SDID e são processados no armazenamento de relatórios do Analytics. Em seguida, os dados do Analytics podem ser visualizados no Analytics e no [!DNL Target] pelos relatórios do [!UICONTROL Analytics for Target] (A4T). |

O diagrama a seguir ilustra a interação entre seu visitante, o navegador, a at.js 2.5.0+ e o artefato de regra JSON em cache para a próxima ocorrência de página ou visita recorrente do visitante. Como o artefato de regras JSON já está armazenado em cache e disponível no navegador, a decisão é tomada imediatamente, sem uma chamada de rede de bloqueio. Este diagrama de fluxo captura a navegação de página subsequente ou os visitantes recorrentes.

(Clique na imagem para expandir até a largura total.)

![Diagrama de fluxo somente no dispositivo para navegação de página subsequente e visitas repetidas](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only-subsequent.png "Diagrama de fluxo somente no dispositivo para navegação de página subsequente e visitas repetidas"){zoom=&quot;yes&quot;}

A lista a seguir corresponde aos números no diagrama:

>[!NOTE]
>
>[!DNL Adobe Target] Os servidores de administração qualificam todas as suas atividades qualificadas para [!UICONTROL decisão no dispositivo], gere o artefato de regras JSON e o propague para o Akamai CDN. Suas atividades são continuamente monitoradas em busca de atualizações para produzir um novo artefato de regras JSON que será propagado para o Akamai CDN.

| Etapa | Descrição |
| --- | --- |
| 1 | A ID de visitante do Experience Cloud é recuperada do [Serviço de identidade da Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | A biblioteca at.js é carregada de modo síncrono e oculta o corpo do documento.<br />A biblioteca at.js também pode ser carregada de forma assíncrona com uma opção que oculta previamente o trecho implementado na página. |
| 3 | A biblioteca at.js oculta o corpo para evitar cintilação. |
| 4 | A biblioteca at.js interpreta o artefato da regra JSON e executa a decisão na memória para recuperar a experiência. |
| 5 | Os elementos testados estão ocultos. |
| 6 | A biblioteca at.js exibe o corpo da página para que o restante da página possa ser carregado para que o visitante a visualize. |
| 7 | A biblioteca at.js manipula o DOM para renderizar a experiência do artefato de regra JSON em cache. |
| 8 | A experiência é renderizada para o visitante. |
| 9 | A página da Web inteira é carregada. |
| 10 | Os dados do Analytics são enviados ao servidores de Coleção de dados. Os dados direcionados correspondem aos dados do Analytics por meio da SDID e são processados no armazenamento de relatórios do Analytics. Em seguida, os dados do Analytics podem ser visualizados no Analytics e no [!DNL Target] pelos relatórios do [!UICONTROL Analytics for Target] (A4T). |

### Híbrido

Híbrido é o método de decisão que deve ser definido na at.js 2.5.0+ quando ambos [!UICONTROL decisão no dispositivo] e atividades que exigem uma chamada de rede para a [!DNL Adobe Target] A rede de borda deve ser executada.

Ao gerenciar ambos [!UICONTROL decisão no dispositivo] atividades no lado do servidor, pode ser um pouco complicado e tedioso ao pensar em como implantar e provisionar [!DNL Target] em suas páginas. Com o método de decisão híbrido, o [!DNL Target] sabe quando deve fazer uma chamada de servidor para a rede de borda do , no caso de atividades que exigem execução no lado do servidor, e quando deve apenas executar decisões no dispositivo.[!DNL Adobe Target]

O artefato de regras JSON inclui metadados para informar à at.js se uma mbox tem uma atividade do lado do servidor em execução ou uma [!UICONTROL decisão no dispositivo] atividade. Esse método de decisão garante que as atividades que você pretende entregar rapidamente sejam realizadas por meio de [!UICONTROL decisão no dispositivo] e para atividades que exigem personalização orientada por aprendizado de máquina mais avançada, essas atividades são feitas por meio do [!DNL Adobe Target] Rede de borda.

O diagrama a seguir ilustra a interação entre seu visitante, o navegador, a at.js 2.5.0+, o Akamai CDN e o [!DNL Adobe Target] Rede de borda para um novo visitante que visita sua página pela primeira vez. O argumento desse diagrama é que o artefato de regras JSON é baixado de forma assíncrona enquanto as decisões são tomadas por meio da variável [!DNL Adobe Target] Rede de borda.

Essa abordagem garante que o tamanho do artefato, que pode incluir muitas atividades, não influencie negativamente a latência da decisão. Baixar o artefato de regras JSON de forma síncrona e tomar a decisão posteriormente também pode ter efeitos adversos na latência e pode ser inconsistente. Portanto, o método de decisão híbrido é uma recomendação de prática recomendada para sempre fazer uma chamada do lado do servidor para a decisão de um novo visitante e, como o artefato de regras JSON, é armazenado em cache em paralelo. Para qualquer visita de página subsequente e visita de retorno, as decisões são tomadas a partir do cache e na memória por meio do artefato de regras JSON.

(Clique na imagem para expandir até a largura total.)

![Diagrama de fluxo híbrido para um visitante novo](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-first-time-visitor.png "Diagrama de fluxo híbrido para um visitante novo"){zoom=&quot;yes&quot;}

A lista a seguir corresponde aos números no diagrama:

>[!NOTE]
>
>[!DNL Adobe Target] Os servidores de administração qualificam todas as suas atividades qualificadas para [!UICONTROL decisão no dispositivo], gere o artefato de regras JSON e o propague para o Akamai CDN. Suas atividades são continuamente monitoradas em busca de atualizações para produzir um novo artefato de regras JSON que será propagado para o Akamai CDN.

| Etapa | Descrição |
| --- | --- |
| 1 | A ID de visitante do Experience Cloud é recuperada do [Serviço de identidade da Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | A biblioteca at.js é carregada de modo síncrono e oculta o corpo do documento.<br />A biblioteca at.js também pode ser carregada de forma assíncrona com uma opção que oculta previamente o trecho implementado na página. |
| 3 | A biblioteca at.js oculta o corpo para evitar cintilação. |
| 4 | Uma solicitação de carregamento de página é feita para o [!DNL Adobe Target] Rede de borda, incluindo todos os parâmetros configurados, como (ECID, ID do cliente, Parâmetros personalizados, Perfil do usuário e assim por diante). |
| 5 | Em paralelo, a at.js faz uma solicitação para recuperar o artefato de regra JSON do CDN do Akamai mais próximo para o visitante. |
| 6 | ([!DNL Adobe Target] Rede de borda) Os scripts de perfil são executados e, em seguida, alimentados na Loja de perfis. A Loja de perfis solicita públicos qualificados da Biblioteca de públicos-alvo (por exemplo, públicos-alvo compartilhados da Adobe Analytics, da Adobe Audience Manager e assim por diante). |
| 7 | O Akamai CDN responde com o artefato de regra JSON. |
| 8 | A Loja de perfis é usada para qualificação de público-alvo e classificação para filtrar atividades. |
| 9 | O conteúdo resultante é selecionado depois que a experiência é determinada a partir do estado ativo [!DNL Target] atividades. |
| 10 | A biblioteca at.js oculta os elementos correspondentes na página que estão associados à experiência que deve ser renderizada. |
| 11 | A biblioteca at.js exibe o corpo da página para que o restante da página possa ser carregado para que o visitante a visualize. |
| 12 | A biblioteca at.js manipula o DOM para renderizar a experiência do [!DNL Target] Rede de borda. |
| 13 | A experiência é renderizada para o visitante. |
| 14 | A página da Web inteira é carregada. |
| 15 | Os dados do Analytics são enviados ao servidores de Coleção de dados. Os dados direcionados correspondem aos dados do Analytics por meio da SDID e são processados no armazenamento de relatórios do Analytics. Em seguida, os dados do Analytics podem ser visualizados no Analytics e no [!DNL Target] pelos relatórios do [!UICONTROL Analytics for Target] (A4T). |

O diagrama a seguir ilustra a interação entre seu visitante, o navegador, a at.js 2.5.0+ e o artefato de regras JSON em cache para uma navegação de página subsequente ou uma visita de retorno. Neste diagrama, concentre-se somente no caso de uso em que uma decisão no dispositivo é tomada para a navegação da página subsequente ou para a visita de retorno. Lembre-se de que, dependendo de quais atividades estão ativas para determinadas páginas, uma chamada do lado do servidor pode ser feita para executar decisões do lado do servidor.

(Clique na imagem para expandir até a largura total.)

![Diagrama de fluxo híbrido para navegação de página subsequente e visitas repetidas](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-subsequent.png "Diagrama de fluxo híbrido para navegação de página subsequente e visitas repetidas"){zoom=&quot;yes&quot;}

A lista a seguir corresponde aos números no diagrama:

>[!NOTE]
>
>[!DNL Adobe Target] Os servidores de administração qualificam todas as suas atividades qualificadas para [!UICONTROL decisão no dispositivo], gere o artefato de regras JSON e o propague para o Akamai CDN. Suas atividades são continuamente monitoradas em busca de atualizações para produzir um novo artefato de regras JSON que será propagado para o Akamai CDN.

| Etapa | Descrição |
| --- | --- |
| 1 | A ID de visitante do Experience Cloud é recuperada do [Serviço de identidade da Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | A biblioteca at.js é carregada de modo síncrono e oculta o corpo do documento.<br />A biblioteca at.js também pode ser carregada de forma assíncrona com uma opção que oculta previamente o trecho implementado na página. |
| 3 | A biblioteca at.js oculta o corpo para evitar cintilação. |
| 4 | Uma solicitação é feita para recuperar uma experiência. |
| 5 | A biblioteca at.js confirma que o artefato de regra JSON já foi armazenado em cache e executa a decisão na memória para recuperar a experiência. |
| 6 | Os elementos testados estão ocultos. |
| 7 | A biblioteca at.js exibe o corpo da página para que o restante da página possa ser carregado para que o visitante a visualize. |
| 8 | A biblioteca at.js manipula o DOM para renderizar a experiência do artefato de regra JSON em cache. |
| 9 | A experiência é renderizada para o visitante. |
| 10 | A página da Web inteira é carregada. |
| 11 | Os dados do Analytics são enviados ao servidores de Coleção de dados. Os dados direcionados correspondem aos dados do Analytics por meio da SDID e são processados no armazenamento de relatórios do Analytics. Em seguida, os dados do Analytics podem ser visualizados no Analytics e no [!DNL Target] pelos relatórios do [!UICONTROL Analytics for Target] (A4T). |

## Como ativar [!UICONTROL decisão no dispositivo]?

[!UICONTROL Decisão no dispositivo] está disponível para todos [!DNL Target] clientes que usam a At.js 2.5.0+.

Para habilitar [!UICONTROL decisão no dispositivo]:

>[!NOTE]
>
>Você precisa ter um Administrador ou Aprovador [função do usuário](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) para ativar ou desativar a opção Decisão no dispositivo.

1. Clique em **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Detalhes da conta]**.
1. Em **[!UICONTROL Detalhes da conta]**, deslize o **[!UICONTROL Decisão no dispositivo]** alterne para a posição &quot;ligado&quot;.

   ![[!UICONTROL Decisão no dispositivo] alternar](assets/on-device-decisioning-toggle.png)

   A caixa de diálogo &quot;Incluir todos os [!UICONTROL decisão no dispositivo] atividades qualificadas no artefato&quot; será exibida se você ativar [!UICONTROL decisão no dispositivo].
1. (Condicional) Deslize o botão de alternância para a posição &quot;ligado&quot; se desejar que todos os seus arquivos em tempo real [!DNL Target] atividades qualificadas para [!UICONTROL decisão no dispositivo] para ser incluído automaticamente no artefato.

   Deixar essa opção desativada significa que você deve recriar e ativar qualquer [!UICONTROL decisão no dispositivo] atividades para que sejam incluídas no artefato de regras gerado. Em outras palavras, qualquer atividade no estado ativo antes de ativar o botão Decisão no dispositivo não é incluída no artefato de regras.

Depois de ativar a opção On-Device Decisioning, [!DNL Target] começa a gerar e propagar [artefatos de regra](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) para o seu cliente.

>[!WARNING]
>
>Certifique-se de ativar o botão de alternância antes de inicializar o [!DNL Adobe Target] SDK a ser usado [!UICONTROL decisão no dispositivo]. Os artefatos de regra precisam primeiro ser gerados e propagados para os CDNs do Akamai para [!UICONTROL decisão no dispositivo] para trabalhar. A propagação pode levar de cinco a dez minutos para que o primeiro artefato de regra seja gerado e propagado para o CDN do Akamai.

## Como configurar o at.js 2.5.0+ para usar [!UICONTROL decisão no dispositivo]?

1. Clique em **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Detalhes da conta]**.
1. Em **[!UICONTROL Métodos de implementação]** > **[!UICONTROL Método de implementação principal]**, clique em **[!UICONTROL Editar]** ao lado da versão do at.js (deve ser at.js 2.5.0 ou posterior).

   ![Editar configurações do Método de implementação principal](assets/main-implementation-method.png)

   >[!WARNING]
   >
   >Antes de alterar essas configurações padrão, consulte o Atendimento ao cliente para não afetar a implementação atual.

1. Selecione o método de decisão desejado:

   * Somente no lado do servidor
   * Somente no dispositivo
   * Híbrido

   ![Editar o painel de configurações da at.js](assets/global-settings.png)

### Configurações globais

É possível configurar um Método de decisão padrão para todos os [!DNL Target] decisões. Os vários métodos de decisão são somente no lado do servidor, somente no dispositivo e híbrido. O método de decisão selecionado na variável [!DNL Target] A interface do usuário está configurada em `window.targetGlobalSettings` no `decisioningMethod` campo. Saiba mais sobre o `decisioningMethod` in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#decisioningmethod).

```javascript {line-numbers="true"}
<head> 
    <script type="text/javascript">

        window.targetGlobalSettings = { 
            clientCode: "yourClientCodeHere", 
            imsOrgId: "imsOrgId@AdobeOrg", 
            decisioningMethod: "on-device"

        }; 
    </script>

    <script type="text/javascript" src="at.js"></script> 
</head>
```

### Configuração personalizada

Se você definir a variável `decisioningMethod` in `window.targetGlobalSettings`, mas gostaria de substituir o `decisioningMethod` para cada [!DNL Adobe Target] de acordo com seu caso de uso, é possível executar esse procedimento especificando `decisioningMethod` em at.js2.5.0+&#39;s [getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) chame.

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
});
```

>[!NOTE]
>
>Para usar &quot;no dispositivo&quot; ou &quot;híbrido&quot; como um método de decisão na chamada getOffers(), verifique se a configuração global `decisioningMethod` como &quot;no dispositivo&quot; ou &quot;híbrido&quot;. A biblioteca at.js 2.5.0+ deve saber se o artefato de regras JSON deve ser baixado e armazenado em cache imediatamente após o carregamento na página. Se o método de decisão da configuração global estiver definido como &quot;lado do servidor&quot;, e o método de decisão &quot;no dispositivo&quot; ou &quot;híbrido&quot; for transmitido para a chamada getOffers(), a at.js 2.5.0+ não terá o artefato de regra JSON armazenado em cache para executar suas decisões no dispositivo.

### TTL de cache de artefato

O Target representa suas atividades qualificadas para [!UICONTROL decisão no dispositivo] como um artefato que consiste em metadados, regras e condições. Esse artefato é armazenado em cache no Akamai CDN. Durante a primeira visita do usuário, o navegador do usuário baixa e armazena em cache o artefato que representa o [!UICONTROL decisão no dispositivo] atividades.

Em visitas subsequentes ao site, o navegador verifica automaticamente se deve baixar uma versão mais recente do artefato. Essa verificação adiciona latência. O TTL de cache do artefato define o número de minutos que você não deseja que o navegador verifique se há um artefato atualizado desde o último download bem-sucedido. Quanto maior o período de tempo, melhor o desempenho. Quanto menor o período, melhor a atualização dos dados, mas à custa de latência adicional.

## Como faço para saber se uma atividade está [!UICONTROL decisão no dispositivo] elegível?

Depois de criar uma atividade que é [!UICONTROL decisão no dispositivo] elegível, um rótulo com a menção Decisão no dispositivo elegível, fica visível na página Visão geral.

![Rótulo Qualificado para Decisão no dispositivo na página Visão geral da atividade.](assets/on-device-decisioning-eligible-label.png)

Esse rótulo não significa que a atividade será sempre entregue via [!UICONTROL decisão no dispositivo]. Somente quando a at.js 2.5.0+ estiver configurada para usar [!UICONTROL decisão no dispositivo] essa atividade será executada no dispositivo. Se a at.js 2.5.0+ não estiver configurada para usar no dispositivo, essa atividade ainda será entregue por uma chamada de servidor feita da at.js.

É possível filtrar todas as atividades que estão [!UICONTROL decisão no dispositivo] elegível na página Atividades por meio do filtro Elegível para Decisão no dispositivo.

![Filtro elegível para decisão no dispositivo na página Atividades.](assets/on-device-decisioning-filter.png)

>[!NOTE]
>
>Depois de criar e ativar uma atividade que é [!UICONTROL decisão no dispositivo] elegível, pode levar de cinco a dez minutos antes de ser incluído no artefato de regras que é gerado e propagado para o ponto de presença do Akamai CDN.

## Resumo das etapas para garantir a [!UICONTROL decisão no dispositivo] As atividades do são fornecidas por meio da At.js 2.5.0+?

1. Acesse o [!DNL Adobe Target] e navegue até **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Detalhes da conta]** para habilitar o **[!UICONTROL Decisão no dispositivo]** alternar.
1. Ativar o **[!UICONTROL &quot;Incluir todos os existentes [!UICONTROL decisão no dispositivo] atividades qualificadas no artefato&quot;]** alternar.

   A primeira geração de artefatos de regras JSON pode levar até 10 minutos.

1. Criar e ativar um [tipo de atividade compatível com o [!UICONTROL decisão no dispositivo]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md)e verifique se está [!UICONTROL decisão no dispositivo] elegíveis.
1. Defina o **[!UICONTROL Método de decisão]** para **[!UICONTROL &quot;Híbrido&quot;]** ou **[!UICONTROL &quot;Somente no dispositivo&quot;]** por meio da interface de configurações do at.js.
1. Baixe e implante o At.js 2.5.0+ em suas páginas.
