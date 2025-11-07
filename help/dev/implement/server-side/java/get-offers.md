---
title: Usar getOffers() em [!DNL Adobe Target] ao usar o Java SDK
description: Saiba como usar getOffers() para executar uma decisão e recuperar uma experiência do  [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9d7bf956-9d6a-4b4f-a401-2e6814f17f3d
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 13%

---

# Obter ofertas (Java)

## Descrição

`getOffers()` é usado para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].

## Método

### getOffers

A assinatura do método `TargetClient.getOffers` é mostrada da seguinte maneira.

**Solicitação**

```javascript {line-numbers="true"}
TargetDeliveryResponse TargetClient.getOffers(TargetDeliveryRequest request)
```

TargetDeliveryRequest é criado usando `TargetDeliveryRequest.builder`.

**Resposta**

```javascript {line-numbers="true"}
TargetDeliveryRequestBuilder TargetDeliveryRequest.builder()
```

## Parâmetros

O objeto `[!UICONTROL TargetDeliveryRequestBuilder]` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| contexto | Contexto | Sim | Especifica o contexto da solicitação |
| sessionId | String | Não | Usado para vincular várias solicitações [!DNL Target] |
| thirdPartyId | String | Não | O identificador de sua empresa para o usuário que você pode enviar com cada chamada |
| cookies | Lista | Não | Lista de cookies retornados na solicitação [!DNL Target] anterior do mesmo usuário. |
| customerIds | Mapa | Não | IDs de cliente em formato compatível com VisitorId |
| executar | ExecuteRequest | Não | Solicitação de PageLoad ou mboxes para execução. Será avaliado no lado do servidor imediatamente |
| pré-busca | PrefetchRequest | Não | Exibições, Carregamento de página ou solicitação de mboxes para realizar a busca prévia. Retorna com o token de notificação a ser retornado na conversão. |
| notificações | Lista | Não | Usado para enviar notificações sobre qual conteúdo previamente buscado era exibido |
| requestId | String | Não | A ID da solicitação que será retornada na resposta. Gerado automaticamente se não estiver presente. |
| impressionId | String | Não | Se presentes, a segunda e as solicitações subsequentes com a mesma id não incrementarão impressões para atividades/métricas. Gerado automaticamente se não estiver presente. |
| environmentId | Longo | Não | ID de ambiente de cliente válida. Se não for especificado, o host será determinado com base no host fornecido. |
| propriedade | Propriedade | Não | Especifica at_property por meio do campo de token. Ela pode ser usada para controlar o escopo do delivery. |
| trace | Trace | Não | Habilita o rastreamento para a API de Entrega. |
| qaMode | QAMode | Não | Use esse objeto para ativar o modo de QA na solicitação. |
| locationHint | String | Não | Dica de local do cluster de borda [!DNL Target]. Usado para direcionar determinado cluster de borda para esta solicitação. |
| visitante | Visitante | Não | Usado para fornecer o objeto de API do visitante personalizado. |
| id | VisitorId | Não | Objeto que contém os identificadores do visitante. P. ex. tntId, thirdParyId, mcId, customerIds. |
| experienceCloud | Experience Cloud | Não | Especifica integrações com o Audience Manager e o Analytics. Preenchido automaticamente usando cookies, se não fornecido. |
| tntId | String | Não | Identificador principal em [!DNL Target] de um usuário. Obtido de targetCookies. Gerado automaticamente se não fornecido. |
| mcId | String | Não | Usado para mesclar e compartilhar dados entre diferentes soluções do [!DNL Adobe] (ECID). Obtido de targetCookies. Gerado automaticamente se não fornecido. |
| trackingServer | String | Não | O Servidor do Adobe Analytics para que [!DNL Adobe Target] e [!DNL Adobe Analytics] unam corretamente os dados. |
| trackingServerSecure | String | Não | O [!UICONTROL Adobe Analytics Secure Server] para que [!DNL Adobe Target] e [!DNL Adobe Analytics] unam corretamente os dados. |
| decisioningMethod | DecisioningMethod | Não | Pode ser usado para definir explicitamente o método de decisão ON_DEVICE ou HYBRID para a decisão no dispositivo |

Os valores de cada campo devem estar em conformidade com a especificação de solicitação *[!UICONTROL Target View Delivery API]*. Para saber mais sobre o *[!UICONTROL Target View Delivery API]*, consulte [http://developers.adobetarget.com/api/#view-delivery-overview](http://developers.adobetarget.com/api/#view-delivery-overview)


## Resposta

O `TargetDeliveryResponse` retornado por `TargetClient.getOffers(`) tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| solicitação | TargetDeliveryRequest&#x200B; | *[!DNL Target]* solicitação |
| resposta | DeliveryResponse | *[!DNL Target]* resposta |
| cookies | Lista | Lista de metadados da sessão para este usuário. Precisa ser passado na próxima solicitação do Target para este usuário. |
| visitorState | Mapa | Estado do visitante a ser definido no lado do cliente para ser usado pela API do visitante |
| responseStatus | StatusResposta | Um objeto que representa o status da resposta |

O `ResponseStatus` na resposta contém os seguintes campos:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| status | int | Status HTTP retornado de [!DNL Target] |
| message | String | Mensagem de status caso o status HTTP não seja 200 |
| remoteMboxes | Lista de strings | Usado para decisões no dispositivo. Contém uma lista de mboxes que têm atividades remotas que não podem ser decididas totalmente no dispositivo. |
| remoteViews | Lista de strings | Usado para decisões no dispositivo. Contém uma lista de exibições com atividades remotas que não podem ser decididas totalmente no dispositivo. |

O objeto `TargetCookie` usado para salvar dados para a sessão de usuário tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| name | String | Nome do cookie |
| value | String    | Valor do cookie, o valor será convertido em string |
| maxAge | Número | A opção maxAge é uma conveniência para definir que expira em relação ao tempo atual em segundos |

Você não precisa se preocupar em expirar os cookies. O Target manipula maxAge na SDK.

## Exemplo

**Solicitação**

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().setMboxes(mboxRequests))
        .build();
```

**Resposta**

```javascript {line-numbers="true"}
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```
