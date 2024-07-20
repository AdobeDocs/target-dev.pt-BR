---
title: Usar getAttributes em  [!DNL Adobe Target]  com o SDK do .NET
description: Saiba como usar getAttributes() para buscar experimentação e experiências personalizadas de [!DNL Target]  e extrair valores de atributo.
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 9%

---

# Obter Atributos (.NET)

## Descrição

`GetAttributes()` é usado para buscar experimentação e experiências personalizadas de [!DNL Target] e extrair valores de atributos.

## Método

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## Parâmetros

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Não | null | A mesma solicitação [!DNL Target] usada para [Obter Ofertas&#x200B;](get-offers.md) |
| mboxNames | cadeia de caracteres de parâmetros[] | Não | null | Uma matriz de parâmetros de nomes de mbox |

## Resultado

Um objeto `TargetAttributes` é retornado de `TargetClient.GetAttributes()` que tem as seguintes propriedades e métodos:

| Propriedade/Método | Tipo de retorno | Descrição |
| --- | --- | --- |
| Resposta | TargetDeliveryResponse | Retorna o objeto de resposta normalmente retornado por [Obter Ofertas](get-offers.md) |
| ToDictionary | IReadOnlyDictionary | Retorna um dicionário de dicionários com pares de valores chave agrupados por nomes de mbox |
| ToMboxDictionary(mboxName) | IReadOnlyDictionary | Retorna um dicionário com os pares de chave-valor da mbox fornecida |
| GetBoolean(mboxName, chave, defaultValue) | bool | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| GetString(mboxName, chave, defaultValue) | string | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| GetInteger(mboxName, chave, defaultValue) | int | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| GetDouble(mboxName, chave, defaultValue) | duplo | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| GetValue(mboxName, chave, defaultValue) | T  | Retorna o valor de um nome de mbox e uma chave de atributo especificados |

## Exemplo

### \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .Build();

var offerAttributes = targetClient.GetAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
var searchProviderId = offerAttributes.GetString("demo-engineering-flags", "searchProviderId");

//returns a simple Dictionary representing the mbox offer
var engineeringFlags = offerAttributes.ToMboxDictionary("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

var assetUrl = $"http://{engineeringFlags["cdnHostname"]}/path/to/asset";
```
