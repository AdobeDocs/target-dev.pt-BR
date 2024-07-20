---
title: Assinar eventos no  [!DNL Adobe Target] SDK Java
description: Saiba como assinar vários eventos que ocorrem no SDK do Java usando o objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# Eventos do SDK (Java)

## Descrição

Ao [inicializar o SDK](initialize-sdk.md), um objeto `OnDeviceDecisioningHandler` opcional pode ser fornecido no objeto `ClientConfig`. Ele pode ser usado para assinar vários eventos que ocorrem no SDK. Por exemplo, o evento `onDeviceDecisioningReady` pode ser usado com uma função de retorno de chamada que será invocada quando o SDK estiver pronto para chamadas de método.

## Eventos 

O objeto `OnDeviceDecisioningHandler` contém os seguintes retornos de chamada, que são chamados para determinados eventos:

| Nome | Argumentos | Descrição |
| --- | --- | --- |
| onDeviceDecisioningReady | None | Chamado apenas uma vez na primeira vez que o cliente estiver pronto para [!UICONTROL on-device decisioning] |
| artifactDownloadSucceeded | byte[] conteúdo do arquivo de artefato | Chamado sempre que um artefato [!UICONTROL on-device decisioning] é baixado |
| artifactDownloadFailed | Exceção | Chamado sempre que há uma falha ao baixar um artefato [!UICONTROL on-device decisioning] |

## Exemplo

### Eventos do SDK

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .defaultDecisioningMethod(DecisioningMethod.ON_DEVICE)
        .onDeviceDecisioningHandler(new OnDeviceDecisioningHandler() {
            @Override
            public void onDeviceDecisioningReady() {
                // make getOffers requests
                makeTargetRequests();
            }

            @Override
            public void artifactDownloadSucceeded(byte[] artifactData) {
                System.out.println("The artifact was successfully downloaded.");
            }

            @Override
            public void artifactDownloadFailed(TargetClientException e) {
                System.out.println("The artifact failed to download.");
            }
        }).build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);


void makeTargetRequests() {
    List<MboxRequest> mboxRequests = new ArrayList<>();
    mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
            .context(new Context().channel(ChannelType.WEB))
            .execute(new ExecuteRequest().setMboxes(mboxRequests))
            .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
}
```
