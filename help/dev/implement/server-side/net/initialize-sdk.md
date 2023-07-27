---
title: Inicialize o SDK do .NET usando o método de criação
description: Saiba como usar o método de criação para inicializar o SDK do Java e instanciar o [!UICONTROL TargetClient] para fazer chamadas para [!DNL Adobe Target] para experimentos e experiências personalizadas.
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 17%

---

# Inicializar o SDK do .NET

## Descrição

Use o `Create` para inicializar o SDK do .NET e instanciar o [!UICONTROL Cliente do Target] para fazer chamadas para [!DNL Adobe Target] para experimentos e experiências personalizadas.

Ao usar a Injeção de Dependência .NET, basta adicionar o SDK na etapa de configuração do serviço, chamando `services.AddTargetLibrary()`;, em seguida, injetar `ITargetClient targetClient` no construtor do aplicativo.

Depois disso, use o `Initialize` Método do SDK para configurar o SDK, concluindo assim a etapa de inicialização.

## Método

`TargetClient` é criado usando `TargetClient.Create`.

## C\
#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig` é criado usando ClientConfig.Builder.

## C\
#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## Parâmetros

`TargetClientConfig.Builder` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| Cliente | string | Sim | None | [!UICONTROL ID do cliente do Target] |
| OrganizationId | string | Sim | None | [!UICONTROL ID da organização Experience Cloud] |
| Tempo limite | int | Não | 10000 | Tempo limite para todas as solicitações em milissegundos |
| Proxy |  | WebProxy | Não | null | Proxy para todos [!DNL Target] solicitações |
| RetryPolicy | Política | Não | null | Política de Repetição para todos [!DNL Target] solicitações |
| AsyncRetryPolicy | AsyncPolicy | Não | null | Política de repetição assíncrona para todos [!DNL Target] solicitações |
| Logger | ILogger | Não | null | Usado para o log de depuração de [!DNL Target] solicitações e respostas |
| ServerDomain | string | Não | `client.tt.omtrdc.net` | Substitui o nome de host padrão |
| Seguro | bool | Não | true | Não definido para impor o esquema HTTP |
| DefaultPropertyToken | string | Não | null | Define o token de propriedade padrão para cada `getOffers` chamar |
| TelemetryEnabled | bool | Não | true | Enviar dados de telemetria para melhorar a experiência de uso do SDK |
| DecisioningMethod | DecisioningMethod enum | Não | ServerSide | Deve ser definido como OnDevice ou Hybrid para ativar a decisão no dispositivo |
| OnDeviceDecisioningReady | Ação | Não | null | Delegar para o evento Pronto para decisão no dispositivo (chamado uma vez quando a decisão no dispositivo está pronta) |
| ArtifactDownloadSucceeded | Ação | Não | null | Delegar para download de artefato de decisão no dispositivo bem-sucedido (chamado em cada download de artefato bem-sucedido) |
| ArtifactDownloadFailed | Ação | Não | null | Delegar para falha no download de artefatos da decisão no dispositivo (chamado em cada download de artefato com falha) |
| OnDeviceEnvironment | string | Não | produção | Pode ser usado para especificar um ambiente diferente no dispositivo, como preparo |
| OnDeviceConfigHostname | string | Não | `assets.adobetarget.com` | Pode ser usado para especificar um host diferente para usar no download do arquivo de artefato da decisão no dispositivo |
| OnDeviceDecisioningPollingIntSecs | int | Não | 300 (5 min) | Número de segundos entre as buscas do arquivo de artefato de decisão no dispositivo |
| OnDeviceArtifactPayload | string | Não | null | Fornece a decisão no dispositivo com uma carga de artefato local para permitir execução imediata |

## Exemplo

## C\
#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
