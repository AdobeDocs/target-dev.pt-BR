---
title: Pré-busca da API de entrega do Adobe Target
description: Como usar a pré-busca no [!UICONTROL API de entrega do Adobe Target]?
keywords: api de entrega
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
source-git-commit: 9a3068b0765c238daa2f9af904c0f6f15b57cc24
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Pré-busca

A pré-busca permite que clientes como aplicativos e servidores móveis busquem conteúdo para várias mboxes ou exibições em uma solicitação, armazenem em cache localmente e notifiquem posteriormente [!DNL Target] quando o usuário visita essas mboxes ou visualizações.

Ao utilizar a busca prévia, é importante se familiarizar com os seguintes termos:

| Nome do campo | Descrição |
| --- | --- |
| `prefetch` | Lista de mboxes e exibições que devem ser buscadas, mas não devem ser marcadas como visitadas. A variável [!DNL Target] Edge retorna um `eventToke`n para cada mbox ou exibição existente na matriz de busca prévia. |
| `notifications` | Lista de mboxes e exibições que foram previamente buscadas e devem ser marcadas como visitadas. |
| `eventToken` | Um token criptografado com hash que é retornado quando o conteúdo é buscado previamente. Este token deve ser enviado de volta para [!DNL Target] no `notifications` matriz. |

## Buscar previamente mboxes

Clientes como aplicativos e servidores móveis podem realizar uma busca prévia por várias mboxes para um determinado usuário em uma sessão e armazená-las em cache para evitar várias chamadas para o [!UICONTROL API de entrega do Adobe Target].

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
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
    "prefetch": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      },
      {
        "name" : "SummerShoesOffer",
        "index" : 2
      },
      {
        "name" : "SummerDressOffer",
        "index" : 3
      }      
    ]
  }
}'
```

No prazo de `prefetch` adicione um ou mais `mboxes` você deseja realizar uma busca prévia de uma só vez para um usuário em uma sessão. Depois de realizar a busca prévia para eles `mboxes` você receberá a seguinte resposta:

```
{
    "status": 200,
    "requestId": "5efee0d8-3779-4b12-a74e-e04848faf191",
    "client": "demo",
    "id": {
        "tntId": "abcdefghijkl00023.1_1"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "mboxes": [
            {
                "index": 1,
                "name": "SummerOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            }
        ]
    }
}
```

Na resposta, você verá o `content` campo que contém a experiência a ser mostrada ao usuário para um determinado `mbox`. Isso é muito útil quando armazenado em cache no servidor, para que, quando um usuário interagir com o aplicativo da Web ou móvel em uma sessão e visitar um `mbox` em qualquer página específica do aplicativo, a experiência pode ser entregue do cache em vez de criar outra [!UICONTROL API de entrega do Adobe Target] chame. No entanto, quando uma experiência é entregue ao usuário pelo `mbox`, um `notification` serão enviados por uma chamada da API de entrega para que o registro de impressões ocorra. Isso ocorre porque a resposta do `prefetch` chamadas são armazenadas em cache, o que significa que o usuário não viu as experiências no momento em que `prefetch` ocorre a chamada. Para saber mais sobre a `notification` processo, consulte [Notificação](notifications.md).

## Buscar previamente mboxes com métricas clickTrack ao usar [!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics para Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html){target=_blank} O (A4T) é uma integração entre soluções que permite criar atividades com base no [!DNL Analytics] métricas de conversão e segmentos de público-alvo.

O trecho de código a seguir é uma resposta de uma busca prévia de uma mbox que contém `clickTrack` métricas para notificar [!DNL Analytics] que uma oferta foi clicada:

```
{
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "<mboxName>",
        "options": [
           ...
        ],
        "metrics": [
          {
            "type": "click",
            "eventToken": "<eventToken>",
             "analytics": {
               "payload": {
                 "pe": "tnt",
                 "tnta": "..."
               }
             }
          },
          }
        ],
        "analytics": {
          "payload": {
            "pe": "tnt",
            "tnta": "347565:1:0|2,347565:1:0|1"
          }
        }
      }
    ]
  }
}
```

>[!NOTE]
>
>A pré-busca de uma mbox contém a variável [!DNL Analytics] carga útil somente para atividades qualificadas. A busca prévia de métricas de sucesso para atividades ainda não qualificadas gera inconsistências de relatório.

## Visualizações de pré-busca

As exibições são compatíveis com Aplicativos de página única (SPA) e aplicativos móveis com mais facilidade. As exibições podem ser vistas como um grupo lógico de elementos visuais que, juntos, constituem uma experiência de SPA ou móvel. Agora, por meio da API de entrega, o VEC criou atividades AB &amp; XT com modificações no [Visualizações para SPA](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md) O agora pode ser buscado previamente.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=a3e7368c62d944c0855d424cd7a03ab0' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "window": {
      "width": 1819,
      "height": 842
    },
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "prefetch": {
    "views": [{}]
  }
}'
```

O exemplo de chamada acima buscará previamente todas as exibições criadas pelo VEC do SPA para atividades AB e XT para exibição na Web `channel`. Observe na chamada que queremos buscar previamente todas as exibições das atividades AB ou XT com as quais um visitante `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` que está visitando o `url`:`https://target.enablementadobe.com/react/demo/#/` qualifica para.

```
{
    "status": 200,
    "requestId": "14ce028e-d2d2-4504-b3da-32740fa8dd61",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "views": [
            {
                "id": 228,
                "name": "checkout-express",
                "key": "checkout-express",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV:nth-of-type(1) > DIV.mb-3:eq(2)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > FORM:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(3)",
                                "content": "<span style=\"color:#000080;\"><strong>*We charge an additional fee of $12.34 for faster delivery. If you choose express delivery get 15% off on your next order.</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 5,
                "name": "home",
                "key": "home",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
                                "content": "<span style=\"color:#800000;\"><strong>Trending Items</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 6,
                "name": "products",
                "key": "products",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setStyle",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > DIV.heading:eq(0) > BUTTON.btn:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > BUTTON:nth-of-type(1)",
                                "content": {
                                    "background-color": "rgba(191,0,0,1)",
                                    "priority": "important"
                                }
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            }
        ]
    }
}
```

No `content` da resposta, observe metadados como `type`, `selector`, `cssSelector`, e `content`, que são usados para renderizar a experiência para o usuário final quando um usuário visita sua página. Observe que `prefetched` o conteúdo pode ser armazenado em cache e renderizado para o usuário quando necessário.
