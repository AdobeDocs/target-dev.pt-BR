---
title: Notificações da API de entrega do Adobe Target
description: Como acionar notificações usando o [!UICONTROL API de entrega do Adobe Target]?
keywords: api de entrega
exl-id: 711388fd-2c1f-4ca4-939f-c56dc4bdc04a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Notificações

As notificações devem ser disparadas quando uma mbox ou visualização previamente buscada for visitada ou renderizada para o usuário final.

Para que as notificações sejam desativadas para a mbox ou exibição correta, certifique-se de rastrear os eventos correspondentes `eventToken` para cada mbox ou exibição. Notificações com o correto `eventToken` para as mboxes ou exibições correspondentes, são necessárias para que os relatórios sejam refletidos corretamente.

## Notificações para mboxes buscadas previamente

Uma ou várias notificações podem ser enviadas por meio de uma única chamada de entrega. Determine se a métrica que precisa ser rastreada é uma `click` ou `display` para cada mbox, de modo que as `type` da notificação possa ser refletida corretamente. Além disso, transmita em um `id` para cada notificação, de modo que seja possível determinar se uma notificação foi enviada corretamente[!UICONTROL  API de entrega do Adobe Target]. A variável `timestamp` também é importante ser encaminhado para [!DNL Target] para indicar quando a variável `click` ou `display` ocorreu para uma determinada mbox para fins de relatórios.

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
    "id": {
      "tntId": "abcdefghijkl00023.1_1"
    },
    "context": {
      "channel": "web",
      "browser" : {
        "host" : "demo"
      },
      "address" : {
        "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
      },
      "screen" : {
        "width" : 1200,
        "height": 1400
      }
    },
      "notifications": [
      {
      "id" : "SummerOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerShoesOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerShoesOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerDressOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerDressOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
    } 
    ]
  }'
```

O exemplo de chamada acima resultará em uma resposta que indica a `notifications` A solicitação do foi processada com sucesso.

```
{
  "status": 200,
  "requestId": "36014eed-4772-4c48-a9e2-e532762b6a85",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "notifications": [
      {
          "id": "SummerOfferNotification"
      },
      {
          "id": "SummerDressOfferNotification"
      },
      {
          "id": "SummerShoesOfferNotification"
      }
  ]
}
```

Se todas as `notifications` enviado para [!DNL Target] forem processados corretamente, aparecerão no `notifications` na resposta. No entanto, se uma `notifications` `id` está ausente, essa `notification` não foi aprovado. Nesse cenário, uma lógica de nova tentativa pode ser colocada em prática até que uma `notification` a resposta do será recuperada. Verifique se a lógica de repetição tem um tempo limite especificado para que a chamada à API não seja bloqueada e cause atrasos de desempenho.

## Notificações para Exibições Pré-buscadas

Uma ou várias notificações podem ser enviadas por meio de uma única chamada de entrega. Determine se a métrica que precisa ser rastreada é uma `click` ou `display` para cada mbox, para que o tipo de notificação possa ser refletido corretamente. Além disso, transmita em um `id` para cada notificação, de modo que seja possível determinar se uma notificação foi enviada corretamente [!UICONTROL API de entrega do Adobe Target]. O carimbo de data e hora também é importante para ser encaminhado ao [!DNL Target] para indicar quando a variável `click` ou `display` ocorreu para uma determinada exibição para fins de relatório.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "notifications": [{
      "id": "228",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "checkout-express",
      }
    },
    {
      "id": "5",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "home",
      }
    },
    {
      "id": "6",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "products",
      }
    }
  ]
}'
```

O exemplo de chamada acima resultará em uma resposta que indica a `notifications` A solicitação do foi processada com sucesso.

```
{
    "status": 200,
    "requestId": "85cc7394-c19a-4398-9b8b-bbee1e4c4579",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "notifications": [
        {
            "id": "5"
        },
        {
            "id": "6"
        },
        {
            "id": "228"
        }
    ]
}
```

Se todas as `notifications` enviado para  [!DNL Target] forem processados corretamente, aparecerão no `notifications` na resposta. No entanto, se uma `notifications` `id` falta, essa notificação específica não foi recebida. Nesse cenário, uma lógica de nova tentativa pode ser colocada em prática até que uma resposta de notificação bem-sucedida seja recuperada. Verifique se a lógica de repetição tem um tempo limite especificado para que a chamada à API não seja bloqueada e cause atrasos de desempenho.
