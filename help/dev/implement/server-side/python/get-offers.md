---
title: Usar getOffers() em [!DNL Adobe Target] ao usar o SDK do Python
description: Saiba como usar getOffers() para executar uma decisão e recuperar uma experiência do  [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---

# Obter Ofertas (Python)

## Descrição

`get_offers()` é usado para executar uma decisão e recuperar uma experiência de [!DNL Adobe Target].


## Método

### getOffers

```python {line-numbers="true"}
target_client_instance.get_offers(options)
```

## Parâmetros

O diretório `options` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| solicitação | DeliveryRequest | Sim | None | Está em conformidade com a solicitação [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | str | não | None | [!DNL Target] cookie |
| target_location_hint | str | não | None | [!DNL Target] dica de localização |
| consumer_id | str | não | None | Ao compilar várias chamadas, IDs de consumidor diferentes devem ser fornecidas |
| customer_ids | list[CustomerId] | não | None | Uma lista de IDs de cliente em formato compatível com a ID de visitante |
| session_id | str | não | None | Usado para vincular várias solicitações |
| callback | chamável | não | None | Se manipular a solicitação de forma assíncrona, o retorno de chamada será chamado quando a resposta estiver pronta |
| err_callback | chamável | não | None | Se estiver tratando a solicitação de forma assíncrona, o retorno de chamada de erro é chamado quando a exceção é gerada |

## Devoluções

Retorna `TargetDeliveryResponse` se for chamado de forma síncrona (padrão), ou `AsyncResult` se for chamado com um retorno de chamada. `TargetDeliveryResponse` tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| resposta | DeliveryResponse | Está em conformidade com a resposta [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | dict | [!DNL Target] cookie |
| target_location_hint_cookie | dict | Cookie de dica de localização [!DNL Target] |
| analytics_details | list[AnalyticsResponse] | Carga do Analytics, em caso de uso do Analytics no lado do cliente |
| trace | lista[dica] | Dados de rastreamento agregados para todas as mboxes/exibições de solicitação |
| response_tokens | lista[dica] | Uma lista de &#x200B;[Tokens de Resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| meta | dict | Metadados de decisão adicionais para uso com decisão no dispositivo |

Os objetos `target_cookie` e `target_location_hint_cookie` usados para transmitir dados de volta ao navegador têm a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| name | str | Nome do cookie |
| value | any | Valor do cookie, o valor será convertido em string |
| max_age | int | O `max_age option` é uma conveniência para que a configuração expire em relação ao tempo atual em segundos |

O objeto `meta` usado para indicar o status da resposta de destino tem a seguinte estrutura:

| Nome | Tipo | Descrição |
| --- | --- | --- |
| método_de_decisão | str | Qual método de decisão foi usado: no dispositivo ou no servidor |
| remote_mboxes | lista`[str]` | Quando o Método de Decisão é `on-device`, uma matriz de nomes de mbox que não puderam ser totalmente decididos no dispositivo é fornecida. Em outras palavras, uma solicitação [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) é necessária. |
| remote_views | lista`[str]` | Quando o método de decisão é no dispositivo, uma matriz de nomes de visualização que não puderam ser totalmente decididos no dispositivo é fornecida. Em outras palavras, uma solicitação [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) é necessária. |

## Exemplo

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }

    target_delivery_response = target_client.get_offers(get_offers_options)


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
