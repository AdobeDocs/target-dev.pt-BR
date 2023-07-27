---
title: Saiba como configurar o Cliente HTTP personalizado
description: Saiba como configurar o TargetClient usando ClientConfig.builder().httpClient().
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Configuração do cliente HTTP personalizado (Java)

Se o aplicativo que executa o SDK exigir um cliente HTTP personalizado, para habilitar recursos como configurar o SSL ou adicionar cabeçalhos padrão a solicitações, então a variável `TargetClient` precisará ser configurado usando `ClientConfig.builder().httpClient()`:

## Configuração básica de cliente HTTP personalizado

Atualmente, o SDK é compatível com clientes HTTP que implementam o `org.apache.http.client.HttpClient` interface.

### Implementação básica

```java {line-numbers="true"}
CloseableHttpClient httpClient = HttpClients.custom().build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Configuração do cliente HTTP personalizado com configuração SSL

Este é um exemplo de como configurar o SSL no `TargetClient` personalizando o `HttpClient` passado para o `ClientConfig`. O trecho de código a seguir usa classes do `org.apache.http.conn.ssl` pacote para configuração do SSL.

### Implementação de SSL

```java {line-numbers="true"}
SSLContext context = SSLContextBuilder.create().build();
SSLConnectionSocketFactory sslSocketFactory = new SSLConnectionSocketFactory(context);
CloseableHttpClient httpClient = HttpClients.custom().setSSLSocketFactory(sslSocketFactory).build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
