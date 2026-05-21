---
title: Padrão de implementação do Recommendations usando at.js
description: Entenda como usar o padrão de implementação do Recommendations com a at.js
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
TQID: https://experienceleague.adobe.com/uYNa5mL-8ffPS-ddjnQzILnPFMbjNJqKZDmQT8qFeGA
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
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 152
ht-degree: 0%

---

# Visão geral do padrão de implementação [!DNL Recommendations] usando at.js

Este padrão de implementação ajuda você a entender e criar sua implementação do [!DNL Adobe Target Recommendations] ao usar a [biblioteca at.js de JavaScript](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md).

Clique na imagem para expandir para tela inteira.

![Diagrama de arquitetura do Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Observe que os números na imagem não indicam a sequência de operações:

1. SDKs do lado cliente para [!DNL Adobe Target] e [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] chamada
1. Chamada de aquisição de [!UICONTROL Experience Cloud ID] (ECID)
1. API de atualização de perfil em massa e serviço de autoridade de certificação (CA) [!DNL Customer Attributes]
1. Assimilação de dados de perfil das fontes de dados do cliente para [!DNL Target] armazenamento de perfil
1. Coletar dados de perfil e comportamentais e decidir qual experiência mostrar ao visitante
1. As experiências são renderizadas na página
1. O at.js renderiza as experiências na página

Cada padrão consiste em diferentes partes, com cada parte correspondendo a um requisito de implementação crítico para sua implementação [!DNL Target].

Cada parte é explicada em um artigo separado neste guia:

* [Inicializar SDKS](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Configurar coleção de dados](/help/dev/patterns/recs-atjs/data-collection.md)
* [Renderizar experiências](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Notificar Destino](/help/dev/patterns/recs-atjs/notify-target.md)
