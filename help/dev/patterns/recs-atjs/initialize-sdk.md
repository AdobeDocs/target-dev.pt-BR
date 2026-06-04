---
title: Inicializar SDKs
description: Verifique se todas as etapas necessárias para carregar a biblioteca JavaScript do at.js [!DNL Adobe Target] foram executadas na sequência correta.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 250a8382-1fdd-4a70-b712-a25af5adad71
TQID: https://experienceleague.adobe.com/PxAKvxntUCdacBLopvANAI7-8OWe-ELQqFRJu-n3RWo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1879
ht-degree: 4%

---

# Inicializar SDKs

Siga as etapas do diagrama *Inicializar o SDK* para garantir que todas as tarefas necessárias para carregar a biblioteca at.js de JavaScript do [!DNL Adobe Target] sejam executadas na sequência correta.

>[!TIP]
>
>Clique nas imagens neste tópico para expandir para tela inteira.

## Inicializar diagrama de SDKs {#diagram}

Para aplicativos de várias páginas, esse fluxo ocorre sempre que a página é recarregada ou o visitante navega para uma nova página no site.

>[!NOTE]
>
>Os números de etapa na ilustração a seguir correspondem às seções abaixo. Os números de etapa não estão em uma ordem específica e não refletem a ordem das etapas realizadas na interface do usuário [!DNL Target] ao criar a atividade.

![Inicializar o diagrama de SDKs](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

Clique nos links a seguir para navegar até as seções desejadas:

* [1.1: Carregar API SDK do visitante](#load)
* [1.2: Definir ID do cliente](#set)
* [1.3: Configurar solicitação automática de carregamento de página](#automatic)
* [1.4: Configurar o tratamento de cintilação](#flicker)
* [1.5: Configurar mapeamento de dados](#data-mapping)
* [1.6: Promoção](#promotion)
* [1.7: Critérios baseados no carrinho](#cart)
* [1.8: Critérios baseados na popularidade](#popularity)
* [1.9: Critérios baseados em itens](#item)
* [1.10: Critérios com base no usuário](#user)
* [1.11: Critérios personalizados](#custom)
* [1.12: Fornecer atributos usados nas regras de inclusão](#inclusion)
* [1.13: Fornecer excludedIds](#exclude)
* [1.14: Transmitir o parâmetro entity.event.detailsOnly=true](#true)
* [1.15: Configurar mapeamento de dados remotos](#remote)
* [1.16: Carregar at.js](#web)

## 1.1: Carregar API SDK do visitante {#load}

Esta etapa ajuda a garantir que a biblioteca `VisitorAPI.js` seja carregada, configurada e inicializada corretamente.

+++Ver detalhes

![Carregar diagrama SDK da API de Visitante](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Para usar a ID de visitante/API Service, sua empresa deve estar habilitada para o [!DNL Adobe Experience Cloud] e ter uma [!UICONTROL ID da organização]. Para obter mais informações, consulte [Requisitos da Experience Cloud: ID da Organização](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} no guia *Ajuda do Serviço de Identidade*.
* Você precisa do arquivo `VisitorAPI.js`. Você já deve ter este arquivo se tiver o [!DNL Adobe Analytics] implementado. Este arquivo também pode ser adicionado por meio da [[!DNL Adobe Experience Platform] extensão de tags](https://experienceleague.adobe.com/docs/tags.html){target=_blank} ou pode ser baixado do [Gerenciador de Códigos Adobe Analytics](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank}.

**Configurar e consultar VisitorAPI.js**

Para obter mais informações, consulte [Implementar o Serviço da Experience Cloud para Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**Leituras**

* [Visão geral do serviço de identidade da Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [Sobre o serviço de ID](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies e o serviço de identidade da Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Como o serviço de identidade da Experience Cloud solicita e define IDs](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [Como entender a sincronização de ID e as taxas de correspondência](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**Ações**

* Incorpore o arquivo `VisitorAPI.js` às suas páginas da Web.
* Leia sobre as [configurações disponíveis para o Serviço de ID/API do Visitante](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* Depois que o arquivo `VisitorAPI.js` for carregado, use o método `Visitor.getInstance` para inicializar usando as configurações necessárias.
* Familiarize-se com os [métodos disponíveis](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.2: Definir ID do cliente {#set}

Essa etapa ajuda a garantir que as IDs conhecidas dos seus visitantes (CRM ID, ID de usuário e assim por diante) sejam vinculadas à ID anônima do [!DNL Adobe] para personalização entre dispositivos.

+++Ver detalhes

![Definir ID do Cliente](/help/dev/patterns/recs-atjs/assets/set-customer-id-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* A ID conhecida dos visitantes deve estar disponível na camada de dados.

**Definir ID do cliente**
Para obter mais informações, consulte [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**Leituras**

* [Sincronização de perfil em tempo real para mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**Ações**

* Use `visitor.setCustomerIDs` para definir a ID conhecida do visitante.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.3: Configurar solicitação automática de carregamento de página {#automatic}

Essa etapa permite que a at.js busque todas as experiências que devem ser renderizadas na página ao carregar o arquivo da biblioteca JavaScript at.js.

+++Ver detalhes

![Configurar solicitação automática de carregamento de página](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Nem todos os dados na camada de dados devem ser enviados para [!DNL Target]. Consulte sua equipe de negócios (equipe de marketing digital) para determinar quais dados são valiosos para experimentação, otimização e personalização. Somente estes dados devem ser enviados para [!DNL Target].
* Certifique-se de não enviar dados de Informações de Identificação Pessoal (PII) para [!DNL Target].

**Configurar solicitação automática de carregamento de página**

Para obter mais informações, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Leituras**

Saiba mais sobre a configuração `pageLoadEnabled` em [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Ações**

* Modifique o objeto `window.targetGlobalSettings` para habilitar solicitações automáticas de carregamento de página.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.4: Configurar o tratamento de cintilação {#flicker}

Essa etapa ajuda a garantir que não haja cintilação da página ao fornecer experiências.

+++Ver detalhes

![Configurar diagrama de manipulação de cintilação](/help/dev/patterns/recs-atjs/assets/flicker-handling-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Discussões com a equipe responsável pelo desempenho da página da Web sobre os prós e contras do controle da cintilação usando o método padrão usado pela at.js. Pesquise por padrões de design que permitam usar a solução personalizada de manipulação de cintilação, como a animação de carregador. Se não encontrar um padrão, você poderá solicitar um novo padrão.

**Configurar tratamento de cintilação**

Para obter mais informações, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

A configuração de `bodyHidingEnabled` como `true` oculta o corpo inteiro da página enquanto a solicitação de carregamento de página está em andamento. Se você não tiver habilitado a solicitação automática de carregamento de página por qualquer motivo (dados não prontos posteriormente, por exemplo), é melhor definir essa configuração como `false`.

Se você desabilitou o `bodyHidingEnabled` porque não deseja acionar a APLR e deseja acionar a solicitação de página mais tarde, ou não precisa do tratamento de cintilação, você deve implementar seu próprio tratamento de cintilação. Você pode lidar com a cintilação de duas maneiras: ocultando as seções em teste ou mostrando um ladrão nas seções em teste.

**Leituras**

* [Como a at.js gerencia a cintilação](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Saiba mais sobre os objetos bodyHiddenStyle e bodyHidingEnabled em [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Ações**

* Modifique o objeto `window.targetGlobalSettings` para definir `bodyHiddenStyle` e `bodyHidingEnabled`.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.5: Configurar mapeamento de dados {#data-mapping}

Esta etapa ajuda a garantir que todos os dados que devem ser enviados para [!DNL Target] sejam definidos.

+++Ver detalhes

![Diagrama de mapeamento de dados](/help/dev/patterns/recs-atjs/assets/data-mapping-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* A camada de dados deve estar pronta com todos os dados que devem ser enviados para [!DNL Target].
* Recommendations: enriqueça o perfil.
   * Envie `entity.id` para capturar dados de critérios e itens visualizados recentemente com base em critérios baseados no último produto visualizado.
   * Envie `entity.id` para capturar dados para critérios de popularidade com base na categoria favorita.
   * Passe o atributo de perfil se os critérios personalizados se basearem nele ou se forem usados na filtragem da regra de inclusão em qualquer critério.
* Recommendations: assimilar dados do produto.
   * Outros parâmetros de entidade (reservados e personalizados) podem ser passados para assimilar ou atualizar o catálogo de produtos em [!DNL Recommendations].
   * O catálogo de produtos também pode ser atualizado usando feeds de entidade com a interface ou a API [!DNL Target].

**Mapear dados para[!DNL Target]**

Para obter mais informações, consulte [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Leituras**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Planejar e implementar o Recomendações](/help/dev/implement/recommendations/recommendations.md)
* [Configurar o catálogo de recomendações](/help/dev/implement/recommendations/recommendations.md)

**Ações**

* Use a função `targetPageParams()` para definir todos os dados necessários que devem ser enviados para [!DNL Target].

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.6: Promoção {#promotion}

Adicione itens promovidos e controle o posicionamento nos [!DNL Target Recommendations] [designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Ver detalhes

**Opções disponíveis**

* Promover por IDs
* [Promover por coleção](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promover por atributo](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Parâmetros de entidade necessários**

* O atributo de item na promoção deve ser passado ao usar a opção &quot;promover por atributo&quot;.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.7: Critérios baseados no carrinho {#cart}

Faça recomendações com base no conteúdo do carrinho do usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Pessoas que os visualizaram, visualizaram]
* [!UICONTROL Pessoas que os viram, compraram]
* [!UICONTROL Pessoas que Compraram Estes, Compraram Aqueles]

**Parâmetros de entidade necessários**

* cartIds

**Leituras**

* [Baseado em carrinho](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.8: Critérios baseados na popularidade {#popularity}

Faça recomendações com base na popularidade geral de um item em todo o site ou na popularidade de itens na categoria, marca, gênero e assim por diante favoritas ou mais visualizadas de um usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Mais visualizados em todo o site]
* [!UICONTROL Mais Visualizados por Categoria]
* [!UICONTROL Mais Visualizados pelo Atributo de Item]
* [!UICONTROL Mais vendidos em todo o site]
* [!UICONTROL Mais vendidos por categoria]
* [!UICONTROL Mais vendidos por atributo de item]
* [!UICONTROL Métrica Top by Analytics]

**Parâmetros de entidade necessários**

* `entity.categoryId` ou o atributo de item para popularidade com base no critério do item atual ou no atributo de item.
* Nada deve ser passado para Mais visualizados/Principais vendidos no site.

**Leituras**

* [Baseado em popularidade](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.9: Critérios baseados em itens {#item}

Fazer recomendações com base na localização de itens semelhantes a um item que o usuário está visualizando ou que foi visualizado recentemente.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Pessoas Que Visualizaram Isto, Visualizaram Aquilo]
* [!UICONTROL Pessoas que Visualizaram Isto, Compraram Aquilo]
* [!UICONTROL Pessoas que Compraram Isto, Compraram Aquilo]
* [!UICONTROL Itens com Atributos Semelhantes]

**Parâmetros de entidade necessários**

* `entity.id` ou qualquer atributo de perfil usado como uma chave

**Leituras**

* [Baseado em item](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.10: Critérios com base no usuário {#user}

Faça recomendações com base no comportamento do usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Itens visualizados recentemente]
* [!UICONTROL Recomendado para você]

**Parâmetros de entidade necessários**

* `entity.id`

**Leituras**

* [Baseado em usuário](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.11: Critérios personalizados {#custom}

Fazer recomendações com base em um arquivo personalizado que você carregou.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Algoritmo personalizado]

**Parâmetros de entidade necessários**

`entity.id` ou o atributo usado como uma chave para o algoritmo personalizado

**Leituras**

* [Critérios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.12: Fornecer atributos usados nas regras de inclusão {#inclusion}

+++Ver detalhes

**Leituras**

* [Uso das regras de inclusão estática e dinâmica](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.13: Fornecer excludedIds {#exclude}

Transmita IDs de entidade para entidades que você deseja excluir de suas recomendações. Por exemplo, você pode desejar excluir itens que já estão no carrinho de compras.

+++Ver detalhes

**Leituras**

* [Posso excluir dinamicamente uma entidade?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.14: Passar o parâmetro `entity.event.detailsOnly=true` {#true}

Use atributos de entidade para passar informações sobre o produto ou conteúdo para [!DNL Target Recommendations].

+++Ver detalhes

**Leituras**

* [Atributos da entidade](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.15: Configurar mapeamento de dados remotos (remoto)

Esta etapa garante que todos os dados que devem ser enviados para [!DNL Target] sejam definidos.

+++Ver detalhes

![Diagrama de mapeamento de dados remoto](/help/dev/patterns/recs-atjs/assets/remote-data-mapping-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* A camada de dados deve estar pronta com todos os dados que devem ser enviados para [!DNL Target].

**Configurar provedores de dados**

Para obter mais informações, consulte [Provedores de dados](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Leituras**

[função targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Ações**

Use a função `targetPageParams()` para definir todos os dados necessários que devem ser enviados para [!DNL Target].

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.16: Carregar at.js {#web}

Essa etapa garante que a biblioteca JavaScript at.js seja carregada e inicializada.

+++Ver detalhes

![Carregar diagrama at.js do Adobe Target](/help/dev/patterns/recs-atjs/assets/load-atjs-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Baixe ou peça o arquivo da biblioteca JavaScript `at.js 2.*x*` à sua equipe de marketing digital.

*Leituras*

* [Como o Target funciona](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [Como a at.js funciona](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Implementação do Target sem um gerenciador de tags](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Ações**

Incorpore o arquivo at.js em todas as páginas da Web em que experimentação, otimização, personalização e coleta de dados devem ocorrer.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

Vá para a Etapa 2: [Configurar a coleta de dados](/help/dev/patterns/recs-atjs/data-collection.md).
