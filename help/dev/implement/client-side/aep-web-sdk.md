---
keywords: Adobe Experience Platform Web SDK, aep web sdk, web sdk, sdk, adobe experience cloud, platform edge network, adobe experience platform edge network, edge network, aep edge network, Adobe Experience Platform Web SDK0
description: Saiba como usar o [!UICONTROL Adobe Experience Platform Web SDK] para interagir com os vários serviços na [!UICONTROL Adobe Experience Cloud] por meio da [!UICONTROL Rede de borda da AEP].
title: Como implementar o com a [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 13%

---

# [!UICONTROL SDK da Web da Adobe Experience Platform]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) é uma biblioteca JavaScript do lado do cliente que permite aos clientes da [!UICONTROL Adobe Experience Cloud] para interagir com os vários serviços na [!DNL Adobe Experience Cloud] (incluindo [!DNL Target]) por meio da [!UICONTROL Rede de borda Adobe Experience Platform]. Além da biblioteca do JavaScript, há uma [!UICONTROL Adobe Experience Platform] para ajudar nas configurações do SDK da Web.

Para obter mais informações, consulte os seguintes links na *[!UICONTROL Adobe Experience Platform Web SDK]* ajuda:

* Para obter informações abrangentes: [O que é o [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
* Para obter informações específicas sobre [!DNL Target]: [[!DNL Target] Visão geral](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=pt-BR)

## Tutoriais

Os seguintes tutoriais ajudam na implementação do:

### Implementar [!DNL Adobe Experience Cloud] com [!DNL Platform Web SDK]

Saiba como implementar o [!DNL Experience Cloud] aplicativos usando [!DNL Adobe Experience Platform Web SDK] com [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR). Para obter informações específicas sobre [!DNL Target], consulte a seção tutorial intitulada [Configurar [!DNL Target] com o SDK da Web da Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migrar [!DNL Target] da at.js 2.*x* para [!DNL Platform Web SDK]

Saiba como migrar o [!DNL Target] implementação da at.js 2.*x* para o [!DNL Adobe Experience Platform Web SDK] com [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=pt-BR).

## Documentação recomendada

Além do [!UICONTROL SDK da Web da Platform] documentação mencionada acima, os tópicos deste guia também têm informações específicas para a [!UICONTROL SDK da Web da Platform] no que diz respeito a [!DNL Target] recursos e funcionalidade.

| Recurso | Descrição/Link |
| --- | --- |
| [Controle de qualidade da atividade](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Usar URLs de controle de qualidade no [!DNL Target] para realizar o controle de qualidade das atividades com facilidade utilizando links de visualização que nunca mudam, direcionamento opcional de público-alvo e relatórios de controle de qualidade que permanecem segmentados a partir dos dados de atividade em tempo real. O controle de qualidade da atividade permite que você teste completamente seu [!DNL Target] atividades antes de iniciá-las em tempo real.<p>Consulte [Compatibilidade da biblioteca JavaScript do Target Modo de QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) e [Visualizar URLs](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [Analytics for Target (A4T) ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics para Target] O (A4T) é uma integração entre soluções que permite criar atividades com base no [!DNL Analytics] métricas de conversão e segmentos de público-alvo. A integração A4T permite que você use os relatórios do Analytics para examinar os resultados.<p>Consulte [Tipos de atividades compatíveis](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) e [Etapas de implementação para uma implementação do SDK da Web da Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Públicos-alvo em [!DNL Target] determine quem vê o conteúdo e as experiências em uma atividade direcionada.<p>Consulte [Usar a lista de Públicos](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) e [Combinar vários públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Criar públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=pt-BR) | O uso de públicos criados na [!DNL Adobe Experience Platform] fornece dados mais avançados do cliente, o que resulta em personalizações mais impactantes.<p>Consulte [Usar públicos do Adobe Experience Platform](https://experienceleague.adobe.com/docs/?lang=pt-BRtarget/using/audiences/create-audiences/audiences.html#aep). |
| [Decisões de oferta](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Adicionar decisões de oferta criadas em [!DNL Adobe Journey Optimizer] para [!DNL Target] atividades de (teste A/B manual ou direcionamento de experiência) para determinar e fornecer a próxima melhor oferta para seus visitantes na Web e em dispositivos móveis. |
| [Ofertas de redirecionamento - Perguntas frequentes sobre o A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | As ofertas de redirecionamento fazem com que os navegadores dos visitantes redirecionem para uma nova página.<p>Consulte [O faz [!UICONTROL Adobe Experience Platform Web SDK] oferecer suporte às ofertas de redirecionamento para A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Os tokens de resposta permitem enviar [!DNL Target] dados para Google Analytics e outras integrações de terceiros.<p>Consulte [Envio de dados para o Google Analytics por meio do SDK da Web da plataforma](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) para ver uma amostra de código de como realizar essa tarefa. |
| [Implementação de aplicativos de página única](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) no *[!UICONTROL SDK da Web da Platform] visão geral* guia. | [!UICONTROL Adobe Experience Platform Web SDK] O fornece recursos avançados para sua empresa personalizar tecnologias de próxima geração no lado do cliente, como aplicativos de página única (SPA). |
| [Alterações na criptografia do TLS (Transport Layer Security)](../../before-implement/tls-transport-layer-security-encryption.md) | O TLS (Transport Layer Security) ajuda você a manter os mais altos padrões de segurança e a promover a segurança dos dados do cliente. |
