---
title: Logon do lado do servidor para dados do A4T no Experience Platform Web SDK
description: Saiba como ativar o registro do lado do servidor para o Adobe Analytics for Target (A4T) usando o Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;destino;web;sdk;plataforma;registro;
feature: Implementation
exl-id: 716f7343-69a6-44d7-baec-a0a0df1b6e1f
TQID: https://experienceleague.adobe.com/I7-G2VO2AN3qFsgkk4JX2Pg6WJfZq0HZkcGL4XQNoWg
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 153
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
