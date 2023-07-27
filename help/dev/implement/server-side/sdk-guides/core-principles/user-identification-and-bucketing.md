---
title: Identificação e segmentação do usuário
description: Identificação e segmentação do usuário
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 5%

---

# Identificação e segmentação do usuário

## Identificação do usuário

Há várias maneiras de identificar um usuário no [!DNL Adobe Target]. [!UICONTROL Target] O usa os seguintes identificadores:

| Nome do campo | Descrição |
| --- | --- |
| `tntID` | A variável `tntId` é o identificador principal em [!DNL Target] para um usuário. Você pode fornecer essa ID ou [!DNL Target] O será gerado automaticamente se a solicitação não contiver um. |
| `thirdPartyId` | A variável `thirdPartyId` é o identificador da sua empresa para o usuário, que você pode enviar com cada chamada. Quando um usuário faz logon no site de uma empresa, a empresa normalmente cria uma ID vinculada à conta, ao cartão de fidelidade, ao número de associado ou a outros identificadores aplicáveis do visitante dessa empresa. |
| `marketingCloudVisitorId` | A variável `marketingCloudVisitorId` O é usado para mesclar e compartilhar dados entre diferentes soluções de Adobe. O marketingCloudVisitorId é necessário para integrações com o Adobe Analytics e o Adobe Audience Manager. |
| `customerIds` | Juntamente com a ID de visitante do Experience Cloud, [IDs do cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) e um status autenticado para cada visitante também pode ser usado. |

## [!DNL Target] ID (tntID)

A variável [!DNL Target] ID ou `tntId`, pode ser considerado uma ID de dispositivo. Este `tntId` é gerado automaticamente por [!DNL Adobe Target] se não for fornecido no pedido. As solicitações subsequentes precisam incluir isso `tntId` para que o conteúdo correto seja entregue a um dispositivo usado pelo mesmo usuário.

A amostra de chamada a seguir demonstra uma situação em que um `tntId` não é passado para [!DNL Target].

>[!BEGINTABS]

>[!TAB SDK do Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
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

>[!TAB SDK do Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Na ausência de uma `tntId`, [!DNL Adobe Target] gera um `tntId` e o fornece na resposta, como segue.

```json {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "acmeclient",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.35_0"
  },
  "edgeHost": "mboxedge35.tt.omtrdc.net",
  ...
}
```

Neste exemplo, a variável `tntId` é `10abf6304b2714215b1fd39a870f01afc.35_0`. Observe que `tntId` precisa ser usado para o mesmo usuário nas sessões.

## ID de terceiros (thirdPartyId)

Se sua organização usar uma ID para identificar o visitante, você poderá usar `thirdPartyID` para fornecer conteúdo. A `thirdPartyID` O é uma ID persistente que sua empresa usa para identificar um usuário final, independentemente de ele interagir com sua empresa a partir de canais da Web, móveis ou da IoT. Por outras palavras, a `thirdPartyId` O faz referência aos dados de perfil do usuário que podem ser utilizados em canais. No entanto, você deve fornecer a `thirdPartyID` para cada [!DNL Adobe Target] Chamada de API de entrega que você faz.

O exemplo de chamada a seguir demonstra o uso de um `thirdPartyId`.

>[!BEGINTABS]

>[!TAB SDK do Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      thirdPartyId: "B234A029348"
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

>[!TAB SDK do Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .thirdPartyId("B234A029348");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Nesse cenário, [!DNL Adobe Target] gerará uma `tntId` já que não foi passado para a chamada original, que será mapeada para a variável `thirdPartyId`.

## ID de visitante do Marketing Cloud (marketingCloudVisitorId)

A variável `marketingCloudVisitorId` O é uma ID persistente e universal que identifica os visitantes em todas as soluções da Adobe Experience Cloud. Quando sua organização implementa o serviço de ID, essa ID permite identificar o mesmo visitante do site e seus dados em soluções de Experience Cloud diferentes, incluindo [!DNL Adobe Target], Adobe Analytics e Adobe Audience Manager. Observe a `marketingCloudVisitorId` é necessário ao integrar [!DNL Target] com [!DNL Adobe Analytics] e [!DNL Adobe Audience Manager].

O exemplo de chamada a seguir demonstra como um `marketingCloudVisitorId` que foi recuperado do Serviço da Experience Cloud ID é passado para [!DNL Target].

>[!BEGINTABS]

>[!TAB SDK do Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId: "10527837386392355901041112038610706884"
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

>[!TAB SDK do Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Nesse cenário, [!DNL Target] gerará uma `tntId` já que não foi passado para a chamada original, que será mapeada para a variável `marketingCloudVisitorId`.

## ID do cliente (customerIds)

[IDs de cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) podem ser adicionados a uma ID de visitante do Experience Cloud ou associados a ela. Sempre que enviar `customerIds`, o `marketingCloudVisitorId` também devem ser fornecidas. Além disso, um status de autenticação pode ser fornecido junto com cada `customerId` para cada visitante. Os seguintes status de autenticação podem ser usados:

| Status de autenticação | Status do usuário |
| --- | --- |
| `unknown` | Desconhecido ou nunca autenticado. Esse estado pode ser usado para cenários como aquele em que um visitante chega ao seu site clicando em um anúncio de exibição. |
| `authenticated` | O usuário está autenticado no momento com uma sessão ativa no seu site ou aplicativo. |
| `logged_out` | O usuário foi autenticado, mas fez logout ativamente. O usuário pretendia se desconectar do estado autenticado. O usuário não deseja mais ser tratado como autenticado. |

Observe que somente quando a variável `customerId` está em um estado autenticado irá [!DNL Target] faça referência aos dados do perfil do usuário armazenados e vinculados à customerId. Se a variável `customerId` está em um ou desconhecido `logged_out` será ignorado e quaisquer dados de perfil de usuário que possam estar associados a esse `customerId` não serão aproveitados para direcionamento de público-alvo.

>[!BEGINTABS]

>[!TAB SDK do Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId : "10527837386392355901041112038610706884",
      customerIds: [{
        id: "134325423",
        integrationCode : "crm_data",
        authenticatedState : "authenticated"
      }]
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

>[!TAB SDK do Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

CustomerId customerId = new CustomerId()
  .id("134325423")
  .integrationCode("crm_data")
  .authenticatedState(AuthenticatedState.AUTHENTICATED);
VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884")
  .customerIds(Arrays.asList(customerId));
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

O exemplo acima demonstra como enviar uma `customerId` com um `authenticatedState`. Ao enviar uma `customerId`, o `integrationCode`, `id`, e `authenticatedState` bem como a `marketingCloudVisitorId` são obrigatórios. A variável `integrationCode` é o alias do [arquivo de atributos do cliente](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=pt-BR) você forneceu por meio do CRS.

## Perfil mesclado

É possível combinar `tntId`, `thirdPartyID`, e `marketingCloudVisitorId` no mesmo pedido. Nesse cenário, [!DNL Adobe Target] manterá o mapeamento de todas essas IDs e o fixará a um visitante. Saiba como os perfis são [mesclado e sincronizado em tempo real](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) usando os diferentes identificadores.

>[!BEGINTABS]

>[!TAB SDK do Node.js]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId: "B234A029348",
      marketingCloudVisitorId : "10527837386392355901041112038610706884"
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

>[!TAB SDK do Java]

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

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

O exemplo acima demonstra como é possível combinar `tntId`, `thirdPartyID`, e `marketingCloudVisitorId` no mesmo pedido.

## Classificação

Seus usuários são classificados para ver uma experiência, dependendo de como você configura o [!DNL Adobe Target] atividades. Entrada [!DNL Adobe Target], a classificação é:

* **Determinístico**: MurmurHash3 é usado para garantir que o usuário seja segmentado e veja a variação correta todas as vezes, desde que a ID de usuário seja consistente.
* **Fixo**: [!DNL Adobe Target] O armazena a variação que seu usuário vê no perfil do usuário para garantir que a variação seja mostrada consistentemente para esse usuário em sessões e canais. As variações e a adesão são garantidas ao usar a decisão do lado do servidor. Quando a decisão no dispositivo é usada, a adesão não é garantida.

## Fluxo de trabalho de classificação de ponta a ponta

Antes de mergulhar no algoritmo de segmentação real, é importante destacar que etapas semelhantes são usadas para selecionar atividades com base na porcentagem de alocação de tráfego, bem como selecionar uma experiência em uma atividade.

### Etapas de seleção de atividade

1. Gerar uma ID de dispositivo, geralmente uma UUID
1. Obter o código de cliente
1. Obter a ID da atividade
1. Pegue o sal, que geralmente é uma corda como &quot;atividade&quot;
1. Calcular o hash usando MurmurHash3
1. Obter o valor absoluto do hash
1. Dividir o valor absoluto de hash por 10000
1. Divida o restante por 10000, o que deve produzir um valor entre 0 e 1
1. Multiplicar o resultado por 100%
1. Compare a porcentagem de alocação de tráfego de atividade com a porcentagem obtida. Se a porcentagem de alocação de tráfego for menor, a atividade será selecionada. Caso contrário, a atividade será ignorada.

### Etapas de seleção de experiência

1. Gerar uma ID de dispositivo, geralmente uma UUID
1. Obter o código de cliente
1. Obter a ID da atividade
1. Pegue o sal, que geralmente é uma corda como &quot;experiência&quot;
1. Calcular o hash usando MurmurHash3
1. Obter o valor absoluto do hash
1. Dividir o valor absoluto de hash por 10000
1. Divida o restante por 10000, o que deve produzir um valor entre 0 e 1
1. Multiplica o resultado pelo número total de experiências na atividade.
1. Arredondar o resultado. Isso deve produzir o índice de experiência.

### Exemplo

Considere o seguinte:

* Cliente C com código de cliente `acmeclient`
* Atividade A com ID `1111` e três experiências `E1`, `E2`, `E3`
* As experiências têm a seguinte distribuição: `E1` - 33%, `E2` - 33%, `E3` - 34%

O fluxo de seleção tem esta aparência:

1. ID do dispositivo `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. Código de cliente `acmeclient`
1. ID da atividade `1111`
1. Sal `experience`
1. Valor para hash `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, valor de hash `-919077116`
1. Valor absoluto do hash `919077116`
1. Resto após divisão por 10000, `7116`
1. O valor após o restante é dividido por 10000, `0.7116`
1. Resultado após multiplicar o valor pelo número total de experiências `3 * 0.7116 = 2.1348`
1. O índice de experiência é `2`, que significa a terceira experiência, já que estamos usando o `0` indexação com base em.
