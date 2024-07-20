---
title: Como usar solicitações assíncronas no  [!DNL Adobe Target] Python SDK
description: Saiba como o  [!DNL Target] Python SDK oferece suporte a solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 4%

---

# Solicitações assíncronas (Python)

## Descrição

Um benefício da integração do lado do servidor é que você pode aproveitar a grande largura de banda e os recursos de computação disponíveis no lado do servidor usando o paralelismo. O SDK do Python [!DNL Target] é compatível com solicitações assíncronas, o que pode reduzir o tempo de destino efetivo para zero.

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
