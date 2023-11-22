---
keywords: versões da at.js, versões da at.js, notas de versão
description: Exibir os detalhes sobre as alterações em cada versão do [!DNL Adobe Target] Biblioteca JavaScript at.js.
title: O que está incluído em cada versão da at.js?
feature: at.js
exl-id: 609dacba-2ab8-45e9-b189-928d59938c98
source-git-commit: 09ecaa3be954fe5a002e09a422ceeb7a4ed0750a
workflow-type: tm+mt
source-wordcount: '4712'
ht-degree: 72%

---

# Detalhes da versão da at.js

Detalhes sobre alterações em cada versão da biblioteca at.js de JavaScript do [!DNL Adobe Target].

>[!IMPORTANT]
>
>[!DNL Adobe Target] O é compatível com at.js 1.*x* e at.js 2.*x*.
>
>at.js 1.*x*   entrou no modo de manutenção. A variável [!DNL Target] O time lança correções de bugs e patches de segurança quando necessário.
>
>A variável [!DNL Target] A equipe do fornece suporte total para a at.js 2.*x* O e o lança correções de erros, patches de segurança, recursos e otimização de desempenho continuamente.
>
>Você deve atualizar para as versões mais recentes do 1.*x* ou 2.*x* para obter correções de erros e patches de segurança para problemas descobertos em qualquer versão secundária anterior da versão principal correspondente.

Tags em [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) são o método preferido para atualizar o at.js. Os desenvolvedores de extensão adicionam continuamente novos recursos a suas extensões e corrigem erros com frequência. Essas atualizações são colocadas em novas versões de uma extensão e disponibilizadas no catálogo da Adobe Experience Platform como atualizações. Para obter mais informações, consulte [Atualizações de extensão](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/extensions/extension-upgrade.html) no *Visão geral das tags* guia.6+

## at.js versão 2.11.3 (21 de novembro de 2023)

* Correção de um problema que impedia o envio de tokens de resposta no `at-content-rendering-failed` eventos.

## at.js versão 2.11.2 (26 de outubro de 2023)

* Correção de um problema que causava inconsistências nos tokens de resposta enviados em eventos personalizados.

## at.js versão 2.11.1 (13 de outubro de 2023)

* Correção de um problema que causava erros não detectados enquanto uma página que executava a at.js estava no modo quirks.

## at.js versão 2.11.0 (10 de outubro de 2023)

* Adição de suporte para configuração personalizada [!DNL Adobe Experience Platform] (AEP) `sandboxId` e `sandboxName` in `targetGlobalSettings`, que é passado para a API de entrega em `getOffer/getOffers` chamadas.
* Correção de DOM de sombra para encadeamento `:eq()` em seletores.

## at.js versão 2.10.3 (12 de setembro de 2023)

* Correção de um problema que acionava incorretamente a variável `at-content-rendering-succeeded` evento personalizado quando nenhuma oferta é renderizada. O evento correto, `at-content-rendering-no-offers`, agora é acionado.
* Adicionado `eventToken` e `responseTokens` ao objeto de erro para o `at-content-rendering-failed` evento personalizado.

## at.js versão 2.10.2 (7 de março de 2023)

* Correção de um problema que fazia com que a função `trackEvent` sempre retornasse um erro.

## at.js versão 2.10.1 (2 de fevereiro de 2023)

* Correção de um erro no qual as atividades que envolviam regras de público e continham parâmetros com pontos em seus nomes não retornavam a experiência esperada de decisão no dispositivo.
* Correção de um bug introduzido na at.js 2.6.0, no qual a at.js disparava uma chamada de entrega, mesmo quando a mboxDisable estava ativada.

## at.js versão 2.10.0 (19 de setembro de 2022)

* Adição de suporte a cookies de terceiros.

## at.js versão 2.9.0 (27 de maio de 2022)

* Foi adicionado suporte a [User Agent Client Hints](user-agent-and-client-hints.md).
* Correção de um erro em que várias solicitações de mbox na mesma página tinham IDs de impressão diferentes.

## Versão 2.8.1 da at.js (28 de janeiro de 2022)

* Correção do `pageLoad` que não era mapeado para a target-global-mbox no modo de execução híbrido On Device Decisioning (ODD).
* Correção de um problema com detalhes de análise para a solicitação de mbox.
* As dependências de desenvolvimento foram atualizadas para corrigirem vulnerabilidades de segurança.

## Versão 2.8.0 da at.js (7 de janeiro de 2022)

A biblioteca JavaScript at.js do [!DNL Target] agora coleta dados de uso de recursos e de telemetria de desempenho. Os dados pessoais não são coletados. A opção de recusa para este recurso está disponível ao configurar `telemetryEnabled` para falso em `targetGlobalSettings`. Para mais informações, consulte [telemetryEnabled em targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).

## at.js versão 2.7.0 (28 de outubro de 2021)

Esta versão inclui os seguintes aprimoramentos:

* Suporte adicionado para [Componentes da web](https://developer.mozilla.org/pt-BR/docs/Web/Web_Components). Esta versão da at.js é necessária para criar e testar experiências e ofertas personalizadas em elementos personalizados e em elementos dentro de elementos personalizados. Essa funcionalidade está incluída na versão 21.10.5 do [!DNL Target Standard/Premium].

## at.js 1.8.3 (21 de setembro de 2021)

Esta versão contém as seguintes alterações:

* Remoção da `reactor-window` e `reactor-document` módulos do Adobe Experience Platform Launch para garantir que o build do Platform launch funcione corretamente para clientes que `window.default` ou `document-default` definido.
* A at.js 1.8.3 agora define explicitamente o `Samesite=None` e `Secure` para garantir que cookies de domínio de terceiros sejam definidos corretamente.

## at.js 2.6.1 (16 de agosto de 2021)

* Correção de erros para &quot;Nenhum artefato em cache disponível para modo híbrido&quot; ao usar a decisão no dispositivo.

## at.js 2.6.0 (16 de julho de 2021)

* Adição do atributo seguro aos cookies sempre que as configurações `secureOnly` da at.js estiverem definidas como `true`.
* Os tokens de resposta agora estão disponíveis ao usar o `triggerView()`.
* Correção de um problema relacionado ao evento `CONTENT_RENDERING_NO_OFFERS`. Agora, esse evento é acionado corretamente sempre que não há conteúdo retornado do [!DNL Target].
* [!UICONTROL Analytics for Target] Os detalhes das métricas de clique do (A4T) são retornados corretamente ao usar `prefetch` solicitações.
* A geração UUID não usa mais `Math.random()`, mas depende de `window.crypto`.
* A expiração do cookie `sessionId` é estendida corretamente em cada chamada de rede.
* A inicialização do cache de visualização do Aplicativo de página única (SPA) agora é manipulada corretamente e atende às configurações `viewsEnabled`. Configuração `viewsEnabled` para o `false` agora o valor desativa o `triggerView()` função. Consulte [Ordem de operação do carregamento inicial da página](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md#order).

## at.js 2.5.0 (13 de maio de 2021)

Essa versão da at.js inclui os seguintes aprimoramentos e alterações:

* [Suporte à decisão no dispositivo](/help/dev/implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md) para at.js.
* [Suporte a links de pré-visualização](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) para atividade de Automated Personalization

Esta versão também remove o suporte ao Microsoft Internet Explorer 10 e versões posteriores.

## at.js 2.4.1 (23 de março de 2021)

Essa versão do at.js é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

* Correção de um problema em que `targetPageParams` era incluído nas solicitações da mbox. `targetPageParams` deve ser incluído somente em solicitações `pageLoad`. (TNT-40247)
* Globais de janela e documento otimizados que fazem referência à extensão do Adobe Experience Platform. (TNT-37124)

## at.js 2.4.0 (14 de janeiro de 2021)

Essa versão do at.js é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

* Adiciona suporte para id de perfil/plataforma unificada para API de entrega de customerIds.
* Corrige a injeção de tag de estilo inválida.

## at.js 2.3.3 (13 de novembro de 2020)

Essa versão do at.js é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

* Correção de um problema relacionado ao rastreamento de cliques da mbox e ao A4T. Com 0n-clique, [!DNL Target] O acionou uma chamada da API de entrega com os parâmetros corretos de mbox e mbox. No entanto, a SDID não correspondeu à do [!DNL Analytics] chamada de, portanto, não houve ocorrência de identificação e conversão. (TNT-38372)

## at.js 2.3.2 (24 de julho de 2020)

Essa versão do at.js é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

* Correção de um erro quando um script ou código adicionava uma propriedade padrão à janela ou ao documento.

## at.js 1.8.2 (15 de junho de 2020)

Essa versão do at.js é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

* Correção de um problema ao usar a substituição de CNAME e borda, at.js 1.O *x* pode criar o domínio do servidor incorretamente, o que resultou na falha da solicitação do [!DNL Target]. (TNT-35064)

## Versões 2.3.1 da at.js (15 de junho de 2020)

Essa versão do at.js é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

* A configuração `deviceIdLifetime` foi substituída por [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md). (TNT-36349)
* Correção de um problema ao usar a substituição de CNAME e borda, at.js 2.O *x* pode criar o domínio do servidor incorretamente, o que resultou na falha da solicitação do [!DNL Target]. (TNT-35065)
* Correção de um problema ao usar o [!DNL Target] extensão v2 e o [!UICONTROL Adobe Analytics Launch] extensão, [!DNL Target] atrasou o [!DNL Analytics] `sendBeacon` chame. (TNT-36407, TNT-35990, TNT-36000)

## at.js versão 2.3.0 (25 de março de 2020)

Essa versão do at.js é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

* Suporte à configuração de nonces da Política de segurança de conteúdo nas tags SCRIPT e STYLE, que são anexadas ao DOM da página ao aplicar as tags entregues [!DNL Target] ofertas. Os clientes podem definir `targetGlobalSettings.cspScriptNonce` e `targetGlobalSettings.cspStyleNonce` para que a at.js possa definir os nonces de tag de script e estilo correspondentes em ofertas aplicadas. Consulte  [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) para obter mais detalhes.
* Correção de um problema ao compilar a at.js com o compilador de Fechamento do Google para implantação do Google Tag Manager.
* O cookie de verificação da at.js foi renomeado de `check` para `at_check` para evitar colisões com as implementações dos clientes.

## at.js versão 1.8.1 (25 de março de 2020)

Essa versão do at.js é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

* O cookie de verificação da at.js foi renomeado de `check` para `at_check` para evitar colisões com as implementações dos clientes.

## at.js versão 2.2.0 (10 de outubro de 2019)

Essa versão do at.js inclui os seguintes aprimoramentos e correções:

* Correção de um problema no qual o rastreamento de cliques não relatava conversões no [!DNL Analytics for Target] (A4T) quando [!DNL Adobe Analytics] o código não estava presente nos elementos da página.
* Desempenho aprimorado ao usar o Serviço de ID de Experience Cloud (ECID) v4.4 e a at.js 2.2 em suas páginas da Web.
* Anteriormente, a ECID fazia duas chamadas de bloqueio antes que a at.js pudesse buscar experiências. Isso foi reduzido a uma única chamada, o que melhora significativamente o desempenho.
* Correção de um processamento de exibição pré-buscado incorreto, em que os tokens de evento de ofertas padrão não eram incluídos nas notificações enviadas.

>[!NOTE]
>
>Atualize sua extensão ECID para v4.4 para aproveitar esse aprimoramento de desempenho.

* A at.js versão 2.2 também fornece uma nova configuração chamada `serverState`. Essa configuração pode ser usada para otimizar o desempenho da página quando uma integração híbrida de [!DNL Target] está implementado. A integração híbrida significa que você está usando a at.js v2.2+ no lado do cliente e a API de entrega ou uma [!DNL Target] SDK no lado do servidor para fornecer experiências. O `serverState` fornece ao at.js v2.2+ a capacidade de aplicar experiências diretamente de conteúdo buscado no lado do servidor e retornado ao cliente como parte da página que está sendo veiculada. Para obter mais informações, consulte &quot;serverState&quot; em [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverstate).

## at.js versão 1.8.0 (10 de outubro de 2019)

Essa versão do at.js inclui os seguintes aprimoramentos e correções:

* Desempenho aprimorado ao usar o Serviço de ID de Experience Cloud (ECID) v4.4 e o at.js 1.8 nas páginas da Web.
* Anteriormente, a ECID fazia duas chamadas de bloqueio antes que a at.js pudesse buscar experiências. Isso foi reduzido a uma única chamada, o que melhora significativamente o desempenho.

>[!NOTE]
>
>Atualize sua extensão ECID para v4.4 para aproveitar esse aprimoramento de desempenho.

## at.js versão 2.1.1 (24 de julho de 2019)

Essa versão do at.js é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

(Os números de edição entre parênteses são para uso interno da Adobe.)

* Correção de um problema que fazia com que vários beacons fossem acionados ao usar a métrica de Rastreamento de cliques na página Metas e configurações no Visual Experience Composer (VEC). (TNT-32812)
* Correção de um problema que fazia com que o `triggerView()` não renderizasse ofertas mais de uma vez. (TNT-32780)
* Correção de um problema no `triggerView()` para garantir que a solicitação contivesse informações da Experience Cloud ID (ECID). (TNT-32776)
* Correção de um problema que impedia o acionamento da notificação do `triggerView()`, mesmo se não houvesse exibições salvas. (TNT-32614)
* Correção de um problema que causava um erro devido ao uso de decodeURIcomponent, que causava problemas quando o URL continha um parâmetro da sequência de consulta malformado. (TNT-32710)
* Agora o sinalizador de beacon é definido como “true” no contexto de solicitações de entrega enviadas por meio da API do `Navigator.sendBeacon()`. (TNT-32683)
* Correção de um problema que impedia que as ofertas do Recommendations fossem exibidas nos sites de alguns clientes. Os clientes podem ver o conteúdo da oferta na chamada da API de entrega, mas a oferta não foi aplicada no site. (TNT-32680)
* Correção de um problema que fazia com que o rastreamento de cliques em várias experiências não funcionasse como esperado. (TNT-32644)
* Correção de um problema que impedia o at.js de aplicar a segunda métrica após a falha da renderização da primeira métrica. (TNT-32628)
* Correção de um problema ao passar o `mbox3rdPartyId` usando a função do `targetPageParams` que fazia com que a carga da solicitação não estivesse presente nos parâmetros de consulta ou na carga da solicitação. (TNT-32613)
* Correção de um problema que fazia com que as respostas da notificação de cliques fossem bloqueadas nos navegadores Chromium (incluindo Google Chrome). (TNT-32290)

## at.js versão 2.1.0 (segunda-feira, 3 de junho de 2019)

Esta versão inclui os seguintes recursos e melhorias:

* **Suporte ao Adobe Opt-in**: o Adobe Opt-in é uma maneira de simplificar as integrações das soluções da Adobe com as plataformas de gerenciamento de consentimento. Para obter mais informações sobre o Adobe Opt-in, consulte [Privacidade e Regulamento Geral sobre a Proteção de Dados (GDPR)](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

* **Compatível com o CSP padrão do setor**: a at.js não usa mais eval() para executar o JavaScript.

* **Registro de análises do cliente**: forneça aos clientes controle total sobre como enviar dados de análise para o [!DNL Adobe Analytics], seja no cliente ou no servidor.

  Para obter mais informações, consulte [Lado do cliente [!DNL Analytics] fazendo logon](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html#client-side).

* **Enviar notificações**: permite aos desenvolvedores enviar notificações quando uma experiência é renderizada pelo seu código em vez de usar `applyOffer()` ou `applyOffers()`.

  Para obter mais informações, consulte [adobe.target.sendNotifications(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md).

* **Tamanho da at.js reduzido em ~24%**: o tamanho da at.js foi reduzido em ~24%. O tamanho de arquivo menor melhora o desempenho do carregamento da página e reduz o tempo para baixar a at.js na página.

## at.js versão 2.0.1 (terça-feira, 19 de março de 2019)

Essa é uma versão de manutenção e inclui os seguintes aprimoramentos e correções:

(Os números de edição entre parênteses são para uso interno da Adobe.)

* Correção de uma condição de corrida no código de pesquisa DOM que causava exceções de JavaScript para determinados clientes. (TNT-31869)
* As notificações que renderizaram as exibições foram desassociadas dos manipuladores de eventos do rastreamento de cliques. Inicialmente, [!DNL Target] não enviava notificações se os manipuladores de eventos de clique pertencentes a uma exibição renderizada não pudessem ser anexados. [!DNL Target]O agora envia uma notificação de exibição mesmo se os elementos de clique não forem encontrados. (TNT-31969)
* Correção de um problema que fazia com que o sinalizador de redirecionamento do evento de solicitação sucedida fosse sempre definido como verdadeiro. (TNT-31907)
* Correção de um problema que fazia com que a ação de reorganizar do VEC fosse registrada como êxito, mesmo quando os elementos estavam ausentes. (TNT-31924)
* Correção de um problema que fazia com que as notificações de determinados clientes não contivessem o token de propriedade das Permissões empresariais. (TNT-31999)

## at.js versão 1.7.1 (terça-feira, 19 de março de 2019)

Essa é uma versão de manutenção e inclui a seguinte correção:

(Os números de edição entre parênteses são para uso interno da Adobe.)

* Correção de uma condição de corrida no código de pesquisa DOM que causava exceções de JavaScript para determinados clientes. (TNT-31869)

## at.js versão 2.0.0

A at.js 2.x fornece conjuntos de recursos avançados para sua empresa personalizar tecnologias de próxima geração no lado do cliente. Essa nova versão tem como foco a atualização da at.js para ter interações harmoniosas com aplicativos de página única (SPAs).

Estes são alguns benefícios do uso da at.js 2.x que não estão disponíveis nas versões anteriores:

* A capacidade de armazenar todas as ofertas em cache quando a página é carregada para reduzir o número de chamadas de servidor a apenas uma chamada.
* Melhore bastante as experiências dos usuários finais em seu site, uma vez que as ofertas são exibidas imediatamente por meio do cache, sem o atraso imposto pelas chamadas tradicionais do servidor.
* Uma linha de código simples e uma configuração de desenvolvedor única para permitir que seus profissionais de marketing criem e executem atividades A/B e Experience (XT) por meio do Visual Experience Composer (VEC) em seus aplicativos de página única.

A at.js 2.x apresenta as seguintes novas funções:

* getOffers()
* applyOffers()
* triggerView()

As seguintes funções foram descontinuadas com a introdução da at.js 2.x:

* mboxCreate()
* mboxDefine
* registerExtension()

Para obter mais informações, consulte [Atualização da at.js 1.x para at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md) e [funções da at.js](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).

>[!NOTE]
>
>Se você precisar de suporte para o Adobe Opt-in para o [Regulamento Geral sobre a Proteção de Dados](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) (GDPR), no momento, você deve usar a at.js 1.7.0, ou at.js 2.1.0 ou posterior.

## at.js versão 1.7.0

O at.js 1.7.0 traz suporte à Adobe Opt-In. O Adobe Opt-In é uma maneira de simplificar as integrações das soluções da Adobe com as plataformas de gerenciamento de consentimento.

Para obter mais informações sobre o Adobe Opt-in, consulte [Privacidade e Regulamento Geral sobre a Proteção de Dados](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) (GDPR).

Essa versão também corrige um problema em que [!DNL Target] O pode substituir parâmetros de URL de redirecionamento por parâmetros provenientes do URL de redirecionamento.

>[!NOTE]
>
>Se você precisar de suporte do Adobe Opt-in para o GDPR, use a at.js 1.7.0, ou 2.1.0 ou posterior.

## at.js versão 1.6.4

O at.js 1.6.4 é uma versão de manutenção e aborda o seguinte problema:

* Correção de uma condição de corrida que se manifestava no Microsoft Internet Explorer 11 e que causava a aplicação de ofertas duplicadas.

## at.js versão 1.6.3

A versão 1.6.3 do at.js inclui as seguintes correções e aprimoramentos:

* Os seletores agora têm o CSS ignorado se contiverem IDs ou classes CSS que comecem com um dígito, dois hifens ou um hífen seguido de um dígito (por exemplo #-123). (TNT-31061)
* Correção de um problema introduzido na at.js 1.6.2 em que as ofertas do Visual Experience Composer (VEC) com diferentes atividades aplicáveis a um mesmo seletor CSS não respeitavam a prioridade das atividades. (TNT-31052)
* Correção de um problema de limite de tempo para promessas em ambientes em que não havia suporte nativo a promessas. (TNT-30974)
* Os problemas agora são capturados e relatados corretamente pelo evento de falha de renderização de conteúdo. Anteriormente, o JavaScript podia relatar uma execução bem-sucedida, mesmo que não fosse o caso. (TNT-30599)

## at.js versão 1.6.2

Esta é uma versão de manutenção e aborda o seguinte problema:

* Corrigido um problema que, em alguns sites de clientes, resultava em um loop &quot;async&quot; infinito.

>[!WARNING]
>
>Além disso, a versão 1.6.2 da at.js também contém todos os aprimoramentos e correções incluídos na versão 1.6.1 e 1.6.0 da at.js. Essas versões não estão mais disponíveis para download. Recomendamos que você atualize para a versão 1.6.2, se estiver usando a 1.6.1 ou 1.6.0

Aqui estão as melhorias e correções incluídas na at.js versão 1.6.1:

* Corrigido um problema na at.js 1.6.0 que fazia com que as recomendações fossem duplicadas no Microsoft Internet Explorer 11. (TNT-30593)
* A at.js agora garante que a lógica de substituição de borda verifique a existência de um cookie de cluster de borda para evitar um número de borda diferente se um usuário pular bordas durante uma sessão. (TNT-30563)
* Corrigido um problema que impedia a at.js de executar ações subsequentes se o conteúdo HTML contivesse um código JS inválido. A at.js agora registra o erro e renderiza as ações restantes sem problema. (TNT-30546)
* Foram feitas alterações para que haja uma exceção quando uma página de redirecionamento se requalificar para uma atividade de redirecionamento. (TNT-30532)
* Corrigido um problema que impedia que o tempo limite de solicitação correto fosse propagado da solicitação da API getOffer (). (TNT-30498)
* Corrigido um problema que impedia a at.js 1.6.0 de salvar cookies ao usar o protocolo de arquivo. (TNT-30454)
* Correção de um problema que fazia com que nem todas as experiências fossem entregues com redirecionamentos ao usar [!DNL Analytics for Target] (A4T). (TNT-30444)
* Correção de um problema que fazia com que a página ficasse oculta após o [!DNL Target] chamada bem-sucedida. (TNT-30358)

Aqui estão as melhorias e correções incluídas na at.js versão 1.6.0:

* As ofertas de redirecionamento agora são automaticamente compatíveis com o [!UICONTROL Analytics for Target] (A4T). A solução alternativa do lado do cliente foi removida. (TNT-30247)
* O roteamento de borda do lado do cliente agora está ativado por padrão. (TNT-30261)
* Corrigido um problema com a renderização de ação do Visual Experience Composer (VEC) quando há dependências entre as ações. (TNT-30248)

## at.js versão 1.5.0

A at.js versão 1.5.0 já está disponível.

* Os detalhes do evento `at-request-succeeded` contêm sinalizador de redirecionamento. Esse sinalizador pode ser usado para determinar se a página será redirecionada a um URL diferente. Caso queira saber o URL, cadastre-se em `at-content-rendering-redirect`. (TNT-29834)
* Correção de um problema que fazia com que `window.targetGlobalSettings.enabled` falhasse com uma exceção de tempo de execução se fosse definido como false. (TNT-29829)
* Correção de um problema que fazia com que a página falhasse ao carregar o Visual Experience Composer (VEC) se estivesse usando o código personalizado para acionar uma solicitação de mbox global o usando ocultação do evento body. (TNT-29795)
* Suporte adicionado para `screenOrientation`, `devicePixelRatio`e `webGLRenderer`. Esses novos [!DNL Target] Os parâmetros de solicitação do são usados para detecção de iPhone X e outra detecção de dispositivo moderna. Para obter mais informações, consulte [Dispositivo móvel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html). (TNT-29781)
* Correção de um problema em que a dica de localização do Adobe Audience Manager (AAM) não é sempre enviada. (TNT-29695)
* Em navegadores com suporte para isso, o at.js 1.5.0 é alternado para MutationObserver para polling de seletor. Versões anteriores ao at.js 1.0.0 usavam um polyfill MutationObserver, que se mostrou problemático. Para evitar problemas de polyfill, a versão 1.5.0 usa o seguinte pseudocódigo para decidir qual mecanismo de agendamento utilizar:

  ```
  if MutationObserver is supported
    scheduler = MutationObserver
  else if document is visible
    scheduler = requestAnimationFrame
  else
    scheduler = setTimeout
  ```

## at.js versão 1.3.0

A at.js versão 1.3.0 já está disponível.

* Os seguintes novos eventos estão disponíveis para ajudar no rastreamento, depuração e personalização das interações com a at.js:

   * LIBRARY_LOADED
   * REQUEST_START
   * CONTENT_RENDERING_START
   * CONTENT_RENDERING_NO_OFFERS
   * CONTENT_RENDERING_REDIRECT

  Para obter mais informações, consulte [Eventos personalizados da at.js](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md).

* É possível aumentar uma solicitação de at.js com parâmetros adicionais provenientes de provedores de dados. Os provedores de dados devem ser adicionados a `window.targetGlobalSettings` sob o `dataProviders key`.

  Para obter mais informações, consulte [Provedores de dados](atjs-functions/targetglobalsettings.md#data-providers).

* As solicitações de at.js agora usam GET, mas mudam para POST quando o tamanho do URL excede 2048 caracteres. Existe uma nova propriedade chamada `urlSizeLimit`, na qual você pode aumentar o limite de tamanho, se necessário. Essa alteração permite [!DNL Target] para alinhar a at.js ao AppMeasurement, que usa a mesma técnica.
* [!DNL Target]O agora reforça que a chave da `mbox` é usada na função `adobe.target.applyOffer(options)`. Essa chave foi necessária no passado, mas [!DNL Target] a sua utilização para garantir que os [!DNL Target] O tem a validação adequada e os clientes estão usando a função corretamente.
* A at.js melhorou a funcionalidade de rastreamento de eventos e cliques. O at.js usa `navigator.sendBeacon()` para enviar dados de rastreamento de eventos e fallback para XHR síncrono quando `navigator.sendBeacon()` não é suportado. Esse fallback afeta, principalmente, o Internet Explorer 10 e 11 e algumas versões do Safari. O Safari adicionará suporte para `navigator.sendBeacon()` no próximo iOS versão 11.3.
* A at.js agora pode renderizar ofertas mesmo quando uma página é aberta em guias em segundo plano. Alguns [!DNL Target] Os clientes encontraram um problema ao `requestAnimationFrame()` foi desabilitado devido ao comportamento de controle do navegador para guias em segundo plano.
* Esta versão adiciona muitas melhorias de desempenho, incluindo callstacks mais curtos ao inspecionar um perfil de CPU do Chrome.
* A at.js 1.3.0 não oferece mais suporte à entrega de conteúdo no Microsoft Internet Explorer 9. Para obter uma lista de navegadores compatíveis, consulte [Navegadores suportados](/help/dev/before-implement/supported-browsers.md). A partir de agora, todas as solicitações serão executadas por `XMLHttpRequest` com suporte ao CORS sem solicitações JSONP. Essa alteração melhora muito a segurança.

## at.js versão 1.2.3

A at.js versão 1.2.3 já está disponível.

* Adiciona suporte para ofertas JSON. As ofertas JSON são suportadas apenas em atividades criadas usando o Experience Composer baseado em formulário. Atualmente, a única maneira de usar as ofertas do JSON é por meio de chamadas diretas à API. Consulte [Criar ofertas JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html).

## at.js versão 1.2.2

A at.js versão 1.2.2 já está disponível.

* Correção de um problema que retornava um erro de JavaScript quando a variável [!DNL Target] biblioteca carregada em uma página usando o modo QUIRKS. (TNT-28312)
* Correção de um problema que causava [!DNL Target] rastreamento de cliques para interromper [!DNL Analytics] chamadas de coleta de dados. (TNT-28261)
* Correção de um problema que causava a falha dos `getOffer() params` quando `targetPageParams()` retornava uma string em branco. (TNT-28359)
* Correção de um problema com geração da ID de sessão ao usar somente x. (TNT-28361)

## at.js versão 1.2.1

A at.js versão 1.2.1 já está disponível.

* Correção de um problema impedido o rastreamento de cliques em que um link com target=&quot;_blank&quot; [!DNL Target] de abrir o link em uma nova guia.

## at.js versão 1.2.0

A at.js versão 1.2 já está disponível como uma versão de manutenção que contém a maioria das correções de problemas. 

* Correção de um problema que impedia ações padrão para casos especiais de rastreamento de cliques. (TNT-28089)
* Correção de um problema no rastreamento de cliques em que um link com `target="_blank"` impedia o de abrir o link em uma nova guia.[!DNL Target] (TNT-28072)
* Endereços IP podem ser usados como domínios de cookies. (TNT-28002)
* Correção de um problema que causava cintilação nas ofertas de redirecionamento com uma mbox global ou outras mboxes regionais. (TNT-27978)
* Correção de um problema no [!UICONTROL Direcionamento de experiência] Falha na configuração da atividade no VEC ao alternar entre Procurar e Compor. (TNT-27942)
* Correção de tratamento incorreto em classes de estilo de cintilação para elementos de rastreamento de cliques. (TNT-27896)
* Correção de um problema que fazia com que os parâmetros globais da mbox se misturassem com todos os parâmetros da mbox. (TNT-27846)
* Alterações feitas para garantir que o Handlebars, o Mustache e outras bibliotecas de modelos do lado do cliente sejam manipuladas adequadamente pela at.js. (TNT-27831)
* Alterações feitas para garantir que `sdidParamExpiry` seja inicializado e passado corretamente para a API do visitante. Esta é uma regressão que foi adicionada à `at.js 1.1.0`. As versões anteriores da at.js não foram afetadas. Isso afeta apenas clientes que usam ofertas de redirecionamento e o A4T. (TNT-27791)
* Alterações feitas para garantir que `SCRIPT` seja executado, independentemente do atributo de tipo que está sendo usado. (TNT-27865)

## at.js versão 1.1.0

**Data:** 2 de agosto de 2017

Os seguintes aprimoramentos e correções estão incluídos na at.js versão 1.1:

* Adição do tratamento de token de resposta. Para obter mais informações, consulte [Tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html).
* Solução de um problema para que `document.currentScript polyfill` não interfira com o Angular 1.X.
* Alterações feitas para garantir que o rastreamento de cliques não interfira na propriedade de visibilidade. Os elementos de rastreamento de cliques são marcados com a classe CSS `at-element-click-tracking`, em vez de `at-element-marker`.

## at.js versão 1.0.0

**Data:** sexta-feira, 7 de julho de 2017

Os seguintes aprimoramentos e correções estão incluídos na at.js versão 1.0:

* Suporte para carregar a at.js de forma assíncrona para carregamentos de página mais rápidos.
* Suporte para pré-ocultar o conteúdo da página ao carregar a at.js de forma assíncrona.
* Mensagem de erro melhorada quando a entrega de conteúdo está desativada.
* Melhorias de desempenho ao entregar várias atividades.
* Suporte ao Compactador YUI.
* Relatório de erros para eventos personalizados durante a entrega da atividade.
* Correção para problemas de desempenho no Microsoft Internet Explorer 11.
* Correção para a função `getOffer()` que retornava um erro em alguns sites.
* Carregue o [!DNL Target] biblioteca de maneira assíncrona. Para obter mais informações, consulte [Perguntas frequentes da at.js](/help/dev/implement/client-side/atjs/target-atjs-faq.md).

## at.js versão 0.9.7

**Data:** segunda-feira, 22 de maio de 2017

Os seguintes aprimoramentos e correções estão incluídos na at.js versão 0.9.7:

* Correção de um problema relacionado a uma chave de ativo que estava faltando nas ações `insertAfter` e `insertBefore` no Visual Experience Composer (VEC). Esses problemas estavam relacionados com a migração de ofertas visuais para modelos de ofertas.

## at.js versão 0.9.6

**Data:** quinta-feira, 13 de abril de 2017

Os seguintes aprimoramentos e correções estão incluídos na at.js versão 0.9.6:

* Suporte à oferta de redirecionamento para A4T. Depois de baixar e instalar a at.js versão 0.9.6, poderá usar as ofertas de redirecionamento nas atividades que usam o [!UICONTROL Adobe Analytics como Fonte dos relatórios para o Target] (A4T). Além da at.js versão 0.9.6, há outros requisitos mínimos que sua implementação deve atender para usar as ofertas de redirecionamento e o A4T. Para obter mais informações e outras informações importantes que você deveria saber, consulte [Perguntas frequentes das Ofertas de redirecionamento - A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html).
* Antes da at.js 0.9.6, quando a API de visitante estava presente na página e a variável `visitorApiTimeout` a configuração era muito agressiva, [!DNL Target] situação em que não foram enviados dados MCID na lista de [!DNL Target] solicitação. Isso pode levar a problemas como ocorrências não corrigidas no [!DNL Analytics] ao usar o A4T.

  Esse comportamento foi alterado na at.js 0.9.6, mesmo que a variável `visitorApiTimeout` é definido para dizer 1 ms, [!DNL Target] O tentará coletar dados de SDID, servidores de rastreamento e IDs do cliente e enviá-los na [!DNL Target] solicitação.

* Adição da configuração `selectorsPollingTimeout`. Para obter mais informações, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
* O formato do formulário de resposta de `getOffer()` foi alterado. Para obter mais informações, consulte [adobe.target.getOffer(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md).
* O registro do console foi adicionado para declarações `<!DOCTYPE>` não suportadas.
* Correção de um problema em que [!DNL Target Classic] os plug-ins do não eram aplicados corretamente quando várias ofertas padrão eram entregues a uma única mbox. (TGT-22664)
* Configuração de cookie aprimorada para domínios de primeiro nível (TLDs) com duas letras para garantir que o cookie da mbox seja definido corretamente para esses domínios (por exemplo, test.no, autodrives.ca e assim por diante).
* O algoritmo para extrair o domínio de nível superior que deve ser usado ao salvar cookies foi alterado na at.js versão 0.9.6. Por causa dessa alteração, os cookies não pode ser salvos em endereços que usam IP. Na maioria das vezes, os endereços IP são usados para fins de teste, mas, como solução alternativa, é possível usar entradas de DNS ou ajustar o arquivo de hosts em uma caixa local.
* Correção das ações de mover e reorganizar quando as propriedades são valores de cadeia de caracteres em vez de números inteiros.

## at.js versão 0.9.4

**Data:** quinta-feira, 19 de janeiro de 2017

* Os nomes das mboxes agora podem conter caracteres especiais, incluindo &quot;E&quot; comercial (&amp;). 

  Para obter uma lista de caracteres especiais permitidos, consulte [Configuração da at.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md).

* Adição da configuração `secureOnly`, que indica se a at.js deve usar somente HTTPS ou pode alternar entre HTTP e HTTPS com base no protocolo da página. Esta é uma configuração avançada cujo padrão é Falso e pode ser substituída por `targetGlobalSettings`.
* A opção Suporte a navegador herdado está disponível na at.js versão 0.9.3 e posteriores. Esta opção foi removida na at.js versão 0.9.4.

## at.js versão 0.9.3

**Data:** segunda-feira, 10 de outubro de 2016

* Garante que as chamadas da mbox sejam acionadas no Microsoft Internet Explorer 11 quando os navegadores herdados estiverem desativados nas configurações da at.js.
* Garante que o conteúdo padrão seja renderizado se uma oferta remota dinâmica falhar (por exemplo, se o URL estiver incorreto e retornar um erro 404).
* Garante que os elementos sejam revelados rapidamente quando os seletores de rastreamento de cliques do VEC não puderem ser encontrados no DOM.

## at.js versão 0.9.2

**Data:** quarta-feira, 21 de setembro de 2016

* Adição de uma configuração `optoutEnabled` para ativar ou desativar a não participação no Gráfico de dispositivos. Se essa configuração for definida como `true` e o visitante tiver desativado o rastreamento, o navegador do visitante não fará chamadas de mbox. O Gráfico de dispositivos está atualmente na versão beta. Esta configuração é definida para `false` por padrão, mas deve ser definido para `true` se você estiver usando o Gráfico de dispositivos.
* Adição do suporte a `CustomEvent` ao mecanismo de notificação. Anteriormente, o mecanismo de notificação de eventos da at.js não podia ser usado por meio das APIs DOM padrão, como `document.addEventListener()`. Agora você pode usar `document.addEventListener()` para assinar eventos at.js, como eventos de solicitação e eventos de renderização de conteúdo.
* Correção de um problema relacionado às ofertas criadas no Visual Experience Composer (VEC). Antes desta versão, [!DNL Target] ocultou os seletores e os exibia apenas quando todos os seletores eram correspondidos. Na at.js 0.9.2 [!DNL Target] exibe os seletores assim que correspondidos.

## at.js versão 0.9.1

**Data:** quinta-feira, 14 de julho de 2016

* Fornece à at.js um tempo limite para o Serviço de ID de visitante, que é independente do tempo limite do próprio serviço.
* Corrige um problema na versão 0.9.0 que afetava as implementações que usavam at.js em algumas páginas e mbox.js (descontinuada) em outras.
* Se você usar [!DNL Adobe Analytics] como fonte de relatórios da atividade, não é necessário especificar um servidor de rastreamento durante a criação da atividade se você estiver usando a mbox.js versão 61 (ou posterior) ou a at.js versão 0.9.1 (ou posterior). A biblioteca at.js envia automaticamente os valores do servidor de rastreamento ao [!DNL Target]. Durante a criação da atividade, é possível deixar o campo Servidor de rastreamento em branco na página Metas e configurações.

## at.js versão 0.9.0

**[!DNL Target]Versão:** 16.6.1

**Data:** 23 de junho de 2016

* Corrige um problema de tela branca ao usar ofertas do VEC. Qualquer pessoa que utilize a at.js deve atualizar para esta nova versão.
* Nova API `registerExtension`.

  Esta nova API permite que os desenvolvedores acessem determinados módulos jQuery usados na at.js para desenvolver extensões (também conhecidos como plug-ins) para a biblioteca. Existem algumas implicações para essa alteração. Isso afeta apenas os usuários que usam esses recursos:

   * A API `getSettings()` () removida, mas a mesma funcionalidade está disponível usando `registerExtension()`.
   * A API `getTracking()` () removida, mas a mesma funcionalidade está disponível usando `registerExtension()`.

   * A extensões existentes (por exemplo, as extensões AngularJS) devem ser atualizadas para usar a abordagem `registerExtension()`.

* Nova API de notificação da at.js.

  O objetivo desse sistema de notificação é fornecer mais informações sobre o que a at.js está fazendo na página e quando há problemas. Um problema comum observado com o VEC: uma versão de TI altera a página, um seletor de VEC é interrompido e o teste para de fornecer conteúdo corretamente. Um objetivo desse sistema de notificação é tornar esse problema de entrega conhecido na página, para que os desenvolvedores possam acessar essas informações, transmiti-las para um sistema como o [!DNL Adobe Analytics] e enviar alertas aos proprietários do negócio, informando-os de que ocorreram problemas no teste.

* Novo método da API `targetGlobalSettings()`.

  Você pode substituir as configurações na biblioteca at.js do em vez de configurá-las na [!DNL Target Standard/Premium] ou usando APIs REST.

## at.js versão 0.8.0

**Data:** 5 de maio de 2016.

Esta é a primeira versão oficial da biblioteca at.js.

A at.js é uma nova biblioteca de implementação do [!DNL Target], projetada para implementações típicas da Web e aplicativos de página única.

A at.js substitui a mbox.js para implementações do [!DNL Adobe Target].

Entre outros benefícios, a at.js melhora o tempo de carregamento de página para implementação da Web, melhora a segurança e fornece opções de implementações melhores para aplicativos de página única.

A at.js contém os componentes que foram incluídos em target.js; portanto, target.js não é mais chamada.

Ao implementar a at.js, esteja ciente do seguinte:

* As versões do Internet Explorer anteriores à 8 não são suportadas.
* A implementação assíncrona significa que integrações legadas, como [!UICONTROL Test&amp;Target para o plug-in do SiteCatalyst], podem não funcionar.
* [!DNL Target]Os plug-ins do que referenciam objetos e métodos da mbox.js não são suportados.
* Todas as chamadas ao [!DNL Target] são feitas por XMLHTTPRequest e o conteúdo é retornado por JSON.
