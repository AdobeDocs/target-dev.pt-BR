---
title: Permissões de usuário da API de entrega do Adobe Target
description: Permissões de usuário da API de entrega do Adobe Target
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium newtab=true" tooltip="Consulte o que está incluído no Target Premium."
keywords: api de entrega
exl-id: 332f90bd-4079-4653-aa38-b35837631c94
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Permissões de usuário (Premium)

O [!DNL Adobe] permite que os clientes gerenciem permissões para seus usuários ao usar o Adobe Target. Para fazer uma chamada [!UICONTROL Adobe Target Delivery API] bem-sucedida, um token com as permissões certas deve ser passado na chamada de API. Para saber mais sobre as permissões de usuário e como recuperar a visita ao token, [esta documentação](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

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

Depois de ter o token correspondente, passe-o para `property` -> `token` para cada chamada de API feita. Se o `property` -> `token` não for transmitido em cada chamada de API, você não receberá nenhum `content` de volta da Adobe Target.

```
{
    "status": 200,
    "requestId": "07ce783d-58b9-461c-9f4c-6873aeb00c01",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage"
            }
        ]
    }
}
```

Como você pode ver acima, sem passar a `property` -> `token`, você não receberá nenhum conteúdo de volta. Se você espera conteúdo da sua chamada à API, mas não está recuperando nenhum conteúdo da resposta, é provável que o `property` -> `token` não tenha sido fornecido ou que esteja sendo passado sem as permissões corretas.
