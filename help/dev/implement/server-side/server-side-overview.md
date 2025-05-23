---
keywords: lado do servidor, lado do servidor, api, sdk, node.js, nodejs, node js, api de recomendações, api, apis, server side1
description: Saiba mais sobre as [!DNL Adobe Target] APIs de entrega, os SDKs e as [!DNL Target Recommendations] APIs do lado do servidor.
title: Onde posso obter mais informações sobre  [!DNL Target] APIs e SDKs de entrega no lado do servidor?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
source-git-commit: 75af30045684b95d5989b0a1f877ba95bb8cd883
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 13%

---

# Lado do servidor: implementar o [!DNL Target]

Informações sobre [!DNL Adobe Target] APIs de entrega do lado do servidor, SDKs e [!DNL Target Recommendations] APIs.

>[!NOTE]
>
>Se sua implementação usar at.js e [!DNL AppMeasurement] no lado do cliente, você deverá usar o [!UICONTROL Target Delivery API] e os SDKs do lado do servidor discutidos abaixo.
>
>Se sua implementação usa o [!UICONTROL Adobe Experience Platform Web SDK], você deve usar o [[!UICONTROL Adobe Experience Platform] [!UICONTROL Edge Network Server API]](https://experienceleague.adobe.com/pt-br/docs/experience-platform/edge-network-server-api/overview){target=_blank}.

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

* Ofereça experiências na Web, incluindo SPA, e canais móveis, bem como dispositivos IoT não baseados em navegador, como TVs conectadas, quiosques ou telas digitais na loja.
* Fornecer experiências de qualquer plataforma ou aplicativo do lado do servidor que possa fazer chamadas HTTP/s.
* Forneça experiências consistentes e personalizadas a um visitante, independentemente do canal ou dos dispositivos que o visitante usou para se envolver com sua empresa.
* Armazene em cache experiências de um visitante em uma sessão no servidor para que várias chamadas de API possam ser evitadas, o que resulta em melhor desempenho.
* Integre-se perfeitamente a produtos da Adobe Experience Cloud, como Adobe Analytics, Adobe Audience Manager (AAM) e o Serviço de ID de Experience Cloud do lado do servidor.

## SDKs do servidor

A documentação do SDK do lado do servidor do [!DNL Adobe Target] ajuda a implementar o [!DNL Target] nos servidores no idioma de sua escolha.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Através dos SDKs do lado do servidor do [!DNL Adobe Target], você pode:

* Execute e execute os **sinalizadores de recursos**, **implantações** e **experimentos A/B** na **latência quase zero**.
* Entregue experiências em **web**, incluindo **SPA** e **canais móveis**, bem como **dispositivos de IoT (Internet das Coisas) não baseados em navegador**, como uma TV conectada, um quiosque ou uma tela digital na loja.
* Forneça **experiências personalizadas orientadas por aprendizado de máquina** para um usuário, independentemente do canal ou dispositivo com o qual o usuário tenha se envolvido em sua empresa.
* **Integre perfeitamente com produtos da Adobe Experience Cloud**, como o **Adobe Analytics**, o **Adobe Audience Manager** e o **Serviço de ID de Experience Cloud**, do lado do servidor.

Consulte a página [Introdução](sdk-guides/getting-started/getting-started.md) para saber como executar um caso de uso de sinalização de recurso simples via [decisão no dispositivo](sdk-guides/on-device-decisioning/overview.md).

Confira nossos [Aplicativos de exemplo](sdk-guides/sample-apps/sample-apps.md) para se divertir e se divertir!

## [!DNL Target Recommendations] APIs

Link: [APIs do Recommendations do Target](https://developers.adobetarget.com/api/recommendations) e [Visão geral da API do Adobe Recommendations](../../before-administer/recs-api/overview.md).

As APIs do Recommendations permitem interagir programaticamente com os servidores de recomendações do [!DNL Target]. Essas APIs podem ser integradas a uma variedade de pilhas de aplicativos para executar funções que normalmente seriam realizadas por meio da interface do usuário do [!DNL Target].
