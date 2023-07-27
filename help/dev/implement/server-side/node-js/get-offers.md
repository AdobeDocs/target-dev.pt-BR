---
title: Uso [!UICONTROL getOffers()] in [!DNL Adobe Target] ao usar o SDK do Node.js
description: Saiba como usar o [!UICONTROL getOffers()] para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 22%

---

# [!UICONTROL Obter ofertas] (Node.js)

## Descrição

`[!UICONTROL getOffers()]` é usado para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].


## Método

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Parâmetros

A variável `options` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- |--- | --- | --- | --- |
| Solicitação | Objeto | Sim | None | Está em conformidade com [[!DNL Target] API de entrega](/help/dev/implement/delivery-api/overview.md) solicitação |
| visitorCookie | String | Não | None | Cookie da ECID (VisitorId) |
| targetCookie | String | Não | None | [!DNL Target] cookie |
| targetLocationHint | String | Não | None | [!DNL Target] dica de localização |
| consumerId | Sequência | Não | None | consumerIds para [!UICONTROL Analytics for Target] Compilação do (A4T) |
| CustomerIds | Matriz | Não | None | IDs do cliente em formato compatível com VisitorId |
| sessionId | String | Não | None | Usado para vincular vários [!DNL Target] solicitações |
| visitante | Objeto | Não | novo VisitorId | Forneça uma instância externa de VisitorId |

## Promessa

`Promise` devolvido tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| solicitação | Objeto | [[!UICONTROL API de entrega do Target]](/help/dev/implement/delivery-api/overview.md) solicitação |
| resposta | Objeto | [[!UICONTROL API de entrega do Target]](/help/dev/implement/delivery-api/overview.md) resposta |
| visitorState | Objeto | Objeto que deve ser passado para a API do visitante `getInstance()` |
| targetCookie | Objeto | [!DNL Target] cookie |
| targetLocationHintCookie | Objeto | [!DNL Target] cookie de dica de localização |
| analyticsDetails | Matriz | Carga do Analytics, em caso de uso do Analytics no lado do cliente |
| responseTokens | Matriz | Uma lista de [Tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| trace | Matriz | Dados de rastreamento agregados para todas as mboxes/exibições de solicitação |
| status | Objeto | Um objeto que contém o status da resposta. |
| decisioningMethod | String    | Determina que método de decisão usar ([no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), lado do servidor, híbrido) |

`targetCookie` e `targetLocationHintCookie` os objetos usados para enviar dados de volta para o navegador têm a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| name | String | Nome do cookie |
| value | Qualquer | Valor do cookie, o será convertido em string |
| maxAge | Número | A variável `maxAge` é uma conveniência para que a configuração expire em relação ao tempo atual em segundos |

A variável `status` objeto usado para indicar o status da resposta do target tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| status | Número | Código de status HTTP |
| message | String | Uma mensagem sobre a resposta. Por exemplo, pode indicar se a resposta foi decidida [no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) ou no lado do servidor |
| remoteMboxes | Matriz | Quando o método de decisão é `on-device`, uma matriz de nomes de mbox que não puderam ser totalmente decididos no dispositivo é fornecida. Por outras palavras, uma [[!UICONTROL API de entrega do Target]](/help/dev/implement/delivery-api/overview.md) é necessária. |

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
