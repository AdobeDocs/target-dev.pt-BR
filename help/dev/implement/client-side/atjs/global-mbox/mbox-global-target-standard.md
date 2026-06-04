---
keywords: mbox global, target classic, usar mbox global do target classic
description: Saiba como usar uma mbox global herdada para suas atividades do  [!DNL Adobe Target]  se você já criou uma mbox global em suas páginas para as implementações herdadas.
title: Posso usar uma mbox global de uma implementação existente?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
TQID: https://experienceleague.adobe.com/BCubNDwB8gxZ9bpuCNhxcnFnjB1xQK8ZRkLveinPj4w
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 304
ht-degree: 19%

---

# Usar uma mbox global por meio de uma implementação herdada

Por padrão, [!DNL Target] cria uma mbox global chamada target-global-mbox, que é usada para executar atividades criadas em [!DNL Target]. No entanto, se já tiver criado uma mbox global em suas páginas para as implementações herdadas, você poderá usar essa mbox para suas atividades do [!DNL Target].

>[!NOTE]
>
>Você só pode ter uma mbox por conta.

Para usar sua mbox global existente no [!DNL Target] e em sua implementação existente, você deve definir alguns parâmetros.

1. Vá para [!DNL Target] e clique em **[!UICONTROL Administração]** > **[!UICONTROL Implementação]**.

   Por padrão, **[!UICONTROL Carregamento de página habilitado (a mbox global de criação automática]** está habilitada, e a mbox global personalizada é chamada `target-global-mbox`.

1. Se quiser usar uma mbox existente, desative a **[!UICONTROL Mbox global]** para carregamento de página (Criação automática de mbox global) e especifique o nome da mbox global criada anteriormente no campo **[!UICONTROL Mbox global]**.

   A lista suspensa Mbox global lista todas as mboxes na sua conta. Se você quiser usar uma mbox que ainda não existe, crie a mbox.

1. Clique em **[!UICONTROL Salvar]**.

   As configurações da sua conta são atualizadas.

1. Baixe o novo arquivo at.js e cite-o em seu site.

   Todas as atividades existentes foram atualizadas para usar a mbox global especificada, inclusive as atividades que foram anteriormente criadas e implementadas.

## Solução de problemas de implementação da mbox global

As seguintes perguntas frequentes podem ser usadas para solucionar problemas de implementação da mbox global:

### Por que a mbox global não está carregando ou por que há uma latência no carregamento da mbox global quando a página carrega?

Verifique se a referência da at.js é a primeira chamada do JavaScript na página. Para outras soluções para esse problema, consulte [Perguntas frequentes sobre a Mbox global](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
