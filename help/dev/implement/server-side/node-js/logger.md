---
title: Inicializar o [!DNL Adobe Target] SDK do Node.js para registrar solicitações
description: Saiba como registrar solicitações no [!DNL Adobe Target] SDK do Node.js.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# Logger (Node.js)

## Descrição

Quando [inicialização do SDK](initialize-sdk.md), o `options.logger` é um objeto opcional. No entanto, para depurar efetivamente quando ocorrer um problema, uma variável `logger` O objeto deve ser fornecido ao inicializar o SDK.

A variável `logger` espera-se que o objeto tenha um `debug()` e uma `error()` método. Quando um log apropriado é fornecido, como `console`, [!DNL Target] as solicitações e respostas serão registradas.

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
