---
title: Integração com o Experience Cloud
description: Integração com o Experience Cloud
keywords: api de entrega
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 7%

---

<!-- The content on this page was originally pulled from the legacy Delivery API doc site, and was subsequently found to be an outdated version of information now found on [Implement > Server-side > Integration > A4T Reporting](../../implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md) and [Implement > Server-side > Integration > AAM Segments](../../implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md). Therefore sunsetting this page, but not deleting it from the repo immediately, pending a more thorough examination to avoid inadvertently deleting relevant content. -->


# Integração com o Experience Cloud

## Adobe Analytics for Target (A4T)

Quando uma chamada da API de entrega do Target é acionada no servidor, o Adobe Target retorna a experiência para esse usuário e, além disso, o Adobe Target retorna a carga do Adobe Analytics de volta para o chamador ou a encaminha automaticamente para o Adobe Analytics. Para enviar informações de atividade do Target para o Adobe Analytics no lado do servidor, há alguns pré-requisitos que precisam ser atendidos:

1. A atividade é configurada na interface do usuário do Adobe Target com o Adobe Analytics como fonte de relatórios e as contas são ativadas para A4T
1. A ID de visitante do Adobe Marketing Cloud é gerada pelo usuário da API e está disponível quando a chamada da API de entrega do Target é acionada

### O Adobe Target encaminha automaticamente a carga do Analytics

O Adobe Target pode encaminhar automaticamente a carga do Analytics para o Adobe Analytics por meio do lado do servidor se os seguintes identificadores forem fornecidos:

1. `supplementalDataId` - A ID usada para compilar entre o Adobe Analytics e o Adobe Target
1. `trackingServer` - O Adobe Analytics Server Para que o Adobe Target e o Adobe Analytics compilem os dados corretamente, o mesmo `supplementalDataId` precisa ser passado para o Adobe Target e o Adobe Analytics.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "supplementalDataId" : "23423498732598234",
          "trackingServer": "ags041.sc.omtrdc.net",
          "logging": "server_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

### Recuperar carga do Analytics do Adobe Target

Os consumidores da API de entrega do Adobe Target podem recuperar a carga do Adobe Analytics para uma mbox correspondente, para que o consumidor possa enviar a carga para o Adobe Analytics por meio da [API de inserção de dados](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Quando uma chamada do Adobe Target do lado do servidor for disparada, passe `client_side` para o campo `logging` na solicitação. Isso retornará uma carga se a mbox estiver presente em uma atividade que usa o Analytics como fonte de relatórios.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "logging": "client_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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

Depois de especificar `logging` = `client_side`, você receberá a carga no campo `mbox`, como mostrado abaixo.

```
{
    "status": 200,
    "requestId": "4b8855a5-8354-4ac4-8ae7-c551f7c0bb8a",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",

                    }
                ],
                "analytics": {
                    "payload": {
                        "pe": "tnt",
                        "tnta": "285408:0:0|2"
                    }
                }
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

Se a resposta do Target contiver qualquer item na propriedade `analytics` -> `payload`, encaminhe-a como está para a Adobe Analytics. O Analytics sabe processar essa carga. Isso pode ser feito em uma solicitação GET usando o seguinte formato:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Parâmetros e variáveis da string de consulta

| Nome do campo | Obrigatório | Descrição |
| --- | --- | --- |
| `rsid` | Sim | A ID do conjunto de relatórios |
| `pe` | Sim | Evento de página. Sempre definida como `tnt` |
| `tnta` | Sim | Carga do Analytics retornada pelo servidor de Destino em `analytics` -> `payload` -> `tnta` |
| `mid` | ID de visitante da Marketing Cloud |  |

### Valores de cabeçalho obrigatórios

| Nome do cabeçalho | Valor do cabeçalho |
| --- | --- |
| Host | Servidor de coleta de dados do Analytics (por exemplo: adobeags421.sc.omtrdc.net) |

### Exemplo de chamada Get HTTP da Inserção de dados A4T

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```

## Adobe Audience Manager

Os segmentos do Adobe Audience Manager (AAM) também podem ser aproveitados por meio das APIs de entrega do Adobe Target. Para aproveitar os segmentos do AAM, os seguintes campos devem ser fornecidos:

| Nome do campo | Obrigatório | Descrição |
| --- | --- | --- |
| `locationHint` | Sim | A DCS Location Hint é usada para determinar qual terminal DCS da AAM deve ser acessado para recuperar o perfil. Deve ser >= 1. |
| `marketingCloudVisitorId` | Sim | ID de visitante da Marketing Cloud |
| `blob` | Sim | O AAM Blob é usado para enviar dados adicionais para o AAM. Não pode estar em branco e seu tamanho &lt;= 1024. |

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "audienceManager": {
          "locationHint": 9,
          "blob": "32fdghkjh34kj5h43"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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
