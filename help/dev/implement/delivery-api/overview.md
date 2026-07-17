---
title: Visão geral da API de entrega do Adobe Target
description: Visão geral da API de entrega do Adobe Target
keywords: api de entrega
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/gPXGax6ccvZZPklT3jnZbqyOj3mCClEfSpdufAFPtSs
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: b6b447ccb88925a8efb6ff6a80ae475c8780dbc8
workflow-type: tm+mt
source-wordcount: 244
ht-degree: 0%

---

# Visão geral da API de entrega

O [!DNL Adobe Target Delivery API] é baseado em REST. Esta documentação descreve os recursos que compõem o [!DNL Adobe Target] [!DNL Delivery API]. Os métodos HTTP são utilizados para executar operações nesses recursos.

>[!IMPORTANT]
>
>O [!DNL Delivery API] documentado aqui destina-se a [!DNL at.js] e implementações diretas do lado do servidor. Se você estiver implementando o [!DNL Target] usando o [!DNL Adobe Experience Platform Web SDK], use a API do Interact, acessada por meio do comando `sendEvent` no [!UICONTROL Experience Platform Edge Network], em vez de chamar o [!DNL Delivery API] diretamente. Consulte [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md) e [Comparar a biblioteca at.js com o Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) para obter mais informações.

Usando a [!UICONTROL API de entrega do Adobe Target], você pode:

* Ofereça experiências na Web, incluindo SPAs e canais móveis, bem como dispositivos IoT não baseados em navegador, como TV conectada, quiosque ou tela digital na loja.
* Fornecer experiências de qualquer plataforma ou aplicativo do lado do servidor que possa fazer chamadas HTTP/s.
* Ofereça experiências consistentes e personalizadas a um usuário, independentemente do canal ou dos dispositivos que o usuário tenha envolvido em sua empresa.
* Armazene em cache experiências de um usuário em uma sessão no seu servidor, para que várias chamadas de API possam ser evitadas e, como resultado, alcançar um desempenho melhor.
* Integre facilmente com [!DNL Adobe Experience Cloud] produtos, como [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] e o [!DNL Experience Cloud ID Service] a partir do lado do servidor.

>[!NOTE]
>
>Você ainda pode acessar a [documentação da API /v1/mbox herdada e /v2/batchmbox](https://developers.adobetarget.com/api/legacy-api/index.html). No entanto, os recursos serão desenvolvidos na API de entrega (conforme documentado aqui), que não terá suporte para as APIs herdadas.
