---
title: Identificação e segmentação do usuário
description: Identificação e segmentação do usuário
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 3%

---

# Identificação e segmentação do usuário

## Identificação do usuário

Há várias maneiras pelas quais um usuário pode ser identificado dentro de [!DNL Adobe Target]. [!UICONTROL Target] usa os seguintes identificadores:

| Nome do campo | Descrição |
| --- | --- |
| `tntID` | O `tntId` é o identificador principal em [!DNL Target] de um usuário. Você pode fornecer essa ID, ou [!DNL Target] irá gerá-la automaticamente se a solicitação não contiver uma. |
| `thirdPartyId` | O `thirdPartyId` é o identificador de sua empresa para o usuário, que você pode enviar com cada chamada. Quando um usuário faz logon no site de uma empresa, a empresa normalmente cria uma ID vinculada à conta, ao cartão de fidelidade, ao número de associado ou a outros identificadores aplicáveis do visitante dessa empresa. |
| `marketingCloudVisitorId` | O `marketingCloudVisitorId` é usado para mesclar e compartilhar dados entre diferentes soluções de Adobe. O marketingCloudVisitorId é necessário para integrações com o Adobe Analytics e o Adobe Audience Manager. |
| `customerIds` | Juntamente com a ID de visitante do Experience Cloud, também podem ser utilizadas [IDs adicionais do cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=pt-BR) e um status autenticado para cada visitante. |

## [!DNL Target] ID (tntID)

A ID [!DNL Target], ou `tntId`, pode ser considerada uma ID de dispositivo. Este `tntId` é gerado automaticamente por [!DNL Adobe Target] se não for fornecido na solicitação. As solicitações subsequentes precisam incluir este `tntId` para que o conteúdo correto seja entregue a um dispositivo usado pelo mesmo usuário.

A chamada de exemplo a seguir demonstra uma situação em que um `tntId` não é passado para [!DNL Target].

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

>[!TAB SDK Java]

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

Na ausência de um `tntId`, [!DNL Adobe Target] gera um `tntId` e o fornece na resposta, da seguinte maneira.

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

Neste exemplo, o `tntId` gerado é `10abf6304b2714215b1fd39a870f01afc.35_0`. Observe que este `tntId` precisa ser usado para o mesmo usuário em todas as sessões.

## ID de terceiros (thirdPartyId)

Se sua organização usar uma ID para identificar o visitante, você poderá usar o `thirdPartyID` para fornecer conteúdo. Um `thirdPartyID` é uma ID persistente que sua empresa utiliza para identificar um usuário final, independentemente de ele interagir com sua empresa a partir da Web, de dispositivos móveis ou da IoT. Em outras palavras, o `thirdPartyId` faz referência aos dados do perfil do usuário que podem ser utilizados entre canais. No entanto, você deve fornecer o `thirdPartyID` para cada chamada da API de entrega [!DNL Adobe Target] que você fizer.

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

>[!TAB SDK Java]

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

Neste cenário, [!DNL Adobe Target] gerará um `tntId` já que não foi passado para a chamada original, que será mapeada para o `thirdPartyId` fornecido.

## ID de visitante do Marketing Cloud (marketingCloudVisitorId)

O `marketingCloudVisitorId` é uma ID persistente e universal que identifica os visitantes em todas as soluções da Adobe Experience Cloud. Quando sua organização implementa o serviço de ID, essa ID permite identificar o mesmo visitante do site e seus dados em diferentes soluções de Experience Cloud, incluindo o [!DNL Adobe Target], o Adobe Analytics e o Adobe Audience Manager. Observe que `marketingCloudVisitorId` é necessário ao integrar [!DNL Target] a [!DNL Adobe Analytics] e [!DNL Adobe Audience Manager].

A chamada de exemplo a seguir demonstra como um `marketingCloudVisitorId` que foi recuperado do Serviço de ID de Experience Cloud é passado para [!DNL Target].

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

>[!TAB SDK Java]

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

Neste cenário, [!DNL Target] gerará um `tntId` já que não foi passado para a chamada original, que será mapeada para o `marketingCloudVisitorId` fornecido.

## ID do cliente (customerIds)

[As IDs do cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=pt-BR) podem ser adicionadas a uma ID de visitante do Experience Cloud ou associadas a ela. Ao enviar `customerIds`, `marketingCloudVisitorId` também deve ser fornecido. Além disso, um status de autenticação pode ser fornecido com cada `customerId` para cada visitante. Os seguintes status de autenticação podem ser usados:

| Status de autenticação | Status do usuário |
| --- | --- |
| `unknown` | Desconhecido ou nunca autenticado. Esse estado pode ser usado para cenários como aquele em que um visitante chega ao seu site clicando em um anúncio de exibição. |
| `authenticated` | O usuário está autenticado no momento com uma sessão ativa no seu site ou aplicativo. |
| `logged_out` | O usuário foi autenticado, mas fez logout ativamente. O usuário pretendia se desconectar do estado autenticado. O usuário não deseja mais ser tratado como autenticado. |

Observe que somente quando `customerId` estiver em um estado autenticado, [!DNL Target] fará referência aos dados do perfil do usuário armazenados e vinculados ao customerId. Se o `customerId` estiver em um estado desconhecido ou `logged_out`, ele será ignorado e os dados de perfil de usuário associados a esse `customerId` não serão aproveitados para direcionamento de público-alvo.

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

>[!TAB SDK Java]

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

O exemplo acima demonstra como enviar um `customerId` com um `authenticatedState`. Ao enviar um `customerId`, os `integrationCode`, `id` e `authenticatedState` e também o `marketingCloudVisitorId` são obrigatórios. O `integrationCode` é o alias do [arquivo de atributos do cliente](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=pt-BR) fornecido pelo CRS.

## Perfil mesclado

Você pode combinar `tntId`, `thirdPartyID` e `marketingCloudVisitorId` na mesma solicitação. Neste cenário, [!DNL Adobe Target] manterá o mapeamento de todas essas IDs e as fixará a um visitante. Saiba como os perfis são [mesclados e sincronizados em tempo real](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=pt-BR) usando identificadores diferentes.

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

>[!TAB SDK Java]

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

O exemplo acima demonstra como você pode combinar `tntId`, `thirdPartyID` e `marketingCloudVisitorId` na mesma solicitação.

## Classificação

Seus usuários são classificados para ver uma experiência, dependendo de como você configura suas atividades do [!DNL Adobe Target]. Em [!DNL Adobe Target], a segmentação é:

* **Determinístico**: MurmurHash3 é usado para garantir que o usuário seja classificado e veja a variação correta todas as vezes, desde que a ID do usuário seja consistente.
* **Fixo**: [!DNL Adobe Target] armazena a variação que seu usuário vê no perfil de usuário para garantir que a variação seja mostrada consistentemente para esse usuário em sessões e canais. As variações e a adesão são garantidas ao usar a decisão do lado do servidor. Quando a decisão no dispositivo é usada, a adesão não é garantida.

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
1. Código do cliente `acmeclient`
1. ID da atividade `1111`
1. Sal `experience`
1. Valor para hash `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, valor de hash `-919077116`
1. Valor absoluto do hash `919077116`
1. Restante após divisão por 10000, `7116`
1. O valor após o restante é dividido por 10000, `0.7116`
1. Resultado após multiplicar o valor pelo número total de experiências `3 * 0.7116 = 2.1348`
1. O índice de experiência é `2`, o que significa a terceira experiência, pois estamos usando a indexação baseada em `0`.
