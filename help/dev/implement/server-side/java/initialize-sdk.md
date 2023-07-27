---
title: Inicialize o SDK do Java usando o método de criação
description: Saiba como usar o método de criação para inicializar o SDK do Java e instanciar o [!UICONTROL TargetClient] para fazer chamadas para [!DNL Adobe Target] para experimentos e experiências personalizadas.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 18%

---

# Inicializar o SDK Java

## Descrição

Use o `create` para inicializar o SDK do Java e instanciar o [!UICONTROL Cliente do Target] para fazer chamadas para [!DNL Adobe Target] para experimentos e experiências personalizadas.

## Método

[!UICONTROL TargetClient] é criado usando `TargetClient.create`.

### criar

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig é criado usando `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Parâmetros

`ClientConfigBuilder` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| cliente | String | Sim | None | [!UICONTROL ID do cliente do Target] |
| organizationId | String | Sim | None | [!UICONTROL ID da organização Experience Cloud] |
| connectTimeout | Número | Não | 10000 | Tempo limite de conexão para todas as solicitações em milissegundos |
| socketTimeout | Número | Não | 10000 | Tempo limite do soquete para todas as solicitações em milissegundos |
| maxConnectionsPerHost | Número | Não | 100 | Máximo de Conexões por [!DNL Target] host |
| maxConnectionsTotal | Número | Não | 200 | Máximo de conexões, incluindo todas [!DNL Target] hosts |
| enableRetries | Booleano | Não | true | Tentativas automáticas para tempos limite de soquete (máx. 4) |
| logRequests | Booleano | Não | false | Log [!DNL Target] solicitações e respostas na depuração |
| logRequestStatus | Booleano | Não | false | Log [!DNL Target] tempo de resposta, status e URL |
| serverDomain | String | Não | `*client*.tt.omtrdc.net` | Substitui o nome de host padrão |
| seguro | Booleano | Não | true | Não definido para impor o esquema HTTP |
| requestInterceptor | HttpRequestInterceptor | Não | Nulo | Adicionar interceptor de solicitação personalizado |
| defaultPropertyToken | String | Não | None | Define o token de propriedade padrão para cada `getOffers` chame. **Para decisões no dispositivo**, o SDK baixará somente o artefato que contém as atividades qualificadas para o token de propriedade definido em `defaultPropertyToken` |
| defaultDecisioningMethod | DecisioningMethod enum | Não | SERVER_SIDE | Deve ser definido como ON_DEVICE ou HYBRID para ativar a decisão no dispositivo |
| telemetryEnabled | Booleano | Não | true | Permite que os clientes recusem a coleta de dados adicional durante as solicitações para [!DNL Target] servidores |
| proxyConfig | ClientProxyConfig | Não | None | Permite que o cliente forneça seus próprios detalhes de proxy |
| exceptionHandler | TargetExceptionHandler | Não | None | Pode ser usado para implementar o tratamento personalizado de exceções durante o processamento de regras |
| httpClient | HttpClient | Não | None | Permite que os usuários substituam o [!DNL Target] Cliente HTTP com um cliente HTTP personalizado |
| onDeviceEnvironment | String | Não | produção | Pode ser usado para especificar um ambiente diferente no dispositivo, como preparo |
| onDeviceConfigHostname | String | Não | `assets.adobetarget.com` | Pode ser usado para especificar um host diferente para usar no download do arquivo de artefato da decisão no dispositivo |
| onDeviceDecisioningPollingIntSecs | int | Não | 300 (5 minutos) | Número de segundos entre as buscas do arquivo de artefato de decisão no dispositivo |
| onDeviceArtifactPayload | byte[] | Não | None | Fornece a decisão no dispositivo com a carga de artefato anterior para permitir execução imediata |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | Não | None | Registra retornos de chamada para eventos de decisão no dispositivo |
| onDeviceAllMatchingRulesMboxes | Lista\&lt;string> | Não | None | Permite que os usuários especifiquem mboxes para as quais todo o conteúdo de regra correspondente será retornado durante a tomada de decisão no dispositivo |

## Exemplo

### Java

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient.create(clientConfig);

// make calls to Adobe Target
```
