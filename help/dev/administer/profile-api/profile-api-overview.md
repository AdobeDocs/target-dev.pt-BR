---
title: Atualizar perfis
description: Saiba como usar as APIs de perfil do Adobe Target para enviar dados do visitante para o  [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 315e8fbe67938588c3c9a0135e0cd85fa1f12187
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# Atualizar perfis

Um perfil de usuário contém informações demográficas e comportamentais de um visitante da página da Web, como idade, gênero, produtos comprados, última visita e assim por diante. [!DNL Adobe Target] usa essas informações para personalizar o conteúdo que elas oferecem a cada visitante.

As informações de perfil de cada visitante são armazenadas em cookies ou em aplicativos de terceiros.

Se sua página da Web implementa o código [!DNL Target] ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) ou o [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)), as informações de perfil dos cookies serão passadas para [!DNL Target] usando parâmetros de perfil. [!DNL Target] identifica cada visitante exclusivamente por meio de um `pcID` gerado nos cookies do visitante. No entanto, você pode passar parâmetros de perfil de um aplicativo externo por meio de chamadas mbox usando `mbox3rdPartyIds`.

Use as APIs de perfil do [!DNL Adobe Target] quando tiver dados de perfil sobre seus visitantes para enviar para o [!DNL Target] que você não pode ou não quer enviar como parte de sua integração baseada em página com o [!DNL Target]. Podem ser dados de um sistema de CRM (relacionamento com o cliente) ou de POS (ponto de venda) que não está disponível na página. Ou esses dados podem ser de natureza mais sensível que não faz sentido passar na página.

Há duas maneiras de atualizar perfis por meio da API:

* [API de atualização de perfil único](/help/dev/administer/profile-api/profile-single-api.md)
* [Atualização de perfil em massa por lote](/help/dev/administer/profile-api/profile-bulk-api.md)
