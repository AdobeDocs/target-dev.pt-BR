---
title: Assinar eventos no SDK do  [!DNL Adobe Target] .NET
description: Saiba como assinar vários eventos que ocorrem no SDK do .NET usando o objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Eventos do SDK (.NET)

## Descrição

Ao [inicializar o SDK](initialize-sdk.md), um representante `OnDeviceDecisioningReady` opcional pode ser fornecido no objeto `TargetClientConfig`, que será chamado quando o SDK estiver pronto para chamadas de método no dispositivo. Há também alguns outros representantes disponíveis para lidar com o download de artefatos do [!UICONTROL on-device decisioning].

## Eventos 

Os seguintes delegados podem ser configurados para determinados eventos:

| Nome | Argumentos | Descrição |
| --- | --- | --- |
| OnDeviceDecisioningReady | None | Chamado apenas uma vez na primeira vez que o cliente estiver pronto para [!UICONTROL on-device decisioning] |
| ArtifactDownloadSucceeded | conteúdo da string do arquivo de artefato | Chamado sempre que um artefato [!UICONTROL on-device decisioning] é baixado |
| ArtifactDownloadFailed | Exceção | Chamado sempre que há uma falha ao baixar um artefato [!UICONTROL on-device decisioning] |

## Exemplo

### \.NET

```dotnet {line-numbers="true"}
var clientConfig = new TargetClientConfig.Builder("acmeclient", "1234567890@AdobeOrg")
    .SetDecisioningMethod(DecisioningMethod.OnDevice)
    .SetOnDeviceDecisioningReady(DecisioningReady)
    .SetArtifactDownloadSucceeded(artifact => Console.WriteLine("The artifact was successfully downloaded. Contents: " + artifact))
    .SetArtifactDownloadFailed(exception => Console.WriteLine("The artifact failed to download. Exception: " + exception.Message))
    .Build();

var targetClient = TargetClient.Create(clientConfig);

// ...

static void DecisioningReady()
{
    var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

    var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
        .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
        .Build();

    var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
}
```
