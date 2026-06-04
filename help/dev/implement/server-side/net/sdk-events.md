---
title: Assinar eventos no  [!DNL Adobe Target] .NET SDK
description: Saiba como assinar vários eventos que ocorrem no .NET SDK usando o objeto [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
TQID: https://experienceleague.adobe.com/oeGknU-pW1-XjVrxn8JNEPoFBF8Gntt-vaVnqjdyTC8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 133
ht-degree: 5%

---

# Eventos da SDK (.NET)

## Descrição

Ao [inicializar o SDK](initialize-sdk.md), um representante `OnDeviceDecisioningReady` opcional pode ser fornecido no objeto `TargetClientConfig`, que será chamado quando o SDK estiver pronto para chamadas de método no dispositivo. Há também alguns outros representantes disponíveis para lidar com o download de artefatos da [!UICONTROL decisão no dispositivo].

## Eventos

Os seguintes delegados podem ser configurados para determinados eventos:

| Nome | Argumentos | Descrição |
| --- | --- | --- |
| OnDeviceDecisioningReady | None | Chamado apenas uma vez na primeira vez que o cliente estiver pronto para a [!UICONTROL decisão no dispositivo] |
| ArtifactDownloadSucceeded | conteúdo da string do arquivo de artefato | Chamado sempre que um artefato [!UICONTROL de decisão no dispositivo] é baixado |
| ArtifactDownloadFailed | Exceção | Chamado sempre que há uma falha ao baixar um artefato [!UICONTROL de decisão no dispositivo] |

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
