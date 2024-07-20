---
title: Inicialize o  [!DNL Adobe Target] Python SDK para registrar solicitações
description: Saiba como registrar solicitações no  [!DNL Adobe Target] Python SDK.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Logger (Python)

## Descrição

Ao [inicializar o SDK](initialize-sdk.md), o objeto `options["logger"]` é opcional. Por padrão, um agente de nível INFO será criado no namespace `adobe.target`. No entanto, para personalizar efetivamente o nível de log ou depurar quando ocorrer um problema, um objeto `logger` pode ser fornecido ao inicializar o SDK.

O objeto `logger` deve ter um método `debug()` e `error()`. Quando um agente de log apropriado for fornecido, [!DNL Target] solicitações e respostas serão registradas.

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
