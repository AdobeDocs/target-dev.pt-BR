---
title: Padrão de implementação do Recommendations usando at.js
description: Entenda como usar o padrão de implementação do Recommendations com a at.js
feature: APIs/SDKs
level: Experienced
role: Developer
source-git-commit: 723bb2f33a011995757009193ee9c48757ae1213
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# [!DNL Recommendations] padrão de implementação usando a visão geral da at.js

Esse padrão de implementação ajuda você a entender e criar seus [!DNL Adobe Target Recommendations] implementação ao usar o [Biblioteca JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

Clique na imagem para expandir para tela inteira.

![Diagrama da arquitetura do Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Observe que os números na imagem não indicam a sequência de operações:

1. SDKs do lado do cliente para [!DNL Adobe Target] e [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] chamar
1. [!UICONTROL ID do Experience Cloud] Chamada de aquisição de (ECID)
1. API de atualização de perfil em massa e [!DNL Customer Attributes] (CA) serviço
1. Assimilação de dados do perfil das fontes de dados do cliente para [!DNL Target] loja de perfis
1. Coletar dados de perfil e comportamentais e decidir qual experiência mostrar ao visitante
1. As experiências são renderizadas na página
1. O at.js renderiza as experiências na página

Cada padrão consiste em diferentes partes, com cada parte correspondendo a um requisito crítico de implementação para o [!DNL Target] execução.

Cada parte é explicada em um artigo separado neste guia:

* [Inicializar SDKS](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Configurar coleção de dados](/help/dev/patterns/recs-atjs/data-collection.md)
* [Renderizar experiências](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Notificar Destino](/help/dev/patterns/recs-atjs/notify-target.md)

