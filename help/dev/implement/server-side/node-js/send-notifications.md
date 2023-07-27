---
title: Enviar notificações de exibição ou clique para [!DNL Adobe Target] usar o SDK do Node.js
description: Saiba como usar sendNotifications() para enviar notificações de exibição ou clique em [!DNL Adobe Target] para medição e relatórios.
feature: APIs/SDKs
exl-id: 84bb6a28-423c-457f-8772-8e3f70e06a6c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 4%

---

# Enviar notificações (Node.js)

## Descrição

`[!UICONTROL sendNotifications()]` é usado para enviar notificações de exibição ou clique para [!DNL Adobe Target] para medição e relatórios.

>[!NOTE]
>
>Quando um `execute` Se um objeto com parâmetros obrigatórios estiver dentro da própria solicitação, a impressão será aumentada automaticamente para atividades qualificadas.

Os métodos do SDK que incrementarão uma impressão automaticamente são:

* `getOffers()`
* `getAttributes()`

Quando um `prefetch` for transmitido na solicitação, a impressão não será automaticamente aumentada para as atividades com mboxes na variável `prefetch` objeto. `sendNotifications()` deve ser usado para experiências previamente buscadas para incrementar impressões e conversões.

## Método

### criar

```js {line-numbers="true"}
TargetClient.sendNotifications(options: Object): Promise
```

### Parâmetros

`options` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão |
| --- | --- | --- | --- |
| solicitação | Objeto | Sim | None |

## Exemplo

Primeiro, vamos criar o Target DSolicitação de API de entrega para busca prévia de conteúdo para o `home` e `product1` mboxes.

### Node.js

```js {line-numbers="true"}
const prefetchMboxesRequest = {
  prefetch: {
    mboxes: [
      { name: "home" },
      { name: "product1" }
    ]
  }
};
// Next, we fetch the offers via Target Node.js SDK getOffers() API
const targetResponse = await targetClient.getOffers({ request: prefetchMboxesRequest });
```

Uma resposta bem-sucedida conterá uma [!UICONTROL API de entrega do Target] objeto de resposta, que contém conteúdo previamente buscado para as mboxes solicitadas. Uma amostra `targetResponse.response` pode aparecer da seguinte maneira:

### Node.js

```js {line-numbers="true"}
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

Observe a mbox `name` e `state` campos, bem como a variável `eventToken` , em cada um dos [!DNL Target] opções de conteúdo. Estes devem ser fornecidos no quadro `sendNotifications()` assim que cada opção de conteúdo for exibida. Vamos supor que o `product1` A mbox foi exibida em um dispositivo que não é um navegador. A solicitação de notificações será exibida da seguinte maneira:

### Node.js

```js {line-numbers="true"}
const mboxNotificationRequest = {
  notifications: [{
    id: "1",
    timestamp: Date.now(),
    type: "display",
    mbox: {
      name: "product1",
      state: "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    },
    tokens: [ "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" ]
  }]
};
```

Observe que incluímos o estado da mbox e o token de evento correspondente ao [!DNL Target] oferta entregue na resposta de pré-busca. Depois de criar a solicitação de notificações, podemos enviá-la para [!DNL Target] por meio da `sendNotifications()` Método da API:

### Node.js

```js {line-numbers="true"}
const notificationResponse = await targetClient.sendNotifications({ request: mboxNotificationRequest });
```
