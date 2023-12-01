---
title: Visão geral das APIs de perfil do Adobe Target
description: Saiba como usar as APIs de perfil do Adobe Target para enviar dados do visitante para o [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 1%

---

# [!DNL Adobe Target Profile APIs overview]

Um perfil de usuário contém informações demográficas e comportamentais de um visitante da página da Web, como idade, gênero, produtos comprados, última visita e assim por diante. [!DNL Adobe Target] O usa essas informações para personalizar o conteúdo disponibilizado a cada visitante.

As informações de perfil de cada visitante são armazenadas em cookies ou em aplicativos de terceiros.

Se a página da Web implementar o código do Target ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) ou o [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)), as informações de perfil dos cookies são passadas para [!DNL Target] usando parâmetros de perfil. [!DNL Target] identifica cada visitante exclusivamente por meio de um `pcID` que gera os cookies do visitante. No entanto, você pode passar parâmetros de perfil de um aplicativo externo por meio de chamadas mbox usando `mbox3rdPartyIds`.

Use o [!DNL Adobe Target] APIs de perfil quando você tem dados de perfil sobre seus visitantes para enviar [!DNL Target] que você não pode ou não quer enviar como parte de sua integração baseada em página com o [!DNL Target]. Podem ser dados de um sistema de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) ou de POS (Point of Sale, ponto de venda) que não estão disponíveis na página ou dados de natureza mais confidencial que não fazem sentido serem transmitidos na página.

Há duas maneiras de atualizar perfis por meio da API:

* [API de atualização de perfil único](/help/dev/administer/profile-api/profile-single-api.md)
* [Atualização de perfil em massa por lote](/help/dev/administer/profile-api/profile-bulk-api.md)
