---
keywords: Adobe Experience Platform Web SDK, sdk da web da aep, sdk da web, sdk, adobe experience cloud, rede de borda da plataforma, rede de borda da adobe experience platform, rede de borda, rede de borda da aep, Adobe Experience Platform Web SDK0
description: Saiba como usar o [!UICONTROL Adobe Experience Platform Web SDK] para interagir com os vários serviços no [!UICONTROL Adobe Experience Cloud] por meio do [!UICONTROL AEP Edge Network].
title: Como implementar o com o [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: ac03d5d15875ab4945b07b3e95037ce9ecde1044
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 8%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

O [!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) é uma biblioteca JavaScript do lado do cliente que permite aos clientes do [!UICONTROL Adobe Experience Cloud] interagir com os vários serviços no [!DNL Adobe Experience Cloud] (incluindo o [!DNL Target]) até o [!UICONTROL Adobe Experience Platform Edge Network]. Além da biblioteca do JavaScript, há uma extensão [!UICONTROL Adobe Experience Platform] para ajudar nas configurações do Web SDK.

Para obter mais informações, consulte os seguintes links na ajuda do *[!UICONTROL Adobe Experience Platform Web SDK]*:

* Para obter informações abrangentes: [O que é [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
* Para obter informações específicas sobre [!DNL Target]: [[!DNL Target] Visão geral](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=pt-BR)

## Tutoriais

Os seguintes tutoriais ajudam na implementação do:

### Implementar [!DNL Adobe Experience Cloud] com [!DNL Platform Web SDK]

Saiba como implementar aplicativos do [!DNL Experience Cloud] usando o [!DNL Adobe Experience Platform Web SDK] com [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR). Para obter informações específicas do [!DNL Target], consulte a seção de tutorial intitulada [Configurar [!DNL Target] com o Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migrar [!DNL Target] da at.js 2.*x* para [!DNL Platform Web SDK]

Saiba como migrar a implementação do [!DNL Target] da at.js 2.*x* para o [!DNL Adobe Experience Platform Web SDK] com [este tutorial](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=pt-BR).

## Documentação recomendada

Além da documentação do [!UICONTROL Platform Web SDK] mencionada acima, os tópicos deste guia também têm informações específicas do [!UICONTROL Platform Web SDK], pois ele se relaciona aos recursos e funcionalidades do [!DNL Target].

| Recurso | Descrição/Link |
| --- | --- |
| [Controle de qualidade da atividade](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Use as URLs de controle de qualidade no [!DNL Target] para realizar o controle de qualidade das atividades com facilidade utilizando links de visualização que nunca mudam, direcionamento opcional de público-alvo e relatórios de controle de qualidade que permanecem segmentados a partir dos dados de atividade em tempo real. O Controle de qualidade da atividade permite que você teste completamente suas atividades do [!DNL Target] antes de inicializá-las.<p>Consulte [Compatibilidade da biblioteca JavaScript do Target Modo de QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) e [URLs de visualização](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | O [!UICONTROL Adobe Analytics for Target] (A4T) é uma integração entre soluções que permite criar atividades com base nas métricas de conversão e nos segmentos de público-alvo do [!DNL Analytics]. A integração A4T permite que você use os relatórios do Analytics para examinar os resultados.<p>Consulte [Tipos de atividades com suporte](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) e [Etapas de implementação para uma implementação do Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Os públicos-alvo em [!DNL Target] determinam quem vê o conteúdo e as experiências em uma atividade direcionada.<p>Consulte [Usar a lista de Públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) e [Combinar vários públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Criar públicos-alvo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=pt-BR) | O uso de públicos-alvo criados no [!DNL Adobe Experience Platform] fornece dados mais avançados do cliente, o que resulta em personalizações mais impactantes.<p>Consulte [Usar públicos-alvo da Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep). |
| [Decisões de oferta](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Adicione decisões de oferta criadas em [!DNL Adobe Journey Optimizer] às atividades de [!DNL Target] (Teste A/B manual ou Direcionamento de experiência) para determinar e entregar a próxima melhor oferta para seus visitantes na Web e em dispositivos móveis. |
| [Ofertas de redirecionamento - Perguntas frequentes sobre o A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | As ofertas de redirecionamento fazem com que os navegadores dos visitantes redirecionem para uma nova página.<p>Consulte [O [!UICONTROL Adobe Experience Platform Web SDK] oferece suporte às ofertas de redirecionamento para o A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Os tokens de resposta permitem enviar dados do [!DNL Target] para a Google Analytics e outras integrações de terceiros.<p>Consulte [Enviando dados para a Google Analytics via Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) para ver uma amostra de código de como realizar essa tarefa. |
| [Implementação do aplicativo de página única](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) no guia *[!UICONTROL Platform Web SDK]de visão geral*. | O [!UICONTROL Adobe Experience Platform Web SDK] fornece recursos avançados para sua empresa personalizar tecnologias de próxima geração no lado do cliente, como aplicativos de página única (SPAs). |
| [Alterações na criptografia do TLS (Transport Layer Security)](/help/dev/before-implement/tls-transport-layer-security-encryption.md) | O TLS (Transport Layer Security) ajuda você a manter os mais altos padrões de segurança e a promover a segurança dos dados do cliente. |
