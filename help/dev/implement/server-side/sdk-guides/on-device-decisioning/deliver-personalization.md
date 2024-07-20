---
title: Fornecer personalização usando SDKs da Adobe Target
description: Saiba como fornecer personalização usando o [!UICONTROL on-device decisioning].
feature: APIs/SDKs
exl-id: bac64c78-0d3a-40d7-ae2b-afa0f1b8dc4f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Entregar personalização

## Resumo das etapas

1. Habilitar [!UICONTROL on-device decisioning] para sua organização
1. Criar uma atividade [!UICONTROL Experience Targeting] (XT)
1. Definir experiência personalizada por público
1. Verificar experiência personalizada por público-alvo
1. Configurar relatórios
1. Adicionar métricas para KPIs de rastreamento
1. Implementar ofertas personalizadas em seu aplicativo
1. Implementar código para rastrear eventos de conversão
1. Ativar sua atividade de personalização do [!UICONTROL Experience Targeting] (XT)

Suponha que você seja uma empresa de turismo. Você deseja entregar uma oferta personalizada com 25% de desconto em determinados pacotes de viagem. Para que a oferta repercuta com seus usuários, você decide mostrar um ponto de referência da cidade de destino. Além disso, verifique se a entrega de suas ofertas personalizadas tem latência próxima de zero para que não afete negativamente as experiências do usuário e distorça os resultados.

## 1. Habilitar [!UICONTROL on-device decisioning] para sua organização

1. A ativação da decisão no dispositivo garante que uma atividade A/B seja executada com latência próxima a zero. Para habilitar este recurso, navegue até **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** em [!DNL Adobe Target] e habilite a alternância **[!UICONTROL On-Device Decisioning]**.

   ![alt imagem](assets/asset-odd-toggle.png)

   >[!NOTE]
   >
   >Você deve ter a [função de usuário](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) de Administrador ou Aprovador para habilitar ou desabilitar a [!UICONTROL On-Device Decisioning].

   Depois de habilitar a alternância **[!UICONTROL On-Device Decisioning]**, [!DNL Adobe Target] começa a gerar *artefatos de regra* para o seu cliente.

## 2. Criar uma atividade do [!UICONTROL Experience Targeting] (XT)

1. Em [!DNL Adobe Target], navegue até a página **[!UICONTROL Activities]** e selecione **[!UICONTROL Create Activity]** > **[!UICONTROL Experience Targeting]**.

   ![alt imagem](assets/asset-xt.png)

1. No modal **[!UICONTROL Create Experience Targeting Activity]**, deixe a opção **[!UICONTROL Web]** padrão selecionada (1), selecione **[!UICONTROL Form]** como compositor de experiência (2), selecione um espaço de trabalho e uma propriedade (3) e clique em **[!UICONTROL Next]** (4).

   ![alt imagem](assets/asset-xt-next.png)

## 3. Definir uma experiência personalizada por público

1. Na etapa **[!UICONTROL Experiences]** da criação da atividade, clique em **[!UICONTROL Change Audience]** para criar um público-alvo para os visitantes que desejam viajar para São Francisco, Califórnia.

   ![alt imagem](assets/asset-change-audience.png)

1. No modal **[!UICONTROL Create Audience]**, defina uma regra personalizada onde `destinationCity = San Francisco`. Isso define o grupo de usuários que deseja viajar para São Francisco.

   ![alt imagem](assets/asset-audience-sf.png)

1. Ainda na etapa **[!UICONTROL Experiences]**, digite o nome do local (1) no aplicativo em que deseja renderizar uma oferta especial sobre o Golden Gate Bridge, mas apenas para aqueles que vão para São Francisco. No exemplo mostrado aqui, homepage é o local selecionado para a oferta HTML (2), que é definido na área **[!UICONTROL Content]**.

   ![alt imagem](assets/asset-content-sf.png)

1. Adicione outro público-alvo de direcionamento clicando em **[!UICONTROL Add Experience Targeting]**. Desta vez, direcione a um público que gostaria de viajar para Nova York definindo uma regra de público em que `destinationCity = New York`. Defina o local no aplicativo onde deseja renderizar uma oferta especial sobre o Empire State Building. No exemplo mostrado aqui, `homepage` é o local selecionado para a oferta HTML (2), que é definido na área **[!UICONTROL Content]**.

   ![alt imagem](assets/asset-content-ny.png)

## 4. Verificar a experiência personalizada por público

Na etapa **[!UICONTROL Targeting]**, verifique se você configurou a experiência personalizada desejada por público-alvo.

![alt imagem](assets/asset-verify-sf-ny.png)

## 5. Configurar relatórios

Na etapa **[!UICONTROL Goals & Settings]**, escolha **[!UICONTROL Adobe Target]** como **[!UICONTROL Reporting Source]** para exibir os resultados da atividade na interface do usuário [!DNL Adobe Target], ou **[!UICONTROL Adobe Analytics]** para exibi-los na interface do usuário do Adobe Analytics.

![alt imagem](assets/asset-reporting-sf-ny.png)

## 6. Adicionar métricas para rastrear KPIs

Escolha um **[!UICONTROL Goal Metric]** para medir o sucesso da atividade. Neste exemplo, uma conversão bem-sucedida se baseia no fato de o usuário clicar na oferta de destino personalizada.

## 7. Implemente suas ofertas personalizadas no aplicativo

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {      
    execute: {
      pageLoad: {
        parameters: {
          destinationCity: "San Francisco"
        }
      }
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## 8. Implementar código para rastrear eventos de conversão

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

//When a conversion happens
TargetClient.sendNotifications({
    targetCookie,
    "request" : {
      "notifications" : [
        {
          type: "click",
          timestamp : Date.now(),
          id: "conversion",
          mbox : {
            name : "destinationOffer"
          }
        }
      ]
    }
})
```

>[!TAB Java]

```java {line-numbers="true"
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);
NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();

Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.CLICK);
notification.setTimestamp(System.currentTimeMillis());
notification.setTokens(
    Collections.singletonList(
        "IbG2Jz2xmHaqX7Ml/YRxRGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="));

TargetDeliveryRequest targetDeliveryRequest =
    TargetDeliveryRequest.builder()
        .context(context)
        .execute(executeRequest)
        .notifications(Collections.singletonList(notification))
        .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
notificationDeliveryService.sendNotification(request);
```

>[!ENDTABS]

## 9. Ativar sua atividade de Direcionamento de experiência (XT)

![alt imagem](assets/asset-xt-activate.png)
