---
title: Inicializar o .NET SDK usando o método de criação
description: Saiba como usar o método de criação para inicializar o Java SDK e instanciar o [!UICONTROL TargetClient] para fazer chamadas para [!DNL Adobe Target] experiências e experiências personalizadas.
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
TQID: https://experienceleague.adobe.com/uOEojoWWjXmcDl2yY1UmSRD-EXL0j9p-p-eE8PXa7Rk
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: b18c88053a47a97d6718a69cb72cb4e5d99969c8
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 15%

---

# Inicializar o .NET SDK

## Descrição

Use o método `Create` para inicializar o .NET SDK e instanciar o [!UICONTROL Cliente de Destino] a fazer chamadas para [!DNL Adobe Target] para experiências e experiências personalizadas.

Ao usar a Injeção de Dependência .NET, basta adicionar o SDK na etapa de configuração do serviço, chamando `services.AddTargetLibrary()`; e inserir `ITargetClient targetClient` no construtor do aplicativo.

Depois disso, use o método `Initialize` do SDK para configurar o SDK, concluindo assim a etapa de inicialização.

## Método

`TargetClient` é criado usando `TargetClient.Create`.

## C#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig` é criado usando ClientConfig.Builder.

## C#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## Parâmetros

`TargetClientConfig.Builder` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| Cliente | string | Sim | None | [!UICONTROL ID do Cliente de Destino] |
| OrganizationId | string | Sim | None | [!UICONTROL ID da organização da Experience Cloud] |
| Tempo-limite | int | Não | 10000 | Tempo limite para todas as solicitações em milissegundos |
| Proxy | WebProxy | Não | null | Proxy para todas as [!DNL Target] solicitações |
| RetryPolicy | Política | Não | null | Tentar novamente a política para todas as solicitações [!DNL Target] |
| AsyncRetryPolicy | AsyncPolicy | Não | null | Política de repetição assíncrona para todas as [!DNL Target] solicitações |
| Logger | ILogger | Não | null | Usado para o log de depuração de [!DNL Target] solicitações e respostas |
| ServerDomain | string | Não | `client.tt.omtrdc.net` | Substitui o nome de host padrão |
| Seguro | bool | Não | true | Não definido para impor o esquema HTTP |
| DefaultPropertyToken | string | Não | null | Define o token de propriedade padrão para cada chamada de `getOffers` |
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

## C#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
