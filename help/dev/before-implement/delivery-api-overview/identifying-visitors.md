---
title: API de entrega do Adobe Target para identificação de visitantes
description: Como posso identificar o usuário no [!DNL Adobe Target]?
keywords: api de entrega
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 9%

---

# Identificação de visitantes

Há várias maneiras de identificar um visitante no [!DNL Adobe Target].

O Target usa três identificadores:

| Nome do campo | Descrição |
| --- | --- |
| `tntId` | A variável `tntId` é o identificador principal em [!DNL Target] para um usuário. Você pode fornecer essa ID ou [!DNL Target] O será gerado automaticamente se a solicitação não contiver um. |
| `thirdPartyId` | A variável `thirdPartyId` é o identificador da sua empresa para o usuário que você pode enviar com cada chamada. Quando um usuário faz logon no site de uma empresa, a empresa normalmente cria uma ID vinculada à conta, ao cartão de fidelidade, ao número de associado ou a outros identificadores aplicáveis do visitante dessa empresa. |
| `marketingCloudVisitorId` | A variável `marketingCloudVisitorId` O é usado para mesclar e compartilhar dados entre diferentes soluções de Adobe. A variável `marketingCloudVisitorId` O é necessário para integrações com a Adobe Analytics e a Adobe Audience Manager. |
| `customerIds` | Juntamente com a ID de visitante do Experience Cloud, [IDs do cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) e um status autenticado para cada visitante pode ser utilizado. |

## [!DNL Target] ID

A variável [!DNL Target] ID ou `tntId` pode ser visto como uma ID de dispositivo. Este `tntId` é gerado automaticamente por [!DNL Target] se não for fornecido na solicitação. Posteriormente, os pedidos subsequentes devem incluir este `tntId` para que o conteúdo correto seja entregue a um dispositivo usado pelo usuário.

```http {line-numbers="true"}
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
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

O exemplo de chamada acima demonstra que um `tntId` não precisa ser transmitido. Nesse cenário, [!DNL Target]  gera um `tntId` e forneça na resposta, como mostrado aqui:

```URI {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "demo",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  ...
}
```

O gerado `tntId` é `10abf6304b2714215b1fd39a870f01afc.28_20`. Observe que `tntId` precisa ser usado ao chamar o [!UICONTROL API de entrega do Adobe Target] para o mesmo usuário em todas as sessões.

## ID de visitante da Marketing Cloud

A variável `marketingCloudVisitorId` O é uma ID universal e persistente que identifica os visitantes em todas as soluções da Experience Cloud. Quando sua organização implementa o serviço de ID, essa ID permite identificar o mesmo visitante do site e seus dados em soluções de Experience Cloud diferentes, como Adobe Target, Adobe Analytics ou Adobe Audience Manager. Observe que a variável `marketingCloudVisitorId` é necessário ao aproveitar e integrar com o Analytics e o Audience Manager.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "marketingCloudVisitorId": "10527837386392355901041112038610706884"
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

O exemplo de chamada acima demonstra como uma `marketingCloudVisitorId` que foi recuperado do Serviço da Experience Cloud ID é transmitido para a Adobe Target. Nesse cenário, [!DNL Target] gera um `tntId` já que não foi transmitido para a chamada original que será mapeada para a variável `marketingCloudVisitorId` como se vê na resposta abaixo.

## ID de terceiros

Se sua organização usar uma ID para identificar o visitante, você poderá usar `thirdPartyID` para fornecer conteúdo. No entanto, você deve fornecer a `thirdPartyID` para cada [!UICONTROL API de entrega do Adobe Target] ligue para fazer.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "thirdPartyId": "B234A029348"
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

O exemplo de chamada acima mostra uma `thirdPartyId`, que é uma ID persistente que sua empresa usa para identificar um usuário final, independentemente de ele estar interagindo com sua empresa a partir da Web, de dispositivos móveis ou da IoT. Por outras palavras, a `thirdPartyId` fará referência aos dados do perfil do usuário que podem ser utilizados em canais. Nesse cenário, [!DNL Target] gera um `tntId`, já que não foi passado para a chamada original, que será mapeada para a variável fornecida `thirdPartyId` como se vê na resposta abaixo.

```
{
    "status": 200,
    "requestId": "55de9886-bd14-4dee-819c-7d1633b79b90",
    "client": "demo",
    "id": {
        "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20",
        "thirdPartyId": "B234A029348"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    ...
}
```

## Customer ID

[IDs de cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) podem ser adicionados e associados a uma ID de visitante do Experience Cloud. Sempre que enviar `customerIds` o `marketingCloudVisitorId` também devem ser fornecidas. Além disso, um status de autenticação pode ser fornecido junto com cada `customerId` para cada visitante. O seguinte status de autenticação pode ser levado em consideração:

| Status de autenticação | Status do usuário |
| --- | --- |
| `unknown` | Desconhecido ou nunca autenticado. Esse estado pode ser usado para cenários como um visitante que chegou ao seu site clicando em um anúncio de exibição. |
| `authenticated` | O usuário está autenticado no momento com uma sessão ativa no seu site ou aplicativo. |
| `logged_out` | O usuário foi autenticado, mas fez logout ativamente. O usuário quis se desconectar do estado autenticado. O usuário não deseja mais ser tratado como autenticado. |

Observe que somente quando a ID do cliente estiver em `authenticated` O estado do terá como referência os dados de perfil do usuário armazenados e vinculados à id do cliente. Se a ID do cliente estiver em `unknown` ou `logged_out` , a id do cliente será ignorada e todos os dados de perfil do usuário que puderem ser associados a ela não serão aproveitados para direcionamento de público.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "customerIds": [{
          "id": "134325423",
          "integrationCode" : "crm_data",
          "authenticatedState" : "authenticated"
        }]
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
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

O exemplo de chamada acima demonstra como enviar uma `customerId` com um `authenticatedState`. Ao enviar uma `customerId`, o `integrationCode`, `id`, e `authenticatedState` bem como a `marketingCloudVisitorId` são obrigatórios. A variável `integrationCode` é o alias do [arquivo de atributos do cliente](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=pt-BR) você forneceu por meio do CRS.

## Perfil mesclado

É possível combinar `tntId`, `thirdPartyID`, e `marketingCloudVisitorId` no mesmo pedido. Nesse cenário, o Adobe Target manterá o mapeamento de todas essas IDs e o fixará a um visitante. Saiba como os perfis são [mesclado e sincronizado em tempo real](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) usando os diferentes identificadores.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "tntId": "d359234570e044f14e1faeeba02d6ab23439914e.28_78",
        "thirdPartyId":"23423432"
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

O exemplo de chamada acima demonstra como você pode combinar `tntId`, `thirdPartyID`, e `marketingCloudVisitorId` no mesmo pedido. Todas as três IDs também são retornadas na resposta.
