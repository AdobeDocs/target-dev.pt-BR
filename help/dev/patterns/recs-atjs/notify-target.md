---
title: Notificar Destino
description: Verifique se todos os eventos que precisam ser rastreados por  [!DNL Target] são enviados usando o método trackEvent.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: efccadab-d139-4423-8613-c2743d87b3a0
TQID: https://experienceleague.adobe.com/u-RPLXjG8UBI7bDu2HgPFFnNBU--Yr0UydVX-Q-dcTc
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 0%

---

# Notificar [!DNL Target]

A conclusão desta etapa garante que todos os eventos que devem ser enviados para [!DNL Adobe Target] sejam enviados usando o método `trackEvent`.

Qualquer evento que precise ser rastreado em [!DNL Target] pode ser um evento de conversão principal ou uma métrica de sucesso.

>[!TIP]
>
>Clique nas imagens neste tópico para expandir para tela inteira.

## Notificar diagrama [!DNL Target] {#diagram}

O número da etapa na ilustração a seguir corresponde à seção abaixo.

![Notificar diagrama de Destino](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1: Acionar a API de rastreamento [!DNL Adobe Target]

Esta etapa ajuda a garantir que todos os eventos que devem ser enviados para [!DNL Target] sejam enviados usando o método `trackEvent`.

+++Ver detalhes

![Acionar o diagrama da API do Adobe Target Track](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

Você envia os atributos de conversão do pedido conforme mencionado na seção *Pré-requisitos* abaixo. O nome da mbox não importa, mas a conversão é usar `orderConfirmPage`.

Não é necessário incluir os atributos de conversão de pedido nesta chamada. Essas chamadas registram, idealmente, métricas de sucesso que podem ser consideradas eventos de miniconversão antes dos eventos de conversão principais. `CardIds` deve ser incluído nas recomendações baseadas no carrinho com base no evento `Add to Cart`.

+++

**Pré-requisitos**

* Encontre sua equipe de negócios para identificar todos os eventos que podem ser considerados métricas de conversão ou de sucesso. Você também deve identificar o evento de conversão que gera receita para que esses detalhes possam ser enviados para [!DNL Target] junto com os dados do evento.
* Verifique se os seguintes atributos estão disponíveis na camada de dados para que você possa enviá-los com o evento de conversão. O evento de conversão gera receita, como uma compra de produto ou um evento Adicionar ao carrinho.

   * `productPurchaseId`: IDs de produto que foram compradas como parte do pedido. Separe vários produtos usando vírgulas.
   * `orderTotal`: Total do pedido para a compra.
   * `orderId`: ID do pedido da compra.

  A ilustração a seguir mostra uma [regra para [!DNL tags] em [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/tags.html?lang=pt-BR){target=_blank} que deve ser acionada somente na página [!UICONTROL Confirmação].

  ![Página Configuração de ação](/help/dev/patterns/recs-atjs/assets/action-configuration.png){width="400" zoomable="yes"}

* Se você estiver rastreando um evento para adição ao carrinho, envie `cartIds` como parâmetro. Uma lista separada por vírgulas de IDs de produtos pode ser passada para `cardIds`.

**Leituras**

* [método adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds para critérios baseados em carrinho](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=pt-BR#cart-based){target=_blank}

**Ações**

* Use o método `adobe.target-trackEvent()` para enviar todos os dados que devem ser enviados para [!DNL Target].
