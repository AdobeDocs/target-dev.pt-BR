---
keywords: controle de qualidade, visualização, link de visualização, dispositivo móvel, visualização móvel
description: Use os links de visualização móvel para realizar tarefas completas de controle da qualidade para atividades de aplicativos móveis.
title: Como usar links de visualização móvel no [!DNL Adobe Target] Dispositivo móvel?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 0bcfa16cb79644e7ce10e33daf6c8385104c197f
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 27%

---

# [!DNL Target] visualização móvel

Use os links de visualização móvel para realizar facilmente tarefas completas de controle da qualidade e participar de experiências diferentes usando seu dispositivo sem dispositivos de teste especiais.

A funcionalidade de visualização móvel permite que você teste completamente suas atividades no aplicativo móvel antes de inicializá-las.

## Pré-requisitos

1. **Usar uma versão compatível do SDK:** O recurso de visualização móvel exige que você baixe e instale a versão apropriada da [!DNL Adobe Mobile SDK] nos aplicativos correspondentes.

   Para obter instruções sobre como baixar o SDK apropriado, consulte [Versões atuais do SDK](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} no *[!DNL Adobe Experience Platform Mobile SDK]* documentação.

1. **Defina um esquema de URL:** o link de visualização usa um esquema de URL para abrir seu aplicativo. Especifique um esquema de URL exclusivo para a visualização.

   Para obter mais informações, consulte [Visualização visual](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Configurar a extensão do Target na interface da conexão de dados* no *[!DNL Mobile SDK]* documentação.

   Os links a seguir contêm mais informações:

   * **iOs**: para obter mais informações sobre como configurar esquemas de URL para o iOS, consulte [Definição de um esquema de URL personalizado para seu aplicativo](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} no *Desenvolvedor do Apple* site.
   * **Android**: para obter mais informações sobre como configurar esquemas de URL para o Android, consulte [Criar deep links para conteúdo do aplicativo](https://developer.android.com/training/app-links/deep-linking){target=_blank} no *Desenvolvedores do Android* site.

1. **Configurar o `collectLaunchInfo` API (somente i0S)**

   Para obter mais informações, consulte [Visualização visual](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Configurar a extensão do Target na interface da conexão de dados* no *[!DNL Mobile SDK]* documentação.

## Gerar um link de visualização

1. No [!DNL Target] clique no link **[!UICONTROL Mais opções]** (as reticências verticais) e selecione **[!UICONTROL Criar link de visualização móvel]**.

   ![imagem alt](assets/mobile-preview-create.png)

1. Selecione as atividades que deseja visualizar e clique em **[!UICONTROL Gerar link de visualização móvel]**.

   >[!NOTE]
   >
   >Você pode selecionar somente Baseado em formulário [!UICONTROL Teste A/B] e [!UICONTROL Direcionamento de experiência] (XT) Atividades.

   ![imagem alt](assets/mobile-preview-select-activities.png)

1. Especifique o esquema de URL do seu aplicativo.

   O esquema de URL deve ser o mesmo que o presente no aplicativo iOS ou Android. Repita esse processo separadamente para iOS e Android, se necessário.

   ![imagem alt](assets/mobile-preview-enter-url-scheme.png)

1. Clique em **[!UICONTROL Gerar link de visualização móvel]**, depois copie o link.

   ![imagem alt](assets/mobile-preview-generate-and-copy.png)

## Visualizar no seu dispositivo

Abra o link em um navegador móvel em um dispositivo onde você tem seu aplicativo instalado. Este aplicativo pode ser o aplicativo de produção que você baixou do [!DNL Apple App Store] ou o [!DNL Google Play Store]. O aplicativo não precisa ser uma build especial. Se você tiver um link de visualização ativo, poderá visualizar as experiências no dispositivo.

1. Abra o link no seu navegador móvel.

   Compartilhar o link copiado na seção anterior da [!DNL Target] para o seu dispositivo móvel de forma conveniente, por exemplo, usando texto, email ou [!DNL Slack].

   |![link direto da visualização 1](assets/mobile-preview-open-deeplink.png)|![link direto da visualização 2](assets/mobile-preview-open-app.png)|

   Seu aplicativo abre e inicia o [!DNL Target] [!UICONTROL Modo de visualização móvel].

1. Selecione a combinação de experiências que deseja ver e clique em **[!UICONTROL Executar experiências]**.

   |![visualização móvel 1](assets/mobile-preview-experience-selection-1.png)|![visualização móvel 2](assets/mobile-preview-experience-result-1-france.png)|![visualização móvel 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![visualização móvel 4](assets/mobile-preview-experience-selection-2.png)|![visualização móvel 5](assets/mobile-preview-experience-result-2-aus.png)|![visualização móvel 6](assets/mobile-preview-experience-result-2-10off.png)|

## Limitações

* A visualização deve carregar novamente para que o novo conteúdo seja exibido após o botão **[!UICONTROL Executar experiências]** é clicado. O modo mais fácil é mudar para uma tela diferente e voltar para a tela onde você esperava a mudança acontecer.
* A visualização móvel não é suportada em versões do Android anteriores a API-19 (KitKat).
