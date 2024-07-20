---
title: Como usar solicitações assíncronas no  [!DNL Adobe Target] Python SDK
description: Saiba como o  [!DNL Target] Python SDK oferece suporte a solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.
feature: APIs/SDKs
exl-id: fafb9e28-5ac5-41c1-8e7f-f40550b6749f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 16%

---

# Obter atributos (Python)

## Descrição

`get_attributes()` é usado para buscar experimentação e experiências personalizadas de [!DNL Target] e extrair valores de atributos.


## Método

### getAttributes

```python {line-numbers="true"}
target_client_instance.get_attributes(mbox_names, options)
```

## Parâmetros

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| mbox_names | lista[str] | Sim | None | Uma lista de nomes de mbox |
| opções | dict | Não | None | As mesmas opções usadas para [Obter Ofertas](get-offers.md) |

## AttributesProvider

O `AttributesProvider` retornado por `target_client.get_attributes()` tem os seguintes métodos:

| Método | Tipo de retorno | Descrição |
| --- | --- | --- |
| get_value(mbox_name, chave) | any | Retorna o valor de um nome de mbox e uma chave de atributo especificados |
| as_object(mbox_name) | dict | Retorna um objeto json simples com pares de valores chave |
| get_response() | [TargetDeliveryResponse](https://github.com/adobe/target-python-sdk/blob/main/target_python_sdk/types/target_delivery_response.py) | Retorna o objeto de resposta normalmente retornado por `get_offers` |

## Exemplo

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_attributes_options = {
      "request": delivery_request
    }

    attributes_provider = target_client.get_attributes(["demo-engineering-flags"], get_attributes_options)
    # returns just the value of searchProviderId from the demo-engineering-flags mbox offer
    search_provider_id = attributes_provider.get_value("demo-engineering-flags", "searchProviderId")

    # returns a simple dict object representing the demo-engineering-flags mbox offer
    engineering_flags = attributes_provider.as_object("demo-engineering-flags")
    """  the value of engineeringFlags looks like this
        {
            "cdnHostname": "cdn.cloud.corp.net",
            "searchProviderId": 143,
            "hasLegacyAccess": false
        }
    """

    asset_url = "http://{}/path/to/asset".format(engineering_flags.get("cdnHostname"))


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
