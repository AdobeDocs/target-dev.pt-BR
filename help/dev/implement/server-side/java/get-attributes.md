---
title: Usar getAttributes em  [!DNL Adobe Target]  com o Java SDK
description: Saiba como usar getAttributes() para buscar experimentação e experiências personalizadas de [!DNL Target]  e extrair valores de atributo.
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
TQID: https://experienceleague.adobe.com/ZZy9nUXiyR-qwBmOgv-TPS6ZuilvAuW850gH1Doqquo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 169
ht-degree: 13%

---

# Obter atributos (Java)

## Descrição

`getAttributes()` é usado para buscar experimentação e experiências personalizadas de [!DNL Target] e extrair valores de atributos.

## Método

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## Parâmetros

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Sim | None | A mesma solicitação de destino usada para [Obter Ofertas&#x200B;](get-offers.md) |
| mboxNames | matriz var-args | Não | None | Uma matriz var-args de nomes de mbox |


## Resultado

Um objeto `Attributes` é retornado de `TargetClient.getAttributes()` que tem os seguintes métodos:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| getBoolean(mboxName, key) | Booleano | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| getString(mboxName, key) | String | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
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
