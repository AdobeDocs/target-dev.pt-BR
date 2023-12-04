---
title: Atualizar perfis
description: Saiba como usar as APIs de perfil do Adobe Target para enviar dados do visitante para o [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 9707680ddcf0c373c635aa9f3cb5ba1b74cf90a3
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%

---

# Atualizar perfis

Um perfil de usuário contém informações demográficas e comportamentais de um visitante da página da Web, como idade, gênero, produtos comprados, última visita e assim por diante. [!DNL Adobe Target] O usa essas informações para personalizar o conteúdo disponibilizado a cada visitante.

As informações de perfil de cada visitante são armazenadas em cookies ou em aplicativos de terceiros.

Se a página da Web implementar a variável [!DNL Target] código ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) ou o [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)), as informações de perfil dos cookies são passadas para [!DNL Target] usando parâmetros de perfil. [!DNL Target] identifica cada visitante exclusivamente por meio de um `pcID` que ele gera nos cookies do visitante. No entanto, você pode passar parâmetros de perfil de um aplicativo externo por meio de chamadas mbox usando `mbox3rdPartyIds`.

Use o [!DNL Adobe Target] APIs de perfil quando você tem dados de perfil sobre seus visitantes para enviar [!DNL Target] que você não pode ou não quer enviar como parte de sua integração baseada em página com o [!DNL Target]. Podem ser dados de um sistema de CRM (relacionamento com o cliente) ou de POS (ponto de venda) que não está disponível na página. Ou esses dados podem ser de natureza mais sensível que não faz sentido passar na página.

Há duas maneiras de atualizar perfis por meio da API:

* [API de atualização de perfil único](/help/dev/administer/profile-api/profile-single-api.md)
* [Atualização de perfil em massa por lote](/help/dev/administer/profile-api/profile-bulk-api.md)

A documentação da API de perfis herdada pode ser encontrada aqui: [https://developers.adobetarget.com/api/#profiles](https://developers.adobetarget.com/api/#profiles){target=_blank}
