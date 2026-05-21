---
title: Como usar solicitações assíncronas no  [!DNL Adobe Target] Java SDK
description: Saiba como o  [!DNL Target] Java SDK oferece suporte a solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
TQID: https://experienceleague.adobe.com/Y9oTl8aU4-4HpMajdmy5KfvAwEFOpV0y9vUg7BdBRk8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 130
ht-degree: 3%

---

# Solicitações assíncronas (Java)

## Descrição

Um benefício da integração do lado do servidor é que você pode aproveitar a grande largura de banda e os recursos de computação disponíveis no lado do servidor usando o paralelismo. [!DNL Target] O Java SDK é compatível com solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.

## Métodos suportados

### Métodos

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## Exemplo

Um controlador de aplicativo `Spring` de exemplo pode ser semelhante a:

### Controlador de amostra

```javascript {line-numbers="true"}
@RestController
public class TargetRestController {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/mboxTargetOnlyAsync")
        public TargetDeliveryResponse mboxTargetOnlyAsync(
                @RequestParam(name = "mbox", defaultValue = "server-side-mbox") String mbox,
                HttpServletRequest request, HttpServletResponse response) {
            ExecuteRequest executeRequest = new ExecuteRequest()
                    .mboxes(getMboxRequests(mbox));

            TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                    .context(getContext(request))
                    .execute(executeRequest)
                    .cookies(getTargetCookies(request.getCookies()))
                    .build();
            CompletableFuture<TargetDeliveryResponse> targetResponseAsync =
                    targetJavaClient.getOffersAsync(targetDeliveryRequest);
            targetResponseAsync.thenAccept(tr -> setCookies(tr.getCookies(), response));
            simulateIO();
            TargetDeliveryResponse targetResponse = targetResponseAsync.join();
            return targetResponse;
        }

    /**
     * Function for simulating network calls like other microservices and database calls
     */
    private void simulateIO() {
        try {
            Thread.sleep(200L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```

Este exemplo supõe que você tenha [inicializado o SDK](initialize-sdk.md) como um bean de mola e que você tenha [métodos de utilitário](utility-methods.md) disponíveis.

A solicitação [!DNL Target] é acionada antes de `simulateIO` e, quando for executada, o resultado alvo também deve estar pronto. Mesmo que não seja, você terá uma economia significativa na maioria dos casos.
