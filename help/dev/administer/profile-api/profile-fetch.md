---
title: Buscar perfis
description: Saiba como usar as APIs de perfil do Adobe Target para buscar dados do visitante para usar no [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: 49acf92bbe06dbcee36fef2b7394acd7ce37baad
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Atualizar perfis

A [!DNL Target] O perfil do pode ser obtido de três maneiras: usando uma `[!DNL Experience Cloud Visitor ID]` (`ECID`), `tntid` ou `thirdPartyId`.

## Uso de um [!DNL Experience Cloud Visitor ID] (ECID)

Você pode buscar um perfil com base na variável `ECID`. O método HTTP deve ser GET.

O URL é semelhante ao seguinte exemplo:

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

Substituir `<clientCode>` com o seu [!DNL Target] [!UICONTROL Código do cliente] e `<ECID>` com o seu [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID]).

## Uso de um tntid

[!DNL Target] atribui automaticamente um `tntid` para cada solicitação.

O exemplo a seguir mostra o formato da solicitação para buscar um perfil usando um `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Substituir `<your-client-code>` e `your-tnt-id` e acione uma solicitação do GET. Este é um exemplo de chamada de busca de perfil usando um `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Uso de um thirdPartyId

[!DNL Adobe Target] os perfis podem ser aumentados com seu próprio identificador (por exemplo: ID de CRM, `uuid`, número de associação e assim por diante).

Consulte [Atualizar perfis](/help/dev/administer/profile-api/profile-api-overview.md) para saber como anexar um `thirdPartyId` ao seu perfil.

O exemplo a seguir mostra o formato da solicitação para buscar um perfil usando um `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Substituir `<your-client-code>` e `your-thirdpartyid` e acione uma solicitação do GET. Este é um exemplo de chamada de busca de perfil usando um [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Quando esta chamada for feita, [!DNL Target] O tenta localizar o perfil primeiro no cluster anotado na solicitação de borda ou onde o perfil estiver localizado e retornar o conteúdo. O conteúdo do perfil é retornado no formato JSON.

## Autenticação

A variável [!DNL Target Profile API] pode ser protegido ativando a autenticação a partir do [!DNL Target] Interface do usuário conforme descrito aqui. Quando a autenticação estiver ativada, todas as solicitações de API de perfil devem ter o token de autenticação de perfil definido nos cabeçalhos da solicitação. O token pode ser gerado usando o [!DNL Target] ou usando as etapas explicadas acima na variável [Token de autenticação de perfil](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} seção.

## Medição

Essas chamadas não contam para suas chamadas da mbox.

## Tratamento de erros

No caso de uma chamada para `/thirdPartyId` com um inválido ou um expirado `thirdPartyId` especificado:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Se o perfil não puder ser localizado ou tiver expirado:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
