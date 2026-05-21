---
title: Implementar configuração de proxy no  [!DNL Adobe Target] Java SDK
description: Saiba como definir a configuração de proxy do TargetClient no  [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
TQID: https://experienceleague.adobe.com/Vo8KrM-3AGIvoO-E-iAQcAPqzXE24BM30LX7ji5E2Nk
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 2%

---

# Configuração de proxy (Java)

## Proxy básico

Se o aplicativo que está executando o SDK exigir um proxy para acessar a Internet, o `TargetClient` precisará ser configurado com uma configuração de proxy da seguinte maneira.

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

Se uma autenticação de proxy for necessária, as credenciais poderão ser passadas como parâmetros para o construtor `ClientProxyConfig`, conforme o exemplo abaixo. Observe que isso só funciona para autenticação de proxy simples de nome de usuário/senha.

### Autenticação básica de proxy

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Decisão no dispositivo

Para solicitações de busca do artefato de regras, o proxy deve ser configurado para não armazenar a resposta em cache. No entanto, se não for possível configurar o mecanismo de cache do proxy para essa solicitação, use uma opção de configuração como solução alternativa para ignorar o cache em nível de proxy. Essa solução alternativa adiciona o cabeçalho `Authorization` com um valor de cadeia de caracteres vazio à solicitação de regras, o que deve indicar ao proxy que a resposta não deve ser armazenada em cache.

Para habilitar essa solução alternativa, defina o seguinte:

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


