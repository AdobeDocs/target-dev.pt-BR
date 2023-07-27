---
title: Implementar configuração de proxy no [!DNL Adobe Target] SDK do Java
description: Saiba como definir a configuração de proxy do TargetClient no [!DNL Adobe Target] SDK do Java.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 1%

---

# Configuração de proxy (Java)

## Proxy básico

Se o aplicativo que executa o SDK exigir um proxy para acessar a Internet, a variável `TargetClient` precisará ser configurado com uma configuração de proxy da seguinte maneira.

### Configuração básica de proxy

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Autenticação

Se uma autenticação de proxy for necessária, as credenciais poderão ser passadas como parâmetros para o `ClientProxyConfig` conforme o exemplo abaixo. Observe que isso só funciona para autenticação de proxy simples de nome de usuário/senha.

### Autenticação básica de proxy

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
