---
title: Usar getOffers() no [!DNL Adobe Target] ao usar o SDK do .NET
description: Saiba como usar getOffers() para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 4d1d1cbd-c7e5-4146-9fea-08e01923874d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 13%

---

# Obter Ofertas (.NET)

## Descrição

`GetOffers()` é usado para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].

## Método

`TargetClient.GetOffers` assinatura de método.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.GetOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest` é criado usando `TargetDeliveryRequest.Builder`.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryRequest.Builder TargetDeliveryRequest.Builder()
```

## Parâmetros

A variável `TargetDeliveryRequest.Builder` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| contexto | Contexto | Sim | Especifica o contexto da solicitação |
| sessionId | String | Não | Usado para vincular vários [!DNL Target] solicitações |
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
| mcId | String | Não | Usado para mesclar e compartilhar dados entre diferentes soluções de Adobe (ECID). Obtido de targetCookies. Gerado automaticamente se não fornecido. |
| trackingServer | String | Não | O servidor do Adobe Analytics para [!DNL Adobe Target] e [!DNL Adobe Analytics] para compilar corretamente os dados. |
| trackingServerSecure | String | Não | A variável [!UICONTROL Adobe Analytics Secure Server] para [!DNL Adobe Target] e [!DNL Adobe Analytics] para compilar corretamente os dados. |
| decisioningMethod | DecisioningMethod | Não | Pode ser usado para definir explicitamente o método de decisão ON_DEVICE ou HYBRID para a decisão no dispositivo |

Os valores de cada campo devem estar em conformidade com [API de entrega do Target](/help/dev/implement/delivery-api/overview.md) especificação da solicitação.

## Resposta

A variável `TargetDeliveryResponse` retornado por `TargetClient.GetOffers()` tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| Solicitação | TargetDeliveryRequest&#x200B; | [API de entrega do Target](/help/dev/implement/delivery-api/overview.md) solicitação |
| Resposta | DeliveryResponse &#x200B; | [API de entrega do Target](/help/dev/implement/delivery-api/overview.md)* resposta |
| Status | HttpStatusCode | Código de status HTTP de resposta |
| Mensagem | string | Mensagem de status de resposta ou mensagem de erro |
| Localizações | Localizações | [!DNL Target] nomes de locais, incluindo nome global da mbox e mboxes/exibições para as quais somente a decisão remota está disponível |
| GetCookies | Dicionário | Retorna um dicionário de metadados da sessão para este usuário. Isso precisa ser passado no próximo [!DNL Target] solicitação para este usuário. |
| VisitorState | IDictionary | Estado do visitante a ser definido no lado do cliente para a inicialização da biblioteca JavaScript da API do visitante |

A variável `TargetCookie` o objeto usado para salvar dados para a sessão do usuário tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| Nome | string | Nome do cookie |
| Valor | string | Valor do cookie |
| MaxAge | int | A variável `MaxAge` é uma conveniência para definir Expira em relação ao tempo atual em segundos |

Você não precisa se preocupar em expirar os cookies. [!DNL Target] alças `MaxAge` no SDK.

## Exemplo

## \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
    .Build();

var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```
