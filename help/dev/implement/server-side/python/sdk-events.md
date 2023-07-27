---
title: Inscrever-se em eventos no [!DNL Adobe Target] Python SDK
description: Saiba como se inscrever em vários eventos que ocorrem no Python SDK usando o [!UICONTROL OnDeviceDecisioningHandler] objeto.
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 3%

---

# Eventos do SDK (Python)

## Descrição

Quando [inicialização do SDK](initialize-sdk.md), o `options["events"]` dict é um objeto opcional com chaves de nome de evento e valores de função de retorno de chamada. Ele pode ser usado para assinar vários eventos que ocorrem no SDK. Por exemplo, a variável `client_ready` O evento pode ser usado com uma função de retorno de chamada que será invocada quando o SDK estiver pronto para chamadas de método.

Quando a variável `callback` for chamada, um objeto de evento será transmitido. Cada evento tem um `type` correspondente ao nome do evento, e alguns eventos incluem propriedades adicionais com informações pertinentes.

## Eventos 

| Nome do evento (tipo) | Descrição | Propriedades adicionais do evento |
| --- | --- | --- |
| client_ready | Emitido quando o artefato é baixado e o SDK está pronto para chamadas get_offers. Recomendado ao usar | no dispositivo. | None |
| artifact_download_succeeded | Emitido sempre que um novo artefato é baixado. | artifact_payload, artifact_location |
| artifact_download_failed | Emitido sempre que ocorre falha no download de um artefato. | artifact_location, erro |

## Exemplo

### Python

```python {line-numbers="true"}
def client_ready_callback():
    # make get_offers requests

def artifact_download_succeeded(event):
    print("The artifact was successfully downloaded from {}".format(event.artifact_location))
    # optionally do something with event.artifact_payload, like persist it

def artifact_download_failed(event):
    print("The artifact failed to download from {} with the following error: {}"
          .format(event.artifact_location, str(event.error)))

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback,
        "artifact_download_succeeded": artifact_download_succeeded,
        "artifact_download_failed": artifact_download_failed
    }
}
target_client = target_client.create(client_options)
```
