---
title: Inscrever-se em eventos no Java SDK [!DNL Adobe Target]
description: Saiba como assinar vários eventos que ocorrem no Java SDK usando o objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
TQID: 'https://experienceleague.adobe.com/x3aig-jM-GXzmLNcUNclZUK9Y49tuSF9-sdkxzJFtiM'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%
---
# Eventos da SDK (Java)

## Descrição

Ao [inicializar o SDK](initialize-sdk.md), um objeto `OnDeviceDecisioningHandler` opcional pode ser fornecido no objeto `ClientConfig`. Ele pode ser usado para assinar vários eventos que ocorrem no SDK. Por exemplo, o evento `onDeviceDecisioningReady` pode ser usado com uma função de retorno de chamada que será invocada quando o SDK estiver pronto para chamadas de método.

## Eventos

O objeto `OnDeviceDecisioningHandler` contém os seguintes retornos de chamada, que são chamados para determinados eventos:

| Nome | Argumentos | Descrição |
| --- | --- | --- |
| onDeviceDecisioningReady | None | Chamado apenas uma vez na primeira vez que o cliente estiver pronto para a [!UICONTROL decisão no dispositivo] |
| artifactDownloadSucceeded | byte[] conteúdo do arquivo de artefato | Chamado sempre que um artefato [!UICONTROL de decisão no dispositivo] é baixado |
| artifactDownloadFailed | Exceção | Chamado sempre que há uma falha ao baixar um artefato de [!UICONTROL decisão no dispositivo] |

## Exemplo

### Eventos da SDK

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
