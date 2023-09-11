---
title: Visão geral dos padrões de implementação
description: Entender como usar os padrões de implementação
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 7a79eb1d263cf42529a5a1b1ca1f9de4db218a49
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Visão geral dos padrões de implementação

[!DNL Adobe Target] Os padrões de implementação do ajudam você a entender e criar a seguinte arquitetura para seus [!DNL Target] execução.

Clique na imagem para expandir para tela inteira.

![Diagrama da arquitetura do Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Observe que os números na imagem não indicam a sequência de operações:

1. SDKs do lado do cliente para [!DNL Adobe Target] e [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] chamar
1. Chamada de aquisição ECID
1. API de atualização de perfil em massa e [!DNL Customer Attributes] (CA) serviço
1. Assimilação de dados do perfil das fontes de dados do cliente para [!DNL Target] loja de perfis
1. Coleta de dados de perfil/comportamentais e decisão sobre qual experiência mostrar ao usuário final
1. As experiências são renderizadas na página
1. O at.js renderiza as experiências na página

Cada padrão consiste em diferentes partes. Cada parte corresponde a um requisito crítico de implementação para sua [!DNL Target] execução.

Cada parte é explicada em uma página separada neste guia. Por exemplo, a variável [[!DNL Recommendations] padrão de implementação usando at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md) contém as seguintes páginas:

* Inicializar SDK
* Configurar coleção de dados
* Renderizar experiências
* Notificar [!DNL Target]

