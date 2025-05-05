---
title: Enviar notificações de exibição ou clique para  [!DNL Adobe Target] usando o Python SDK
description: Saiba como usar sendNotifications() para enviar notificações de exibição ou clique em  [!DNL Adobe Target] para medição e relatórios.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 8%

---

# Enviar notificações (Python)

## Descrição

`send_notifications()` é usado para enviar notificações de clique ou exibição para [!DNL Adobe Target] para medição e relatórios.

>[!NOTE]
>
>Quando um objeto `execute` com parâmetros obrigatórios estiver dentro da própria solicitação, a impressão será aumentada automaticamente para atividades qualificadas.

Os métodos do SDK que incrementarão uma impressão automaticamente são:

* `get_offers()`
* `get_attributes()`

Quando um objeto `prefetch` é transmitido na solicitação, a impressão não é automaticamente incrementada para as atividades com mboxes no objeto `prefetch`. `Send_notifications()` deve ser usado para experiências previamente buscadas para incrementar impressões e conversões.

## Método

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## Parâmetros

`options` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| solicitação | DeliveryRequest | Sim | None | Está em conformidade com a solicitação [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | str | não | None | [!DNL Target] cookie |
| target_location_hint | str | não | None | [!DNL Target] dica de localização |
| consumer_id | str | não | None | Ao compilar várias chamadas, IDs de consumidor diferentes devem ser fornecidas |
| customer_ids | list[CustomerId] | não | None | Uma lista de IDs de cliente em formato compatível com a ID de visitante |
| session_id | str | não | None | Usado para vincular várias solicitações |
| callback | chamável | não | None | Se manipular a solicitação de forma assíncrona, o retorno de chamada será chamado quando a resposta estiver pronta |
| err_callback | chamável | não | None | Se estiver tratando a solicitação de forma assíncrona, o retorno de chamada de erro é chamado quando a exceção é gerada |

## Devoluções

`Returns` um `TargetDeliveryResponse` se for chamado de forma síncrona (padrão), ou um `AsyncResult` se for chamado com um retorno de chamada. `TargetDeliveryResponse` tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| resposta | DeliveryResponse | Está em conformidade com a resposta [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | dict | [!DNL Target] cookie |
| target_location_hint_cookie | dict | Cookie de dica de localização [!DNL Target] |
| analytics_details | list[AnalyticsResponse] | [!DNL Analytics] carga, em caso de uso de [!DNL Analytics] no lado do cliente |
| trace |  | lista[dica] | Dados de rastreamento agregados para todas as mboxes/exibições de solicitação |
| response_tokens | lista[dica] | Uma lista de [ tokens &#x200B; resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=pt-BR) |
| meta | dict | Metadados de decisão adicionais para uso com decisão no dispositivo |

## Exemplo

Primeiro, vamos criar a solicitação [!UICONTROL Target Delivery API] de busca prévia de conteúdo para as mboxes `home` e `product1`.

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

Uma resposta bem-sucedida conterá um objeto de resposta [!UICONTROL Target Delivery API], que contém conteúdo previamente buscado para as mboxes solicitadas. Um objeto de amostra `target_response["response"]` (formatado como um diretório) pode aparecer da seguinte maneira:

### Python

```python {line-numbers="true"}
{
  "status": 200,
  "requestId": "e8ac2dbf5f7d4a9f9280f6071f24a01e",
  "id": {
    "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "adobetargetmobile",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "home",
        "options": [
          {
            "type": "html",
            "content": "HOME OFFER",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      },
      {
        "index": 1,
        "name": "product1",
        "options": [
          {
            "type": "html",
            "content": "TEST OFFER 1",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      }
    ]
  }
}
```

Observe os campos mbox `name` e `state`, bem como o campo `eventToken`, em cada uma das opções de conteúdo do Target. Eles devem ser fornecidos na solicitação `send_notifications()`, assim que cada opção de conteúdo for exibida. Suponhamos que a mbox `product1` tenha sido exibida em um dispositivo que não seja um navegador. A solicitação de notificações será exibida da seguinte maneira:

### Python

```python {line-numbers="true"}
notification_mbox = NotificationMbox(name="product1",
                                     state="J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
notification = Notification(
    id="1",
    type=MetricType.DISPLAY,
    timestamp=1621530726000,  # Epoch time in milliseconds
    mbox=notification_mbox,
    tokens=["t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="]
)
notification_request = DeliveryRequest(notifications=[notification])
```

Observe que incluímos o estado da mbox e o token do evento correspondente à oferta [!DNL Target] entregue na resposta da busca prévia. Depois de criar a solicitação de notificações, podemos enviá-la para [!DNL Target] por meio do método de API `send_notifications()`:

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
