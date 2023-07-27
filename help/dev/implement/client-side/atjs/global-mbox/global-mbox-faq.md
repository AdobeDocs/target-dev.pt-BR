---
keywords: solução de problemas, perguntas frequentes, FAQ, FAQs, global, mbox global
description: Leia as perguntas frequentes e as respostas sobre o Adobe [!DNL Target] mboxes globais.
title: Quais são as perguntas frequentes sobre a mbox global?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 68%

---

# Perguntas frequentes sobre a Mbox global

Lista de perguntas frequentes sobre as mboxes globais.

## Posso ter mais de uma mbox global, se minha [!DNL Target] conta for definida em vários domínios?

Somente uma mbox global é suportada na sua conta.

Você pode limitar o local de execução das atividades, ao adicionar as regras de URL às suas atividades. Para obter mais informações, consulte [Incluir a mesma experiência em páginas semelhantes](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

Você também pode passar um parâmetro para a página usando [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) e depois selecionar esses parâmetros na seção &quot;configurar URL&quot; no [!UICONTROL Visual Experience Composer][!UICONTROL  (VEC) ou adicionar os parâmetros como &quot;refinamentos&quot; no Experience Composer baseado em formulário].

## Como transfiro os dados de receita em um [!DNL Target] mbox global?

Para coletar informações de receita e pedidos na target-global-mbox, &quot;parâmetros da mbox&quot; devem ser enviados para o [!DNL Target]. Esses parâmetros são os pares de nome/valor usados para enviar mais informações ao [!DNL Target]. [!DNL Target]O automaticamente procura esses parâmetros (nomes reservados) para preencher os dados da receita.

Para o `orderConfirmPage`, você deve transmitir `orderTotal`, `orderId`e `productPurchasedId`.

Esses parâmetros devem ser enviados para o target-global-mbox via `targetPageParams()`. Para obter mais informações, consulte [Passar parâmetros para uma mbox global](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

Você também vai querer adicionar o direcionamento ao componente de conversão para que [!DNL Target] O só conta conversões no target-global-mbox quando a página de confirmação de pedido é exibida, conforme mostrado abaixo:

![imagem alt](assets/revenue1.png)

A seção Páginas do site ilustradas acima contém as seguintes seções: Página atual, URL, contém, orderconfirm.

![imagem alt](assets/revenue2.png)

As opções na ilustração acima incluem as configurações a seguir:

* **O que você deseja medir com essa atividade:** Receita
* **Exibição padrão para geração de relatório:** Receita por visitante (RPV)
* **Qual ação foi realizada pelo seu público-alvo para indicar que a sua meta foi alcançada?** Visualizada uma mbox, target-global-mbox
