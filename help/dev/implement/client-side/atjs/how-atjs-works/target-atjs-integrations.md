---
keywords: integração da at.js, integrações suportadas, integrações não suportadas, integrações de terceiros
description: Consulte as integrações compatíveis (e não compatíveis) com o  [!DNL Adobe Target] at.js, incluindo o [!UICONTROL Analytics for Target] (A4T), o [!UICONTROL Serviço da Experience Cloud ID] e muito mais.
title: Quais integrações são compatíveis com a at.js?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
TQID: https://experienceleague.adobe.com/RdcxcIGufo2O5aKPqIAJVINkCzZ1Brcv8EXiX1n4buc
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: df62f171-ac37-440f-8f0f-f41a72ebdd34id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e6ff21d3-dec6-4298-8590-7c749fffaf78id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 530
ht-degree: 54%

---

# Integrações da at.js

Informações sobre integrações comuns com o [!DNL Adobe Target] e seu status de suporte com a at.js.

Se você tiver muita necessidade de uma integração que não seja compatível ou mencionada aqui, entre em contato com o representante ou consultor de conta.

## Integrações suportadas

| Integração | Detalhes |
|--- |--- |
| [!UICONTROL Analytics for Target] (A4T) | Consulte [Adobe Analytics como fonte de relatórios da funcionalidade do Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html). |
| [!UICONTROL Perfis e públicos-alvo] (P&amp;A) | Consulte [Públicos-alvo](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=pt-BR) no *Guia do Usuário dos Serviços Principais*. |
| [!UICONTROL Serviço da Experience Cloud ID] | Consulte a [documentação de Serviço de ID da Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| [!UICONTROL Marcas no Adobe Experience Platform] | [!UICONTROL As marcas no Adobe Experience Platform] são a próxima geração de recursos de gerenciamento de marcas do [!DNL Adobe]. As [!UICONTROL Tags] oferecem aos clientes uma forma simples de implantar e gerenciar as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. Consulte [Implementar [!DNL Target] usando o Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md). |
| [!UICONTROL Adobe Experience Manager] (AEM) Cloud Service | O [!UICONTROL AEM Cloud Service] habilita a criação de [!UICONTROL atividades de Teste A/B] e [!UICONTROL Direcionamento de experiência] dentro do fluxo de trabalho do AEM. Compatível com at.js com [!UICONTROL Adobe Experience Manager] 6.2 com FP-11577 (ou posterior). Para obter mais informações, consulte [Integração com [!DNL Adobe Target]](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt_BR) e selecione sua versão do AEM. |
| [!UICONTROL Fragmentos de experiência do AEM] | Os fragmentos de experiência criados no AEM nas atividades do [!DNL Target] permitem combinar a facilidade de uso e o poder do AEM com os poderosos recursos de Inteligência automatizada (AI) e Aprendizado de Máquina (ML) no [!DNL Target] para testar e personalizar experiências em escala.  O AEM reúne todo o seu conteúdo e ativos em um local central para alimentar sua estratégia de personalização. O AEM permite que você crie conteúdo facilmente para desktops, tablets e dispositivos móveis em um único local sem escrever código. Não há necessidade de criar páginas para cada dispositivo. O AEM ajusta automaticamente cada experiência usando seu conteúdo.  Consulte [Fragmentos de experiência do AEM](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html). |

## Integrações não suportadas

| Integração | Detalhes |
|--- |--- |
| Integração herdada de [!DNL Target] a [!DNL SiteCatalyst] | Esta foi a integração que enviou ids de campanha e receita para [!DNL SiteCatalyst] por meio da chamada de página, para que seja possível fazer a comunicação na interface de usuário do [!DNL SiteCatalyst]. Esse recurso foi substituído por A4T. |
| Integração herdada de [!DNL Target] a [!DNL SiteCatalyst] | Essa era a integração que fazia chamadas de mbox denominadas `"SiteCatalyst: Event"` e `"SiteCatalyst: Purchase"`, portanto, era possível criar métricas de sucesso e perfis de usuário com base em evars e props. Esse recurso foi substituído por A4T e P&amp;A. |
| Integração herdada de [!DNL Audience Manager] (AAM) a [!DNL Target] | Essa foi a integração que fez uma chamada de API front-end para recuperar segmentos do AAM e, em seguida, os enviou como parâmetros mbox para todas as chamadas mbox da página. |

## Integrações de terceiros

| Integração | Detalhes |
|--- |--- |
| Outros gerenciadores de tags | A at.js deve funcionar com plataformas de gerenciamento de tags que não sejam da Adobe, mas tenha cuidado ao usar recursos de integração personalizados desenvolvidos por outros fornecedores. Suas integrações podem ser dependentes de funções da mbox.js que não existem mais na at.js. |
| Provedores de dados de terceiros (por exemplo, Demandbase, Bluekai, APIs de tempo) | Muitos provedores de dados de terceiros usados para complementar o perfil do usuário da Target podem ser integrados usando o recurso [Provedores de dados](../atjs-functions/targetglobalsettings.md#data-providers) da at.js. |
