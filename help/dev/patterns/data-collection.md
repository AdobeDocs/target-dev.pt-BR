---
title: Configurar coleção de dados
description: Verifique se todas as tarefas necessárias para a coleta de dados foram executadas na sequência correta.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 83bb88b48cd1485fdffbc67b38da09c6209b823a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---

# Configurar coleção de dados

Siga as etapas na guia *Coleta de dados* diagrama para garantir que todas as tarefas necessárias para a coleta de dados sejam executadas na sequência correta.

>[!TIP]
>
>Clique nas imagens neste tópico para expandir para tela inteira.

A camada de dados fica pronta durante o carregamento da página ou a camada de dados muda após o carregamento da página.

Se você já tiver mapeado os dados durante o [inicializar fase do SDK](/help/dev/patterns/initialize-sdk.md), você deve executar as etapas neste diagrama se:

* Sua camada de dados é aumentada de qualquer forma na mesma página e você deseja enviar esses dados adicionais para o [!DNL Target]
* Você deseja enviar dados do catálogo de produtos para [!DNL Target Recommendations]

## Coletar diagrama de dados {#diagram}

Os números de etapa na ilustração a seguir correspondem às seções abaixo.

![Diagrama da coleção de dados](/help/dev/patterns/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Clique nos links a seguir para navegar até as seções desejadas:

* [2.1: Configurar mapeamento de dados](#configure)
* [2.2 Vínculo com atributos de entidade](#entity-attributes)
* [2.3 Acionar a API do Adobe Target Track](#fire-api)

## 2.1: Configurar mapeamento de dados {#configure}

Essa etapa ajuda a garantir que todos os dados que devem ser enviados para o [!DNL Adobe Target] está definido.

+++Ver detalhes

![Configurar diagrama de mapeamento de dados](/help/dev/patterns/assets/cofigure-data-mapping.png){width="100" zoomable="yes"}

**Pré-requisitos**

* A camada de dados deve estar pronta com todos os dados que devem ser enviados para o [!DNL Target].

**Leituras**

[função targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Ações**

Use o `targetPageParams()` para definir todos os dados necessários que devem ser enviados para o [!DNL Target].

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 2.2: Link para atributos de entidade {#entity-attributes}

Link para atributos de entidade para os quais atualizar o catálogo de produtos [!DNL Target Recommendations].

+++Ver detalhes

**Leituras**

* [Atributos da entidade](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Considerações**

* Uma maneira alternativa de enviar atributos de entidade é atualizar o catálogo de produtos no [!DNL Target] Interface a ser usada [Feeds de produto do Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}.
* Transmitir atributos de entidade é aplicável somente em páginas em que os dados do catálogo de produtos estão disponíveis na camada de dados.
* Passar o `entity.event.detailsOnly=true` em qualquer chamada tem prioridade.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 2.3 Acionar a API do Adobe Target Track {#fire-api}

Essa etapa ajuda a garantir que todos os dados que devem ser enviados para o [!DNL Target] é enviado.

+++Ver detalhes

![Acionar diagrama da API de rastreamento do Adobe Target](/help/dev/patterns/assets/fire-track-api.png){width="100" zoomable="yes"}

**Pré-requisitos**

* Todo o mapeamento de dados deve ter sido feito usando o [função targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Leituras**

* [método adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Ações**

Uso [método adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) para enviar todos os dados que devem ser enviados ao [!DNL Target].

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

