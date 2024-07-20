---
title: Buscar perfis
description: Saiba como usar as APIs de perfil do Adobe Target para buscar dados do visitante para usar no [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
source-git-commit: b8ccfdcaff6aa17a325727df0a9ffd716e44519b
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Buscar perfis

Um perfil [!DNL Target] pode ser obtido de três maneiras: usando um `[!DNL Experience Cloud Visitor ID]` (`ECID`), `tntid` ou `thirdPartyId`.

## Usando um [!DNL Experience Cloud Visitor ID] (ECID)

Você pode buscar um perfil com base no `ECID`. O método HTTP deve ser GET.

O URL é semelhante ao seguinte exemplo:

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

Substitua `<clientCode>` por [!DNL Target] [!UICONTROL Client Code] e `<ECID>` por [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID]).

## Uso de um tntid

[!DNL Target] atribui automaticamente `tntid` para cada solicitação.

O exemplo a seguir mostra o formato de solicitação para buscar um perfil usando um `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Substitua `<your-client-code>` e `your-tnt-id` e acione uma solicitação GET. Este é um exemplo de chamada de busca de perfil usando um `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Uso de um thirdPartyId

[!DNL Adobe Target] perfis podem ser aumentados com seu próprio identificador (por exemplo: ID do CRM, `uuid`, número de associação e assim por diante).

Consulte [Atualizar perfis](/help/dev/administer/profile-api/profile-api-overview.md) para saber como anexar um `thirdPartyId` ao seu perfil.

O exemplo a seguir mostra o formato de solicitação para buscar um perfil usando um `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Substitua `<your-client-code>` e `your-thirdpartyid` e acione uma solicitação GET. Este é um exemplo de chamada de busca de perfil usando um [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Quando esta chamada é feita, o [!DNL Target] tenta localizar o perfil primeiro no cluster anotado na solicitação de borda, ou onde quer que o perfil esteja localizado e retornar o conteúdo. O conteúdo do perfil é retornado no formato JSON.

## Autenticação

O [!DNL Target Profile API] pode ser protegido ativando a autenticação na interface do usuário do [!DNL Target], conforme descrito aqui. Quando a autenticação estiver ativada, todas as solicitações de API de perfil devem ter o token de autenticação de perfil definido nos cabeçalhos da solicitação. O token pode ser gerado usando a interface do usuário [!DNL Target] ou as etapas explicadas acima, na seção [Token de Autenticação de Perfil](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank}.

## Medição

Essas chamadas não contam para suas chamadas da mbox.

## Tratamento de erros

No caso de uma chamada para `/thirdPartyId` com um `thirdPartyId` inválido ou expirado especificado:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Se o perfil não puder ser localizado ou tiver expirado:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
