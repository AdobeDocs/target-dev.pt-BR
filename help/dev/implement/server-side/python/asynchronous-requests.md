---
title: Como usar solicitações assíncronas no  [!DNL Adobe Target] Python SDK
description: Saiba como o  [!DNL Target] Python SDK oferece suporte a solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
TQID: https://experienceleague.adobe.com/ZWRw2OlSbuEHorY0MXPOaBw3uePIW5dzpsuqho0Jtqk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 142
ht-degree: 4%

---

# Solicitações assíncronas (Python)

## Descrição

Um benefício da integração do lado do servidor é que você pode aproveitar a grande largura de banda e os recursos de computação disponíveis no lado do servidor usando o paralelismo. [!DNL Target] O Python SDK é compatível com solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.

## Métodos suportados

### Python

```python {line-numbers="true"}
get_offers(options)
send_notifications(options)
get_attributes(mbox_names, options)
```

## Exemplo

Um aplicativo de exemplo que usa o módulo `asyncio` async/await no Python 3.9+ pode ser semelhante a:

### Python

```python {line-numbers="true"}
async def execute_mboxes(self, mboxes):
    context = Context(channel=ChannelType.WEB)
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }
    return await asyncio.to_thread(target_client.get_offers, get_offers_options)

async def get_target_delivery_response(mboxes):
    target_delivery_response = await execute_mboxes(mboxes)
    response = Response(target_delivery_response.get("response").to_str(), status=200, mimetype='application/json')
    return response

mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
return asyncio.run(get_target_delivery_response(mboxes)
```

Este exemplo pressupõe que você esteja usando o Python 3.9+. Se estiver usando uma versão mais antiga do Python, você ainda poderá enviar solicitações assíncronas ao passar `options.callback` para `get_offers`. Confira o aplicativo Flask de amostra para obter mais detalhes sobre a execução assíncrona usando retornos de chamada ou assíncrono/aguardar, [aqui](https://github.com/adobe/target-python-sdk/blob/main/samples/app.py).
