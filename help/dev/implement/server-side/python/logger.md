---
title: Inicializar o [!DNL Adobe Target] Python SDK para registrar solicitações
description: Saiba como registrar solicitações no [!DNL Adobe Target] Python SDK.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Logger (Python)

## Descrição

Quando [inicialização do SDK](initialize-sdk.md), o `options["logger"]` é um objeto opcional. Por padrão, um agente de log de nível INFO será criado em `adobe.target` namespace. No entanto, para personalizar o nível de log ou depurar efetivamente quando ocorrer um problema, uma variável `logger` objeto pode ser fornecido ao inicializar o SDK.

A variável `logger` espera-se que o objeto tenha um `debug()` e uma `error()` método. Quando um logger apropriado é fornecido, [!DNL Target] as solicitações e respostas serão registradas.

## Exemplo

### Python

```python {line-numbers="true"}
logger = logging.getLogger("org.logger")
logger.setLevel(logging.DEBUG)

client_options = {
  "client": "acmeclient",
  "organization_id": "1234567890@AdobeOrg",
  "logger": logger
}
target_client = TargetClient.create(client_options)
```

Você deve ver solicitações e respostas sendo impressas no console.
