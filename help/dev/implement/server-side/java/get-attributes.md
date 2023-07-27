---
title: Usar getAttributes no [!DNL Adobe Target] com o SDK do Java
description: Saiba como usar getAttributes() para buscar experimentação e experiências personalizadas de [!DNL Target] e extrair valores de atributo.
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 13%

---

# Obter atributos (Java)

## Descrição

`getAttributes()` O é usado para buscar experiências e experiências personalizadas de [!DNL Target] e extrair valores de atributo.

## Método

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## Parâmetros

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Sim | None | A mesma solicitação de público alvo que foi usada para [Obter ofertas&#x200B;](get-offers.md) |
| mboxNames | matriz var-args | Não | None | Uma matriz var-args de nomes de mbox |


## Resultado

Um `Attributes` o objeto é retornado de `TargetClient.getAttributes()` que tem os seguintes métodos:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| getBoolean(mboxName, key) | Booleano | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| getString(mboxName, key) | String    | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| getInteger(mboxName, chave) | Número inteiro | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| getDouble(mboxName, key) | Dupla | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| toMboxMap(mboxName) | Mapa | Retorna um Mapa simples com pares de valores chave |
| getResponse() | TargetDeliveryResponse | Retorna o objeto de resposta normalmente retornado por getOffers |

## Exemplo

### Java

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .build();

Attributes offerAttributes = targetJavaClient.getAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
String searchProviderId = offerAttributes.getString("demo-engineering-flags", "searchProviderId");

//returns a simple Map representing the mbox offer
Map<String, Object> engineeringFlags = offerAttributes.toMboxMap("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

String assetUrl = "http://" + engineeringFlags.cdnHostname + "/path/to/asset";
```
