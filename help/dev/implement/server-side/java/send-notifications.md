---
title: Enviar notificações de exibição ou clique para [!DNL Adobe Target] usando o Java SDK
description: Saiba como usar sendNotifications() para enviar notificações de exibição ou clique em  [!DNL Adobe Target] para medição e relatórios.
feature: APIs/SDKs
exl-id: 9231b480-f50f-40d1-ab06-0b9f2a2d79e3
TQID: https://experienceleague.adobe.com/aoa6x9BkuaC-6XaqU03mvWXqWucNSF9eJAk41Bk0-nE
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 232
ht-degree: 2%

---

# Enviar notificações (Java)

## Descrição

`sendNotifications()` é usado para enviar notificações de clique ou exibição para [!DNL Adobe Target] para medição e relatórios.

>[!NOTE]
>
>Quando um objeto `execute` com parâmetros obrigatórios estiver dentro da própria solicitação, a impressão será aumentada automaticamente para atividades qualificadas.

Os métodos do SDK que incrementarão uma impressão automaticamente são:

* `getOffers()`
* `getAttributes()`

Quando um objeto `prefetch` é transmitido na solicitação, a impressão não é automaticamente incrementada para as atividades com mboxes no objeto `prefetch`. `sendNotifications()` deve ser usado para experiências previamente buscadas para incrementar impressões e conversões.

## Método

### criar

```javascript {line-numbers="true"}
ResponseStatus TargetClient.sendNotifications(TargetDeliveryRequest request)
```

## Exemplo

Primeiro, vamos criar a solicitação [!DNL Target Delivery API] de busca prévia de conteúdo para as mboxes `home` e `product1`.

### Pré-busca

```javascript {line-numbers="true"}
List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("home").index(1));
mboxRequests.add((MboxRequest) new MboxRequest().name("product1").index(2));
PrefetchRequest prefetchMboxesRequest = new PrefetchRequest().setMboxes(mboxRequests)

// Next, we fetch the offers via Target Java SDK getOffers() API
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```

Uma resposta bem-sucedida conterá um objeto de resposta [!UICONTROL API de Entrega de Destino], que contém conteúdo previamente buscado para as mboxes solicitadas. Um objeto de amostra `targetResponse.response` pode ter a seguinte aparência:

### Resposta

```javascript {line-numbers="true"}
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

Observe os campos mbox `name` e `state`, bem como o campo `eventToken`, em cada uma das opções de conteúdo [!DNL Target]. Eles devem ser fornecidos na solicitação `sendNotifications()`, assim que cada opção de conteúdo for exibida. Suponhamos que a mbox `product1` tenha sido exibida em um dispositivo que não seja um navegador. A solicitação de notificações terá esta aparência:

### Solicitação

```javascript {line-numbers="true"}
TargetDeliveryRequest mboxNotificationRequest = TargetDeliveryRequest.builder().notifications(new ArrayList() {{
    add(new Notification()
            .id("1")
            .timestamp(System.currentTimeMillis())
            .type(MetricType.DISPLAY)
            .mbox(new NotificationMbox()
                    .name("product1")
                    .state("J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
            )
            .tokens(Arrays.asList(new String[]{"t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="}))
    );
}}).build();
```

Observe que incluímos o estado da mbox e o token de evento correspondente à oferta [!DNL Target] entregue na resposta de busca prévia. Depois de criar a solicitação de notificações, podemos enviá-la para [!DNL Target] por meio do método de API `sendNotifications()`:

### Resposta

```javascript {line-numbers="true"}
ResponseStatus notificationResponse = targetJavaClient.sendNotifications(mboxNotificationRequest);
```
