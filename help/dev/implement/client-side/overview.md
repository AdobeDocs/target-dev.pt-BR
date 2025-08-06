---
keywords: implementar, implementação, at.js, sdk da web da adobe experience platform, sdk da web da aep
description: Saiba como implementar o [!DNL Adobe Target] para Web no lado do cliente usando o [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) ou a biblioteca de JavaScript at.js.
title: Como implementar o  [!DNL Target] para Web no lado do cliente
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 7e2f1620c839393051432485192a45ddda2390a0
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 28%

---

# Visão geral: implementar o [!DNL Target] para Web no lado do cliente

Em uma implementação no lado do cliente do [!DNL Adobe Target], o [!DNL Target] fornece as experiências associadas a uma atividade diretamente para o navegador do cliente. O navegador decide qual experiência será exibida e realiza a ação. Com uma implementação no lado do cliente, você pode usar um editor WYSIWYG, o [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) ou uma interface não visual, o [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para criar experiências de atividade e personalização.

Para implementar o [!DNL Target] no lado do cliente, você deve usar uma das seguintes bibliotecas JavaScript:

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  O [!UICONTROL Adobe Experience Platform Web SDK] permite que você interaja com os vários serviços no [!DNL Adobe Experience Cloud] (incluindo o [!DNL Target]) até o [!UICONTROL Adobe Experience Edge Network]. Se você optar por migrar para o [!UICONTROL Adobe Experience Platform Web SDK], consulte [O que é [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md).

* [Biblioteca JavaScript at.js do [!DNL Target]](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)

  A biblioteca at.js do JavaScript melhora os tempos de carregamento de página de implementações da Web, melhora a segurança e fornece opções de implementações melhores para aplicativos de página única. Se você optar por migrar para a at.js, consulte [Como a at.js funciona](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) e [[!DNL Adobe Target] Skill Builder: bate-papo com o desenvolvedor, migre da mbox.js do Adobe Target para a at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Consulte [Comparação da biblioteca at.js com o Web SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) para saber mais sobre as diferenças entre as duas abordagens de implementação.