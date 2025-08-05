---
user-guide-title: Guia do desenvolvedor do Adobe Target
breadcrumb-title: Guia do desenvolvedor do Target
user-guide-description: Saiba como definir e personalizar a experiência de seus clientes para que você possa maximizar a receita em sites da Web e móveis, aplicativos, mídia social e outros canais digitais.
source-git-commit: ac13e0dd7f67de50b77778921c90a95f12c2b9e4
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 44%

---


# Guia do desenvolvedor do Adobe Target {#developer}

+ [Guia do desenvolvedor do Adobe Target](overview.md)
+ Introdução {#implementation}
   + Antes da implementação {#before-implement}
      + [Antes da implementação](before-implement/considerations-before-you-implement-target.md)
      + [Preparação para implementar o Target](before-implement/prepare-to-implement-target.md)
   + Privacidade e segurança {#privacy}
      + [Visão geral de privacidade](before-implement/privacy/privacy.md)
      + [Privacidade e regulamentos sobre proteção de dados](before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)
      + [Cookies do Target](before-implement/privacy/cookie-behavior.md)
      + [Excluir o cookie do Target](before-implement/privacy/cookie-deleting.md)
      + [O impacto da descontinuação de cookies de terceiros no Target (at.js)](/help/dev/before-implement/privacy/third-party-cookie-deprecation.md)
      + [Políticas de cookies do Google Chrome para SameSite](before-implement/privacy/google-chrome-samesite-cookie-policies.md)
      + [Apple Intelligent Tracking Prevention (ITP) 2.x](before-implement/privacy/apple-itp-2x.md)
      + [Diretivas da Política de segurança de conteúdo (CSP)](before-implement/privacy/content-security-policy.md)
      + [Lista de permissões de nós de borda no Target](before-implement/privacy/allowlist-edges.md)
   + Métodos para colocar os dados no Target {#methods}
      + [Visão geral dos métodos](before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md)
      + [Parâmetros da página](before-implement/methods-to-get-data-into-target/page-parameters.md)
      + [Atributos de perfil na página](before-implement/methods-to-get-data-into-target/in-page-profile-attributes.md)
      + [Atributos de perfil de script](before-implement/methods-to-get-data-into-target/script-profile-attributes.md)
      + [Provedores de dados](before-implement/methods-to-get-data-into-target/data-providers.md)
      + [API de atualização de perfil em massa](before-implement/methods-to-get-data-into-target/bulk-profile-update-api.md)
      + [API de atualização de perfil único](before-implement/methods-to-get-data-into-target/single-profile-update-api.md)
      + [Atributos do cliente](before-implement/methods-to-get-data-into-target/customer-attributes.md)
      + [Configurações da API de perfil](before-implement/methods-to-get-data-into-target/profile-api-settings.md)
   + [Visão geral da segurança no Target](before-implement/target-security-overview.md)
   + [Navegadores compatíveis](before-implement/supported-browsers.md)
   + [Alterações na criptografia do TLS (Transport Layer Security)](before-implement/tls-transport-layer-security-encryption.md)
   + [CNAME e Adobe Target](before-implement/implement-cname-support-in-target.md)
+ Implementação do lado do cliente {#client-side}
   + [Visão geral: implementar o Target para Web no lado do cliente](implement/client-side/overview.md)
   + Adobe Experience Platform Web SDK {#web-sdk}
      + [Visão geral da implementação do Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)
      + [Usar o Adobe Target e o Web SDK para personalização](/help/dev/implement/client-side/aep-web-sdk/target-overview.md)
   + Implementação da at.js {#at-js-implementation}
      + [Visão geral da at.js](implement/client-side/atjs/how-atjs-works/overview.md)
      + Como a at.js funciona {#at-js}
         + [Como a visão geral do at.js funciona](implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
         + [Como a at.js gerencia a cintilação](implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
         + [Integrações da at.js](implement/client-side/atjs/how-atjs-works/target-atjs-integrations.md)
      + Como implantar a at.js {#deploy-at-js}
         + [Como implantar a at.js](implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)
         + [Implementar o Target usando a Adobe Experience Platform](implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)
         + [Implementação do Target sem um gerenciador de tags](implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)
         + [Implementar o Target usando o gerenciador dinâmico de tags (DTM)](implement/client-side/atjs/how-to-deployatjs/implement-target-using-dtm.md)
         + [Implementar o Target para Aplicativos de página única (SPA)](implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)
      + Decisão no dispositivo {#on-device-decisioning}
         + [Visão geral da decisão no dispositivo](implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md)
         + [Recursos compatíveis](implement/client-side/atjs/on-device-decisioning/supported-features.md)
         + [Artefato de regra](implement/client-side/atjs/on-device-decisioning/rule-artifact.md)
         + [Solução de problemas](implement/client-side/atjs/on-device-decisioning/troubleshooting-on-device-decisioning.md)
      + Funções da at.js {#functions-overview}
         + [Visão geral de funções do at.js](implement/client-side/atjs/atjs-functions/atjs-functions.md)
         + [adobe.target.getOffer()](implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md)
         + [adobe.target.getOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
         + [adobe.target.applyOffer()](implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)
         + [adobe.target.applyOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)
         + [adobe.target.triggerView() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)
         + [adobe.target.trackEvent()](implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
         + [mboxCreate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)
         + [targetGlobalSettings()](implement/client-side/atjs/atjs-functions/targetglobalsettings.md)
         + [mboxDefine() e mboxUpdate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)
         + [targetPageParams()](implement/client-side/atjs/atjs-functions/targetpageparams.md)
         + [targetPageParamsAll()](implement/client-side/atjs/atjs-functions/targetpageparamsall.md)
         + [registerExtension() - at.js 1.x](implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)
         + [sendNotifications() - at.js 2.1](implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)
         + [Eventos personalizados da at.js](implement/client-side/atjs/atjs-functions/atjs-custom-events.md)
         + [Depuração da at.js usando o depurador da Adobe Experience Cloud](implement/client-side/target-debugging-atjs/target-debugging-atjs.md)
         + [Usar instâncias baseadas em nuvem com o Target](implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md)
      + [Perguntas frequentes do at.js](implement/client-side/atjs/target-atjs-faq.md)
      + [Detalhes da versão da at.js](implement/client-side/atjs/target-atjs-versions.md)
      + [Atualização da at.js 1.x para at.js 2.x](implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md)
      + [Cookies do at.js](implement/client-side/atjs/atjs-cookies.md)
   + [User-agent e client hints](implement/client-side/atjs/user-agent-and-client-hints.md)
   + Entender a mbox global {#global-mbox}
      + [Compreender a visão geral da mbox global](implement/client-side/atjs/global-mbox/global-mbox-overview.md)
      + [Personalizar uma mbox global](implement/client-side/atjs/global-mbox/customize-global-mbox.md)
      + [Usar uma mbox global por meio de uma implementação herdada](implement/client-side/atjs/global-mbox/mbox-global-target-standard.md)
      + [Envio de parâmetros para uma mbox global](implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)
      + [Perguntas frequentes sobre a mbox global](implement/client-side/atjs/global-mbox/global-mbox-faq.md)
+ Implementação no servidor {#server-side}
   + [Lado do servidor: implementar a visão geral do Target](implement/server-side/server-side-overview.md)
   + [Introdução aos SDKs do Target](implement/server-side/sdk-guides/getting-started/getting-started.md)
   + [Aplicativos de exemplo](implement/server-side/sdk-guides/sample-apps/sample-apps.md)
   + [Transição de APIs herdadas do Target para o Adobe I/O](implement/server-side/transition-from-target-classic-apis.md)
   + Princípios fundamentais {#core-principles}
      + [Visão geral dos princípios principais](implement/server-side/sdk-guides/core-principles/overview.md)
      + [ID de usuário e segmentação](implement/server-side/sdk-guides/core-principles/user-identification-and-bucketing.md)
      + [Direcionamento de público](implement/server-side/sdk-guides/core-principles/audience-targeting.md)
      + [Rastreamento de eventos](implement/server-side/sdk-guides/core-principles/event-tracking.md)
      + [Permissões e propriedades do usuário](implement/server-side/sdk-guides/core-principles/user-permissions-and-properties.md)
   + Integração {#integration}
      + [Visão geral da integração](implement/server-side/sdk-guides/integration-with-experience-cloud/overview.md)
      + [Serviço da Experience Cloud ID (ECID)](implement/server-side/sdk-guides/integration-with-experience-cloud/ecid.md)
      + [Relatórios do Analytics for Target (A4T)](implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md)
      + [Segmentos do AAM](implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md)
   + Decisão no dispositivo {#on-device-decisioning}
      + [Visão geral da decisão no dispositivo](implement/server-side/sdk-guides/on-device-decisioning/overview.md)
      + Artefato de regra {#rule-artifact}
         + [Visão geral do artefato da regra](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)
         + [Baixar via Adobe Target SDK](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-sdk.md)
         + [Baixar via carga JSON](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-json.md)
         + [Exemplo de artefato de regra](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-example.md)
      + [Executar testes A/B com sinalizadores de recursos](implement/server-side/sdk-guides/on-device-decisioning/execute-ab-tests-with-feature-flags.md)
      + [Executar testes de recursos com atributos](implement/server-side/sdk-guides/on-device-decisioning/execute-feature-tests-with-attributes.md)
      + [Gerenciar implantações para testes de recursos](implement/server-side/sdk-guides/on-device-decisioning/manage-rollouts-for-feature-tests.md)
      + [Entregar personalização](implement/server-side/sdk-guides/on-device-decisioning/deliver-personalization.md)
      + [Visão geral dos recursos compatíveis](implement/server-side/sdk-guides/on-device-decisioning/supported-features.md)
      + [Solução de problemas da decisão no dispositivo](implement/server-side/sdk-guides/on-device-decisioning/troubleshooting.md)
      + [Práticas recomendadas](implement/server-side/sdk-guides/best-practices/best-practices.md)
   + Referência do SDK da Node.js {#node-js}
      + [Visão geral do SDK Node.js](implement/server-side/node-js/overview.md)
      + [Instalar o SDK Node.js](implement/server-side/node-js/install-sdk.md)
      + [Inicializar o SDK Node.js](implement/server-side/node-js/initialize-sdk.md)
      + [Obter ofertas (Node.js)](implement/server-side/node-js/get-offers.md)
      + [Obter atributos (Node.js)](implement/server-side/node-js/get-attributes.md)
      + [Enviar notificações (Node.js)](implement/server-side/node-js/send-notifications.md)
      + [Eventos da SDK (Node.js)](implement/server-side/node-js/sdk-events.md)
      + [Logger (Node.js)](implement/server-side/node-js/logger.md)
      + [Configuração de proxy (Node.js)](implement/server-side/node-js/proxy-configuration.md)
   + Referência do Java SDK {#java}
      + [Visão geral do Java SDK](implement/server-side/java/overview.md)
      + [Instalar o Java SDK](implement/server-side/java/install-sdk.md)
      + [Inicializar o Java SDK](implement/server-side/java/initialize-sdk.md)
      + [Obter ofertas (Java)](implement/server-side/java/get-offers.md)
      + [Obter atributos (Java)](implement/server-side/java/get-attributes.md)
      + [Enviar notificações (Java)](implement/server-side/java/send-notifications.md)
      + [Eventos da SDK (Java)](implement/server-side/java/sdk-events.md)
      + [Logger (Java)](implement/server-side/java/logger.md)
      + [Solicitações assíncronas (Java)](implement/server-side/java/asynchronous-requests.md)
      + [Configuração de proxy (Java)](implement/server-side/java/proxy-configuration.md)
      + [Configuração do cliente HTTP personalizado (Java)](implement/server-side/java/custom-http-client.md)
      + [Métodos de utilitário (Java)](implement/server-side/java/utility-methods.md)
   + Referência do .NET SDK {#net}
      + [Visão geral do .NET SDK](implement/server-side/net/overview.md)
      + [Instalar o .Net SDK](implement/server-side/net/install-sdk.md)
      + [Inicializar o .NET SDK](implement/server-side/net/initialize-sdk.md)
      + [Obter Ofertas (.NET)](implement/server-side/net/get-offers.md)
      + [Obter Atributos (.NET)](implement/server-side/net/get-attributes.md)
      + [Enviar Notificações (.NET)](implement/server-side/net/send-notifications.md)
      + [Eventos da SDK (.NET)](implement/server-side/net/sdk-events.md)
      + [Solicitações Assíncronas (.NET)](implement/server-side/net/asynchronous-requests.md)
   + Referência do Python SDK {#python}
      + [Visão geral do Python SDK](implement/server-side/python/overview.md)
      + [Instalar o Python SDK](implement/server-side/python/install-sdk.md)
      + [Inicializar o Python SDK](implement/server-side/python/initialize-sdk.md)
      + [Obter Ofertas (Python)](implement/server-side/python/get-offers.md)
      + [Obter atributos (Python)](implement/server-side/python/get-attributes.md)
      + [Enviar notificações (Python)](implement/server-side/python/send-notifications.md)
      + [Eventos da SDK (Python)](implement/server-side/python/sdk-events.md)
      + [Solicitações assíncronas (Python)](implement/server-side/python/asynchronous-requests.md)
      + [Logger (Python)](implement/server-side/python/logger.md)
+ [Implementação híbrida](implement/hybrid/hybrid-overview.md)
+ [Implementação do Recommendations](implement/recommendations/recommendations.md)
+ [Implementação beta do Recommendations](/help/dev/implement/recommendations/recommendations-beta.md)
+ Implementação do aplicativo móvel {#mobile-apps}
   + [Visão geral do Target para aplicativos para dispositivos móveis](implement/mobile/overview.md)
   + [Visualização do Target Mobile](implement/mobile/target-mobile-preview.md)
   + [Usar serviço de localização](implement/mobile/use-location-service.md)
   + [Perguntas frequentes sobre o Target para aplicativos móveis](implement/mobile/mobile-faq.md)
   + [Implementar o Target com o AEP Mobile SDK em um aplicativo nativo com visualizações da Web](/help/dev/implement/mobile/native-app.md)
+ Implementação de email {#implement-email}
   + [Email: implementação da visão geral do Target](implement/email/overview.md)
   + [Criar uma AdBox para uma imagem](implement/email/testing-content-with-the-adbox.md)
   + [Testar uma Adbox de imagem de email](implement/email/testing-email-image-adbox.md)
   + [Trabalhar com redirecionadores](implement/email/working-with-redirectors.md)
+ Guias da API {#api}
   + [Visão geral da API do Target](/help/dev/before-administer/target-api-overview.md)
   + [Configurar autenticação para APIs do Target](/help/dev/before-administer/configure-authentication.md)
   + Guia da API de entrega {#delivery-api}
      + [Visão geral da API de entrega](/help/dev/implement/delivery-api/overview.md)
      + [SDKs para interagir com a API de entrega](/help/dev/before-implement/delivery-api-overview/sdks.md)
      + [Introdução](/help/dev/before-implement/delivery-api-overview/getting-started.md)
      + [Permissões de usuário (Premium)](/help/dev/before-implement/delivery-api-overview/user-permissions.md)
      + [Identificação de visitantes](/help/dev/before-implement/delivery-api-overview/identifying-visitors.md)
      + [Entrega única ou em lote](/help/dev/before-implement/delivery-api-overview/single-or-batch.md)
      + [Pré-busca](/help/dev/before-implement/delivery-api-overview/prefetch.md)
      + [Notificações](/help/dev/before-implement/delivery-api-overview/notifications.md)
      + [Integração com o Experience Cloud](before-implement/delivery-api-overview/integration.md)
      + [Considerações e limitações conhecidas](/help/dev/before-implement/delivery-api-overview/known-limitations.md)
      + [Client Hints](/help/dev/before-implement/delivery-api-overview/client-hints.md)
      + [API de entrega](/help/dev/implement/delivery-api/delivery-api.md)
   + API de administração {#admin-api}
      + [Visão geral da API de administração](before-administer/admin-api-overview/admin-api-overview.md)
      + [API de administração do Adobe Target](/help/dev/administer/admin-api/admin-api-overview-new.md)
   + API de perfil {#profile-apis}
      + [Visão geral da API de perfis](/help/dev/administer/profile-api/profiles-api.md)
      + [Buscar perfis](/help/dev/administer/profile-api/profile-fetch.md)
      + [Atualizar perfis](/help/dev/administer/profile-api/profile-api-overview.md)
      + [API de atualização de perfil único](/help/dev/administer/profile-api/profile-single-api.md)
      + [API de atualização de perfil em massa](/help/dev/administer/profile-api/profile-bulk-api.md)
   + [API de relatórios](/help/dev/administer/reporting-api/reporting-api.md)
   + API do Recommendations {#recommendations-api}
      + [Visão geral da API do Recommendations](before-administer/recs-api/overview.md)
      + [Gerencie seu catálogo com APIs](before-administer/recs-api/manage-catalog.md)
      + [Gerenciar critérios personalizados](before-administer/recs-api/manage-custom-criteria.md)
      + [Usar a API de entrega com o Recommendations](before-administer/recs-api/fetch-recs-server-side-delivery-api.md)
      + [API do Recommendations](/help/dev/administer/recommendations-api/recommendations-api.md)
   + API de modelos {#models-api}
      + [Visão geral da API de modelos (Incluir na lista de bloqueios)](before-administer/models-api.md)
      + [API de modelos](/help/dev/administer/models-api/models-api-overview.md)
   + [APIs do Adobe Admin Console](/help/dev/before-implement/delivery-api-overview/adobe-console-api.md)
   + [API do Adobe Experience Platform Edge Network Server](/help/dev/before-implement/delivery-api-overview/aep-edge-network-server-api.md)
+ Padrões de implementação {#implementation-patterns}
   + [Visão geral dos padrões de implementação](/help/dev/patterns/pattern-overview.md)
   + Padrão de implementação do Recommendations usando at.js {#atjs}
      + [Padrão de implementação do Recommendations usando a visão geral da at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md)
      + [Inicializar SDKs](/help/dev/patterns/recs-atjs/initialize-sdk.md)
      + [Configurar coleção de dados](/help/dev/patterns/recs-atjs/data-collection.md)
      + [Renderizar experiências](/help/dev/patterns/recs-atjs/render-experiences.md)
      + [Notificar Destino](/help/dev/patterns/recs-atjs/notify-target.md)


