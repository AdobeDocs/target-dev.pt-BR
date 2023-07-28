---
title: Renderizar experiências
description: Verifique se todas as etapas necessárias para renderizar experiências foram executadas na sequência correta.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 9b65380febf64896a3885c49f8bb79e4bb33f604
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 5%

---

# Renderizar experiências

Siga as etapas na guia *Renderizar experiências* diagrama para garantir que todas as tarefas necessárias para renderizar experiências sejam executadas na sequência correta.

>[!TIP]
>
>Clique nas imagens neste tópico para expandir para tela inteira.

## Renderizar diagrama de experiências {#diagram}

O tratamento automático de cintilação pronto para uso disponível com a at.js só faz sentido quando você [!UICONTROL Solicitação automática de carregamento de página] ativado. Essa opção oculta todo o corpo do HTML enquanto busca as experiências do [!DNL Target]. Nesse caso, é sua responsabilidade lidar com a cintilação. Procure por padrões de implementação disponíveis para tratamento de cintilação para obter orientação.

Os números de etapa na ilustração a seguir correspondem às seções abaixo.

![Renderizar diagrama de experiências](/help/dev/patterns/assets/diagram-render-experiences.png){width="600" zoomable="yes"}

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

Adicionar itens promovidos e controlar seu posicionamento no Recommendations do Target [designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Ver detalhes

**Opções disponíveis**

* Promover por IDs
* [Promover por coleção](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Promover por atributo](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Parâmetros de entidade obrigatórios**

* O atributo de item em promoções deve ser transmitido ao usar a opção &quot;promover por atributo&quot;.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.2: Critérios baseados no carrinho {#cart}

Faça recomendações com base no conteúdo do carrinho do usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Pessoas que visualizaram isto, visualizaram aquilo]
* [!UICONTROL Pessoas que visualizaram e compraram essas]
* [!UICONTROL Pessoas que compraram isto, compraram aquilo]

**Parâmetros de entidade obrigatórios**

* cartIds

**Leituras**

* [Baseado em carrinho](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.3: Critérios baseados na popularidade {#popularity}

Faça recomendações com base na popularidade geral de um item em todo o site ou na popularidade de itens na categoria, marca, gênero e assim por diante favoritas ou mais visualizadas de um usuário.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Mais visualizados no site]
* [!UICONTROL Mais visualizados por categoria]
* [!UICONTROL Mais visualizados pelo atributo de item]
* [!UICONTROL Mais vendidos em todo o site]
* [!UICONTROL Mais vendidos por categoria]
* [!UICONTROL Mais Vendidos por Atributo de Item]
* [!UICONTROL Comece pela métrica do Analytics]

**Parâmetros de entidade obrigatórios**

* `entity.categoryId` ou o atributo de item para popularidade com base no critério do atributo atual ou do item.
* Nada deve ser passado para Mais visualizados/Principais vendidos no site.

**Leituras**

* [Baseado em popularidade](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.4: Critérios baseados em itens {#item}

Fazer recomendações com base na localização de itens semelhantes a um item que o usuário está visualizando ou que foi visualizado recentemente.

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Pessoas que visualizaram isto, visualizaram aquilo]
* [!UICONTROL Pessoas que visualizaram isto, compraram aquilo]
* [!UICONTROL Pessoas que compraram isto, compraram aquilo]
* [!UICONTROL Itens com atributos similares]

**Parâmetros de entidade obrigatórios**

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

* [!UICONTROL Itens visualizados recentemente ]
* [!UICONTROL Recomendado para você]

**Parâmetros de entidade obrigatórios**

* `entity.id`

**Leituras**

* [Baseado em usuário](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.6: Critérios personalizados {#custom}

Fazer recomendações com base em um arquivo personalizado que você carregou

+++Ver detalhes

**Critérios disponíveis**

* [!UICONTROL Algoritmo personalizado]

**Parâmetros de entidade obrigatórios**

`entity.id` ou o atributo usado como uma chave para o algoritmo personalizado

**Leituras**

* [Critérios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.7: Fornecer atributos usados nas regras de inclusão {#inclusion}

+++Ver detalhes

**Leituras**

* [Uso das regras de inclusão estática e dinâmica](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.8: Fornecer excludedIds {#exclude}

Transmita IDs de entidade para entidades que você deseja excluir de suas recomendações. Por exemplo, você pode desejar excluir itens que já estão no carrinho de compras.

+++Ver detalhes

**Leituras**

* [Posso excluir dinamicamente uma entidade?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.9: Fornecer atributos de entidade para atualizar o catálogo de produtos do [!DNL Recommendations] {#entity-attributes}

+++Ver detalhes

**Leituras**

* [Atributos da entidade](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

Também é possível realizar essa etapa criando feeds de produto usando o [!DNL Target] Interface para atualizar o catálogo de produtos para [!DNL Recommendations].

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

Essa etapa aciona um [!DNL Delivery API] chamar com `execute` > `pageLoad` carga na solicitação. A variável `getOffers()` O método busca a experiência e `applyOffers()` renderiza a experiência na página. A solicitação pageLoad é necessária para renderizar experiências criadas no [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++Ver detalhes

![Acionar diagrama de solicitação de carregamento de página](/help/dev/patterns/assets/fire-page-load-request.png){width="100" zoomable="yes"}

**Pré-requisitos**

* Todo o mapeamento de dados deve ser feito usando o `targetPageParams` função.

**Leituras**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Ações**

* Use o `getOffers` e `applyOffers` métodos para buscar a experiência do usando uma chamada da API Solicitação de carregamento de página.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 3.12: Acionar solicitação de localização regional (#location)

Essa etapa aciona um [!DNL Delivery API] chamar com `execute` > `mboxes` carga útil na sua solicitação. A variável `getOffers` O método busca a experiência e `applyOffers` renderiza a experiência para a página. Você pode enviar mais de uma mbox no `execute` > `mboxes` carga útil.

+++Ver detalhes

![Acionar diagrama de solicitação de localização regional](/help/dev/patterns/assets/fire-regional-location-request.png){width="100" zoomable="yes"}

**Pré-requisitos**

* Todo o mapeamento de dados deve ser feito usando o `targetPageParams` função.

**Leituras**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Ações**

* Use o `getOffers` e `applyOffers` métodos para buscar a experiência do usando uma chamada da API Solicitação de carregamento de página.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)