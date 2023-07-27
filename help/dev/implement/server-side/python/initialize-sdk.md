---
title: Inicialize o Python SDK usando o método de criação
description: Saiba como usar o método de criação para inicializar o Python SDK e instanciar o [!UICONTROL TargetClient] para fazer chamadas para [!DNL Adobe Target] para experimentos e experiências personalizadas.
feature: APIs/SDKs
exl-id: 3e231e8e-696d-45c7-b733-79bf99da5bec
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 19%

---

# Inicializar o SDK do Python

Descrição Use o `create` para inicializar o Python SDK e instanciar o [!UICONTROL Cliente do Target] para fazer chamadas para [!DNL Adobe Target] para experimentos e experiências personalizadas.

## Método

### criar

```python {line-numbers="true"}
TargetClient.create(options)
```

## Parâmetros

`options` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| cliente | str | Sim | None | [!UICONTROL ID de cliente do Adobe Target] |
| organization_id | str | Sim | None | [!UICONTROL ID da organização Experience Cloud] |
| timeout | int | Não | 3000 | Tempo limite em milissegundos |
| server_domain | str | Não | `client.tt.omtrdc.net` |  | Substitui o nome de host padrão |
| seguro | bool | Não | true | Não definido para impor o esquema HTTP |
| logger | principal | Não | Agente de informações |  | Substitui o agente de log INFO padrão |
| target_location_hint | str | Não | None | [!DNL Target] dica de localização |
| property_token | str | Não | None | [!DNL Target] Token de propriedade. Se especificado aqui, todas as chamadas get_offers usarão esse valor. |
| método_de_decisão | str | Não | lado do servidor | Determina que método de decisão usar ([no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), lado do servidor, híbrido) |
| polling_interval | int | Não | 300000 (5 minutos) | Intervalo de sondagem para o [artefato da regra de decisão no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (em ms) |
| localização_artefato | str | Não | None | Um url totalmente qualificado para o [artefato da regra de decisão no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Substitui o local determinado internamente. |
| artifact_payload | principal | Não | None | A carga JSON do [artefato da regra de decisão no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Se especificado, é usado em vez de solicitar um de um URL. |
| [events](sdk-events.md) | dict &lt;str callable=&quot;&quot;> | Não | None | Um objeto opcional com chaves de nome de evento e valores de função de retorno de chamada |
| environment_id | int | Não | produção | A variável [!DNL Target] ID do ambiente |
| ambiente | str | Não | produção | A variável [!DNL Target] nome do ambiente |
| cdn_environment | str | Não | produção | O nome do ambiente CDN |
| telemetry_enabled | bool | Não | Verdadeiro | Se definido como Falso, os dados de telemetria não serão enviados para [!DNL Adobe] |
| version | str | Não | None | O número da versão deste SDK |

## Exemplo

### Python

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def client_ready_callback(ready_event):
    # make calls to Adobe Target

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
