---
title: Saiba como configurar o Cliente HTTP personalizado
description: Saiba como configurar o TargetClient usando ClientConfig.builder().httpClient().
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
TQID: 'https://experienceleague.adobe.com/SwijRIrhqSG4Mlij4sBH9Kx8tRB-6Bo7eyMoUZREOW8'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
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
