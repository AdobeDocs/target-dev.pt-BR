---
title: API de perfis do Adobe Target
description: Saiba como usar as APIs de perfil do Adobe Target para enviar dados do visitante para o [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: 289299a52e5611c0da341f313aa4a447fcf3666a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# [!DNL Adobe Target Profiles API] visão geral

[!DNL Adobe Target] O cria e mantém um perfil para cada usuário individual. Esse perfil é armazenado no [!DNL Target] cluster de borda e é atualizado em tempo real após cada visita.

## Perfis [!DNL Postman] coleção

[!DNL Postman] O é um aplicativo que facilita o acionamento de chamadas de API. Este [!DNL Postman] a coleção contém todos os [!DNL Profile API] chamadas. Clique em [Executar no Postman](https://www.getpostman.com/collections/ec7376f9028977ccaa99){target=_blank} para importar a coleção de APIs de perfil.

## Documentação da API de perfis herdados.

A documentação da API de perfis herdada pode ser encontrada aqui: [https://developers.adobetarget.com/api/#profiles](https://developers.adobetarget.com/api/#profiles){target=_blank}

## Estrutura de um [!DNL Target] perfil

Um perfil do Target consiste nos seguintes objetos:

| Objeto | Detalhes |
| --- | --- |
| `clientcode` | A variável [!DNL Target] código de cliente ao qual o perfil está associado. |
| `visitorId` | O identificador do perfil. Isso pode ser um `tntid`, `thirdpartyid`ou `marketingcloudvisitorid`. |
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
