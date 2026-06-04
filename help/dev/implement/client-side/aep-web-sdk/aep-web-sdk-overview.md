---
keywords: Adobe Experience Platform Web SDK, sdk da web da aep, sdk da web, sdk, adobe experience cloud, rede de borda da plataforma, rede de borda da adobe experience platform, rede de borda, rede de borda da aep, Adobe Experience Platform Web SDK0
description: Saiba como usar a [!UICONTROL Adobe Experience Platform Web SDK] para interagir com os vários serviços na [!UICONTROL Adobe Experience Cloud] por meio da [!UICONTROL AEP Edge Network].
title: Como implementar o com a [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
TQID: https://experienceleague.adobe.com/j3-KSuCkcyyTB2KG4Icm2E7xpAfcuPkaOlhxitd5q-4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 786
ht-degree: 9%

---

# [!UICONTROL SDK da Web da Adobe Experience Platform]

A [!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) é uma biblioteca JavaScript no lado do cliente que permite aos clientes da [!UICONTROL Adobe Experience Cloud] interagir com os vários serviços no [!DNL Adobe Experience Cloud] (incluindo o [!DNL Target]) por meio da [!UICONTROL Adobe Experience Platform Edge Network]. Além da biblioteca JavaScript, há uma extensão [!UICONTROL Adobe Experience Platform] para ajudar nas configurações do Web SDK.

Para obter mais informações, consulte os seguintes links na ajuda do *[!UICONTROL Adobe Experience Platform Web SDK]*:

* Para obter informações abrangentes: [O que é a [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
* Para obter informações específicas sobre [!DNL Target]: [[!DNL Target] Visão geral](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=pt-BR)

## Tutoriais

Os seguintes tutoriais ajudam na implementação do:

### Implementar [!DNL Adobe Experience Cloud] com [!DNL Platform Web SDK]

Saiba como implementar aplicativos do [!DNL Experience Cloud] usando o [!DNL Adobe Experience Platform Web SDK] com [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR). Para obter informações específicas do [!DNL Target], consulte a seção de tutorial intitulada [Configurar [!DNL Target] com o Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migrar [!DNL Target] da at.js 2.*x* para [!DNL Platform Web SDK]

Saiba como migrar sua implementação do [!DNL Target] da at.js 2.*x* para o [!DNL Adobe Experience Platform Web SDK] com [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=pt-BR).

## Documentação recomendada

Além da documentação do [!UICONTROL Platform Web SDK] mencionada acima, os tópicos deste guia também contêm informações específicas do [!UICONTROL Platform Web SDK], pois ele se relaciona aos recursos e funcionalidades do [!DNL Target].

| Recurso | Descrição/Link |
| --- | --- |
| [Controle de qualidade da atividade](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Use as URLs de controle de qualidade no [!DNL Target] para realizar o controle de qualidade das atividades com facilidade utilizando links de visualização que nunca mudam, direcionamento opcional de público-alvo e relatórios de controle de qualidade que permanecem segmentados a partir dos dados de atividade em tempo real. O Controle de qualidade da atividade permite que você teste completamente suas atividades do [!DNL Target] antes de inicializá-las.<p>Consulte [Compatibilidade da biblioteca JavaScript do Target Modo de QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) e [URLs de visualização](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics para Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | O [!UICONTROL Adobe Analytics for Target] (A4T) é uma integração entre soluções que permite criar atividades com base em [!DNL Analytics] métricas de conversão e segmentos de público-alvo. A integração A4T permite que você use os relatórios do Analytics para examinar os resultados.<p>Consulte [Tipos de atividades com suporte](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) e [Etapas de implementação para uma implementação do Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Os públicos-alvo em [!DNL Target] determinam quem vê o conteúdo e as experiências em uma atividade direcionada.<p>Consulte [Usar a lista de Públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) e [Combinar vários públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Criar públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=pt-BR) | O uso de públicos-alvo criados no [!DNL Adobe Experience Platform] fornece dados mais avançados do cliente, o que resulta em personalizações mais impactantes.<p>Consulte [Usar públicos-alvo da Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep). |
| [Decisões de oferta](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Adicione decisões de oferta criadas em [!DNL Adobe Journey Optimizer] às atividades de [!DNL Target] (Teste A/B manual ou Direcionamento de experiência) para determinar e entregar a próxima melhor oferta para seus visitantes na Web e em dispositivos móveis. |
| [Ofertas de redirecionamento - Perguntas frequentes sobre o A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | As ofertas de redirecionamento fazem com que os navegadores dos visitantes redirecionem para uma nova página.<p>Consulte [O [!UICONTROL Adobe Experience Platform Web SDK] oferece suporte a ofertas de redirecionamento para o A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Os tokens de resposta permitem enviar dados do [!DNL Target] para a Google Analytics e outras integrações de terceiros.<p>Consulte [Enviando dados para a Google Analytics via Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) para ver uma amostra de código de como realizar essa tarefa. |
| [Implementação do aplicativo de página única](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) no guia de *[!UICONTROL visão geral] do Platform Web SDK*. | O [!UICONTROL Adobe Experience Platform Web SDK] fornece recursos avançados que fazem com que sua empresa execute personalização em tecnologias de próxima geração no lado do cliente, como aplicativos de página única (SPAs). |
| [Alterações na criptografia do TLS (Transport Layer Security)](/help/dev/before-implement/tls-transport-layer-security-encryption.md) | O TLS (Transport Layer Security) ajuda você a manter os mais altos padrões de segurança e a promover a segurança dos dados do cliente. |
