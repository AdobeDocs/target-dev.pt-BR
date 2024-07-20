---
keywords: controle de qualidade, visualização, link de visualização, dispositivo móvel, visualização móvel
description: Use os links de visualização móvel para realizar tarefas completas de controle da qualidade para atividades de aplicativos móveis.
title: Como usar links de visualização móvel no  [!DNL Adobe Target] Mobile?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 15e42d0fb049f9243ff5468ff5f22a8e79c55c79
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 23%

---

# Visualização móvel de [!DNL Target]

Use os links de visualização móvel para realizar facilmente tarefas completas de controle da qualidade e participar de experiências diferentes usando seu dispositivo sem dispositivos de teste especiais.

A funcionalidade de visualização móvel permite que você teste completamente suas atividades no aplicativo móvel antes de inicializá-las.

## Pré-requisitos

1. **Use uma versão do SDK com suporte:** O recurso de visualização móvel exige que você baixe e instale a versão apropriada do [!DNL Adobe Mobile SDK] nos aplicativos correspondentes.

   Para obter instruções sobre como baixar o SDK apropriado, consulte [Versões atuais do SDK](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} na documentação *[!DNL Adobe Experience Platform Mobile SDK]*.

1. **Defina um esquema de URL:** o link de visualização usa um esquema de URL para abrir seu aplicativo. Especifique um esquema de URL exclusivo para a visualização.

   Para obter mais informações, consulte [Visualização visual](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} em *Configurar a extensão do Target na interface da Conexão de Dados* na documentação *[!DNL Mobile SDK]*.

   Os links a seguir contêm mais informações:

   * **iOs**: Para obter mais informações sobre como configurar esquemas de URL para o iOS, consulte [Definindo um esquema de URL personalizado para seu aplicativo](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} no site *Apple Developer*.
   * **Android**: Para obter mais informações sobre como configurar esquemas de URL para o Android, consulte [Criar deep links para conteúdo do aplicativo](https://developer.android.com/training/app-links/deep-linking){target=_blank} no site *Desenvolvedores do Android*.

1. **Configurar a API `collectLaunchInfo` (somente i0S)**

   Para obter mais informações, consulte [Visualização visual](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} em *Configurar a extensão do Target na interface da Conexão de Dados* na documentação *[!DNL Mobile SDK]*.

## Gerar um link de visualização

1. Na interface do usuário do [!DNL Target], clique no ícone **[!UICONTROL More Options]** (as reticências verticais) e selecione **[!UICONTROL Create Mobile Preview Link]**.

   ![alt imagem](assets/mobile-preview-create.png)

1. Selecione as atividades que deseja visualizar e clique em **[!UICONTROL Generate Mobile Preview Link]**.

   >[!NOTE]
   >
   >Você pode selecionar apenas atividades [!UICONTROL A/B Test] e [!UICONTROL Experience Targeting] (XT) baseadas em formulário.

   ![alt imagem](assets/mobile-preview-select-activities.png)

1. Especifique o esquema de URL do seu aplicativo.

   O esquema de URL deve ser o mesmo que o presente no aplicativo iOS ou Android. Repita esse processo separadamente para iOS e Android, se necessário.

   ![alt imagem](assets/mobile-preview-enter-url-scheme.png)

1. Clique em **[!UICONTROL Generate Mobile Preview Link]** e copie o link.

   ![alt imagem](assets/mobile-preview-generate-and-copy.png)

## Visualizar no seu dispositivo

Abra o link em um navegador móvel em um dispositivo onde você tem seu aplicativo instalado. Este aplicativo pode ser o aplicativo de produção que você baixou do [!DNL Apple App Store] ou do [!DNL Google Play Store]. O aplicativo não precisa ser uma build especial. Se você tiver um link de visualização ativo, poderá visualizar as experiências no dispositivo.

1. Abra o link no seu navegador móvel.

   Compartilhe o link copiado na seção anterior da interface do usuário do [!DNL Target] com seu dispositivo móvel de forma conveniente, por exemplo, usando texto, email ou [!DNL Slack].

   |![link direto da visualização 1](assets/mobile-preview-open-deeplink.png)|![link direto da visualização 2](assets/mobile-preview-open-app.png)|

   Seu aplicativo abre e inicia o [!DNL Target] [!UICONTROL Mobile Preview Mode].

1. Selecione a combinação de experiências que deseja ver e clique em **[!UICONTROL Launch Experiences]**.

   |![visualização móvel 1](assets/mobile-preview-experience-selection-1.png)|![visualização móvel 2](assets/mobile-preview-experience-result-1-france.png)|![visualização móvel 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![visualização móvel 4](assets/mobile-preview-experience-selection-2.png)|![visualização móvel 5](assets/mobile-preview-experience-result-2-aus.png)|![visualização móvel 6](assets/mobile-preview-experience-result-2-10off.png)|

## Limitações

* A exibição deve ser carregada novamente para que o novo conteúdo seja exibido após o clique no botão **[!UICONTROL Launch Experiences]**. O modo mais fácil é mudar para uma tela diferente e voltar para a tela onde você esperava a mudança acontecer.
* A visualização móvel não é suportada em versões do Android anteriores a API-19 (KitKat).
