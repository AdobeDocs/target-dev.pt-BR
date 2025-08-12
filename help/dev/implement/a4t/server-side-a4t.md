---
title: Logon do lado do servidor para dados do A4T no Experience Platform Web SDK
description: Saiba como ativar o registro do lado do servidor para o Adobe Analytics for Target (A4T) usando o Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;destino;web;sdk;plataforma;registro;
feature: Implementation
source-git-commit: b1b0424bfe61fb8b4e88723e6bb2c565d75f8351
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Logon do lado do servidor para dados A4T em [!DNL Experience Platform Web SDK]

O [!DNL Adobe Experience Platform Web SDK] permite implementar a funcionalidade [!UICONTROL Adobe Analytics for Target] (A4T) em [!UICONTROL Experience Platform Edge Network]. Quando o registro em log do lado do servidor estiver habilitado, todas as [!DNL Analytics] ocorrências enviadas pelo Edge Network serão aumentadas com [!DNL Target] detalhes no lado do servidor, sem precisar passar pelo processo de compilação de ocorrências.

O log do lado do servidor para [!DNL Analytics] está habilitado quando [!DNL Analytics] está habilitado na configuração da sequência de dados:

![Configuração de sequência de dados do Analytics habilitada](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

O diagrama a seguir mostra como os dados fluem pelo sistema quando o log do [!DNL Analytics] do lado do servidor está habilitado:

![Fluxo de log do lado do servidor](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## Próximas etapas

Este guia abordou o registro no lado do servidor para dados do A4T no Web SDK. Consulte o manual no [registro no lado do cliente](/help/dev/implement/a4t/client-side-logging.md) para obter mais informações sobre como lidar com dados do A4T no lado do cliente.