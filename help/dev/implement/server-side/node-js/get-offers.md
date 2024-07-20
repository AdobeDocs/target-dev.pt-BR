---
title: Usar [!UICONTROL getOffers()] em [!DNL Adobe Target] ao usar o SDK do Node.js
description: Saiba como usar o [!UICONTROL getOffers()] para executar uma decisão e recuperar uma experiência do  [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 22%

---

# [!UICONTROL Get Offers] (Node.js)

## Descrição

`[!UICONTROL getOffers()]` é usado para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].


## Método

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Parâmetros

O objeto `options` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- |--- | --- | --- | --- |
| Solicitação | Objeto | Sim | None | Está em conformidade com a solicitação da [[!DNL Target] API de entrega](/help/dev/implement/delivery-api/overview.md) |
| visitorCookie | String | Não | None | Cookie da ECID (VisitorId) |
| targetCookie | String | Não | None | [!DNL Target] cookie |
| targetLocationHint | String | Não | None | [!DNL Target] dica de localização |
| consumerId | Sequência | Não | None | consumerIds para compilação de [!UICONTROL Analytics for Target] (A4T) |
| CustomerIds | Matriz | Não | None | IDs do cliente em formato compatível com VisitorId |
| sessionId | String | Não | None | Usado para vincular várias solicitações [!DNL Target] |
| visitante | Objeto | Não | novo VisitorId | Forneça uma instância externa de VisitorId |

## Promessa

`Promise` retornado tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| solicitação | Objeto | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) solicitação |
| resposta | Objeto | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) resposta |
| visitorState | Objeto | Objeto que deve ser passado para a API do Visitante `getInstance()` |
| targetCookie | Objeto | [!DNL Target] cookie |
| targetLocationHintCookie | Objeto | Cookie de dica de localização [!DNL Target] |
| analyticsDetails | Matriz | Carga do Analytics, em caso de uso do Analytics no lado do cliente |
| responseTokens | Matriz | Uma lista de [tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| trace | Matriz | Dados de rastreamento agregados para todas as mboxes/exibições de solicitação |
| status | Objeto | Um objeto que contém o status da resposta. |
| decisioningMethod | String    | Determina qual método de decisão usar ([no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), no lado do servidor, híbrido) |

Os objetos `targetCookie` e `targetLocationHintCookie` usados para transmitir dados de volta ao navegador têm a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| name | String | Nome do cookie |
| value | Qualquer | Valor do cookie, o será convertido em string |
| maxAge | Número | A opção `maxAge` é uma conveniência para que a configuração expire em relação ao tempo atual em segundos |

O objeto `status` usado para indicar o status da resposta de destino tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| status | Número | Código de status HTTP |
| message | String | Uma mensagem sobre a resposta. Por exemplo, pode indicar se a resposta foi decidida [no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) ou no lado do servidor |
| remoteMboxes | Matriz | Quando o Método de Decisão é `on-device`, uma matriz de nomes de mbox que não puderam ser totalmente decididos no dispositivo é fornecida. Em outras palavras, uma solicitação [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) é necessária. |

## Exemplo

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    context: {channel: "web"},
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
}};

const response = await targetClient.getOffers({ request });
```
