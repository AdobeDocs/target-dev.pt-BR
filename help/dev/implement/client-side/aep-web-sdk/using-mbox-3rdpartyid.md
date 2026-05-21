---
title: Sincronização de perfil em tempo real para mbox3rdPartyId
description: Saiba como usar mbox3rdPartyId com o  [!DNL Adobe Experience Platform Web SDK].
keywords: personalização;destino;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
feature: AEP Web SDK
exl-id: 1c5067ef-38b3-4bf1-bd39-ea0f2cbd1074
TQID: https://experienceleague.adobe.com/Ej2sYVnBD9orRTlsMQG85JJV7dvn-9gnABDa0b8uBlM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 34%

---

# Usar mbox3rdPartyId

A `mbox3rdPartyId` no [!DNL Adobe Target] é a ID de visitante da sua empresa, como a ID de associação do programa de fidelidade da empresa.

Quando um visitante faz logon no site de uma empresa, a empresa normalmente cria uma ID associada à conta, ao cartão de fidelidade, ao número de associado ou a outros identificadores aplicáveis do visitante dessa empresa. [Saiba mais](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)

## Como usar o `mbox3rdPartyId` com o [!DNL Platform Web SDK]

### Etapa 1: configurar o `Target Third Party ID Namespace`

Configure o `Target Third Party ID Namespace` na sua [Sequência de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview), usando o Namespace de ID que você deseja usar como uma ID de terceiros para a mbox. [Saiba mais sobre namespaces de ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![Interface do usuário do Experience Platform mostrando o campo de namespace da ID de terceiros do Target.](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### Etapa 2: Enviar o `mbox3rdpartyId` para [!DNL Target]

Envie o `mbox3rdpartyId` para [!DNL Target] no comando `sendEvent`, usando o namespace de ID que você configurou na Etapa 1.
[Saiba mais sobre como enviar IDs](/help/dev/implement/client-side/aep-web-sdk/using-mbox-3rdpartyid.md)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
