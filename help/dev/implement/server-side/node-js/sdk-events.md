---
title: Assinar eventos no  [!DNL Adobe Target] SDK do Node.js
description: Saiba como assinar vários eventos que ocorrem no SDK do Node.js usando o objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 2%

---

# Eventos do SDK (Node.js)

## Descrição

Ao [inicializar o SDK](initialize-sdk.md), o objeto `options.events` é opcional com chaves de nome de evento e valores de função de retorno de chamada. Ele pode ser usado para assinar vários eventos que ocorrem no SDK. Por exemplo, o evento `clientReady` pode ser usado com uma função de retorno de chamada que será invocada quando o SDK estiver pronto para chamadas de método.

Quando a função de retorno de chamada é chamada, um objeto de evento é transmitido. Cada evento tem um `type` correspondente ao nome do evento. Alguns eventos incluem propriedades adicionais com informações pertinentes.

## Eventos 

| Nome do evento (tipo) | Descrição | Propriedades adicionais do evento |
| --- | --- | --- |
| clientReady | Emitido quando o artefato é baixado e o SDK está pronto para `getOffers` chamadas. Recomendado ao usar o método de decisão no dispositivo. |
| artifactDownloadSucceeded | Emitido sempre que um novo artefato é baixado. | artifactPayload, artifactLocation |
| artifactDownloadFailed | Emitido sempre que ocorre falha no download de um artefato. | artifactLocation, erro |

## Exemplo

### Node.js

```js {line-numbers="true"}
const targetClient = TargetClient.create({
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device",
    events: {
        clientReady: onTargetClientReady,
        artifactDownloadSucceeded: onArtifactDownloadSucceeded,
        artifactDownloadFailed: onArtifactDownloadFailed
    }
});

function onTargetClientReady() {
    // make getOffers requests
    targetClient.getOffers({...})            
}

function onArtifactDownloadSucceeded(event) {
    console.log(`The artifact was successfully downloaded from '${event.artifactLocation}'`);
    // optionally do something with event.artifactPayload, like persist it
}

function onArtifactDownloadFailed(event) {
    console.log(`The artifact failed to download from '${event.artifactLocation}' with the following error message: ${event.error.message}`);
}
```
