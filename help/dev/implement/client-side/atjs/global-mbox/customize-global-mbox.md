---
keywords: mbox global, personalizar mbox global, editar at.js, at.js, implementar at.js
description: Saiba como personalizar uma mbox global para at.js na página [!UICONTROL Administração]-[!UICONTROL Implementação] em [!DNL Adobe Target].
title: Como personalizar uma mbox global?
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
TQID: https://experienceleague.adobe.com/MtbjwpKrZ-WmBnE5tBY74oJgQVB-zPLrCuFDrFshkGo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 227
ht-degree: 16%

---

# Personalizar uma mbox global

Informações para ajudar a personalizar uma mbox global [!DNL Adobe Target] para at.js.

1. Clique em **[!UICONTROL Administração]** > **[!UICONTROL Implementação]**.

1. Desabilite **[!UICONTROL Carregamento de página habilitado (Criar mbox global automaticamente)]** e adicione o nome da mbox global personalizada que você gostaria de usar para entregar atividades de [!DNL Target].

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
>Todas as atividades na sua conta sincronizam com esta mbox. Verifique se a mbox global está presente no site para que as atividades continuem funcionando. Edite e salve novamente as atividades afetadas que foram criadas com o [!UICONTROL Visual Experience Composer] (VEC) que se sincronizam com esta mbox. Não é necessário salvar novamente as atividades criadas no [!UICONTROL Experience Composer baseado em formulário] ou via API.
