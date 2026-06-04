---
title: Inscrever-se em eventos no  [!DNL Adobe Target] Python SDK
description: Saiba como assinar vários eventos que ocorrem no Python SDK usando o objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
TQID: https://experienceleague.adobe.com/iFtlxw8Wlc9EMtDTndtXD7a2gu1TzGM6ijXire9gHPk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 166
ht-degree: 3%

---

# Eventos da SDK (Python)

## Descrição

Ao [inicializar o SDK](initialize-sdk.md), o dict `options["events"]` é um objeto opcional com chaves de nome de evento e valores de função de retorno de chamada. Ele pode ser usado para assinar vários eventos que ocorrem no SDK. Por exemplo, o evento `client_ready` pode ser usado com uma função de retorno de chamada que será invocada quando o SDK estiver pronto para chamadas de método.

Quando a função `callback` é chamada, um objeto de evento é transmitido. Cada evento tem um `type` correspondente ao nome do evento, e alguns eventos incluem propriedades adicionais com informações pertinentes.

## Eventos

| Nome do evento (tipo) | Descrição | Propriedades adicionais do evento |
| --- | --- | --- |
| client_ready | Emitido quando o artefato é baixado e o SDK está pronto para chamadas get_offers. Recomendado ao usar o método de decisão no dispositivo. | None |
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
