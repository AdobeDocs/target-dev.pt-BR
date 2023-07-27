---
keywords: implementar, implementação, at.js, sdk da web da adobe experience platform, sdk da web da aep
description: Saiba como implementar o [!DNL Adobe Target] para Web no lado do cliente usando o [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) ou a biblioteca at.js de JavaScript.
title: Como implementar o [!DNL Target] para Web no lado do cliente
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 30%

---

# Visão geral: implementar o [!DNL Target] para Web no lado do cliente

Em uma implementação no lado do cliente do [!DNL Adobe Target], o [!DNL Target] fornece as experiências associadas a uma atividade diretamente para o navegador do cliente. O navegador decide qual experiência será exibida e realiza a ação. Com uma implementação no lado do cliente, você pode usar um editor WYSIWYG, o [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) ou uma interface não visual, o [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para criar experiências de atividade e personalização.

Para implementar [!DNL Target] No lado do cliente, você deve usar uma das seguintes bibliotecas JavaScript:

* [SDK da Web da Adobe Experience Platform](/help/dev/implement/client-side/aep-web-sdk.md)

  A variável [!UICONTROL Adobe Experience Platform Web SDK] permite interagir com os vários serviços na [!DNL Adobe Experience Cloud] (incluindo [!DNL Target]) por meio da [!UICONTROL Adobe Experience Edge Network]. Se você optar por migrar para a [!UICONTROL Adobe Experience Platform Web SDK], consulte [O que é o [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk.md).

* [[!DNL Target] Biblioteca JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  A biblioteca JavaScript at.js do melhora os tempos de carregamento de página de implementações da Web, melhora a segurança e fornece opções de implementações melhores para aplicativos de página única. Se optar por migrar para a at.js, consulte [Como a at.js funciona](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) e [[!DNL Adobe Target] Skill Builder: bate-papo com o desenvolvedor, migre da mbox.js do Adobe Target para a at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).
