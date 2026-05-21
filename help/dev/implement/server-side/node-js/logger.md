---
title: Inicialize o  [!DNL Adobe Target] Node.js SDK para registrar solicitações
description: Saiba como registrar solicitações na  [!DNL Adobe Target] SDK do Node.js.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
TQID: https://experienceleague.adobe.com/tC6xT-eAHOO17h1BK-PwWTBmwg3Dy0Wj8KYrV3W-VR4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 83
ht-degree: 2%

---

# Logger (Node.js)

## Descrição

Ao [inicializar o SDK](initialize-sdk.md), o objeto `options.logger` é opcional. No entanto, para depurar efetivamente quando ocorrer um problema, um objeto `logger` deve ser fornecido ao inicializar o SDK.

O objeto `logger` deve ter um método `debug()` e `error()`. Quando um agente de log apropriado for fornecido, como `console`, [!DNL Target] solicitações e respostas serão registradas.

## Exemplo

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  logger: console
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
    }
};

const response = await targetClient.getOffers({ request, targetCookie });
```

Você deve ver solicitações e respostas sendo impressas no console.
