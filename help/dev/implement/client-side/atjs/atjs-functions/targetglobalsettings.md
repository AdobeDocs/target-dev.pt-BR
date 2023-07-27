---
keywords: serverstate, targetGlobalSettings, targetglobalsettings, globalSettings, globalsettings, configurações globais, at.js, funções, função, clientCode, clientcode, serverDomain, serverdomain, cookieDomain, serverstate5, serverstate6, serverstate7, serverstate8, serverstate9, targetGlobalSettings0, targetGlobalSettings1, targetGlobalSettings2, targetGlobalSettings3, targetGlobalSettings4, targetGlobalSettings5, cookiedomain, crossDomain, crossdomain, timeout, global MboxAutoCreate, visitorApiTimeout, defaultContentHiddenStyle, defaultContentVisibleStyle, bodyHiddenStyle, bodyHidingEnabled, imsOrgId, secureOnly, overrideMboxEdgeServer, overrideMboxEdgeServerTimeout, cookiedomain5, cookiedomain6, cookiedomain7, cookiedomain8, cookiedomain9, crossDomain0, crossDomain1, crossDomain2, crossDomain2 3, crossDomain4, crossDomain5, optoutEnabled, optout, opt out, seletoresPollingTimeout, dataProviders, Personalização híbrida, deviceIdLifetime
description: Use o [!UICONTROL targetGlobalSettings()] para a [!DNL Adobe Target] Biblioteca JavaScript at.js para substituir configurações em vez de usar o [!DNL Target] Interface do usuário ou APIs REST.
title: Como usar o [!UICONTROL targetGlobalSettings()] Função?
feature: at.js
exl-id: f6218313-6a70-448e-8555-b7b039e64b2c
source-git-commit: d5d25c6a559dafe446d26cca6c03d8e693cbd508
workflow-type: tm+mt
source-wordcount: '2521'
ht-degree: 70%

---

# [!UICONTROL targetGlobalSettings()]

É possível substituir as configurações na biblioteca at.js usando `[!UICONTROL targetGlobalSettings()]`, em vez de configurá-los na variável [!DNL Target] ou usando APIs REST.

## Configurações

É possível anular pelas seguintes configurações:

### artifactLocation

* **Tipo**: String
* **Valor padrão**: Nenhuma
* **Descrição**: um url totalmente qualificado para o [artefato da regra de decisão no dispositivo](../../../server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)

### bodyHiddenStyle

* **Tipo**: String
* **Valor padrão**: corpo { opacidade: 0 }
* **Descrição**: usado apenas quando `globalMboxAutocreate === true` para minimizar a chance de cintilação.

  Para obter mais informações, consulte [Como o at.js gerencia a cintilação](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

### bodyHidingEnabled

* **Tipo**: Booleano
* **Valor padrão**: verdadeiro
* **Descrição**: usado para controlar a cintilação quando a `target-global-mbox` é usada para entregar ofertas criadas no Visual Experience Composer, também conhecido como ofertas visuais.

### clientCode

* **Tipo**: String
* **Valor padrão**: valor definido pela interface do usuário.
* **Descrição**: representa o código de cliente.

### cookieDomain

* **Tipo**: String
* **Valor padrão**: se possível, definir como domínio de nível superior.
* **Descrição**: representa o domínio usado ao salvar cookies.

### crossDomain

* **Tipo**: String
* **Valor padrão**: valor definido pela interface do usuário.
* **Descrição**: indica se o rastreamento de domínio cruzado está ativado ou não. Os valores permitidos dependem da versão da at.js. Para at.js v1.*x*, especifique se os recursos entre domínios são `disabled` (navegadores definem cookies no seu domínio (somente cookies primários), `x only` (os navegadores definem cookies no [!DNL Target]somente), ou ambos, selecionando `enabled` (os navegadores definem cookies próprios e de terceiros). Para at.js v2.10 e posterior, especifique se os recursos entre domínios são `enabled` (os navegadores definem cookies próprios e de terceiros) ou `disabled` (os navegadores não definem cookies de terceiros).

### cspScriptNonce

* **Tipo**: consulte a [Política de segurança de conteúdo](#content-security-policy) abaixo.
* **Valor padrão**: consulte a [Política de segurança de conteúdo](#content-security-policy) abaixo.
* **Descrição**: consulte a [Política de segurança de conteúdo](#content-security-policy) abaixo.

### cspStyleNonce

* **Tipo**: consulte a [Política de segurança de conteúdo](#content-security-policy) abaixo.
* **Valor padrão**: consulte a [Política de segurança de conteúdo](#content-security-policy) abaixo.
* **Descrição**: consulte a [Política de segurança de conteúdo](#content-security-policy) abaixo.

### dataProviders

* **Tipo**: consulte os [Provedores de dados](#data-providers) abaixo.
* **Valor padrão**: consulte os [Provedores de dados](#data-providers) abaixo.
* **Descrição**: consulte os [Provedores de dados](#data-providers) abaixo.

### decisioningMethod

* **Tipo**: String
* **Valor padrão**: lado do servidor
* **Outros valores**: no dispositivo, híbrido
* **Descrição**: consulte os Métodos de decisão abaixo.

  **Métodos de decisão**

  Com a decisão no dispositivo, [!DNL Target] A apresenta uma nova configuração chamada Método de decisão que determina como a at.js fornece suas experiências. O `decisioningMethod` tem três valores: somente do lado do servidor, somente no dispositivo e híbrido. Quando o `decisioningMethod` é definido no `targetGlobalSettings()`, ele age como o método de decisão padrão para todas as decisões do [!DNL Target].

  **Somente no lado do servidor**:

  Somente no lado do servidor é o método de decisão padrão definido imediatamente quando a at.js 2.5+ é implementada e implantada em suas propriedades da Web.

  Usar somente no lado do servidor como configuração padrão significa que todas as decisões são tomadas na rede de borda do [!DNL Target], o que envolve uma chamada de servidor de bloqueio. Essa abordagem pode apresentar latência incremental, mas também oferece benefícios significativos, como a capacidade de aplicar [!DNL Target]Os recursos de aprendizado de máquina do que incluem [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) e [Direcionamento automático](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) atividades.

  Além disso, aprimorar suas experiências personalizadas usando [!DNL Target]O perfil de usuário do, que é mantido em sessões e canais, pode fornecer resultados significativos para sua empresa.

  Por fim, somente no lado do servidor permite usar a Adobe Experience Cloud e refinar públicos-alvo que podem ser direcionados por meio de segmentos do Audience Manager e do Adobe Analytics.

  **Somente no dispositivo**:

  Somente no dispositivo é o método de decisão que deve ser definido na at.js 2.5+ quando a tomada de decisão no dispositivo precisar ser usada somente em suas páginas da Web.

  A decisão no dispositivo entrega experiências e atividades de personalização em uma velocidade extremamente rápida, pois as decisões são tomadas a partir de um artefato de regras em cache que contém todas as suas atividades qualificadas para decisões no dispositivo.

  Para saber mais sobre quais atividades se qualificam para decisões no dispositivo, consulte a seção de recursos compatíveis.

  Esse método de decisão deve ser usado somente se o desempenho for altamente crítico em todas as páginas que exigem decisões do [!DNL Target]. Além disso, lembre-se de que, quando esse método de decisão é selecionado, as atividades do [!DNL Target] que não se qualificam para a tomada de decisão no dispositivo não são entregues ou executadas. A biblioteca at.js 2.5+ está configurada para procurar somente pelo artefato de regras em cache para tomar decisões.

  **Híbrido**:

  O método de decisão híbrido é o que deve ser definido na at.js 2.5+, quando a tomada de decisão no dispositivo e as atividades que exigem uma chamada de rede para o [!DNL Adobe Target] A rede de borda deve ser executada.

  Ao gerenciar atividades de decisão no dispositivo e atividades no lado do servidor, você pode achar complicado e cansativo pensar em como implantar e provisionar o [!DNL Target] em suas páginas. Com o método de decisão híbrido, o [!DNL Target] sabe quando deve fazer uma chamada de servidor para a rede de borda do , no caso de atividades que exigem execução no lado do servidor, e quando deve apenas executar decisões no dispositivo.[!DNL Adobe Target]

  O artefato de regras JSON inclui metadados para informar à at.js se uma mbox tem uma atividade do lado do servidor em execução ou uma atividade de decisão no dispositivo. Esse método de decisão garante que as atividades que você pretende entregar rapidamente sejam realizadas por meio de decisões no dispositivo e, para atividades que exigem personalização mais avançada orientada por aprendizado de máquina, essas atividades são realizadas por meio da [!DNL Adobe Target] Rede de borda.

### defaultContentHiddenStyle

* **Tipo**: String
* **Valor padrão**: visibilidade: oculto
* **Descrição**: usado apenas para mboxes de encapsulamento que usam DIV com nome de classe “mboxDefault” e são executadas por meio de `mboxCreate()`, `mboxUpdate()`, ou `mboxDefine()` para ocultar conteúdo padrão.

### defaultContentVisibleStyle

* **Tipo**: String
* **Valor padrão**: visibilidade: visível
* **Descrição**: usado apenas para mboxes de encapsulamento que usam DIV com nome de classe “mboxDefault” e são executadas por meio de `mboxCreate()`, `mboxUpdate()`, ou `mboxDefine()` para revelar uma oferta aplicada, caso exista, ou conteúdo padrão.

### deviceIdLifetime

* **Tipo**: número
* **Valor padrão**: 63244800000 ms = 2 anos
* **Descrição**: a quantidade de tempo `deviceId` é mantida nos cookies.

>[!NOTE]
>
>A configuração deviceIdLifetime pode ser substituída na versão 2.3.1 ou posterior da at.js.

### ativado

* **Tipo**: Booleano
* **Valor padrão**: verdadeiro
* **Descrição**: quando habilitada, uma solicitação do [!DNL Target] para recuperar experiências e a manipulação de DOM para renderizar as experiências são executadas automaticamente. Além disso, as chamadas do [!DNL Target] podem ser executadas manualmente por meio de `getOffer(s)` / `applyOffer(s)`.

  Quando desativadas, as solicitações do [!DNL Target] não são executadas automática ou manualmente.

### globalMboxAutoCreate

* **Tipo**: número
* **Valor padrão**: valor definido pela interface do usuário.
* **Descrição**: indica se a solicitação global de mbox deve ser disparada ou não.

### imsOrgId

* **Tipo**: String
* **Valor padrão**: verdadeiro
* **Descrição**: representa a ID de organização do IMS.

### optinEnabled

* **Tipo**: Booleano
* **Valor padrão**: falso
* **Descrição**: [!DNL Target] O oferece suporte à funcionalidade de opt-in por meio do Adobe Experience Platform, para ajudar a apoiar a estratégia de gerenciamento de consentimento. A funcionalidade de opt-in permite que os clientes controlem como e quando a tag do [!DNL Target] é acionada. Além disso, há uma opção por meio do Adobe Experience Platform para pré-aprovar o [!DNL Target] tag. Para ativar a capacidade de usar a aceitação na biblioteca at.js do [!DNL Target], você deve adicionar a configuração `optinEnabled=true`. No Adobe Experience Platform, você deve selecionar &quot;ativar&quot; na lista suspensa Aceitação de GDPR, na exibição de instalação da extensão. Consulte a [documentação da Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) para obter mais detalhes. Para obter mais informações sobre essa configuração, que está relacionada às regulamentações de privacidade e proteção de dados, incluindo o Regulamento Geral sobre a Proteção de Dados (GDPR) da União Europeia e a Lei de Privacidade do Consumidor da Califórnia (CCPA), consulte [Privacidade e regulamentos sobre proteção de dados](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

### optoutEnabled

* **Tipo**: Booleano
* **Valor padrão**: falso
* **Descrição**[!DNL Target]: indica se o deve chamar a função `isOptedOut()` da API de visitante. Isso é parte da ativação do gráfico de dispositivos.

### overrideMboxEdgeServer

* **Tipo**: Booleano
* **Valor padrão**: verdadeiro (a partir da at.js versão 1.6.2)
* **Descrição**: indica se deve-se usar o domínio `<clientCode>.tt.omtrdc.net` ou o domínio `mboxedge<clusterNumber>.tt.omtrdc.net`.

  Se este valor for true, o domínio `mboxedge<clusterNumber>.tt.omtrdc.net` será salvo em um cookie. No momento, não funciona com [CNAME](/help/dev/before-implement/implement-cname-support-in-target.md) ao usar versões da at.js anteriores à 1.8.2 e 2.3.1. Se isso for um problema para você, considere [atualizar a at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md) para uma versão mais recente e compatível.

### overrideMboxEdgeServerTimeout

* **Tipo**: número
* **Valor padrão**: 1860000 => 31 minutos
* **Descrição**: indica o tempo de vida do cookie que contém o valor `mboxedge<clusterNumber>.tt.omtrdc.net`.

### pageLoadEnabled

* **Tipo**: Booleano
* **Valor padrão**: verdadeiro
* **Descrição**: quando ativado, recupera automaticamente as experiências que devem ser retornadas ao carregar a página.

### pollingInterval

* **Tipo**: número
* **Valor padrão**: 300000 (cinco minutos em milissegundos)
* **Descrição**: intervalo em que a at.js busca uma nova versão de um artefato de decisão no dispositivo e atualiza o cache. 300000 é o valor mínimo permitido para `pollingInterval`.

### secureOnly

* **Tipo**: Booleano
* **Valor padrão**: falso
* **Descrição**: indica se a at.js deve usar somente HTTPS ou se pode alternar entre HTTP e HTTPS com base no protocolo da página. Quando definido como verdadeiro, o secureOnly também define os atributos Secure e SameSite como o cookie da mbox.

### selectorsPollingTimeout

* **Tipo**: número
* **Valor padrão**: 5000 ms = 5 s
* **Descrição**: na at.js 0.9.6, o [!DNL Target] apresentou essa nova configuração, que pode ser substituída por meio de `targetGlobalSettings`.

  A configuração `selectorsPollingTimeout` representa quanto tempo o cliente está disposto a esperar até que todos os elementos identificados por seletores sejam exibidos na página.

  Atividades criadas pelo Visual Experience Composer (VEC) têm ofertas que contêm seletores.

### serverDomain

* **Tipo**: String
* **Valor padrão**: valor definido pela interface do usuário.
* **Descrição**[!DNL Target]: representa o servidor de borda do 

### serverState

* **Tipo**: consulte [Personalização híbrida](#hybrid-personalization) abaixo.
* **Valor padrão**: consulte [Personalização híbrida](#hybrid-personalization) abaixo.
* **Descrição**: consulte [Personalização híbrida](#hybrid-personalization) abaixo.

### telemetryEnabled

* **Tipo**: Booleano
* **Valor padrão**: verdadeiro
* **Descrição**: quando ativado, o Adobe coleta os dados de uso de recursos do SDK e de telemetria de desempenho. Os dados pessoais não são coletados.

### timeout

* **Tipo**: número
* **Valor padrão**: valor definido pela interface do usuário.
* **Descrição**: representa o tempo limite da solicitação da borda do [!DNL Target].

### viewsEnabled {#viewsenabled}

* **Tipo**: Booleano
* **Valor padrão**: verdadeiro
* **Descrição**: quando ativado, as exibições são recuperadas automaticamente quando a página é carregada. Quando `triggerView` for chamado, as exibições aplicáveis serão exibidas no navegador. Se essa opção estiver desativada, as exibições não serão recuperadas no momento do carregamento da página e `triggerView` não faz nada. As exibições são compatíveis com a at.js 2.somente *x.*

### visitorApiTimeout

* **Tipo**: número
* **Valor padrão**: 2000 ms = 2 s
* **Descrição**: representa o tempo limite da solicitação da API de visitante.

## Uso

Esta função pode ser definida antes que a at.js seja carregada ou em **Administração** > **Implementação** > **Editar configurações da at.js** > **Configurações de código** > **Cabeçalho da biblioteca**.

O campo Cabeçalho da biblioteca permite que você entre no JavaScript do formulário gratuito. O código de personalização deve ser semelhante ao seguinte exemplo:

```javascript {line-numbers="true"}
window.targetGlobalSettings = {
   timeout: 200, // using custom timeout
   visitorApiTimeout: 500, // using custom API timeout
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com
};
```

## Provedores de dados {#data-providers}

Essa configuração permite que os clientes reúnam dados de provedores de dados de terceiros, como Demandbase, BlueKai e serviços personalizados, além de enviar os dados para [!DNL Target] como parâmetros mbox na solicitação global da mbox. Ela é compatível com a coleta de dados de múltiplos provedores via solicitações síncronas e assíncronas. Usar esta abordagem facilita o gerenciamento de cintilação ou conteúdo padrão da página, enquanto inclui tempos limites independentes para cada provedor para limitar o impacto sobre o desempenho da página

>[!NOTE]
>
>Os provedores de dados exigem o at.js 1.3 ou posterior.

Os seguintes vídeos contêm mais informações:

| Vídeo | Descrição |
|--- |--- |
| [Uso de provedores de dados do Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html) | Os provedores de dados são uma função que permite passar dados de terceiros facilmente para o Target. Um terceiro pode ser um serviço de clima, um DMP ou até mesmo o seu próprio serviço Web. É possível então usar esses dados para criar públicos-alvo, conteúdo de direcionamento e enriquecer o perfil do visitante. |
| [Implementação de provedores de dados no Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html) | Detalhes de implementação e exemplos de como usar o Adobe [!DNL Target]O recurso dataProviders do para recuperar dados de provedores de dados de terceiros e transmiti-los no [!DNL Target] solicitação. |

A configuração `window.targetGlobalSettings.dataProviders` é uma matriz de provedores de dados.

Cada provedor de dados tem a seguinte estrutura:

| Chave | Tipo | Descrição |
|--- |--- |--- |
| name | String | Nome do provedor. |
| version | String | Versão do provedor. Essa tecla será usada para evolução do provedor. |
| timeout | Número | Representa o tempo limite do provedor se essa for uma solicitação de rede.  Essa tecla é opcional. |
| provider | Função | A função que contém a lógica de obtenção de dados do provedor.<p>A função tem um único parâmetro obrigatório: `callback`. O parâmetro retorno de chamada é uma função que só deve ser invocada quando os dados forem obtidos com êxito ou houver um erro.<p>O retorno de chamada espera dois parâmetros:<ul><li>error: Indica que ocorreu um erro. Se tudo estiver OK, este parâmetro deve ser definido como nulo.</li><li>parâmetros: um objeto JSON, representando os parâmetros que serão enviados em um [!DNL Target] solicitação.</li></ul> |

O exemplo a seguir mostra onde o provedor de dados está usando a execução sincrônica:

```javascript {line-numbers="true"}
var syncDataProvider = {
  name: "simpleDataProvider",
  version: "1.0.0",
  provider: function(callback) {
    callback(null, {t1: 1});
  }
};

window.targetGlobalSettings = {
  dataProviders: [
    syncDataProvider
  ]
};
```

Após at.js processar `window.targetGlobalSettings.dataProviders`[!DNL Target], a solicitação do conterá um novo parâmetro: `t1=1`.

Veja a seguir um exemplo de se os parâmetros que você deseja adicionar à variável [!DNL Target] As solicitações de são buscadas de um serviço de terceiros, como Bluekai, Demandbase e assim por diante:

```javascript {line-numbers="true"}
var blueKaiDataProvider = {
   name: "blueKai",
   version: "1.0.0",
   provider: function(callback) {
      // simulating network request
     setTimeout(function() {
       callback(null, {t1: 1, t2: 2, t3: 3});
     }, 1000);
   }
}

window.targetGlobalSettings = {
   dataProviders: [
      blueKaiDataProvider
   ]
};
```

Após at.js processar `window.targetGlobalSettings.dataProviders`[!DNL Target], a solicitação do conterá novos parâmetros: `t1=1`, `t2=2` e `t3=3`.

O exemplo a seguir usa provedores de dados para coletar dados da API de tempo e enviá-los como parâmetros em uma [!DNL Target] solicitação. A variável [!DNL Target] terá parâmetros adicionais, como `country` e `weatherCondition`.

```javascript {line-numbers="true"}
var weatherProvider = {
      name: "weather-api",
      version: "1.0.0",
      timeout: 2000,
      provider: function(callback) {
        var API_KEY = "caa84fc6f5dc77b6372d2570458b8699";
        var lat = 44.426767399999996;
        var lon = 26.1025384;
        var url = "//api.openweathermap.org/data/2.5/weather?";
        var data = {
          lat: lat,
          lon: lon,
          appId: API_KEY
        }

        $.ajax({
          type: "GET",
                url: url,
          dataType: "json",
          data: data,
          success: function(data) {
            console.log("Weather data", data);
            callback(null, {
              country: data.sys.country,
              weatherCondition: data.weather[0].main
            });
          },
          error: function(err) {
            console.log("Error", err);
            callback(err);
          }
        });
      }
    };

    window.targetGlobalSettings = {
      dataProviders: [weatherProvider]
    };
```

Leve em consideração o seguinte ao trabalhar com a configuração `dataProviders`:

* Se os provedores de dados adicionados a `window.targetGlobalSettings.dataProviders` forem assíncronos, serão executados em paralelo. A solicitação da API de visitante será executada em paralelo com funções adicionadas a `window.targetGlobalSettings.dataProviders` para permitir um tempo mínimo de espera.
* at.js não tentará armazenar os dados em cache. Se o provedor de dados obtiver os dados apenas uma vez, deverá certificar-se de que os dados estão armazenados em cache e, quando a função de provedor for invocada, servir os dados do cache para a segunda invocação.

## Política de segurança de conteúdo

A at.js 2.3.0+ oferece suporte à configuração de nonces da Política de segurança de conteúdo nas tags SCRIPT e STYLE, que são inseridas no DOM da página ao aplicar as tags entregues [!DNL Target] ofertas.

Os nonces de SCRIPT e STYLE devem ser definidos em `targetGlobalSettings.cspScriptNonce` e `targetGlobalSettings.cspStyleNonce` correspondentemente, antes do carregamento da at.js 2.3.0+. Veja um exemplo abaixo:

```javascript {line-numbers="true"}
...
<head>
 <script nonce="<script_nonce_value>">
window.targetGlobalSettings = {
  cspScriptNonce: "<csp_script_nonce_value>",
  cspStyleNonce: "<csp_style_nonce_value>"
};
 </script>
 <script nonce="<script_nonce_value>" src="at.js"></script>
...
</head>
...
```

Depois que as configurações `cspScriptNonce` e `cspStyleNonce` são especificadas, a at.js 2.3.0+ as define como atributos nonce em todas as tags SCRIPT e STYLE inseridas no DOM ao aplicar ofertas do [!DNL Target]

## Personalização híbrida

O `serverState`[!DNL Target] é uma configuração disponível na at.js v2.2+ que pode ser usada para otimizar o desempenho da página quando uma integração híbrida do é implementada. A integração híbrida significa que você está usando a at.js v2.2+ no lado do cliente e a API de entrega ou uma [!DNL Target] SDK no lado do servidor para fornecer experiências. O `serverState` fornece ao at.js v2.2+ a capacidade de aplicar experiências diretamente de conteúdo buscado no lado do servidor e retornado ao cliente como parte da página que está sendo veiculada.

### Pré-requisitos

Você deve ter uma integração híbrida do [!DNL Target].

* **Lado do servidor**: Você deve usar o [API de entrega](/help/dev/implement/delivery-api/overview.md) ou [SDKs do Target](/help/dev/implement/server-side/sdk-guides/getting-started/getting-started.md).
* **Lado do cliente**: você deve usar a [at.js versão 2.2 ou posterior](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

### Amostras de código

Para entender melhor como isso funciona, veja abaixo os exemplos de código que você teria no servidor. O código presume que você está usando o [SDK Node.js do Target](https://github.com/adobe/target-nodejs-sdk).

```javascript {line-numbers="true"}
// First, we fetch the offers via Target Node.js SDK API, as usual
const targetResponse = await targetClient.getOffers(options);
// A successfull response will contain Target Delivery API request and response objects, which we need to set as serverState
const serverState = {
  request: targetResponse.request,
  response: targetResponse.response
};
// Finally, we should set window.targetGlobalSettings.serverState in the returned page, by replacing it in a page template, for example
const PAGE_TEMPLATE = `
<!doctype html>
<html>
<head>
  ...
  <script>
    window.targetGlobalSettings = {
      overrideMboxEdgeServer: true,
      serverState: ${JSON.stringify(serverState, null, " ")}
    };
  </script>
  <script src="at.js"></script>
</head>
...
</html>
`;
// Return PAGE_TEMPLATE to the client ...
```

Uma amostra de `serverState` do objeto JSON para pré-busca de visualização é exibida da seguinte maneira:

```javascript {line-numbers="true"}
{
 "request": {
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "context": {
   "channel": "web",
   "timeOffsetInMinutes": 0
  },
  "experienceCloud": {
   "analytics": {
    "logging": "server_side",
    "supplementalDataId": "7D3AA246CC99FD7F-1B3DD2E75595498E"
   }
  },
  "prefetch": {
   "views": [
    {
     "address": {
      "url": "my.testsite.com/"
     }
    }
   ]
  }
 },
 "response": {
  "status": 200,
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "testclient",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
   "views": [
    {
     "name": "home",
     "key": "home",
     "options": [
      {
       "type": "actions",
       "content": [
        {
         "type": "setHtml",
         "selector": "#app > DIV.app-container:eq(0) > DIV.page-container:eq(0) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
         "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
         "content": "<span style=\"color:#FF0000;\">Latest</span> Products for 2020"
        }
       ],
       "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
       "responseTokens": {
        "profile.memberlevel": "0",
        "geo.city": "dublin",
        "activity.id": "302740",
        "experience.name": "Experience B",
        "geo.country": "ireland"
       }
      }
     ],
     "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    }
   ]
  }
 }
}
```

Depois que a página é carregada no navegador, a at.js aplica todas as ofertas do [!DNL Target] de `serverState` imediatamente, sem disparar chamadas de rede para a borda do [!DNL Target]. Além disso, a at.js pré-oculta apenas os elementos DOM para os quais as ofertas do [!DNL Target] estão disponíveis no conteúdo no lado do servidor, afetando positivamente o desempenho de carregamento da página e a experiência do usuário final.

### Observações importantes

Considere o seguinte ao usar `serverState`:

* No momento, a at.js v2.2 oferece suporte somente para experiências entregues via serverState para:

   * Atividades criadas pelo VEC que são executadas no carregamento da página.
   * Exibições pré-buscadas.

     No caso de aplicativos de página única que usam Exibições do [!DNL Target] e `triggerView()` na API da at.js, a at.js v2.2 armazena em cache o conteúdo de todas as exibições pré-buscadas no lado do servidor e as aplica assim que cada exibição é acionada por meio do `triggerView()`, novamente sem disparar chamadas adicionais de busca de conteúdo para o [!DNL Target].

   * **Observação**: Atualmente, as mboxes recuperadas no lado do servidor não são compatíveis com o `serverState`.

* Ao aplicar as ofertas `serverState`, a at.js considera as configurações `pageLoadEnabled` e `viewsEnabled`, por exemplo, as ofertas de carregamento de página não serão aplicadas se a configuração `pageLoadEnabled` for definida como falso.

  Para ativar essas configurações, habilite a alternância em **Administração > Implementação > Edição > Carregamento de página ativado**.

  ![Configurações do carregamento de página ativado](../../assets/page-load-enabled-setting.png)

* Se estiver usando `serverState` e tags de `<script>` no conteúdo retornado, certifique-se que o conteúdo HTML usa `<\/script>` em vez de `</script>`. Se usar `</script>`, o navegador interpretará `</script>` como o final de um SCRIPT inline e poderá quebrar a página HTML.

### Recursos adicionais

Para saber mais sobre como o `serverState` funciona, confira os seguintes recursos:

* [Código de exemplo](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/advanced-atjs-integration-serverstate).
* [Aplicativo de página única (SPA) de exemplo com `serverState`](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/react-shopping-cart-demo).
