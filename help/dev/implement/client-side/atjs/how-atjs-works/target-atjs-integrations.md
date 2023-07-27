---
keywords: integração da at.js, integrações suportadas, integrações não suportadas, integrações de terceiros
description: Consulte as integrações compatíveis (e não compatíveis) com o [!DNL Adobe Target] at.js, incluindo [!UICONTROL Analytics for Target] (A4T), o [!UICONTROL Serviço de ID Experience Cloud]e muito mais.
title: Quais integrações são compatíveis com a at.js?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 64%

---

# Integrações da at.js

Informações sobre integrações comuns com o [!DNL Adobe Target] e seu status de suporte com a at.js.

Se você tiver muita necessidade de uma integração que não seja compatível ou mencionada aqui, entre em contato com o representante ou consultor de conta.

## Integrações suportadas

| Integração | Detalhes |
|--- |--- |
| [!UICONTROL Analytics for Target] (A4T) | Consulte [Adobe Analytics como Fonte de relatórios do Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html). |
| [!UICONTROL Perfis e públicos-alvo] (P&amp;A) | Consulte [Públicos-alvo](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=pt-BR) no *Guia do Usuário dos Serviços principais*. |
| [!UICONTROL Serviço da Experience Cloud ID] | Consulte a [documentação de Serviço de ID da Adobe Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| [!UICONTROL Tags no Adobe Experience Platform] | [!UICONTROL Tags no Adobe Experience Platform] são os recursos de gerenciamento de tags de última geração da [!DNL Adobe]. [!UICONTROL As tags oferecem aos clientes uma forma simples de implantar e gerenciar as tags de análise, marketing e anúncios necessárias para potencializar experiências relevantes do cliente. ] Consulte [Implementar [!DNL Target] uso do Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md). |
| [!UICONTROL Adobe Experience Manager] Cloud Service (AEM) | A variável [!UICONTROL AEM Cloud Service] permite a criação de [!UICONTROL Teste A/B] e [!UICONTROL Direcionamento de experiência] atividades no fluxo de trabalho do AEM. Compatível com at.js com [!UICONTROL Adobe Experience Manager] 6.2 com FP-11577 (ou posterior). Para obter mais informações, consulte [Integração ao  [!DNL Adobe Target] e selecione a sua versão do AEM.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt_BR) |
| [!UICONTROL Fragmentos de experiência do AEM] | Fragmentos de experiência criados no AEM no [!DNL Target] As atividades do permitem combinar a facilidade de uso e o poder do AEM com recursos avançados de Inteligência automatizada (AI) e Aprendizado de Máquina (ML) no [!DNL Target] para testar e personalizar experiências em escala.  O AEM reúne todo o seu conteúdo e ativos em um local central para alimentar sua estratégia de personalização. O AEM permite que você crie conteúdo facilmente para desktops, tablets e dispositivos móveis em um único local sem escrever código. Não há necessidade de criar páginas para cada dispositivo. O AEM ajusta automaticamente cada experiência usando seu conteúdo.  Consulte [Fragmentos de experiência do AEM](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html). |

## Integrações não suportadas

| Integração | Detalhes |
|--- |--- |
| Herdados [!DNL Target] para [!DNL SiteCatalyst] Integração | Esta foi a integração que enviou ids de campanha e receita para [!DNL SiteCatalyst] por meio da chamada de página, para que seja possível fazer a comunicação na interface de usuário do [!DNL SiteCatalyst]. Esse recurso foi substituído por A4T. |
| Herdados [!DNL Target] para [!DNL SiteCatalyst] Integração | Essa era a integração que fazia chamadas de mbox denominadas `"SiteCatalyst: Event"` e `"SiteCatalyst: Purchase"`, portanto, era possível criar métricas de sucesso e perfis de usuário com base em evars e props. Esse recurso foi substituído por A4T e P&amp;A. |
| Herdados [!DNL Audience Manager] (AAM) para [!DNL Target] Integração | Essa foi a integração que fez uma chamada de API front-end para recuperar segmentos do AAM e, em seguida, os enviou como parâmetros mbox para todas as chamadas mbox da página. |

## Integrações de terceiros

| Integração | Detalhes |
|--- |--- |
| Outros gerenciadores de tags | A at.js deve funcionar com plataformas de gerenciamento de tags que não sejam da Adobe, mas tenha cuidado ao usar recursos de integração personalizados desenvolvidos por outros fornecedores. Suas integrações podem ser dependentes de funções da mbox.js que não existem mais na at.js. |
| Provedores de dados de terceiros (por exemplo, Demandbase, Bluekai, APIs de tempo) | Muitos provedores de dados de terceiros usados para complementar o perfil do usuário da Target podem ser integrados usando o recurso [Provedores de dados](../atjs-functions/targetglobalsettings.md#data-providers) da at.js. |
