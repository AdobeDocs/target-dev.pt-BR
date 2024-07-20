---
title: Configurar coleção de dados
description: Verifique se todas as tarefas necessárias para a coleta de dados foram executadas na sequência correta.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 66e0f18d-c78c-463b-8c47-132ef6332927
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# Configurar coleção de dados

Siga as etapas do diagrama *Coleta de Dados* para garantir que todas as tarefas necessárias para a coleta de dados sejam executadas na sequência correta.

>[!TIP]
>
>Clique nas imagens neste tópico para expandir para tela inteira.

A camada de dados fica pronta durante o carregamento da página ou a camada de dados muda após o carregamento da página.

Se você já tiver mapeado dados durante a [fase de inicialização do SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md), execute as etapas neste diagrama se:

* Sua camada de dados é aumentada de qualquer forma na mesma página e você deseja enviar esses dados adicionais para [!DNL Target]
* Você deseja enviar dados do catálogo de produtos para [!DNL Target Recommendations]

## Coletar diagrama de dados {#diagram}

Os números de etapa na ilustração a seguir correspondem às seções abaixo.

![Diagrama da Coleção de Dados](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Clique nos links a seguir para navegar até as seções desejadas:

* [2.1: Configurar mapeamento de dados](#configure)
* [2.2 Vínculo com atributos de entidade](#entity-attributes)
* [2.3 Acionar a API do Adobe Target Track](#fire-api)

## 2.1: Configurar mapeamento de dados {#configure}

Esta etapa ajuda a garantir que todos os dados que devem ser enviados para [!DNL Adobe Target] sejam definidos.

+++Ver detalhes

![Configurar o diagrama de mapeamento de dados](/help/dev/patterns/recs-atjs/assets/configure-data-mapping-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* A camada de dados deve estar pronta com todos os dados que devem ser enviados para [!DNL Target].

**Leituras**

[função targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Ações**

Use a função `targetPageParams()` para definir todos os dados necessários que devem ser enviados para [!DNL Target].

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 2.2: Link para atributos de entidade {#entity-attributes}

Link para atributos de entidade para atualizar o catálogo de produtos para [!DNL Target Recommendations].

+++Ver detalhes

**Leituras**

* [Atributos da entidade](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Considerações**

* Uma maneira alternativa de transmitir atributos de entidade é atualizar o catálogo de produtos na interface do usuário do [!DNL Target] para usar os [feeds de produtos do Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}.
* Transmitir atributos de entidade é aplicável somente em páginas em que os dados do catálogo de produtos estão disponíveis na camada de dados.
* Passar o parâmetro `entity.event.detailsOnly=true` em qualquer chamada tem prioridade.

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

## 2.3 Acionar a API do Adobe Target Track {#fire-api}

Esta etapa ajuda a garantir que todos os dados que devem ser enviados para [!DNL Target] sejam enviados.

+++Ver detalhes

![Acionar o diagrama da API do Adobe Target Track](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**Pré-requisitos**

* Todo o mapeamento de dados deve ter sido feito usando a [função targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Leituras**

* [método adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Ações**

Use o método [adobe.target.trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) para enviar todos os dados que devem ser enviados para [!DNL Target].

+++

[Retorne ao diagrama na parte superior desta página.](#diagram)

Prossiga para a Etapa 3: [Renderizar experiências](/help/dev/patterns/recs-atjs/render-experiences.md)
