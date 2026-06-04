---
keywords: lado do servidor, lado do servidor, api, sdk, node.js, nodejs, node js, api de recomendações, api, apis, server side1
description: Saiba mais sobre as [!DNL Adobe Target] APIs de entrega, os SDKs e as [!DNL Target Recommendations] APIs do lado do servidor.
title: Onde posso obter mais informações sobre  [!DNL Target] APIs e SDKs de entrega no lado do servidor?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
TQID: https://experienceleague.adobe.com/x5WKb9Eenz2bw-idOnxlpWdtiivTx05n38sNXEt3DNc
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: b050e0cd-2ddd-42cd-a71b-5d9e1fdf75e0
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a6cc21b9-1a36-4fa6-9c61-4acd04d9c88c
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 618
ht-degree: 12%

---

# Lado do servidor: implementar o [!DNL Target]

Informações sobre [!DNL Adobe Target] APIs de entrega do lado do servidor, SDKs e [!DNL Target Recommendations] APIs.

>[!NOTE]
>
>Se sua implementação usa at.js e [!DNL AppMeasurement] no lado do cliente, você deve usar a [!UICONTROL API de entrega do Target] e os SDKs do lado do servidor discutidos abaixo.
>
>Se sua implementação usa a [!UICONTROL Adobe Experience Platform Web SDK], você deve usar a [[!UICONTROL Adobe Experience Platform] [!UICONTROL API do Edge Network Server]](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview){target=_blank}.

O processo a seguir ocorre em uma implementação do lado do servidor do [!DNL Target]:

1. Um dispositivo cliente faz uma solicitação para uma experiência por meio do servidor.
1. O servidor envia essa solicitação para o [!DNL Target].
1. O [!DNL Target] envia a resposta para o servidor.
1. O servidor decide qual experiência deve ser entregue ao dispositivo cliente para que seja renderizada.

A experiência não precisa ser exibida em um navegador. A experiência pode ser exibida em um email ou quiosque, por meio de um assistente de voz ou por alguma outra experiência não visual ou dispositivo não baseado em navegador. Como o servidor fica entre o cliente e o [!DNL Target], esse tipo de implementação também será ideal se você precisar de mais controle e segurança ou de processos de back-end complexos que deseja executar no servidor.

>[!NOTE]
>
>Um visitante de primeira vez pode ser inicializado somente no lado do cliente. Um visitante pela primeira vez *não pode* ser inicializado no lado do servidor. Isso se deve à ECID, que depende do cookie demdex de terceiros e, portanto, precisa ser inicializada por meio da API.js do visitante em uma implementação em que o navegador está envolvido.

As seguintes seções fornecem mais informações sobre as várias APIs e SDKs do lado do servidor:

## APIs de entrega no lado do servidor

Link: [APIs de entrega no lado do servidor](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

Por meio da API de entrega [!DNL Target], você pode:

* Ofereça experiências na Web, incluindo SPAs e canais móveis, bem como dispositivos IoT não baseados em navegador, como TVs conectadas, quiosques ou telas digitais na loja.
* Fornecer experiências de qualquer plataforma ou aplicativo do lado do servidor que possa fazer chamadas HTTP/s.
* Forneça experiências consistentes e personalizadas a um visitante, independentemente do canal ou dos dispositivos que o visitante usou para se envolver com sua empresa.
* Armazene em cache experiências de um visitante em uma sessão no servidor para que várias chamadas de API possam ser evitadas, o que resulta em melhor desempenho.
* Integre-se perfeitamente aos produtos da Adobe Experience Cloud, como o Adobe Analytics, o Adobe Audience Manager (AAM) e o Serviço da Experience Cloud ID do lado do servidor.

## SDKs do servidor

A documentação do SDK do lado do servidor do [!DNL Adobe Target] ajuda a implementar o [!DNL Target] nos servidores no idioma de sua escolha.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Através dos SDKs do lado do servidor do [!DNL Adobe Target], você pode:

* Execute e execute os **sinalizadores de recursos**, **implantações** e **experimentos A/B** na **latência quase zero**.
* Entregar experiências na **web**, incluindo **SPAs** e **canais móveis**, bem como **dispositivos da IoT (Internet das Coisas) não baseados em navegador**, como uma TV conectada, um quiosque ou uma tela digital na loja.
* Forneça **experiências personalizadas orientadas por aprendizado de máquina** para um usuário, independentemente do canal ou dispositivo com o qual o usuário tenha se envolvido em sua empresa.
* **Integre facilmente com a Adobe Experience Cloud** produtos como o **Adobe Analytics**, o **Adobe Audience Manager** e o **Serviço da Experience Cloud ID** do lado do servidor.

Consulte a página [Introdução](sdk-guides/getting-started/getting-started.md) para saber como executar um caso de uso de sinalização de recurso simples via [decisão no dispositivo](sdk-guides/on-device-decisioning/overview.md).

Confira nossos [Aplicativos de exemplo](sdk-guides/sample-apps/sample-apps.md) para se divertir e se divertir!

## [!DNL Target Recommendations] APIs

Link: [APIs do Target Recommendations](https://developers.adobetarget.com/api/recommendations) e [Visão geral da API do Adobe Recommendations](../../before-administer/recs-api/overview.md).

As APIs do Recommendations permitem interagir programaticamente com [!DNL Target] servidores de recomendações. Essas APIs podem ser integradas a uma variedade de pilhas de aplicativos para executar funções que normalmente seriam realizadas por meio da interface do usuário do [!DNL Target].
