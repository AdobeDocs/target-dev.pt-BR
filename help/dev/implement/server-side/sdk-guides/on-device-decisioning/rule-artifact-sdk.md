---
title: Baixar, armazenar e atualizar automaticamente o artefato da regra de decisão no dispositivo
description: Saiba como trabalhar com o artefato de regra de decisão no dispositivo ao inicializar o SDK  [!DNL Adobe Target] .
feature: APIs/SDKs
exl-id: be41a723-616f-4aa3-9a38-8143438bd18a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Baixando, armazenando e atualizando automaticamente o artefato de regra por meio do SDK [!DNL Adobe Target]

Essa abordagem é melhor quando você pode inicializar o SDK do [!DNL Adobe Target] ao mesmo tempo em que inicializa e inicia o servidor Web. O artefato da regra será baixado pelo SDK do [!DNL Adobe Target] e armazenado em cache na memória antes que o aplicativo do servidor Web inicie a veiculação de solicitações. Quando o aplicativo Web estiver em execução, todas as decisões do [!DNL Adobe Target] serão executadas usando o artefato de regra na memória. O artefato da regra em cache será atualizado com base no `pollingInterval` especificado durante a etapa de inicialização do SDK.

## Resumo das etapas

1. Instalar o SDK
1. Inicializar o SDK
1. Armazenar e usar o artefato de regra

## 1. Instalar o SDK

>[!BEGINTABS]

>[!TAB NPM]

```javascript {line-numbers="true"}
npm i @adobe/target-nodejs-sdk -P
```

>[!TAB MVN]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.0</version>
</dependency>
```

>[!ENDTABS]

## 2. Inicializar o SDK

1. Primeiro, importe o SDK. Importar para o mesmo arquivo a partir do qual você pode controlar a inicialização do servidor.

   **Node.js**

   ```javascript {line-numbers="true"}
   const TargetClient = require("@adobe/target-nodejs-sdk");
   ```

   **Java**

   ```javascript {line-numbers="true"}
   import com.adobe.target.edge.client.ClientConfig;
   import com.adobe.target.edge.client.TargetClient;
   ```

1. Para configurar o SDK, use o método de criação.

   **Node.js**

   ```javascript {line-numbers="true"}
   const CONFIG = {
       client: "<your target client code>",
       organizationId: "your EC org id",
       decisioningMethod: "on-device",
       pollingInterval : 300000,
       events: {
           clientReady: startWebServer
       }
   };
   
   const TargetClient = TargetClient.create(CONFIG);
   
   function startWebServer() {
       //Adobe Target SDK has now downloaded the JSON Artifacts and is available in the memory.
       //You can start your web server now to serve requests now.
   }
   ```

   **Java**

   ```javascript {line-numbers="true"}
   ClientConfig config = ClientConfig.builder()
       .client("<you target client code>")
       .organizationId("<your EC org id>")
       .build();
   TargetClient targetClient = TargetClient.create(config);
   ```

1. O cliente e a organizationId podem ser recuperados de [!DNL Adobe Target] navegando até **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**, como mostrado aqui.

   &lt;!— Inserir image-client-code.png —>
   ![Página Implementação em Administração no Destino](assets/asset-rule-artifact-3.png)

## 3. Armazene e use o artefato de regra

Não é necessário gerenciar o artefato da regra por conta própria e chamar os métodos do SDK deve ser simples.

>[!BEGINTABS]

>[!TAB Node.js]

```javascript {line-numbers="true"}
//req is the request object from the server request listener method
const targetCookie = req.cookies[TargetClient.TargetCookieName];
const request = {
    context: {
        channel: "web"
    },
    execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner"
        }],
    },
};

TargetClient.getOffers({
    request,
    targetCookie
}).then(function(response) {
    //This Target response is coming from the In-memory Target artifact.
    console.log("Target response", response);
}).catch(function(err) {
    console.error("Target:", err);
})
```

>[!TAB Java]

```java {line-numbers="true"}
MboxRequest mbox = new MboxRequest().name("homepage").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
TargetDeliveryResponse response = targetClient.getOffers(request);
```

>[!ENDTABS]

>[!NOTE]
>
>Na amostra de código acima, o objeto `TargetClient` contém uma referência ao artefato de regra na memória. Quando você usa esse objeto para chamar métodos SDK padrão, ele usa o artefato da regra na memória para a tomada de decisão. Se o aplicativo estiver estruturado de modo que você precise chamar os métodos SDK em arquivos diferentes daquele que inicializa e escuta as solicitações do cliente, e se esses arquivos não tiverem acesso ao objeto TargetClient, você poderá baixar a carga JSON e armazená-la em um arquivo JSON local para ser consumido em outros arquivos, que precisam inicializar o SDK. Isso é explicado na próxima seção, em relação ao [download do artefato de regra usando uma carga JSON](rule-artifact-json.md).

Este é um exemplo que inicia um aplicativo Web após inicializar o SDK [!DNL Adobe Target].

>[!BEGINTABS]

>[!TAB Node.js]

```javascript {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
    client: "<your target client code>",
    organizationId: "your EC org id",
    decisioningMethod: "on-device",
    pollingInterval : 300000,
    events: {
        clientReady: startWebServer
    }
};

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());

function saveCookie(res, cookie) {
  if (!cookie) {
    return;
  }

  res.cookie(cookie.name, cookie.value, {maxAge: cookie.maxAge * 1000});
}

const getResponseHeaders = () => ({
  "Content-Type": "text/html",
  "Expires": new Date().toUTCString()
});

function sendSuccessResponse(res, response) {
  res.set(getResponseHeaders());
  saveCookie(res, response.targetCookie);
  res.status(200).send(response);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

function startWebServer() {
    app.get('/*', async (req, res) => {
    const targetCookie = req.cookies[TargetClient.TargetCookieName];
    const request = {
        execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner" // Ensure that you have a LIVE Activity running on this location
        }]
        }};

    try {
        const response = await targetClient.getOffers({ request, targetCookie });
        sendSuccessResponse(res, response);
    } catch (error) {
        console.error("Target:", error);
        sendErrorResponse(res, error);
    }
    });

    app.listen(3000, function () {
    console.log("Listening on port 3000 and watching!");
    });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

@Controller
public class TargetController {

  private TargetClient targetClient;

  TargetController() {
    // You should instantiate TargetClient in a Bean and inject the instance into this class 
    // but we show the code here for demonstration purpose.
    ClientConfig config = ClientConfig.builder()
        .client("<you target client code>")
        .organizationId("<your EC org id>")
        .build();
    targetClient = TargetClient.create(config);
  }

  @GetMapping("/")
  public String homePage() {
    MboxRequest mbox = new MboxRequest().name("homepage").index(0);
    TargetDeliveryRequest request = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
        .build();
    TargetDeliveryResponse response = targetClient.getOffers(request);
    // ...
  }
}
```

>[!ENDTABS]
