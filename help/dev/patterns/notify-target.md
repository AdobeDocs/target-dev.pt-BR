---
title: Notificar Destino
description: Garantir que todos os eventos que precisam ser rastreados pelo [!DNL Target] são enviados usando o método trackEvent.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 1291a095a7befed5f795f34099e0411930788e29
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Notificar [!DNL Target]

A conclusão desta etapa garante que todos os eventos que devem ser enviados para o [!DNL Adobe Target] são enviados usando o `trackEvent` método.

Qualquer evento que precise ser rastreado em [!DNL Target] pode ser um evento de conversão principal ou uma métrica de sucesso.

>[!TIP]
>
>Clique nas imagens neste tópico para expandir para tela inteira.

## Notificar [!DNL Target] diagrama {#diagram}

O número da etapa na ilustração a seguir corresponde à seção abaixo.

![Notificar diagrama de destino](/help/dev/patterns/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## Fogo [!DNL Adobe Target] Rastrear API

Esta etapa ajuda a garantir que todos os eventos que devem ser enviados para o [!DNL Target] são enviados usando o `trackEvent` método.

+++Ver detalhes

![Acionar diagrama da API de rastreamento do Adobe Target](/help/dev/patterns/assets/fire-adobe-target-track-api-diagram.png){width="100" zoomable="yes"}

Você envia os atributos de conversão do pedido conforme mencionado na *Pré-requisitos* abaixo. O nome da mbox não importa, mas a conversão é usar `orderConfirmPage`.

Não é necessário incluir os atributos de conversão de pedido nesta chamada. Essas chamadas registram, idealmente, métricas de sucesso que podem ser consideradas eventos de miniconversão antes dos eventos de conversão principais. `CardIds` deve ser incluído nas recomendações baseadas no carrinho com base no `Add to Cart` evento.

**Pré-requisitos**

* Encontre sua equipe de negócios para identificar todos os eventos que podem ser considerados métricas de conversão ou de sucesso. Você também deve identificar o evento de conversão que gera a receita para que esses detalhes possam ser enviados para [!DNL Target] juntamente com os dados do evento.
* Verifique se os seguintes atributos estão disponíveis na camada de dados para que você possa enviá-los com o evento de conversão. O evento de conversão gera receita, como uma compra de produto ou um evento Adicionar ao carrinho.

   * `productPurchaseId`: IDs de produto que foram compradas como parte do pedido. Separe vários produtos usando vírgulas.
   * `orderTotal`: total do pedido da compra.
   * `orderId`: ID do pedido da compra.

* Se você estiver rastreando um evento para adição ao carrinho, envie `cartIds` como parâmetro. Uma lista separada por vírgulas de IDs de produtos pode ser passada para `cardIds`.

**Leituras**

* [método adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds para critérios baseados em carrinho](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**Ações**

* Uso `adobe.target-trackEvent()` para enviar todos os dados que devem ser enviados para [!DNL Target].







