---
title: Inicialize o SDK do Java usando o método de criação
description: Saiba como usar o método de criação para inicializar o SDK do Java e instanciar o [!UICONTROL TargetClient] para fazer chamadas para  [!DNL Adobe Target] experiências e experiências personalizadas.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: 1d080b5e402e5d55039bf06611b44678cc6c36de
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 17%

---

# Inicializar o SDK do Java

## Descrição

Use o método `create` para inicializar o SDK do Java e instanciar o [!UICONTROL Target Client] para fazer chamadas para [!DNL Adobe Target] de experimentos e experiências personalizadas.

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
| cliente | String | Sim | None | [!UICONTROL Target Client Id] |
| organizationId | String | Sim | None | [!UICONTROL Experience Cloud Organization ID] |
| connectTimeout | Número | Não | 10000 | Tempo limite de conexão para todas as solicitações em milissegundos |
| socketTimeout | Número | Não | 10000 | Tempo limite do soquete para todas as solicitações em milissegundos |
| maxConnectionsPerHost | Número | Não | 100 | Máximo de Conexões por [!DNL Target] host |
| maxConnectionsTotal | Número | Não | 200 | Máximo de Conexões incluindo todos os [!DNL Target] hosts |
| connectionTtlMs | Número | Não | -1 | O TTL (Total time to live) define o tempo máximo de vida das conexões persistentes em milissegundos. Por padrão, as conexões serão mantidas ativas indefinidamente |
| idleConnectionValidationMs | Número | Não | 1000 | Período de inatividade em milissegundos após o qual as conexões persistentes são revalidadas antes de serem reutilizadas |
| evictIdleConnectionsAfterSecs | Número | Não | 20 | O tempo em segundos para remover conexões ociosas do pool de conexões |
| enableRetries | Booleano | Não | true | Tentativas automáticas para tempos limite de soquete (máx. 4) |
| logRequests | Booleano | Não | false | Registrar [!DNL Target] solicitações e respostas na depuração |
| logRequestStatus | Booleano | Não | false | Registrar o tempo de resposta, o status e a URL do [!DNL Target] |
| serverDomain | String | Não | `*client*.tt.omtrdc.net` | Substitui o nome de host padrão |
| seguro | Booleano | Não | true | Não definido para impor o esquema HTTP |
| requestInterceptor | HttpRequestInterceptor | Não | Null | Adicionar interceptor de solicitação personalizado |
| defaultPropertyToken | String | Não | None | Define o token de propriedade padrão para cada chamada de `getOffers`. **Para a tomada de decisão no dispositivo**, o SDK baixará somente o artefato que contém as atividades qualificadas para o token de propriedade definido em `defaultPropertyToken` |
| defaultDecisioningMethod | DecisioningMethod enum | Não | SERVER_SIDE | Deve ser definido como ON_DEVICE ou HYBRID para ativar a decisão no dispositivo |
| telemetryEnabled | Booleano | Não | true | Permite que os clientes recusem a coleta de dados adicional durante solicitações para [!DNL Target] servidores |
| proxyConfig | ClientProxyConfig | Não | None | Permite que o cliente forneça seus próprios detalhes de proxy |
| exceptionHandler | TargetExceptionHandler | Não | None | Pode ser usado para implementar o tratamento personalizado de exceções durante o processamento de regras |
| httpClient | HttpClient | Não | None | Permite que os usuários substituam o cliente HTTP [!DNL Target] por um Cliente HTTP personalizado |
| onDeviceEnvironment | String | Não | produção | Pode ser usado para especificar um ambiente diferente no dispositivo, como preparo |
| onDeviceConfigHostname | String | Não | `assets.adobetarget.com` | Pode ser usado para especificar um host diferente para usar no download do arquivo de artefato da decisão no dispositivo |
| onDeviceDecisioningPollingIntSecs | int | Não | 300 (5 minutos) | Número de segundos entre as buscas do arquivo de artefato de decisão no dispositivo |
| onDeviceArtifactPayload | byte[] | Não | None | Fornece a decisão no dispositivo com a carga de artefato anterior para permitir execução imediata |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | Não | None | Registra retornos de chamada para eventos de decisão no dispositivo |
| onDeviceAllMatchingRulesMboxes | Lista\&lt;Cadeia de caracteres\> | Não | None | Permite que os usuários especifiquem mboxes para as quais todo o conteúdo de regra correspondente será retornado durante a tomada de decisão no dispositivo |

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
