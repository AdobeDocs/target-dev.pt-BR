---
title: Visão geral dos padrões de implementação
description: Entender como usar os padrões de implementação
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: c4b9dfed19e5e4a56bfeae26c4310b997a2d617e
workflow-type: tm+mt
source-wordcount: '145'
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

Cada parte é explicada em uma página separada neste guia. Por exemplo, a variável [!DNL Target] padrão de implementação contém as seguintes páginas:

* Inicializar SDK
* Enriquecer perfil
* Renderizar experiências
* Notificar [!DNL Target]

