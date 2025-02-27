---
title: Inicialize o Java SDK  [!DNL Adobe Target]  para registrar solicitações
description: Saiba como registrar solicitações no  [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: 526445fccee9b778b7ac0d7245338f235f11d333
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 4%

---

# Logger (Java)

## Descrição

Ao [inicializar o SDK](initialize-sdk.md), há várias opções no objeto `ClientConfig`, que podem ser definidas para solicitações de log.

| Opção | Descrição |
| --- | --- |
| `logRequests` | Registra todo o corpo da solicitação, bem como o corpo da resposta. |
| `logRequestStatus` | Registra o URL da solicitação, o status e o tempo de resposta. |

O Java SDK [!DNL Target] usa o log `slf4j`. Você precisa fornecer sua implementação do agente de log, como `java.util.logging`, `logback` e `log4j`. Consulte [https://www.slf4j.org/manual.html](https://www.slf4j.org/manual.html) para obter mais informações. Todos os logs serão impressos em `debug`.

## Exemplo

Adicione a dependência `slf4j`.

>[!BEGINTABS]

>[!TAB Gradle]

### Gradle

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

Habilite os logs do `DEBUG` com base na sua implementação e marque os sinalizadores de log de solicitação.

### Depurar

```javascript {line-numbers="true"}
System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
ClientConfig config = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .logRequests(true)
        .logRequestStatus(true)
        .build();

TargetClient targetClient = TargetClient.create(config);
```

Você deve ver solicitações, respostas e tempos de resposta sendo impressos no console.
