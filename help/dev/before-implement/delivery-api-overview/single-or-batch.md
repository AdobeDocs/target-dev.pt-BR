---
title: Entrega em lote ou única API de entrega do Adobe Target
description: Como faço para usar [!UICONTROL Adobe Target Delivery API] chamadas de Entrega em lote ou únicas?
keywords: api de entrega
exl-id: 525cd1f2-616a-486c-8f49-8117615500bb
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Entrega única ou em lote

O [!UICONTROL Adobe Target Delivery API] dá suporte a uma chamada de entrega única ou em lote. Uma pessoa pode fazer uma solicitação de conteúdo do servidor para uma ou várias mboxes.

Avalie os custos de desempenho ao decidir fazer uma única chamada do em comparação com uma chamada em lote. Se você souber todo o conteúdo que precisa ser mostrado para um usuário, a prática recomendada é recuperar o conteúdo de todas as mboxes com uma única chamada de delivery em lote, a fim de evitar fazer várias chamadas de delivery únicas.

## Chamada de entrega única

Você pode recuperar uma experiência para exibir ao usuário para uma mbox por meio do [!UICONTROL Adobe Target Delivery API]. Observe que, se você estiver fazendo uma única chamada de delivery, precisará iniciar outra chamada de servidor para recuperar conteúdo adicional de uma mbox para um usuário. Isso pode ficar muito caro ao longo do tempo, portanto, avalie sua abordagem ao usar a chamada única de API de entrega.

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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

No exemplo de chamada de entrega única acima, a experiência é recuperada para ser exibida ao usuário com `tntId`: `abcdefghijkl00023.1_1` para um `mbox`:`SummerOffer` no canal da Web. Essa única chamada de delivery gerará a seguinte resposta:

```
{
  "status": 200,
  "requestId": "25e0cc42-3d7b-456a-8b49-af60c1fb23d9",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.1_1"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
    }
}
```

Na resposta, observe que o campo `content` contém o HTML que descreve a experiência a ser mostrada ao usuário para a Web que corresponde à mbox SummerOffer.

### Executar carregamento de página

Se houver experiências que devem ser mostradas quando ocorrer um carregamento de página no canal da Web, como o teste AB das fontes localizadas no rodapé ou no cabeçalho, você poderá especificar `pageLoad` no campo `execute` para recuperar todas as modificações que devem ser aplicadas.

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
  "execute": {
    "pageLoad": {}
  }
}'
```

A chamada de exemplo acima recupera todas as experiências para mostrar a um usuário quando a página `https://target.enablementadobe.com/react/demo/#/` é carregada.

```
{
      "status": 200,
      "requestId": "355ebc47-edb6-481f-aeae-ae55d71afaca",
      "client": "demo",
      "id": {
          "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
      },
      "edgeHost": "mboxedge28.tt.omtrdc.net",
      "execute": {
          "pageLoad": {
              "options": [
                  {
                      "content": [
                          {
                              "type": "setHtml",
                              "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV.nav:eq(0) > DIV.container:eq(0) > DIV.nav-right:eq(0) > A.nav-item:eq(0)",
                              "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > A:nth-of-type(1)",
                              "content": "Modified Home"
                          }
                      ],
                      "type": "actions"
                  }
              ],
              "metrics": [
                  {
                      "type": "click",
                      "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV.form-group:eq(0) > BUTTON.btn:eq(0)",
                      "eventToken": "QPaLjCeI9qKCBUylkRQKBg=="
                  }
              ]
          }
      }
  }
```

No campo `content`, a modificação que precisa ser aplicada em um carregamento de página pode ser recuperada. No exemplo acima, observe que um link no cabeçalho precisa ser nomeado como *Início Modificado*.

## Chamada de entrega em lote

Em vez de fazer várias chamadas de delivery com uma única mbox em cada chamada, fazer uma chamada de delivery com um lote de mboxes pode reduzir chamadas desnecessárias do servidor. A chamada de uma chamada de servidor deve ser minimizada o máximo possível para ter alto desempenho.

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
    "execute": {
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

No exemplo de chamada de entrega em lote acima, as experiências são recuperadas para exibição para o usuário com `tntId`: `abcdefghijkl00023.1_1` para vários `mbox`:`SummerOffer`, `SummerShoesOffer` e `SummerDressOffer`. Como sabemos que precisamos mostrar uma experiência para várias mboxes para esse usuário, podemos agrupar essas solicitações e fazer uma chamada de servidor, em vez de três chamadas de delivery individuais.

```
{
  "status": 200,
  "requestId": "fe15286f-effb-434f-85d8-c3db804075ce",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_120"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",

                  }
              ]
          },
          {
              "index": 2,
              "name": "SummerShoesOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>",
                      "type": "html",
                  }
              ]
          },
          {
              "index": 3,
              "name": "SummerDressOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
  }
}
```

Na resposta acima, você pode ver que, no campo `content` de cada mbox, a representação HTML da experiência para mostrar ao usuário para cada mbox é recuperável.
