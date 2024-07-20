---
title: Integração com segmentos do Experience Cloud AAM
description: Integração com o Experience Cloud, integração com o Audience Manager
keywords: api de entrega, lado do servidor, lado do servidor, integração, audience manager, aam
exl-id: c21e0200-23ba-4a0b-adf4-38e03c087f00
feature: Implement Server-side
source-git-commit: e3f14e97fa48ffb1f07b29aca5711d16e75faa80
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 4%

---

# Segmentos do AAM

[!DNL Adobe Audience Manager] segmentos podem ser aproveitados por meio de [!DNL Adobe Target] SDKs. Para aproveitar os segmentos do AAM, os seguintes campos precisam ser fornecidos:

>[!NOTE]
>
>Segmentos de AAM não são compatíveis com atividades de decisão no dispositivo.

| Nome do campo | Obrigatório | Descrição |
| --- | --- | --- |
| `locationHint` | Sim | A DCS Location Hint é usada para determinar qual terminal DCS AAM deve ser acessado para recuperar o perfil. Deve ser >= 1. |
| `marketingCloudVisitorId` | Sim | ID de visitante da Marketing Cloud |
| `blob` | Sim | AAM Blob é usado para enviar dados adicionais para o AAM. Não pode estar em branco e seu tamanho &lt;= 1024. |

O SDK preencherá automaticamente esses campos para você ao fazer uma chamada do método `getOffers`, mas será necessário garantir que um cookie de visitante válido seja fornecido. Para obter esse cookie, você precisa implementar VisitorAPI.js no navegador.

## Guia de implementação

### Uso de cookies

Os cookies são usados para correlacionar [!DNL Adobe Audience Manager] solicitações com [!DNL Adobe Target] solicitações. Estes são os cookies usados nesta implementação.

| Cookie | Nome | Descrição |
| --- | --- | --- |
| cookie de visitante | `AMCVS_XXXXXXXXXXXXXXXXXXXXXXXX%40AdobeOrg` | Este cookie é definido por `VisitorAPI.js` quando é inicializado com `visitorState` da resposta de destino `getOffers`. |
| cookie do target | `mbox` | Seu servidor Web deve definir este cookie usando o nome e o valor de `targetCookie` da resposta de destino `getOffers`. |

### Visão geral das etapas

Suponha que um usuário insira um URL em um navegador que envie uma solicitação para o servidor Web. Ao atender a essa solicitação:

1. O servidor lê os cookies de visitante e de destino da solicitação.
1. O servidor faz uma chamada para o método `getOffers` do SDK [!DNL Target], especificando os cookies de visitante e de destino, se disponíveis.
1. Quando a chamada `getOffers` é atendida, os valores para `targetCookie` e `visitorState` da resposta são usados.
   1. Um cookie é definido na resposta com valores obtidos de `targetCookie`. Isso é feito usando o cabeçalho de resposta `Set-Cookie`, que instrui o navegador a manter o cookie do público-alvo.
   1. É preparada uma resposta HTML que inicializa `VisitorAPI.js` e passa `visitorState` da resposta de destino.
1. A resposta do HTML é carregada no navegador...
   1. `VisitorAPI.js` está incluído no cabeçalho do documento.
   1. VisitorAPI foi inicializado com `visitorState` da resposta do SDK `getOffers`. Isso fará com que o cookie do visitante seja definido no navegador para que seja enviado ao servidor em solicitações subsequentes.

### Exemplo de código

A amostra de código a seguir implementa cada uma das etapas descritas acima. Cada etapa aparece no código como um comentário em linha ao lado de sua implementação.

#### Node.js

Esta amostra depende do [express, uma estrutura da Web Node.js](https://expressjs.com/).

>[!BEGINTABS]

>[!TAB server.js]

```js {line-numbers="true"}
const fs = require("fs");
const express = require("express");
const cookieParser = require("cookie-parser");
const Handlebars = require("handlebars");
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  timeout: 10000,
  logger: console,
};
const targetClient = TargetClient.create(CONFIG);
const TEMPLATE = fs.readFileSync(`${__dirname}/index.handlebars`).toString();
const handlebarsTemplate = Handlebars.compile(TEMPLATE);

Handlebars.registerHelper("toJSON", function (object) {
  return new Handlebars.SafeString(JSON.stringify(object, null, 4));
});

const app = express();
app.use(cookieParser());
app.use(express.static(__dirname + "/public"));

app.get("/", async (req, res) => {
  // The server reads the visitor and target cookies from the request.
  const visitorCookie =
    req.cookies[
      encodeURIComponent(
        TargetClient.getVisitorCookieName(CONFIG.organizationId)
      )
    ];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const address = { url: req.headers.host + req.originalUrl };

  const targetRequest = {
    execute: {
      mboxes: [
        { name: "homepage", index: 1, address },
        { name: "SummerShoesOffer", index: 2, address },
        { name: "SummerDressOffer", index: 3, address }
      ],
    },
  };

  res.set({
    "Content-Type": "text/html",
    Expires: new Date().toUTCString(),
  });

  try {
    // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
    const targetResponse = await targetClient.getOffers({
      request: targetRequest,
      visitorCookie,
      targetCookie,
    });

    // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
    // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
    res.cookie(
      targetResponse.targetCookie.name,
      targetResponse.targetCookie.value,
      { maxAge: targetResponse.targetCookie.maxAge * 1000 }
    );

    // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
    const html = handlebarsTemplate({
      organizationId: CONFIG.organizationId,
      targetResponse,
    });

    res.status(200).send(html);
  } catch (error) {
    console.error("Target:", error);
    res.status(500).send(error);
  }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB index.handlebars]

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>

  <!-- VisitorAPI.js is included in the document header. -->
  <script src="VisitorAPI.js"></script>
  <script>
    // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
    Visitor.getInstance("{{organizationId}}", {serverState: {{toJSON targetResponse.visitorState}} });
  </script>
</head>
<body>
  <h1>response</h1>
  <pre>{{toJSON targetResponse}}</pre>
</body>
</html>
```

>[!ENDTABS]

#### Java

Este exemplo usa [spring, um framework da Web Java](https://spring.io/).

>[!BEGINTABS]

>[!TAB ClientSampleApplication.java]

```java {line-numbers="true"}
@SpringBootApplication
public class ClientSampleApplication {

    public static void main(String[] args) {
        System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
        SpringApplication.run(ClientSampleApplication.class, args);
    }

    @Bean
    TargetClient marketingCloudClient() {
        ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .defaultDecisioningMethod(DecisioningMethod.SERVER_SIDE)
                .build();

        return TargetClient.create(clientConfig);
    }
}
```

>[!TAB TargetController.java]

```java {line-numbers="true"}
@Controller
@RequestMapping("/")
public class TargetController {

    @Autowired
    private TargetClientService targetClientService;

    @GetMapping
    public String index(Model model, HttpServletRequest request, HttpServletResponse response) {
        // The server reads the visitor and target cookies from the request.
        List<TargetCookie> targetCookies = getTargetCookies(request.getCookies());

        Address address = getAddress(request);

        List<MboxRequest> mboxRequests = new ArrayList<>();
        mboxRequests.add((MboxRequest) new MboxRequest().name("homepage").index(1).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerShoesOffer").index(2).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerDressOffer").index(3).address(address));

        TargetDeliveryResponse targetDeliveryResponse = targetClientService.getOffers(mboxRequests, targetCookies, request,
                response);

        // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
        model.addAttribute("visitorState", targetDeliveryResponse.getVisitorState());
        model.addAttribute("targetResponse", targetDeliveryResponse);
        model.addAttribute("organizationId", "1234567890@AdobeOrg");

        return "index";
    }
}
```

>[!TAB TargetClientService.java]

```java {line-numbers="true"}
@Service
public class TargetClientService {

    private final TargetClient targetJavaClient;

    public TargetClientService(TargetClient targetJavaClient) {
        this.targetJavaClient = targetJavaClient;
    }

    public TargetDeliveryResponse getOffers(List<MboxRequest> executeMboxes, List<TargetCookie> cookies, HttpServletRequest request, HttpServletResponse response) {

        Context context = getContext(request);
        ExecuteRequest executeRequest = new ExecuteRequest();
        executeRequest.setMboxes(executeMboxes);

        TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                .context(context)
                .execute(executeRequest)
                .cookies(cookies)
                .build();

        // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
        TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);

        // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
        // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
        setCookies(targetResponse.getCookies(), response);
        return targetResponse;
    }
}
```

>[!TAB TargetRequestUtils.java]

```java {line-numbers="true"}
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Target Only : GetOffer</title>

    <!-- VisitorAPI.js is included in the document header. -->
    <script src="../../js/VisitorAPI.js"></script>
    <script th:inline="javascript">
        // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
        Visitor.getInstance(/*[[${organizationId}]]*/ "", {serverState: /*[[${visitorState}]]*/ {}});
    </script>
</head>
<body>
    <h1>response</h1>
    <pre>[[${targetResponse}]]</pre>
</body>
</html>
```

>[!ENDTABS]

Para obter mais informações sobre `TargetRequestUtils.java`, consulte [Métodos de Utilidade (Java)](https://experienceleague.adobe.com/docs/target-dev/developer/server-side/java/utility-methods.html){target=_blank}
