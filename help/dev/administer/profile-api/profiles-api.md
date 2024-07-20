---
title: API de perfis do Adobe Target
description: Saiba como usar as APIs de perfil do Adobe Target para enviar dados do visitante para o  [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 480cbbbe-4822-48c3-80d4-53628dee57b0
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 1%

---

# Visão geral de [!DNL Adobe Target Profiles API]

[!DNL Adobe Target] cria e mantém um perfil para cada usuário individual. Este perfil está armazenado no cluster de borda [!DNL Target] e é atualizado em tempo real após cada visita.

## Estrutura de um perfil [!DNL Target]

Um perfil do Target consiste nos seguintes objetos:

| Objeto | Detalhes |
| --- | --- |
| `clientcode` | O código de cliente [!DNL Target] ao qual o perfil está associado. |
| `visitorId` | O identificador do perfil. Pode ser um `tntid`, `thirdpartyid` ou `marketingcloudvisitorid`. |
| `modifiedAt` | O carimbo de data e hora de quando o perfil foi atualizado pela última vez. |
| `profileAttributes` | Lista de todos os atributos de perfil armazenados como pares de valores-chave no perfil individual. |

### Exemplo de estrutura de perfil

```
{
    "client": "<your-tenant-name>",
    "visitorId": "a1-mbox3rdPartyId",
    "modifiedAt": "2017-08-18T17:53:39.003-04:00",
    "profileAttributes": {
        "insurance": {
            "value": "false",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "country": {
            "value": "france",
            "modifiedAt": "2017-07-31T14:26:30.879-04:00"
        },
        "checking": {
            "value": "true",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "user.memberlevel": {
            "value": "0.0",
            "modifiedAt": "2017-08-09T18:18:04.661-04:00"
        },
        "param1": {
            "value": "value1",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "param2": {
            "value": "value2",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "firstSessionStart": {
            "value": "1500648715286",
            "modifiedAt": "2017-07-21T10:51:55.286-04:00"
        },
        "entity.name": {
            "value": "my-entityName",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "entity.id": {
            "value": "my-entityId",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        }
    }
}
```
