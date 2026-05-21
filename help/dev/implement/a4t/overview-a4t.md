---
title: Logon do Adobe Analytics for Target (A4T) no Experience Platform Web SDK
description: Saiba como controlar a coleção de dados do Adobe Analytics for Target (A4T) usando o Experience Platform Web SDK.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;registro;analytics;sdk;web sdk;
feature: Implementation
exl-id: 886588bf-4416-4f1e-aecc-467e48c8fb23
TQID: https://experienceleague.adobe.com/cShqvj3wSialxA-ajnROnIpzjuz66pNg3CLM6l2xPLg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 262
ht-degree: 0%

---

# [!DNL Adobe Analytics for Target] (A4T) fazendo logon no [!DNL Experience Platform Web SDK]

Ao usar o [!DNL Adobe Target] para personalização, você pode escolher qual sistema deseja usar para avaliação de desempenho. Cada [Atividade do Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=pt-BR) permite selecionar entre os relatórios [!DNL Target] e os relatórios [!DNL Analytics] do Adobe.

Se você estiver usando os relatórios do [!DNL Analytics], o [!DNL Target] precisará comunicar o seguinte a [!DNL Analytics]:

* Em qual atividade [!DNL Target] seus visitantes entraram
* Qual experiência eles já viram?
* Qual conversão foi alcançada

O [!DNL Adobe Experience Platform Web SDK] dá suporte a dois tipos de log de [!DNL Analytics] para casos de uso de [!UICONTROL Analytics for Target] (A4T):

| Método de registro | Descrição |
| --- | --- |
| Logs do lado do servidor [!DNL Analytics] | Todas as [!DNL Analytics] ocorrências enviadas pelo Edge Network são aumentadas com [!DNL Target] detalhes no lado do servidor, sem precisar passar pelo processo de compilação de ocorrências. |
| Logon [!DNL Analytics] no lado do cliente | Os dados do [!DNL Target] são retornados no lado do cliente, permitindo que você aumente e envie dados manualmente para [!DNL Analytics] usando a [API de Inserção de Dados](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=pt-BR). |

O método de log é determinado se você tem o [!DNL Adobe Analytics] habilitado na sua [sequência de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/datastreams/overview) configurada:

![Fluxo de decisão do método de log](/help/dev/implement/a4t/assets/analytics-logging.png)

## Próximas etapas

Este documento forneceu uma breve introdução aos diferentes métodos de registro de dados do A4T no Web SDK. Para obter informações mais detalhadas sobre cada um desses métodos, consulte a seguinte documentação:

* [Logon do lado do servidor para dados do A4T no Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
* [Logon do lado do cliente para dados do A4T no Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
