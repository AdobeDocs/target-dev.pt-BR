---
keywords: mbox global, implementar a at.js
description: Saiba mais sobre a mbox global na implementação do  [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] .
title: O que é uma mbox global?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
TQID: https://experienceleague.adobe.com/MXEGvHHY8tFMfS6bMHcZYaG9mZtOWEkuODKH24JifZI
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
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 201
ht-degree: 61%

---

# Entender a mbox global

Informações sobre a mbox global, um nome usado para se referir à única chamada de servidor feita na parte superior de cada página da Web na sua implementação do [!DNL Adobe Target].

Por padrão, a mbox global é chamada de `target-global-mbox`. Ela pode ser renomeada para a sua conta, se necessário.

Existem várias diferenças entre uma mbox comum (mbox não global) e a mbox global, incluindo:

| Mbox comum | Mbox global |
|--- |--- |
| Uma mbox comum geralmente envolve conteúdo com uma tag `<DIV>`. | A mbox global está &quot;vazia&quot; e não envolve nenhum conteúdo. |
| O conteúdo de apenas uma atividade pode ser entregue em uma mbox comum. | O conteúdo de várias atividades pode ser entregue em uma resposta a uma mbox global. |

Se várias atividades forem fornecidas por meio da mbox global ou por várias mboxes regulares, o Target [determinará a prioridade](https://experienceleague.adobe.com/docs/target/using/activities/priority.html?lang=pt-BR) pela qual a atividade (ou atividades) será entregue para uma página da Web.

Os dados adicionais da página podem ser enviados para o [!DNL Target] junto com a mbox global usando a função `[!UICONTROL targetPageParams]`. Isso é semelhante à funcionalidade do parâmetro da mbox. Para obter mais informações, consulte [Passar parâmetros para uma mbox global](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).
