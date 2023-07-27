---
keywords: mbox global, implementar a at.js
description: Saiba mais sobre a mbox global no [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] execução.
title: O que é uma mbox global?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 73%

---

# Entender a mbox global

Informações sobre a mbox global, um nome usado para referir-se a uma chamada de servidor única feita na parte superior de cada página da Web na sua implementação do [!DNL Adobe Target].

Por padrão, a mbox global é chamada de `target-global-mbox`. Ela pode ser renomeada para a sua conta, se necessário.

Existem várias diferenças entre uma mbox comum (mbox não global) e a mbox global, incluindo:

| Mbox comum | Mbox global |
|--- |--- |
| Uma mbox comum geralmente envolve conteúdo com uma tag `<DIV>`. | A mbox global está &quot;vazia&quot; e não envolve nenhum conteúdo. |
| O conteúdo de apenas uma atividade pode ser entregue em uma mbox comum. | O conteúdo de várias atividades pode ser entregue em uma resposta a uma mbox global. |

Se várias atividades forem fornecidas por meio da mbox global ou por várias mboxes regulares, o Target [determina a prioridade](https://experienceleague.adobe.com/docs/target/using/activities/priority.html) pela qual a atividade (ou atividades) é entregue a uma página da web.

Os dados adicionais da página podem ser enviados para o [!DNL Target] junto com a mbox global usando a função `[!UICONTROL targetPageParams]`. Isso é semelhante à funcionalidade do parâmetro da mbox. Para obter mais informações, consulte [Passar parâmetros para uma mbox global](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).
