---
title: Padrão de implementação do Recommendations usando at.js
description: Entenda como usar o padrão de implementação do Recommendations com a at.js
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
source-git-commit: 3b0bc0b67800ed4b1da6ba2bfa05c677147a78ba
workflow-type: tm+mt
source-wordcount: '151'
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
