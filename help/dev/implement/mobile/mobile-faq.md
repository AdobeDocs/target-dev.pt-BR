---
keywords: aplicativo móvel, perguntas frequentes, perguntas frequentes, aplicativo móvel do target
description: Veja as perguntas frequentes e suas respostas sobre o  [!DNL Adobe Target]  para aplicativos móveis.
title: Quais são as perguntas frequentes [!DNL About Target] sobre aplicativos móveis?
feature: Implement Mobile
exl-id: 06cae3de-83a4-4018-a832-66fb292a1d0f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---

# Perguntas frequentes sobre o [!DNL Target] for mobile apps

Lista de perguntas frequentes sobre [!DNL Target] para aplicativos móveis.

## Devo usar tags no [!DNL Adobe Experience Platform] para implantar o SDK, ou posso implantar o SDK sem usar o Launch?

O SDK está disponível no [Adobe Marketing Cloud git](https://github.com/Adobe-Marketing-Cloud/acp-sdks/){target=_blank}. Se você não usar [tags na Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR){target=_blank}, deverá gerenciar seu próprio arquivo de configurações e gerenciá-lo no aplicativo.

## Quais SDKs estão disponíveis hoje?

Atualmente, os SDKs do Adobe Experience Platform Mobile são compatíveis com iOS, Android e React. Para obter mais informações, consulte o [guia dos SDKs móveis da Adobe Experience Cloud Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=pt-BR){target=_blank}.

## Qual é a frequência do recurso baseado em localização, em termos de verificação sobre a latitude e a longitude?

Consulte a [documentação do Adobe Places](https://experienceleague.adobe.com/docs/places/using/home.html){target=_blank} para obter mais informações.

## Preciso da at.js para que os SDKs móveis da Adobe Experience Platform funcionem?

Não, você não precisa da at.js para usar os SDKs móveis. A at.js é a biblioteca JavaScript do [!DNL Target] para sites. Os SDKs do Adobe Experience Platform Mobile são para aplicativos móveis.

## O [!DNL Target] Mobile é uma funcionalidade somente da SKU do produto [!DNL Adobe Target] Premium?

Não. Para clientes do [!DNL Adobe Target Standard], você pode usar nossos SDKs móveis para atividades do [!UICONTROL A/B Test] e do [!UICONTROL Experience Targeting] (XT) somente com o complemento de Aplicativo móvel do [!DNL Target Standard]. Se você quiser usar o [!UICONTROL Recommendations] ou recursos alimentados por IA no aplicativo móvel, precisará de uma licença do [Adobe Target Premium](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium).

## Há uma integração de aplicativo móvel entre as atividades móveis de [!DNL Adobe Experience Manager] (AEM) e [!DNL Target]?

Atualmente, você pode compartilhar JSON [Fragmentos de experiência](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html){target=_blank} do AEM com [!DNL Target] e, em seguida, usá-los em uma atividade de aplicativo móvel.
