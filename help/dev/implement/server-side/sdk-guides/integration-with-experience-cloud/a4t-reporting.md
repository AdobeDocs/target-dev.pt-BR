---
title: Integração com os relatórios do Experience Cloud A4T
description: Integração com o Experience Cloud, Relatórios do A4T, Integração do Analytics for Target
keywords: api de entrega, lado do servidor, lado do servidor, integração, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 7%

---

# Relatórios do Analytics for Target (A4T)

O [!DNL Adobe Target] oferece suporte aos relatórios do A4T para decisões no dispositivo e atividades do Target do lado do servidor. Há duas opções de configuração para ativar os relatórios do A4T:

* [!DNL Adobe Target] encaminha automaticamente a carga de análise para [!DNL Adobe Analytics] ou
* O usuário solicita a carga de análise de [!DNL Adobe Target]. ([!DNL Adobe Target] retorna a carga [!DNL Adobe Analytics] para o chamador.)

>[!NOTE]
>
>A decisão no dispositivo só oferece suporte aos relatórios do A4T, dos quais o [!DNL Adobe Target] encaminha automaticamente a carga de análise para [!DNL Adobe Analytics]. Não há suporte para a recuperação da carga de análise de [!DNL Adobe Target].

## Pré-requisitos

1. Configure a atividade na interface do usuário do [!DNL Adobe Target] com [!DNL Adobe Analytics] como fonte de relatórios e verifique se as contas estão habilitadas para A4T.
1. O usuário da API gera a ID de visitante da Adobe Marketing Cloud e garante que essa ID esteja disponível quando a solicitação do Target for executada.

## [!DNL Adobe Target] encaminha automaticamente a carga do Analytics

[!DNL Adobe Target] pode encaminhar automaticamente a carga de análise para [!DNL Adobe Analytics] se os seguintes identificadores forem fornecidos:

1. `supplementalDataId`: A ID usada para compilar entre [!DNL Adobe Analytics] e [!DNL Adobe Target]. Para que [!DNL Adobe Target] e [!DNL Adobe Analytics] compilem os dados corretamente, o mesmo `supplementalDataId` precisa ser passado para [!DNL Adobe Target] e [!DNL Adobe Analytics].
1. `trackingServer`: O Servidor [!DNL Adobe Analytics].

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "server_side",
        supplementalDataId: "7D3AA246CC99FD7F-1B3DD2E75595498E",
        trackingServer: "jimsbrims.sc.omtrds.net"
      }
    }, 
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .trackingServer("jimsbrims.sc.omtrds.net")
        .logging(LoggingType.SERVER_SIDE)
        .supplementalDataId("7D3AA246CC99FD7F-1B3DD2E75595498E");
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## O usuário recupera a carga de análise de [!DNL Adobe Target]

Um usuário pode recuperar a carga [!DNL Adobe Analytics] de determinada mbox e enviá-la para [!DNL Adobe Analytics] por meio da [API de Inserção de Dados](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Quando uma solicitação [!DNL Adobe Target] for acionada, passe `client_side` para o campo `logging` na solicitação. Isso retornará uma carga se a mbox especificada estiver presente em uma atividade que usa o Analytics como fonte de relatórios.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const targetClient = TargetClient.create(CONFIG);
targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "client_side"
      }
    },  
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .logging(LoggingType.CLIENT_SIDE);
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Depois de especificar `logging = client_side`, você receberá a carga no campo mbox.

Se a resposta do Target contiver qualquer item na propriedade `analytics -> payload`, encaminhe-a como está para [!DNL Adobe Analytics]. [!DNL Adobe Analytics] sabe como processar esta carga. Isso pode ser feito em uma solicitação GET usando o seguinte formato:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Parâmetros e variáveis da string de consulta

| Nome do campo | Obrigatório | Descrição |
| --- | --- | --- |
| `rsid` | Sim | A ID do conjunto de relatórios |
| `pe` | Sim | Evento de página. Sempre definida como `tnt` |
| `tnta` | Sim | Carga do Analytics retornada pelo servidor Target em `analytics -> payload -> tnta` |
| `mid` | Sim | ID de visitante da Marketing Cloud |

### Valores de cabeçalho obrigatórios

| Nome do cabeçalho | Valor do cabeçalho |
| --- | --- |
| Host | Servidor de coleta de dados do Analytics (ex.: `adobeags421.sc.omtrdc.net`) |

### Exemplo de chamada Get HTTP da Inserção de dados A4T

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```
