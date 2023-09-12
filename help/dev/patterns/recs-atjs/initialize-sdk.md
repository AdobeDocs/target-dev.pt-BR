---
title: Inicializar SDKs
description: Verifique se todas as etapas necessárias para carregar o [!DNL Adobe Target] A biblioteca JavaScript at.js é executada na sequência correta.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 6cd78f8e3cbdd97a09b0cb6ca3af55994e85f819
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 8%

---

# Inicializar SDKs

Siga as etapas na guia *Inicializar SDK* diagrama para garantir que todas as tarefas necessárias para carregar o [!DNL Adobe Target] A biblioteca JavaScript at.js é executada na sequência correta.

>[!TIP]
>
>Clique nas imagens neste tópico para expandir para tela inteira.

## Inicializar diagrama de SDKs {#diagram}

Para aplicativos de várias páginas, esse fluxo ocorre sempre que a página é recarregada ou o visitante navega para uma nova página no site.

Os números de etapa na ilustração a seguir correspondem às seções abaixo.

![Inicializar diagrama de SDKs](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

Clique nos links a seguir para navegar até as seções desejadas:

* [1.1: Carregar SDK da API do visitante](#load)
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

## 1.1: Carregar SDK da API do visitante {#load}

Essa etapa ajuda a garantir que o `VisitorAPI.js` A biblioteca do é carregada, configurada e inicializada corretamente.

+++Ver detalhes

![Carregar diagrama do SDK da API do visitante](/help/dev/patterns/recs-atjs/assets/load-visitor-api-sdk.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Para usar o Serviço de ID/API do visitante, a empresa deve estar habilitada para o [!DNL Adobe Experience Cloud] e ter uma [!UICONTROL ID da organização]. Para obter mais informações, consulte [Requisitos de Experience Cloud: ID da organização](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} no *Ajuda do Serviço de identidade* guia.
* Você precisa do `VisitorAPI.js` arquivo. Você já deve ter esse arquivo se tiver [!DNL Adobe Analytics] implementado. Esse arquivo também pode ser adicionado por meio da [[!DNL Adobe Experience Platform] extensão de tags](https://experienceleague.adobe.com/docs/tags.html){target=_blank} or can be downloaded from the [Adobe Analytics Code Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank}.

**Configure e consulte VisitorAPI.js**

Para obter mais informações, consulte [Implementar o serviço Experience Cloud para Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**Leituras**

* [Visão geral do serviço de identidade do Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [Sobre o serviço de ID](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies e o serviço de identidade da Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Como o serviço de identidade do Experience Cloud solicita e define IDs](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [Como entender a sincronização de ID e as taxas de correspondência](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**Ações**

* Incorpore o `VisitorAPI.js` em suas páginas da Web.
* Leia sobre o [configurações disponíveis para o Serviço de ID/API do visitante](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* Depois que a variável `VisitorAPI.js` arquivo for carregado, use o `Visitor.getInstance` para inicializar usando as configurações necessárias.
* Familiarize-se com o [métodos disponíveis](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.2: Definir ID do cliente {#set}

Essa etapa ajuda a garantir que as IDs conhecidas dos visitantes (CRM ID, ID de usuário e assim por diante) sejam vinculadas à ID anônima do [!DNL Adobe] para personalização entre dispositivos.

+++Ver detalhes

![Definir ID do cliente](/help/dev/patterns/recs-atjs/assets/set-customer-id.png){width="400" zoomable="yes"}

**Pré-requisitos**

* A ID conhecida dos visitantes deve estar disponível na camada de dados.

**Definir ID do cliente**
Para obter mais informações, consulte [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**Leituras**

* [Sincronização de perfil em tempo real para mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**Ações**

* Uso `visitor.setCustomerIDs` para definir a ID de visitante conhecida.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.3: Configurar solicitação automática de carregamento de página {#automatic}

Esta etapa permite que a at.js busque todas as experiências que devem ser renderizadas na página ao carregar o arquivo da biblioteca at.js de JavaScript.

+++Ver detalhes

![Configurar solicitação automática de carregamento de página](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Nem todos os dados na camada de dados devem ser enviados para [!DNL Target]. Consulte sua equipe de negócios (equipe de marketing digital) para determinar quais dados são valiosos para experimentação, otimização e personalização. Somente esses dados devem ser enviados para [!DNL Target].
* Certifique-se de não enviar dados de Informações pessoais identificáveis (PII) para o [!DNL Target].

**Configurar solicitação automática de carregamento de página**

Para obter mais informações, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Leituras**

Saiba mais sobre o `pageLoadEnabled` configuração em [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Ações**

* Modifique o `window.targetGlobalSettings` para habilitar solicitações automáticas de carregamento de página.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.4: Configurar o tratamento de cintilação {#flicker}

Essa etapa ajuda a garantir que não haja cintilação da página ao fornecer experiências.

+++Ver detalhes

![Configurar diagrama de manipulação de cintilação](/help/dev/patterns/recs-atjs/assets/flicker-handling.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Discussões com a equipe responsável pelo desempenho da página da Web sobre os prós e contras do controle da cintilação usando o método padrão usado pela at.js. Pesquise por padrões de design que permitam usar a solução personalizada de manipulação de cintilação, como a animação de carregador. Se não encontrar um padrão, você poderá solicitar um novo padrão.

**Configurar o tratamento de cintilação**

Para obter mais informações, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

Configuração `bodyHidingEnabled` para `true` oculta o corpo inteiro da página enquanto a solicitação de carregamento de página está em andamento. Se você não tiver ativado a solicitação automática de carregamento de página por qualquer motivo (dados que depois não estarão prontos, por exemplo), é melhor definir essa configuração como `false`.

Se você tiver desativado `bodyHidingEnabled` como você não deseja acionar a APLR e deseja acionar a solicitação de página posteriormente ou porque não precisa do tratamento de cintilação, você deve implementar seu próprio tratamento de cintilação. Você pode lidar com a cintilação de duas maneiras: ocultando as seções em teste ou mostrando um ladrão nas seções em teste.

**Leituras**

* [Como a at.js gerencia a cintilação](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Saiba mais sobre os objetos bodyHiddenStyle e bodyHidingEnabled em [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Ações**

* Modifique o `window.targetGlobalSettings` objeto a ser definido `bodyHiddenStyle` e `bodyHidingEnabled`.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.5: Configurar mapeamento de dados {#data-mapping}

Essa etapa ajuda a garantir que todos os dados que devem ser enviados para o [!DNL Target] está definido.

+++Ver detalhes

![Diagrama de mapeamento de dados](/help/dev/patterns/recs-atjs/assets/data-mapping.png){width="400" zoomable="yes"}

**Pré-requisitos**

* A camada de dados deve estar pronta com todos os dados que devem ser enviados para o [!DNL Target].
* Recommendations: enriqueça o perfil.
   * Aprovado `entity.id` para capturar dados de critérios e itens visualizados recentemente com base em critérios baseados no último produto visualizado.
   * Aprovado `entity.id` para capturar dados para critérios de popularidade com base na categoria favorita.
   * Passe o atributo de perfil se os critérios personalizados se basearem nele ou se forem usados na filtragem da regra de inclusão em qualquer critério.
* Recommendations: assimilar dados do produto.
   * Outros parâmetros de entidade (reservados e personalizados) podem ser passados para assimilar ou atualizar o catálogo de produtos no [!DNL Recommendations].
   * O catálogo de produtos também pode ser atualizado usando feeds de entidade com o [!DNL Target] Interface do usuário ou API.

**Mapear dados para[!DNL Target]**

Para obter mais informações, consulte [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Leituras**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Planejar e implementar o Recommendations](/help/dev/implement/recommendations/recommendations.md)
* [Configurar o catálogo do Recommendations](/help/dev/implement/recommendations/recommendations.md)

**Ações**

* Use o `targetPageParams()` para definir todos os dados necessários que devem ser enviados para o [!DNL Target].

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.6: Promoção {#promotion}

Adicione itens promovidos e controle seu posicionamento no [!DNL Target Recommendations] [designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Ver detalhes

**Opções disponíveis**

* Promover por IDs
* [Promover por coleção](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promover por atributo](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Parâmetros de entidade obrigatórios**

* O atributo de item na promoção deve ser passado ao usar a opção &quot;promover por atributo&quot;.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.7: Critérios baseados no carrinho {#cart}

Faça recomendações com base no conteúdo do carrinho do usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Pessoas que visualizaram isto, visualizaram aquilo]
* [!UICONTROL Pessoas que visualizaram e compraram essas]
* [!UICONTROL Pessoas que compraram isto, compraram aquilo]

**Parâmetros de entidade obrigatórios**

* cartIds

**Leituras**

* [Baseado em carrinho](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.8: Critérios baseados na popularidade {#popularity}

Faça recomendações com base na popularidade geral de um item em todo o site ou na popularidade de itens na categoria, marca, gênero e assim por diante favoritas ou mais visualizadas de um usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Mais visualizados no site]
* [!UICONTROL Mais visualizados por categoria]
* [!UICONTROL Mais visualizados pelo atributo de item]
* [!UICONTROL Mais vendidos em todo o site]
* [!UICONTROL Mais vendidos por categoria]
* [!UICONTROL Mais Vendidos por Atributo de Item]
* [!UICONTROL Comece pela métrica do Analytics]

**Parâmetros de entidade obrigatórios**

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

* [!UICONTROL Pessoas que visualizaram isto, visualizaram aquilo]
* [!UICONTROL Pessoas que visualizaram isto, compraram aquilo]
* [!UICONTROL Pessoas que compraram isto, compraram aquilo]
* [!UICONTROL Itens com atributos similares]

**Parâmetros de entidade obrigatórios**

* `entity.id` ou qualquer atributo de perfil usado como uma chave

**Leituras**

* [Baseado em item](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.10: Critérios com base no usuário {#user}

Faça recomendações com base no comportamento do usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Itens visualizados recentemente ]
* [!UICONTROL Recomendado para você]

**Parâmetros de entidade obrigatórios**

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

**Parâmetros de entidade obrigatórios**

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

## 1.14: Passe o `entity.event.detailsOnly=true` parâmetro {#true}

Use atributos de entidade para passar informações do produto ou conteúdo para o [!DNL Target Recommendations].

+++Ver detalhes

**Leituras**

* [Atributos da entidade](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.15: Configurar mapeamento de dados remotos (remoto)

Essa etapa garante que todos os dados que devem ser enviados para o [!DNL Target] está definido.

+++Ver detalhes

![Diagrama de mapeamento de dados remoto](/help/dev/patterns/recs-atjs/assets/remote-data-mapping.png){width="400" zoomable="yes"}

**Pré-requisitos**

* A camada de dados deve estar pronta com todos os dados que devem ser enviados para o [!DNL Target].

**Configurar provedores de dados**

Para obter mais informações, consulte [Provedores de dados](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Leituras**

[função targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Ações**

Use o `targetPageParams()` para definir todos os dados necessários que devem ser enviados para o [!DNL Target].

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 1.16: Carregar at.js {#web}

Esta etapa garante que a biblioteca de JavaScript at.js do seja carregada e inicializada.

+++Ver detalhes

![Carregar diagrama do SDK da Web do Adobe Target](/help/dev/patterns/recs-atjs/assets/load-web-sdk.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Baixe ou peça à sua equipe de marketing digital para o `at.js 2.*x*` Arquivo da biblioteca JavaScript.

*Leituras*

* [Como o Target funciona](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [Como a at.js funciona](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Implementação do Target sem um gerenciador de tags](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Ações**

Incorpore o arquivo at.js em todas as páginas da Web em que experimentação, otimização, personalização e coleta de dados devem ocorrer.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)





























