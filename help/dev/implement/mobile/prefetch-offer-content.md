---
keywords: oferta, busca prévia, iOS, android, sdk, dispositivo móvel, sdk móvel, $8
description: Use o recurso de busca prévia do [!DNL Adobe Target] nos SDKs móveis para iOS e Android para buscar conteúdo de oferta a menor quantidade de vezes possível, armazenando as respostas do servidor em cache.
title: Posso buscar previamente conteúdo da oferta para aplicativos móveis?
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: d051910f-2bda-47ea-a969-6ade9fcd71f1
    internal-label: Implement mobile
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 37%
---
# Buscar previamente conteúdo da oferta

O recurso de busca prévia do [!DNL Target] usa o SDK móvel do Android e do iOS para buscar conteúdo de oferta a menor quantidade de vezes possível, armazenando as respostas do servidor em cache.

>[!IMPORTANT]
>
>O suporte para os SDKs [!DNL Adobe Mobile] versão 4.*x* terminou a partir de 31 de agosto de 2021 e não é mais recomendado para usuários móveis [!DNL Adobe Target].
>
>O [Adobe Experience Platform SDK para Aplicativos para Dispositivos Móveis](https://developer.adobe.com/client-sdks/documentation/){target=_blank} é a solução recomendada para habilitar soluções e serviços do [!DNL Adobe Experience Cloud] em seus aplicativos para dispositivos móveis.

Esse processo reduz o tempo de carregamento, previne várias chamadas de rede e permite que o [!DNL Target] seja notificado sobre que mbox foi visitada pelo usuário do aplicativo móvel. Todo o conteúdo é recuperado e armazenado em cache durante a chamada da busca prévia e esse conteúdo é recuperado do cache para todas as chamadas futuras que contenham conteúdo armazenado em cache para o nome da mbox especificado.

Considere as seguintes limitações ao usar o método de busca prévia com os SDKs móveis para iOS e Android:

* O conteúdo da busca prévia não persiste entre inicializações. O conteúdo da busca prévia é armazenado em cache enquanto o aplicativo está em uso ou até o método `clearPrefetchCache()` ser chamado.
* Não há suporte para a funcionalidade de busca prévia para os métodos de alocação de tráfego de [!UICONTROL Alocação automática] e [!UICONTROL Direcionamento automático], para os tipos de atividade de [!UICONTROL Automated Personalization] ou [!UICONTROL Recommendations] ou para as ofertas de [recomendações em uma atividade A/B ou XT](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html).

Para obter mais informações, incluindo métodos de busca prévia, classes públicas e exemplos de código, consulte:

* **iOS:** [Buscar previamente conteúdo da oferta no iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html) na *Ajuda do iOS SDK do Mobile Services*.
* **Android:** [Buscar previamente conteúdo da oferta no Android](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html) na *Ajuda do Android SDK do Mobile Services*.
