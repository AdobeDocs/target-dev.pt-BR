---
title: Logon do Adobe Analytics for Target (A4T) no Experience Platform Web SDK
description: Saiba como controlar a coleção de dados do Adobe Analytics for Target (A4T) usando o Experience Platform Web SDK.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;registro;analytics;sdk;web sdk;
feature: Implementation
source-git-commit: b7638f7ab3fe9a6551c9d542a990e22ddb2b27a2
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# [!DNL Adobe Analytics for Target] (A4T) fazendo logon no [!DNL Experience Platform Web SDK]

Ao usar o [!DNL Adobe Target] para personalização, você pode escolher qual sistema deseja usar para avaliação de desempenho. Cada [Atividade do Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) permite selecionar entre os relatórios [!DNL Target] e os relatórios [!DNL Analytics] do Adobe.

Se você estiver usando os relatórios do [!DNL Analytics], o [!DNL Target] precisará comunicar o seguinte a [!DNL Analytics]:

* Em qual atividade [!DNL Target] seus visitantes entraram
* Qual experiência eles já viram?
* Qual conversão foi alcançada

O [!DNL Adobe Experience Platform Web SDK] dá suporte a dois tipos de log de [!DNL Analytics] para casos de uso de [!UICONTROL Analytics for Target] (A4T):

| Método de registro | Descrição |
| --- | --- |
| Logs do lado do servidor [!DNL Analytics] | Todas as [!DNL Analytics] ocorrências enviadas pelo Edge Network são aumentadas com [!DNL Target] detalhes no lado do servidor, sem precisar passar pelo processo de compilação de ocorrências. |
| Logon [!DNL Analytics] no lado do cliente | Os dados do [!DNL Target] são retornados no lado do cliente, permitindo que você aumente e envie dados manualmente para [!DNL Analytics] usando a [API de Inserção de Dados](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

O método de log é determinado se você tem o [!DNL Adobe Analytics] habilitado na sua [sequência de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) configurada:

![Fluxo de decisão do método de log](/help/dev/implement/a4t/assets/analytics-logging.png)

## Próximas etapas

Este documento forneceu uma breve introdução aos diferentes métodos de registro de dados do A4T no Web SDK. Para obter informações mais detalhadas sobre cada um desses métodos, consulte a seguinte documentação:

* [Logon do lado do servidor para dados do A4T no Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
* [Logon do lado do cliente para dados do A4T no Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)