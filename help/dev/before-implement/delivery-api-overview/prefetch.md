---
title: Pré-busca da API de entrega do Adobe Target
description: Como usar a pré-busca no [!UICONTROL Adobe Target Delivery API]?
keywords: api de entrega
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
source-git-commit: 4ff2746b8b485fe3d845337f06b5b0c1c8d411ad
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# Pré-busca

A pré-busca permite que clientes como aplicativos e servidores móveis busquem conteúdo para várias mboxes ou exibições em uma solicitação, armazenem em cache localmente e depois notifiquem [!DNL Target] quando o visitante visitar essas mboxes ou exibições.

Ao usar a busca prévia, é importante se familiarizar com os seguintes termos:

| Nome do campo | Descrição |
| --- | --- |
| `prefetch` | Lista de mboxes e exibições que devem ser buscadas, mas não devem ser marcadas como visitadas. O Edge [!DNL Target] retorna um `eventToken` para cada mbox ou exibição existente na matriz de busca prévia. |
| `notifications` | Lista de mboxes e exibições que foram previamente buscadas e devem ser marcadas como visitadas. |
| `eventToken` | Um token criptografado com hash que é retornado quando o conteúdo é buscado previamente. Este token deve ser enviado de volta para [!DNL Target] na matriz `notifications`. |

## Buscar previamente mboxes

Os clientes, como aplicativos e servidores móveis, podem realizar a busca prévia de várias mboxes para um determinado visitante em uma sessão e armazená-las em cache para evitar várias chamadas para o [!UICONTROL Adobe Target Delivery API].

```shell shell-session
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

No campo `prefetch`, adicione um ou mais `mboxes` que você deseja buscar previamente pelo menos uma vez para um visitante em uma sessão. Depois de realizar uma busca prévia para esses `mboxes`, você receberá a seguinte resposta:

```JSON {line-numbers="true"}
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

Na resposta, você vê o campo `content` que contém a experiência a ser mostrada ao visitante para uma `mbox` específica. Isso é muito útil quando armazenado em cache no servidor, para que, quando um visitante interagir com o aplicativo da Web ou móvel em uma sessão e visitar um `mbox` em qualquer página específica do aplicativo, a experiência possa ser entregue do cache em vez de fazer outra chamada [!UICONTROL Adobe Target Delivery API]. No entanto, quando uma experiência é entregue ao visitante do `mbox`, um `notification` é enviado por meio de uma chamada da API de entrega para que ocorra o registro de impressões. Isso ocorre porque a resposta das chamadas de `prefetch` é armazenada em cache, o que significa que o visitante não viu as experiências no momento em que a chamada de `prefetch` acontece. Para saber mais sobre o processo `notification`, consulte [Notificações](notifications.md).

## Buscar previamente mboxes com `clickTrack` métricas ao usar [!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics for Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=pt-BR){target=_blank} (A4T) é uma integração entre soluções que permite criar atividades com base em [!DNL Analytics] métricas de conversão e segmentos de público-alvo.

O trecho de código a seguir é uma resposta de uma busca prévia de uma mbox contendo `clickTrack` métricas para notificar [!DNL Analytics] que uma oferta foi clicada:

```JSON {line-numbers="true"}
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
>A pré-busca de uma mbox contém a carga [!DNL Analytics] somente para atividades qualificadas. A busca prévia de métricas de sucesso para atividades ainda não qualificadas gera inconsistências de relatório.

## Visualizações de pré-busca

As exibições são compatíveis com Aplicativos de página única (SPA) e aplicativos móveis com mais facilidade. As exibições podem ser vistas como um grupo lógico de elementos visuais que, juntos, constituem uma experiência de SPA ou móvel. Agora, por meio da API de Entrega, as atividades [[!UICONTROL A/B Test]](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=pt-BR){target=_blank} e [[!UICONTROL Experience Targeting]](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=pt-BR){target=_blank} (X)T criadas pelo VEC com modificações em [Exibições para SPA](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md) podem ser buscadas previamente.

```shell  {line-numbers="true"}
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

A chamada de exemplo acima busca previamente todos os Modos de Exibição criados por meio do VEC para SPA para [!UICONTROL A/B Test] e atividades XT para exibição na Web `channel`. Observe que a chamada busca previamente todos os Modos de Exibição das atividades de [!UICONTROL A/B Test] ou XT para os quais um visitante com `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` que está visitando `url`:`https://target.enablementadobe.com/react/demo/#/` se qualifica.

```JSON  {line-numbers="true"}
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

Nos campos `content` da resposta, observe metadados como `type`, `selector`, `cssSelector` e `content`, que são usados para renderizar a experiência para seu visitante quando um usuário visita sua página. Observe que o conteúdo `prefetched` pode ser armazenado em cache e renderizado para o usuário quando necessário.
