---
title: Como usar solicitações assíncronas no  [!DNL Adobe Target] .NET SDK
description: Saiba como o  [!DNL Target] Java SDK oferece suporte a solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.
feature: APIs/SDKs
exl-id: fd36cc7b-a884-4e57-93c2-8aff8256109a
TQID: https://experienceleague.adobe.com/E9rNmPdXe7HYg7XlIffpC4opGM9X6fFoHK-u0oLI-XE
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 91
ht-degree: 4%

---

# Solicitações Assíncronas (.NET)

## Descrição

Uma vantagem da integração do lado do servidor é que é possível aproveitar a grande largura de banda e os recursos de computação disponíveis no lado do servidor usando o paralelismo. [!DNL Target] O .NET SDK dá suporte a solicitações assíncronas, facilitando a integração do [!DNL Target] ao fluxo de trabalho assíncrono existente de um aplicativo.

## Métodos suportados

### \.NET

```dotnet {line-numbers="true"}
Task<TargetDeliveryResponse> GetOffersAsync(TargetDeliveryRequest request);
Task<TargetDeliveryResponse> SendNotificationsAsync(TargetDeliveryRequest request);
Task<TargetAttributes> GetAttributesAsync(TargetDeliveryRequest request, params string[] mboxes);
```

## Exemplo

Um exemplo de uso da API assíncrona do SDK pode ser exibido da seguinte maneira:

### \.NET

```dotnet {line-numbers="true"}
var deliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: new List<MboxRequest> { new MboxRequest(index: 1, name: "a1-serverside-ab") }))
    .Build();

var response = await this.targetClient.GetOffersAsync(deliveryRequest);

var notificationRequest = new TargetDeliveryRequest.Builder()
    .SetSessionId(response.Request.SessionId)
    .SetTntId(response.Response?.Id?.TntId)
    .SetNotifications(new List<Notification>
        {
            new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
                mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
                tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
        })
    .Build();

var notificationResponse = await this.targetClient.SendNotificationsAsync(notificationRequest);
```

Este exemplo supõe que você tenha [inicializado a SDK](initialize-sdk.md).
