---
keywords: aplicativo móvel, sdk de aplicativo móvel, aplicativo móvel target, sdk target móvel, sdk de aplicativo movel, habilitar target no sdk
description: Saiba como adicionar o SDK do Adobe Mobile Services ao seu aplicativo móvel.
title: Como habilitar [!DNL Target] no [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
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
source-wordcount: '303'
ht-degree: 38%
---
# Habilitar [!DNL Target] no SDK

Adicione a [!UICONTROL SDK] do Adobe Mobile Services ao seu aplicativo.

>[!IMPORTANT]
>
>O suporte para os SDKs [!DNL Adobe Mobile] versão 4.*x* terminou a partir de 31 de agosto de 2021 e não é mais recomendado para usuários móveis [!DNL Adobe Target].
>
>O [Adobe Experience Platform SDK para Aplicativos para Dispositivos Móveis](https://developer.adobe.com/client-sdks/documentation/){target=_blank} é a solução recomendada para habilitar soluções e serviços do [!DNL Adobe Experience Cloud] em seus aplicativos para dispositivos móveis.

1. Se ainda não tiver instalado a SDK do Adobe Mobile Services no aplicativo, use suas credenciais do Analytics ou da Experience Cloud e baixe a SDK do site do [Adobe Mobile Services](https://mobilemarketing.adobe.com/).

1. Adicione o [!DNL Adobe Mobile Services SDK] ao seu aplicativo.

   Você encontrará instruções em [Implementação principal e ciclo de vida](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html?lang=pt-BR).

1. Adicione o código do cliente, tempo-limite e habilite o SSL.

   Na Experience Cloud, abra o Mobile Services, depois vá para **[!UICONTROL Administrar configurações do aplicativo]** > **[!UICONTROL Opções do SDK do Target]**.

   Adicione seu clientcode [!DNL Target] e tempo limite. O código do cliente é único para sua conta e empresa. O tempo limite é o tempo em segundos até o qual [!DNL Target] aguardará uma resposta antes de mostrar o conteúdo padrão. Certifique-se de que a opção **[!UICONTROL Usar HTTPS]** está marcada na página Administrar configurações do aplicativo no Adobe Mobile Services. Se o HTTPS não estiver habilitado, todas as chamadas no iOS9+ serão bloqueadas, a menos que você inclua na lista de permissões do servidor [!DNL Target].

   ![alt imagem](assets/mobile-clientcode.png)

1. Depois de criar/localizar seu aplicativo, encontre as configurações do aplicativo e baixe o SDK desejado.

   ![alt imagem](assets/download-sdk.png)

>[!WARNING]
>
> Se você não tiver acesso à interface de marketing para dispositivos móveis, poderá fazer alterações diretamente no arquivo de configuração no código do aplicativo; no entanto, não estará sincronizado com a página de configurações na interface do usuário.
