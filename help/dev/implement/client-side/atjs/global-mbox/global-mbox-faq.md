---
keywords: solução de problemas, perguntas frequentes, FAQ, FAQs, global, mbox global
description: Leia perguntas frequentes e respostas sobre as  [!DNL Target] mboxes globais do Adobe.
title: Quais são as perguntas frequentes sobre a mbox global?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
TQID: https://experienceleague.adobe.com/bxsjCqSQpp6M20StzZtMBrfxjJCKgPEPfS2OlBUP00A
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 309
ht-degree: 32%

---

# Perguntas frequentes sobre a Mbox global

Lista de perguntas frequentes sobre as mboxes globais.

## Posso ter mais de uma mbox global, se minha conta [!DNL Target] estiver configurada em vários domínios?

Somente uma mbox global é suportada na sua conta.

Você pode limitar o local de execução das atividades, ao adicionar as regras de URL às suas atividades. Para obter mais informações, consulte [Incluir a mesma experiência em páginas semelhantes](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

Você também pode passar um parâmetro para a página usando [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) e depois selecionar esses parâmetros na seção &quot;configurar URL&quot; no [!UICONTROL Visual Experience Composer] (VEC) ou adicionar os parâmetros como &quot;refinamentos&quot; no [!UICONTROL Form-Based Experience Composer].

## Como transfiro os dados de receita em uma mbox global [!DNL Target]?

Para coletar informações de receita e pedido da target-global-mbox, os &quot;parâmetros da mbox&quot; devem ser enviados para [!DNL Target]. Esses parâmetros são pares nome/valor usados para enviar mais informações para [!DNL Target]. [!DNL Target] procura automaticamente por esses parâmetros (nomes reservados) para preencher dados de receita.

Para o `orderConfirmPage`, você deve passar em `orderTotal`, `orderId` e `productPurchasedId`.

Esses parâmetros devem ser enviados para o target-global-mbox via `targetPageParams()`. Para obter mais informações, consulte [Passar parâmetros para uma mbox global](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

Você também adicionará o direcionamento ao componente de conversão, para que [!DNL Target] conte somente as conversões no target-global-mbox quando a página de confirmação do pedido for exibida, conforme mostrado abaixo:

![alt imagem](assets/revenue1.png)

A seção Páginas do site ilustradas acima contém as seguintes seções: Página atual, URL, contém, orderconfirm.

![alt imagem](assets/revenue2.png)

As opções na ilustração acima incluem as configurações a seguir:

* **O que você deseja medir com essa atividade:** Receita
* **Exibição padrão para geração de relatório:** Receita por visitante (RPV)
* **Que ação foi realizada pelo seu público-alvo para indicar que a sua meta foi alcançada?** Visualizada uma mbox, target-global-mbox
