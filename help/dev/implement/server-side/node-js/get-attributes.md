---
title: Como usar solicitações assíncronas no [!DNL Adobe Target] Node.js SDK
description: Saiba como o Node.js do SDK [!DNL Target] oferece suporte a solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
TQID: 'https://experienceleague.adobe.com/cIoEnAinSLl-TO2vunG164i97Y2h-9NdE487ZyXJSzs'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
    internal-label: Experimentation
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 17%
---
# Obter atributos (Node.js)

## Descrição

`[!UICONTROL getAttributes()]` é usado para buscar experimentação e experiências personalizadas de [!DNL Target] e extrair valores de atributos.

## Método

### getAttributes

```js {line-numbers="true"}
TargetClient.getAttributes(mboxNames: Array, options: Object): Promise
```

## Parâmetros

| Nome | Tipo | Obrigatório | Padrão |
| --- | --- | --- |--- |
| mboxNames | Matriz | Sim | None |
| opções | Objeto | Não | None |

## Promessa

O `Promise` retornado por `TargetClient.getAttributes()` resolve um objeto com os seguintes métodos:

| Método | Tipo de retorno | Descrição |
| --- | --- | --- |
| getValue(mboxName, key) | Qualquer | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| asObject(mboxName) | Objeto | Retorna um objeto json simples com pares de valores chave |
| getResponse() | [Resposta de getOffers](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | Retorna o objeto de resposta normalmente retornado por `getOffers` |

## Exemplo

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);
const offerAttributes = await targetClient.getAttributes(["demo-engineering-flags"]);


//returns just the value of searchProviderId from the mbox offer
const searchProviderId = offerAttributes.getValue("demo-engineering-flags", "searchProviderId");

//returns a simple JSON object representing the mbox offer
const engineeringFlags = offerAttributes.asObject("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

const assetUrl = `http://${engineeringFlags.cdnHostname}/path/to/asset`;
```
