---
title: API de entrega do Adobe Target para identificação de visitantes
description: Como posso identificar o usuário em  [!DNL Adobe Target]?
keywords: api de entrega
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 7%

---

# Identificação de visitantes

Há várias maneiras pelas quais um visitante pode ser identificado dentro de [!DNL Adobe Target].

O Target usa três identificadores:

| Nome do campo | Descrição |
| --- | --- |
| `tntId` | O `tntId` é o identificador principal em [!DNL Target] de um usuário. Você pode fornecer essa ID ou [!DNL Target] irá gerá-la automaticamente se a solicitação não contiver uma. |
| `thirdPartyId` | O `thirdPartyId` é o identificador de sua empresa para o usuário que você pode enviar com cada chamada. Quando um usuário faz logon no site de uma empresa, a empresa normalmente cria uma ID vinculada à conta, ao cartão de fidelidade, ao número de associado ou a outros identificadores aplicáveis do visitante dessa empresa. |
| `marketingCloudVisitorId` | O `marketingCloudVisitorId` é usado para mesclar e compartilhar dados entre diferentes soluções de Adobe. O `marketingCloudVisitorId` é necessário para integrações com o Adobe Analytics e o Adobe Audience Manager. |
| `customerIds` | Juntamente com a ID de visitante do Experience Cloud, podem ser utilizadas [IDs adicionais do cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=pt-BR) e um status autenticado para cada visitante. |

## [!DNL Target] ID

A [!DNL Target] ID ou `tntId` pode ser vista como uma ID de dispositivo. Este `tntId` é gerado automaticamente por [!DNL Target] se não for fornecido na solicitação. Consequentemente, as solicitações subsequentes precisam incluir este `tntId` para que o conteúdo correto seja entregue a um dispositivo usado pelo usuário.

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

O exemplo de chamada acima demonstra que um `tntId` não precisa ser passado. Neste cenário, [!DNL Target] gera um `tntId` e o fornece na resposta, como mostrado aqui:

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

O `tntId` gerado é `10abf6304b2714215b1fd39a870f01afc.28_20`. Observe que este `tntId` precisa ser usado quando você chamar [!UICONTROL Adobe Target Delivery API] para o mesmo usuário em várias sessões.

## ID de visitante da Marketing Cloud

O `marketingCloudVisitorId` é uma ID persistente e universal que identifica os visitantes em todas as soluções na Experience Cloud. Quando sua organização implementa o serviço de ID, essa ID permite identificar o mesmo visitante do site e seus dados em soluções de Experience Cloud diferentes, como Adobe Target, Adobe Analytics ou Adobe Audience Manager. Observe que o `marketingCloudVisitorId` é necessário ao aproveitar e integrar com o Analytics e o Audience Manager.

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

O exemplo de chamada acima demonstra como um `marketingCloudVisitorId` que foi recuperado do Serviço de ID de Experience Cloud é passado para o Adobe Target. Neste cenário, [!DNL Target] gera um `tntId`, pois ele não foi passado para a chamada original que será mapeada para o `marketingCloudVisitorId` fornecido, como visto na resposta abaixo.

## ID de terceiros

Se sua organização usar uma ID para identificar o visitante, você poderá usar o `thirdPartyID` para fornecer conteúdo. No entanto, você deve fornecer o `thirdPartyID` para cada chamada do [!UICONTROL Adobe Target Delivery API] feita.

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

O exemplo de chamada acima mostra um `thirdPartyId`, que é uma ID persistente que sua empresa utiliza para identificar um usuário final, independentemente de ele estar interagindo com sua empresa a partir da Web, de dispositivos móveis ou da IoT. Em outras palavras, o `thirdPartyId` fará referência aos dados do perfil do usuário que podem ser utilizados entre canais. Neste cenário, [!DNL Target] gera um `tntId`, já que não foi passado para a chamada original, que será mapeada para o `thirdPartyId` fornecido, conforme visto na resposta abaixo.

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

[As IDs do cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=pt-BR) podem ser adicionadas e associadas a uma ID de visitante do Experience Cloud. Sempre que enviar `customerIds`, `marketingCloudVisitorId` também deve ser fornecido. Além disso, um status de autenticação pode ser fornecido com cada `customerId` para cada visitante. O seguinte status de autenticação pode ser levado em consideração:

| Status de autenticação | Status do usuário |
| --- | --- |
| `unknown` | Desconhecido ou nunca autenticado. Esse estado pode ser usado para cenários como um visitante que chegou ao seu site clicando em um anúncio de exibição. |
| `authenticated` | O usuário está autenticado no momento com uma sessão ativa no seu site ou aplicativo. |
| `logged_out` | O usuário foi autenticado, mas fez logout ativamente. O usuário quis se desconectar do estado autenticado. O usuário não deseja mais ser tratado como autenticado. |

Observe que somente quando a ID do cliente estiver no estado `authenticated` o Target referenciará os dados do perfil do usuário armazenados e vinculados à ID do cliente. Se a ID do cliente estiver no estado `unknown` ou `logged_out`, a ID do cliente será ignorada e todos os dados de perfil de usuário que possam estar associados a ela não serão aproveitados para direcionamento de público.

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

O exemplo de chamada acima demonstra como enviar um `customerId` com um `authenticatedState`. Ao enviar um `customerId`, os `integrationCode`, `id` e `authenticatedState` e também o `marketingCloudVisitorId` são obrigatórios. O `integrationCode` é o alias do [arquivo de atributos do cliente](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=pt-BR) fornecido pelo CRS.

## Perfil mesclado

Você pode combinar `tntId`, `thirdPartyID` e `marketingCloudVisitorId` na mesma solicitação. Nesse cenário, o Adobe Target manterá o mapeamento de todas essas IDs e o fixará a um visitante. Saiba como os perfis são [mesclados e sincronizados em tempo real](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=pt-BR) usando identificadores diferentes.

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

O exemplo de chamada acima demonstra como você pode combinar `tntId`, `thirdPartyID` e `marketingCloudVisitorId` na mesma solicitação. Todas as três IDs também são retornadas na resposta.
