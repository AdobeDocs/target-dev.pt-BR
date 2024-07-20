---
title: Enviar notificações de exibição ou de clique para  [!DNL Adobe Target] usando o SDK do .NET
description: Saiba como usar sendNotifications() para enviar notificações de exibição ou clique em  [!DNL Adobe Target] para medição e relatórios.
feature: APIs/SDKs
exl-id: 724e787c-af53-4152-8b20-136f7b5452e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Enviar Notificações (.NET)

## Descrição

`SendNotifications()` é usado para enviar notificações de clique ou exibição para [!DNL Adobe Target] para medição e relatórios.

>[!NOTE]
>
>Quando um objeto `Execute` com parâmetros obrigatórios estiver dentro da própria solicitação, a impressão será aumentada automaticamente para atividades qualificadas.

Os métodos do SDK que incrementarão uma impressão automaticamente são:

* `GetOffers()`
* `GetAttributes()`

Quando um objeto `Prefetch` é transmitido na solicitação, a impressão não é automaticamente incrementada para as atividades com mboxes no objeto `Prefetch`. `SendNotifications()` deve ser usado para experiências previamente buscadas para incrementar impressões e conversões.

## Método

### Criar 

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.SendNotifications(TargetDeliveryRequest request)
```

## Exemplo

Primeiro, vamos criar a solicitação [!UICONTROL Target Delivery API] de busca prévia de conteúdo para as mboxes `home` e `product1`.

### \.NET

```dotnet {line-numbers="true"}
var mboxRequests = new List<MboxRequest>
    {
        new (index: 1, name: "home"),
        new (index: 2, name: "product1"),
    };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetPrefetch(new PrefetchRequest(mboxes: mboxRequests))
    .Build();

// Next, we fetch the offers via Target .NET SDK GetOffers() API
var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```

Uma resposta bem-sucedida conterá um objeto de resposta [!DNL Target Delivery API], que contém conteúdo previamente buscado para as mboxes solicitadas. Um objeto de amostra `targetResponse.Response` pode aparecer da seguinte maneira:

### \.NET

```dotnet {line-numbers="true"}
{
  "status": 200,
  "requestId": "e8ac2dbf5f7d4a9f9280f6071f24a01e",
  "id": {
    "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "adobetargetmobile",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "home",
        "options": [
          {
            "type": "html",
            "content": "HOME OFFER",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      },
      {
        "index": 1,
        "name": "product1",
        "options": [
          {
            "type": "html",
            "content": "TEST OFFER 1",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      }
    ]
  }
}
```

Anote o nome `mbox` e os campos `state`, bem como o campo `eventToken`, em cada uma das opções de conteúdo [!DNL Target]. Eles devem ser fornecidos na solicitação `SendNotifications()`, assim que cada opção de conteúdo for exibida. Suponhamos que a mbox `product1` tenha sido exibida em um dispositivo que não seja um navegador. A solicitação de notificações será exibida da seguinte maneira:

### \.NET

```dotnet {line-numbers="true"}
var mboxNotifications = new List<Notification>
{
    new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
        mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
        tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
}; 

var mboxNotificationRequest = new TargetDeliveryRequest.Builder()
    .SetNotifications(mboxNotifications)
    .Build();
```

Observe que incluímos o estado da mbox e o token do evento correspondente à oferta [!DNL Target] entregue na resposta da busca prévia. Depois de criar a solicitação de notificações, podemos enviá-la para [!DNL Target] por meio do método de API `SendNotifications()`:

### \.NET

```dotnet {line-numbers="true"}
var notificationResponse = targetClient.SendNotifications(mboxNotificationRequest);
```
