---
title: Dicas do cliente da API de entrega do Adobe Target
description: Como faço para usar as Client Hints na API de entrega do  [!DNL Adobe Target] ?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/ijbOsWitZdNHpjNduh8xtPyEYdw2tsWz2rB6jZ5JbQA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: ff2b9b37-92e0-45fc-b853-379d44c08c89
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 282
ht-degree: 0%

---

# Dicas do cliente e a [!UICONTROL API de entrega do Adobe Target]

As Client Hints devem ser enviadas para [!DNL Adobe Target] na solicitação de ofertas.

Geralmente, é recomendável enviar todas as Client Hints disponíveis para [!DNL Target]. Para obter mais informações, consulte [User-agent e Client Hints](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) na seção [Implementação do lado do cliente](../../implement/client-side/overview.md).

## Chamadas diretas da API de entrega

### No navegador

Nesse caso, o navegador enviará Client Hints de baixa entropia para [!DNL Target] automaticamente por meio de cabeçalhos de solicitação. Mas há algumas limitações no nível do navegador com essa implementação. Primeiro - nenhum cabeçalho de Client Hints será enviado do navegador do, a menos que a solicitação esteja sendo feita em https. Segunda - As Client Hints não serão enviadas na primeira solicitação para [!DNL Target] na página. Os cabeçalhos de Client Hints serão enviados somente na segunda solicitação e em todas as solicitações a partir de então. Isso significa que a segmentação e a personalização do público-alvo não podem ser realizadas por [!DNL Target] na primeira visita à página. Para contornar essas duas limitações, recomendamos usar a API User Agent Client Hints no navegador para coletar as Client Hints diretamente e enviá-las na carga da solicitação.

### De um servidor

Nesse caso, as Client Hints devem ser encaminhadas manualmente do navegador para [!DNL Target] na solicitação da API de Entrega.

```
curl -X POST 'http://mboxedge28.tt.omtrdc.net/rest/v1/delivery?client=myClientCode&sessionId=abcdefghijkl00014' -d '{
  "context": {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36",
    "clientHints": {
      "Sec-CH-UA-Model": "iPhone",
      "Sec-CH-UA-Mobile": true,
      "Sec-CH-UA-Platform": "iOS",
      "Sec-CH-UA": "[ { \"brand\": \"Chromium\", \"version\": \"91\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99\" } ]",
      "Sec-CH-UA-Full-Version-List": "[ { \"brand\": \"Chromium\", \"version\": \"91.1.1.1\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99.1.1.1\" } ]",
      "Sec-CH-UA-Platform-Version": "10.0.0",
      "Sec-CH-UA-Arch": "x86",
      "Sec-CH-UA-Bitness": "64"
    }
  },
  "execute": {
    "mboxes": [{
      "name": "home",
      "index": 1
    }]
  }
}'
```

## Formatação

Os cabeçalhos de Client Hints Sec-CH-UA e Sec-CH-UA-Full-Version-List têm um formato diferente dos resultados da API do navegador de Client Hints (navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues). Ambos os formatos são aceitos pela API de entrega. A API de entrega normalizará os valores no formato usado nos cabeçalhos da solicitação, o que é importante ter em mente ao acessar as Client Hints nos scripts de perfil.
