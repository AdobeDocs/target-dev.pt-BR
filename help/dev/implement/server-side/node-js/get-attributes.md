---
title: Como usar solicitações assíncronas no [!DNL Adobe Target] SDK do Node.js
description: Saiba como [!DNL Target] O SDK do Node.js é compatível com solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 18%

---

# Obter atributos (Node.js)

## Descrição

`[!UICONTROL getAttributes()]` O é usado para buscar experiências e experiências personalizadas de [!DNL Target] e extrair valores de atributo.

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

A variável `Promise` retornado por `TargetClient.getAttributes()` O resolve um objeto com os seguintes métodos:

| Método | Tipo de retorno | Descrição |
| --- | --- | --- |
| getValue(mboxName, key) | Qualquer | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| asObject(mboxName) | Objeto | Retorna um objeto json simples com pares de valores chave |
| getResponse() | [Resposta do getOffers](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | Retorna o objeto de resposta normalmente retornado por `getOffers` |

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
