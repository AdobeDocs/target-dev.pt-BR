---
title: Executar testes de recursos com atributos
description: Executar testes de recursos com atributos
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---

# Executar testes de recursos com atributos

## Resumo das etapas

1. Habilitar [!UICONTROL on-device decisioning] para sua organização
1. Criar uma atividade [!UICONTROL A/B Test]
1. Defina seus A e B
1. Adicionar um público
1. Definir alocação de tráfego
1. Definir a distribuição do tráfego para variações
1. Configurar relatórios
1. Adicionar métricas para KPIs de rastreamento
1. Implementar código para executar testes de recursos com atributos
1. Implementar código para rastrear eventos de conversão
1. Ative seus testes de recursos com atributos

>[!NOTE]
>
>Suponha que você seja uma empresa de comércio eletrônico varejista. Você deseja aumentar a taxa de conversão quando os clientes navegarem e classificarem o catálogo de produtos. Você tem uma hipótese de que certos algoritmos de classificação e estratégias de paginação produzem resultados melhores do que outros. Para testar essa teoria, você decide executar um teste de recurso que envolve o redesign do widget de classificação usando diferentes opções de classificação para os usuários finais. Certifique-se de que esse teste de recurso seja executado com latência próxima de zero para que ele não afete negativamente as experiências do usuário e distorça os resultados.

## 1. Habilitar [!UICONTROL on-device decisioning] para sua organização

A ativação da decisão no dispositivo garante que uma atividade A/B seja executada com latência próxima a zero. Para habilitar este recurso, navegue até **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** em [!DNL Adobe Target] e habilite a alternância **[!UICONTROL On-Device Decisioning]**.

![alt imagem](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Você deve ter a [função de usuário](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=pt-BR) de Administrador ou Aprovador para habilitar ou desabilitar a **[!UICONTROL On-Device Decisioning]**.

Depois de habilitar a alternância **[!UICONTROL On-Device Decisioning]**, [!DNL Adobe Target] começa a gerar *artefatos de regra* para o seu cliente.

## 2. Criar uma atividade [!UICONTROL A/B Test]

1. Em [!DNL Adobe Target], navegue até a página **[!UICONTROL Activities]** e selecione **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**.

   ![alt imagem](assets/asset-ab.png)

1. No modal **[!UICONTROL Create A/B Test Activity]**, deixe a opção padrão **[!UICONTROL Web]** selecionada (1), selecione **[!UICONTROL Form]** como compositor de experiência (2), selecione **[!UICONTROL Default Workspace]** com **[!UICONTROL No Property Restrictions]** (3) e clique em **[!UICONTROL Next]** (4).

   ![alt imagem](assets/asset-form.png)

## 3. Defina seus A e B

1. Na etapa de criação da atividade **[!UICONTROL Experiences]**, forneça um nome para a atividade (1) e adicione uma segunda experiência, Experiência B, clicando no botão **[!UICONTROL Add Experience]** (2). Digite o nome do local (3) no aplicativo onde deseja executar o teste de recurso com atributos. No exemplo mostrado abaixo, `product-results-page` é o local definido para a Experiência A. (Também é o local definido para a Experiência B.)

   ![alt imagem](assets/asset-location.png)

   **[!UICONTROL Experience A]** conterá o JSON que sinaliza à sua lógica comercial o seguinte:

   * Iniciar o recurso de algoritmo de classificação por meio do sinalizador de recurso `test_sorting`
   * Executar o algoritmo de classificação recomendado definido no `sorting_algorithm _**_attribute`
   * Retorne 50 produtos por página, conforme definido pela estratégia de paginação definida no `pagination_limit`

1. Na Experiência A, clique para alterar o conteúdo de **[!UICONTROL Default Content]** para JSON ao selecionar **[!UICONTROL Create JSON Offer]** conforme mostrado abaixo (1).

   ![alt imagem](assets/asset-offer.png)

1. Defina o JSON com os sinalizadores e atributos `test_sorting`, `sorting_algorithm` e `pagination_limit` que serão usados para iniciar o algoritmo de classificação recomendado com um limite de paginação de 50 produtos.

   >[!NOTE]
   >
   >Quando [!DNL Adobe Target] agrupa um usuário para ver a Experiência A, o JSON com os atributos definidos no exemplo serão retornados. Em seu código, será necessário verificar o valor do sinalizador de recurso `test_sorting` para ver se o recurso de classificação deve ser ativado. Em caso afirmativo, você usará o valor recomendado do atributo `sorting_algorithm` para mostrar os produtos recomendados na exibição da lista de produtos. O limite de produtos a ser exibido para seu aplicativo será 50, pois esse é o valor do atributo `pagination_limit`.

   ![alt imagem](assets/asset-sorting.png)

   O **[!UICONTROL Experience B]** definirá o JSON que sinaliza à sua lógica comercial o seguinte:

   * Iniciar o recurso de algoritmo de classificação por meio do sinalizador de recurso test_sorting
   * Executar o algoritmo de classificação `best_sellers` definido em `sorting_algorithm _**_attribute`
   * Retorne 50 produtos por página, conforme definido pela estratégia de paginação definida no `pagination_limit`

   >[!NOTE]
   >
   >Quando [!DNL Adobe Target] agrupa um usuário para ver a Experiência B, o JSON com os atributos definidos no exemplo serão retornados. Em seu código, será necessário verificar o valor do sinalizador de recurso `test_sorting` para ver se o recurso de classificação deve ser ativado. Em caso afirmativo, você usará o valor `best_sellers` do atributo `sorting_algorithm` para mostrar os produtos mais vendidos na exibição da lista de produtos. O limite de produtos a ser exibido para seu aplicativo será 50, pois esse é o valor do atributo `pagination_limit`.

   ![alt imagem](assets/asset-sorting-b.png)

## 4. Adicionar um público-alvo

Na etapa **[!UICONTROL Targeting]**, mantenha o público-alvo **[!UICONTROL All Visitors]**. Isso permitirá entender o impacto do recurso de classificação, bem como qual algoritmo e número de itens influenciam melhor os resultados.

![alt imagem](assets/asset-audience-b.png)

## 5. Definir a alocação de tráfego

Defina a porcentagem de seus visitantes em relação à qual você deseja testar os algoritmos de classificação e a estratégia de paginação. Em outras palavras, para que porcentagem de seus usuários você deseja implantar esse teste? Neste exemplo, para implantar este teste para todos os usuários conectados, mantenha a alocação de tráfego em 100%.

![alt imagem](assets/asset-allocation-100.png)

## 6. Definir a distribuição do tráfego para variações

Defina a porcentagem de seus visitantes que verão o algoritmo de classificação recomendado em comparação com os melhores vendedores, com um limite de 50 produtos por página. Neste exemplo, mantenha a distribuição do tráfego dividida em 50/50 entre as Experiências A e B.

![alt imagem](assets/asset-variations-50.png)

## 7. Configurar relatórios

Na etapa **[!UICONTROL Goals & Settings]**, escolha **[!UICONTROL Adobe Target]** como **[!UICONTROL Reporting Source]** para exibir os resultados do teste A/B na interface do usuário [!DNL Adobe Target], ou **[!UICONTROL Adobe Analytics]** para exibi-los na interface do usuário do Adobe Analytics.

![alt imagem](assets/asset-reporting-b.png)

## 8. Adicionar métricas para rastrear KPIs

Escolha um **[!UICONTROL Goal Metric]** para medir o teste de recurso com atributos. Neste exemplo, o sucesso se baseia no fato de o usuário comprar um produto, dependendo do algoritmo de classificação e da estratégia de paginação mostrada.

## 9. Implementar testes de recursos com atributos no aplicativo

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const options = {
  client: "testClient",
  organizationId: "ABCDEF012345677890ABCDEF0@AdobeOrg",
  decisioningMethod: "on-device",
  events: {
    clientReady: targetClientReady
  }
};
const targetClient = TargetClient.create(options);

function targetClientReady() {
  return targetClient.getAttributes(["product-results-page"]).then(function(attributes) {
    const test_sorting = attributes.getValue("product-results-page", "test-sorting");
    const sorting_algorithm = attributes.getValue("product-results-page", "sorting_algorithm");
    const pagination_limit = attributes.getValue("product-results-page", "pagination_limit");
  });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

ClientConfig config = ClientConfig.builder()
    .client("testClient")
    .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
    .build();
TargetClient targetClient = TargetClient.create(config);
MboxRequest mbox = new MboxRequest().name("product-results-page").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 10. Implementar código para rastrear eventos de conversão

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
            name : "product-results-page"
          }
        }
      ]
    }
})
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

Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 11. Ative seus testes de recursos com atributos

![alt imagem](assets/asset-activate.png)
