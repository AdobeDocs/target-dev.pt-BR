---
title: Usar [!UICONTROL getOffers()] em [!DNL Adobe Target] ao usar o SDK Node.js
description: Saiba como usar [!UICONTROL getOffers()] para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
TQID: https://experienceleague.adobe.com/WRGy74F1kUobRl1Pakse0VnXt3cT3-ntCljm4bHtiZ4
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 20%

---

# [!UICONTROL Obter Ofertas] (Node.js)

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
| consumerId | Sequência | Não | None | consumerIds para compilação do [!UICONTROL Analytics for Target] (A4T) |
| CustomerIds | Matriz | Não | None | IDs do cliente em formato compatível com VisitorId |
| sessionId | String | Não | None | Usado para vincular várias solicitações [!DNL Target] |
| visitante | Objeto | Não | novo VisitorId | Forneça uma instância externa de VisitorId |

## Promessa

`Promise` retornado tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| solicitação | Objeto | Solicitação da [[!UICONTROL API de entrega do Target]](/help/dev/implement/delivery-api/overview.md) |
| resposta | Objeto | Resposta da [[!UICONTROL API de Entrega do Target]](/help/dev/implement/delivery-api/overview.md) |
| visitorState | Objeto | Objeto que deve ser passado para a API do Visitante `getInstance()` |
| targetCookie | Objeto | [!DNL Target] cookie |
| targetLocationHintCookie | Objeto | Cookie de dica de localização [!DNL Target] |
| analyticsDetails | Matriz | Carga do Analytics, em caso de uso do Analytics no lado do cliente |
| responseTokens | Matriz | Uma lista de [tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| trace | Matriz | Dados de rastreamento agregados para todas as mboxes/exibições de solicitação |
| status | Objeto | Um objeto que contém o status da resposta. |
| decisioningMethod | String | Determina qual método de decisão usar ([no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), no lado do servidor, híbrido) |

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
| remoteMboxes | Matriz | Quando o Método de Decisão é `on-device`, uma matriz de nomes de mbox que não puderam ser totalmente decididos no dispositivo é fornecida. Em outras palavras, é necessária uma solicitação de [[!UICONTROL API de entrega do Target]](/help/dev/implement/delivery-api/overview.md). |

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
