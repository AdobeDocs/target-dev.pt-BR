---
keywords: mbox global, personalizar mbox global, editar at.js, at.js, implementar at.js
description: Saiba como personalizar uma mbox global para at.js na página [!UICONTROL Administration]-[!UICONTROL Implementation] do  [!DNL Adobe Target].
title: Como personalizar uma mbox global?
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 18%

---

# Personalizar uma mbox global

Informações para ajudar a personalizar uma mbox global [!DNL Adobe Target] para at.js.

1. Clique em **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

1. Desabilite **[!UICONTROL Page load enabled (Auto create global mbox)]** e adicione o nome da mbox global personalizada que você gostaria de usar para entregar atividades de [!DNL Target].

>[!WARNING]
>
>A alteração é salva automaticamente ao selecionar outra mbox global.

Essa mbox global personalizada também será usada para rastreamento de cliques.

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. Implemente a biblioteca at.js no seu site.

   Consulte [Como implantar a at.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md) para obter mais informações.

1. Organize a transição com seu lançamento.

   Quando estiver pronto para que [!DNL Target] comece a usar sua mbox global para todas atividades no futuro, você pode prosseguir com esta etapa.

   Atualize o nome da mbox global personalizada para o mesmo nome usado no passo 2 acima.


>[!WARNING]
>
>Todas as atividades na sua conta sincronizam com esta mbox. Verifique se a mbox global está presente no site para que as atividades continuem funcionando. Edite e salve novamente as atividades afetadas que foram criadas com o [!UICONTROL Visual Experience Composer] (VEC) que se sincronizam com esta mbox. Não é necessário salvar novamente as atividades criadas no [!UICONTROL Form-Based Experience Composer] ou por meio da API.
