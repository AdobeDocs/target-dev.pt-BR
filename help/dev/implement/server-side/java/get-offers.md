---
title: Usar getOffers() no [!DNL Adobe Target] ao usar o SDK do Java
description: Saiba como usar getOffers() para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9d7bf956-9d6a-4b4f-a401-2e6814f17f3d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 13%

---

# Obter ofertas (Java)

## Descrição

`getOffers()` é usado para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].

## Método

### getOffers

A variável `TargetClient.getOffers` a assinatura do método é mostrada da seguinte maneira:

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

A variável `[!UICONTROL TargetDeliveryRequestBuilder]` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| contexto | Contexto | Sim | Especifica o contexto da solicitação |
| sessionId |  | String | Não | Usado para vincular vários [!DNL Target] solicitações |
| thirdPartyId | String | Não | O identificador de sua empresa para o usuário que você pode enviar com cada chamada |
| cookies | Listar | Não | Lista de cookies retornados no anterior [!DNL Target] solicitação do mesmo usuário. |
| customerIds | Mapa | Não | IDs de cliente em formato compatível com VisitorId |
| executar | ExecuteRequest | Não | Solicitação de PageLoad ou mboxes para execução. Será avaliado no lado do servidor imediatamente |
| pré-busca | PrefetchRequest | Não | Exibições, Carregamento de página ou solicitação de mboxes para realizar a busca prévia. Retorna com o token de notificação a ser retornado na conversão. |
| notificações | Listar | Não | Usado para enviar notificações sobre qual conteúdo previamente buscado era exibido |
| requestId | String | Não | A ID da solicitação que será retornada na resposta. Gerado automaticamente se não estiver presente. |
| impressionId | String | Não | Se presentes, a segunda e as solicitações subsequentes com a mesma id não incrementarão impressões para atividades/métricas. Gerado automaticamente se não estiver presente. |
| environmentId | Longo | Não | ID de ambiente de cliente válida. Se não for especificado, o host será determinado com base no host fornecido. |
| propriedade | Propriedade | Não | Especifica at_property por meio do campo de token. Ela pode ser usada para controlar o escopo do delivery. |
| trace | Trace | Não | Habilita o rastreamento para a API de Entrega. |
| qaMode | QAMode | Não | Use esse objeto para ativar o modo de QA na solicitação. |
| locationHint | String | Não | [!DNL Target] dica de local do cluster de borda. Usado para direcionar determinado cluster de borda para esta solicitação. |
| visitante | Visitante | Não | Usado para fornecer o objeto de API do visitante personalizado. |
| id | VisitorId | Não | Objeto que contém os identificadores do visitante. P. ex. tntId, thirdParyId, mcId, customerIds. |
| experienceCloud | Experience Cloud | Não | Especifica integrações com o Audience Manager e o Analytics. Preenchido automaticamente usando cookies, se não fornecido. |
| tntId | String | Não | Identificador principal em [!DNL Target] para um usuário. Obtido de targetCookies. Gerado automaticamente se não fornecido. |
| mcId | String | Não | Usado para mesclar e compartilhar dados entre diferentes [!DNL Adobe] soluções (ECID). Obtido de targetCookies. Gerado automaticamente se não fornecido. |
| trackingServer | String | Não | O servidor do Adobe Analytics para [!DNL Adobe Target] e [!DNL Adobe Analytics] para compilar corretamente os dados. |
| trackingServerSecure | String | Não | A variável [!UICONTROL Adobe Analytics Secure Server] para [!DNL Adobe Target] e [!DNL Adobe Analytics] para compilar corretamente os dados. |
| decisioningMethod | DecisioningMethod | Não | Pode ser usado para definir explicitamente o método de decisão ON_DEVICE ou HYBRID para a decisão no dispositivo |

Os valores de cada campo devem estar em conformidade com *[!UICONTROL API de entrega da exibição do Target]* especificação da solicitação. Para saber mais sobre o *[!UICONTROL API de entrega da exibição do Target]*, consulte [http://developers.adobetarget.com/api/#view-delivery-overview](http://developers.adobetarget.com/api/#view-delivery-overview)


## Resposta

A variável `TargetDeliveryResponse` retornado por `TargetClient.getOffers(`) tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| solicitação | TargetDeliveryRequest&#x200B; | *[!DNL Target]* solicitação |
| resposta | DeliveryResponse | *[!DNL Target]* resposta |
| cookies | Listar | Lista de metadados da sessão para este usuário. Precisa ser passado na próxima solicitação do Target para este usuário. |
| visitorState | Mapa | Estado do visitante a ser definido no lado do cliente para ser usado pela API do visitante |
| responseStatus | StatusResposta | Um objeto que representa o status da resposta |

A variável `ResponseStatus` na resposta contém os seguintes campos:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| status | int | Status do HTTP retornado de [!DNL Target] |
| message | String | Mensagem de status caso o status HTTP não seja 200 |
| remoteMboxes | Lista de strings | Usado para decisões no dispositivo. Contém uma lista de mboxes que têm atividades remotas que não podem ser decididas totalmente no dispositivo. |
| remoteViews | Lista de strings | Usado para decisões no dispositivo. Contém uma lista de exibições com atividades remotas que não podem ser decididas totalmente no dispositivo. |

A variável `TargetCookie` o objeto usado para salvar dados para a sessão do usuário tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| name | String | Nome do cookie |
| value | String    | Valor do cookie, o valor será convertido em string |
| maxAge | Número | A opção maxAge é uma conveniência para definir que expira em relação ao tempo atual em segundos |

Você não precisa se preocupar em expirar os cookies. O Target manipula maxAge dentro do SDK.

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
