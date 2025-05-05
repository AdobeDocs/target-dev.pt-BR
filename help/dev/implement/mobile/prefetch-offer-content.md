---
keywords: oferta, busca prévia, iOS, android, sdk, dispositivo móvel, sdk móvel, $8
description: Use o recurso de busca prévia  [!DNL Adobe Target]  nos SDKs móveis para iOS e Android para buscar conteúdo de oferta a menor quantidade de vezes possível, armazenando as respostas do servidor em cache.
title: Posso buscar previamente conteúdo da oferta para aplicativos móveis?
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 43%

---

# Buscar previamente conteúdo da oferta

O recurso de busca prévia do [!DNL Target] usa o SDK móvel do Android e do iOS para buscar conteúdo de oferta a menor quantidade de vezes possível, armazenando as respostas do servidor em cache.

>[!IMPORTANT]
>
>Suporte para o [!DNL Adobe Mobile] versão 4.Os SDKs do *x* terminaram em 31 de agosto de 2021 e não são mais recomendados para usuários móveis do [!DNL Adobe Target].
>
>O [Adobe Experience Platform SDK para Aplicativos para Dispositivos Móveis](https://developer.adobe.com/client-sdks/documentation/){target=_blank} é a solução recomendada para habilitar soluções e serviços do [!DNL Adobe Experience Cloud] em seus aplicativos para dispositivos móveis.

Esse processo reduz o tempo de carregamento, previne várias chamadas de rede e permite que o [!DNL Target] seja notificado sobre que mbox foi visitada pelo usuário do aplicativo móvel. Todo o conteúdo é recuperado e armazenado em cache durante a chamada da busca prévia e esse conteúdo é recuperado do cache para todas as chamadas futuras que contenham conteúdo armazenado em cache para o nome da mbox especificado.

Considere as seguintes limitações ao usar o método de busca prévia com os SDKs móveis para iOS e Android:

* O conteúdo da busca prévia não persiste entre inicializações. O conteúdo da busca prévia é armazenado em cache enquanto o aplicativo está em uso ou até o método `clearPrefetchCache()` ser chamado.
* Não há suporte para a funcionalidade de busca prévia para os métodos de alocação de tráfego [!UICONTROL Auto-Allocate] e [!UICONTROL Auto-Target], para os tipos de atividade [!UICONTROL Automated Personalization] ou [!UICONTROL Recommendations] ou para as ofertas de [recomendações em uma atividade A/B ou XT](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html?lang=pt-BR).

Para obter mais informações, incluindo métodos de busca prévia, classes públicas e exemplos de código, consulte:

* **iOS:** [Buscar previamente conteúdo da oferta no iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html) na *Ajuda do SDK iOS do Mobile Services*.
* **Android:** [Buscar previamente conteúdo da oferta no Android](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html) na *Ajuda do SDK Android do Mobile Services*.
