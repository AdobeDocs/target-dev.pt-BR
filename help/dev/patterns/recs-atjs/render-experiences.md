---
title: Renderizar experiências
description: Verifique se todas as etapas necessárias para renderizar experiências foram executadas na sequência correta.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 7cf0c70b-a4bc-46f4-9b33-099bdb7dd9a9
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 4%

---

# Renderizar experiências

Siga as etapas do diagrama *Renderizar experiências* para garantir que todas as tarefas necessárias para renderizar experiências sejam executadas na sequência correta.

>[!NOTE]
>
>Se você tiver habilitado a Solicitação Automática de Carregamento de Página durante a [etapa Configurar a Solicitação Automática de Carregamento de Página](/help/dev/patterns/recs-atjs/initialize-sdk.md#automatic) em *Inicializar SDKS* , ignore esta atividade, a menos que queira chamar o Adobe Target SDK para renderizar experiências adicionais usando uma solicitação de local regional.

>[!TIP]
>
>Clique nas imagens neste tópico para expandir para tela inteira.

## Renderizar diagrama de experiências {#diagram}

O tratamento automático de cintilação pronto para uso disponível com a at.js só faz sentido quando o [!UICONTROL Automatic Page Load Request] está habilitado. Esta opção oculta todo o corpo do HTML ao buscar as experiências de [!DNL Target]. Nesse caso, é sua responsabilidade lidar com a cintilação. Procure por padrões de implementação disponíveis para tratamento de cintilação para obter orientação.

>[!NOTE]
>
>Os números de etapa na ilustração a seguir correspondem às seções abaixo. Os números de etapa não estão em uma ordem específica e não refletem a ordem das etapas realizadas na interface do usuário [!DNL Target] ao criar a atividade.

![Renderizar diagrama de experiências](/help/dev/patterns/recs-atjs/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

Clique nos links a seguir para navegar até as seções desejadas:

* [3.1: Promoção](#promotion)
* [3.2: Critérios baseados no carrinho](#cart)
* [3.3: Critérios baseados na popularidade](#popularity)
* [3.4: Critérios baseados em itens](#item)
* [3.5: Critérios baseados no usuário](#user)
* [3.6: Critérios personalizados](#custom)
* [3.7: Fornecer atributos usados nas regras de inclusão](#inclusion)
* [3.8: Fornecer excludedIds](#exclude)
* [3.9: Fornecer atributos de entidade para atualizar o catálogo de produtos do Recommendations](#entity-attributes)
* [3.10: Fornecer atributos de perfil usados como chaves para regras de inclusão](#keys)
* [3.11: Acionar solicitação de carregamento de página](#fire)
* [3.12: Acionar solicitação de localização regional](#location)

## 3.1: Promoção {#promotion}

Adicione itens promovidos e controle seu posicionamento no design de recomendações escolhendo promoções Frente ou Voltar na interface do usuário [!DNL Target] ao criar a atividade.

+++Ver detalhes

**Opções disponíveis**

* Promover por IDs
* [Promover por coleção](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promover por atributo](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Parâmetros de entidade necessários**

* Os atributos de item em promoções devem ser passados ao usar a opção &quot;promover por atributo&quot;.

**Leituras**

* [Adicionar promoções](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/adding-promotions.html){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.2: Critérios baseados no carrinho {#cart}

Faça recomendações com base no conteúdo do carrinho do usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**Parâmetros de entidade necessários**

* cartIds

**Leituras**

* [Baseado em carrinho](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.3: Critérios baseados na popularidade {#popularity}

Faça recomendações com base na popularidade geral de um item em todo o site ou na popularidade de itens na categoria, marca, gênero e assim por diante favoritas ou mais visualizadas de um visitante.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**Parâmetros de entidade necessários**

* `entity.categoryId` ou o atributo de item para popularidade com base no critério atual ou no atributo de item.
* Nada deve ser passado para Mais visualizados/Mais vendidos no site.

**Leituras**

* [Com base em popularidade](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.4: Critérios baseados em itens {#item}

Fazer recomendações com base na localização de itens semelhantes a um item que o usuário está visualizando ou que foi visualizado recentemente.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Parâmetros de entidade necessários**

* `entity.id`
* Se qualquer atributo de perfil for usado como uma chave

**Leituras**

* [Baseado em item](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.5: Critérios baseados no usuário {#user}

Faça recomendações com base no comportamento do usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**Parâmetros de entidade necessários**

* `entity.id`

**Leituras**

* [Baseado em usuário](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.6: Critérios personalizados {#custom}

Fazer recomendações com base em um arquivo personalizado que você carregou.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Custom algorithm]

**Parâmetros de entidade necessários**

`entity.id` ou o atributo usado como uma chave para o algoritmo personalizado

**Leituras**

* [Critérios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.7: Fornecer atributos usados nas regras de inclusão {#inclusion}

+++Ver detalhes

**Leituras**

* [Usar regras de inclusão estática e dinâmica](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.8: Fornecer excludedIds {#exclude}

Transmita IDs de entidade para entidades que você deseja excluir de suas recomendações. Por exemplo, você pode desejar excluir itens que já estão no carrinho de compras.

+++Ver detalhes

**Leituras**

* [Posso excluir dinamicamente uma entidade?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.9: Fornecer atributos de entidade para atualizar o catálogo de produtos para [!DNL Recommendations] {#entity-attributes}

+++Ver detalhes

**Leituras**

* [Atributos da entidade](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

Você também pode realizar esta etapa criando [feeds de produtos](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank} usando a interface do usuário [!DNL Target] para atualizar o catálogo de produtos para [!DNL Recommendations].

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.10: Fornecer atributos de perfil usados como chaves para regras de inclusão {#keys}

Forneça os atributos de perfil usados como chaves para as regras de inclusão em qualquer critério da Recommendations mencionado acima.

+++ Ver detalhes

**Leituras**

* [Atributos do perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.11: Acionar solicitação de carregamento de página {#fire}

Esta etapa aciona uma chamada [!DNL Delivery API] com carga `execute` > `pageLoad` na solicitação. O método `getOffers()` busca a experiência e `applyOffers()` renderiza a experiência na página. A solicitação `pageLoad` é necessária para renderizar experiências criadas no [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++Ver detalhes

![Acionar o diagrama de solicitação de carregamento de página](/help/dev/patterns/recs-atjs/assets/fire-page-load-request-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Todo o mapeamento de dados deve ser feito usando a função `targetPageParams`.

**Leituras**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Ações**

* Use os métodos `getOffers` e `applyOffers` para buscar a experiência usando uma chamada da API de solicitação de carregamento de página.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.12: Acionar solicitação de localização regional (#location)

Esta etapa aciona uma chamada [!DNL Delivery API] com carga `execute` > `mboxes` em sua solicitação. O método `getOffers` busca a experiência e `applyOffers` renderiza a experiência para a página. Você pode enviar mais de uma mbox na carga `execute` > `mboxes`.

+++Ver detalhes

![Acionar o diagrama de solicitação de localização regional](/help/dev/patterns/recs-atjs/assets/fire-regional-location-request-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Todo o mapeamento de dados deve ser feito usando a função `targetPageParams`.

**Leituras**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Ações**

* Use os métodos `getOffers` e `applyOffers` para buscar a experiência usando uma chamada da API de solicitação de carregamento de página.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

Vá para a Etapa 4: [Notificar Destino](/help/dev/patterns/recs-atjs/notify-target.md).
