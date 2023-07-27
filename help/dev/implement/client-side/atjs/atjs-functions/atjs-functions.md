---
keywords: at.js, funções, biblioteca javascript
description: Veja uma lista de funções que podem ser usadas com as versões 1.x e 2.x da biblioteca at.js de JavaScript no [!DNL Adobe Target].
title: Quais funções posso usar com a at.js?
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 73%

---

# Funções da at.js

Lista de funções que podem ser usadas com o [!DNL Adobe Target] Biblioteca JavaScript at.js. Clique nos links na coluna Função para obter mais informações e exemplos.

| Função | Detalhes |
| --- | --- | 
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | Esta função envia uma solicitação para obter uma [!DNL Target] oferta. Use com `adobe.target.applyOffer()` para processar a resposta ou use sua própria manipulação de sucesso. |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(at.js 2.x) | Essa função permite que você recupere várias ofertas passando em várias mboxes. Além disso, várias ofertas podem ser recuperadas para todas as exibições em atividades ativas.<P>**Observação:** essa função foi introduzida com a at.js 2.x. Essa função não está disponível para a at.js versão 1.*x*. |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | Esta função aplica o conteúdo de resposta. |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(at.js 2.x) | Essa função permite aplicar mais de uma oferta que foi recuperada por [!UICONTROL adobe.target.getOffers()].<P>**Observação:** essa função foi introduzida com a at.js 2.x. Essa função não está disponível para a at.js versão 1.*x*. |
| [[!UICONTROL adobe.target.triggerView (viewName, options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(at.js 2.x) | Essa função pode ser chamada sempre que uma nova página é carregada ou quando um componente em uma página é renderizado novamente.<P> Essa função deve ser implementada para aplicativos de página única (SPA) para usar o [!UICONTROL Visual Experience Composer] (VEC) para criar [!UICONTROL Teste A/B] e [!UICONTROL Direcionamento de experiência] (XT) Atividades. |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | Essa função aciona uma solicitação para relatar ações do usuário, como cliques e conversões. Não entrega atividades na resposta. |
| [[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(at.js 1.x) | Executa uma solicitação e aplica a oferta ao DIV mais próximo com o nome de classe mboxDefault.<P>**Observação:** essa função está disponível para a at.js versão 1.somente *x*. Essa função foi descontinuada pelo lançamento da at.js 2.x. Ela retorna o conteúdo padrão se for usada com a 2.x. |
| [[!UICONTROL mboxDefine(options)] e [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(at.js 1.x) | Defina e atualize um mbox.<P>**Observação:** essa função está disponível para a at.js versão 1.somente *x*. Essa função foi descontinuada pelo lançamento da at.js 2.x. Ela retorna o conteúdo padrão se for usada com a 2.x. |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | É possível substituir as configurações na biblioteca at.js usando `[!UICONTROL targetGlobalSettings()]`, em vez de configurá-los na variável [!DNL Target Standard/Premium] ou usando APIs REST.<ul><li>Provedores de dados: essa configuração permite que clientes reúnam dados de provedores de dados de terceiros, como Demandbase, BlueKai e serviços personalizados, além de passar os dados para o Target como parâmetros da mbox na solicitação global da mbox.</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | Este método permite anexar parâmetros ao mbox global de fora do código da solicitação. |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | Este método permite anexar parâmetros a todos os mboxes de fora do código da solicitação. |
| [[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(at.js 1.x) | Fornece uma forma padrão de registrar uma extensão específica.<P>**Observação:** essa função está disponível para a at.js versão 1.somente *x*. Essa função foi descontinuada pelo lançamento da at.js 2.x. Ela retorna o conteúdo padrão se for usada com a 2.x. |
| [[!UICONTROL Eventos personalizados da at.js]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | Os eventos personalizados da at.js informam quando uma solicitação de mbox ou oferta falha ou é bem-sucedida. |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(at.js 2.1.0) | Esta função envia uma notificação para [!DNL Target] borda quando uma experiência é renderizada sem usar `[!UICONTROL adobe.target.applyOffer()]` ou `[!UICONTROL adobe.target.applyOffers()]`.<P>**Observação**: esta função foi introduzida na at.js 2.1.0 e estará disponível em todas as versões a partir da 2.1.0. |
