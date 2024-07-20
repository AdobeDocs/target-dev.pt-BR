---
keywords: mbox global, target classic, usar mbox global do target classic
description: Saiba como usar uma mbox global herdada para suas atividades do  [!DNL Adobe Target]  se você já criou uma mbox global em suas páginas para as implementações herdadas.
title: Posso usar uma mbox global de uma implementação existente?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 20%

---

# Usar uma mbox global por meio de uma implementação herdada

Por padrão, [!DNL Target] cria uma mbox global chamada target-global-mbox, que é usada para executar atividades criadas em [!DNL Target]. No entanto, se já tiver criado uma mbox global em suas páginas para as implementações herdadas, você poderá usar essa mbox para suas atividades do [!DNL Target].

>[!NOTE]
>
>Você só pode ter uma mbox por conta.

Para usar sua mbox global existente no [!DNL Target] e em sua implementação existente, você deve definir alguns parâmetros.

1. Vá para [!DNL Target] e clique em **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

   Por padrão, **[!UICONTROL Page load enabled (Auto-create global mbox]** está habilitado, e a mbox global personalizada é chamada `target-global-mbox`.

1. Se quiser usar uma mbox existente, desabilite **[!UICONTROL Page load enabled (Auto-create global mbox]** e especifique o nome de uma mbox global criada anteriormente no campo **[!UICONTROL Global Mbox]**.

   A lista suspensa Mbox global lista todas as mboxes na sua conta. Se você quiser usar uma mbox que ainda não existe, crie a mbox.

1. Clique em **[!UICONTROL Save]**.

   As configurações da sua conta são atualizadas.

1. Baixe o novo arquivo at.js e cite-o em seu site.

   Todas as atividades existentes foram atualizadas para usar a mbox global especificada, inclusive as atividades que foram anteriormente criadas e implementadas.

## Solução de problemas de implementação da mbox global

As seguintes perguntas frequentes podem ser usadas para solucionar problemas de implementação da mbox global:

### Por que a mbox global não está carregando ou por que há uma latência no carregamento da mbox global quando a página carrega?

Verifique se a referência da at.js é a primeira chamada do JavaScript na página. Para outras soluções para esse problema, consulte [Perguntas frequentes sobre a Mbox global](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
