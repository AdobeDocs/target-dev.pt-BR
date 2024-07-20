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

Se o aplicativo que está executando o SDK exigir um Cliente HTTP personalizado, para habilitar recursos como a configuração do SSL ou a adição de cabeçalhos padrão a solicitações, o `TargetClient` precisará ser configurado usando `ClientConfig.builder().httpClient()`:

## Configuração básica de cliente HTTP personalizado

Atualmente, o SDK oferece suporte a Clientes HTTP que implementam a interface `org.apache.http.client.HttpClient`.

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

Este é um exemplo de como configurar o SSL no `TargetClient` personalizando o `HttpClient` passado para o `ClientConfig`. O trecho de código a seguir usa classes do pacote `org.apache.http.conn.ssl` para configuração SSL.

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
