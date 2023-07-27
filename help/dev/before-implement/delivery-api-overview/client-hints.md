---
title: Dicas do cliente da API de entrega do Adobe Target
description: Como usar as Client Hints na [!DNL Adobe Target] API de entrega?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Client Hints e o [!UICONTROL API de entrega do Adobe Target]

As Client Hints devem ser enviadas para o [!DNL Adobe Target] sobre a solicitação de ofertas.

Geralmente, é recomendável enviar todas as Client Hints disponíveis para o [!DNL Target]. Para obter mais informações, consulte [User-agent e Client Hints](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) no [Implementação do cliente](../../implement/client-side/overview.md) seção.

## Chamadas diretas da API de entrega

### No navegador

Nesse caso, o navegador enviará Client Hints de baixa entropia para o [!DNL Target] automaticamente por meio de cabeçalhos de solicitação. Mas há algumas limitações no nível do navegador com essa implementação. Primeiro - nenhum cabeçalho de Client Hints será enviado do navegador do, a menos que a solicitação esteja sendo feita em https. Segunda - as Client Hints não serão enviadas na primeira solicitação para o [!DNL Target] na página. Os cabeçalhos de Client Hints serão enviados somente na segunda solicitação e em todas as solicitações a partir de então. Isso significa que a segmentação e a personalização do público-alvo não podem ser executadas pelo [!DNL Target] na primeira visita de página. Para contornar essas duas limitações, recomendamos usar a API User Agent Client Hints no navegador para coletar as Client Hints diretamente e enviá-las na carga da solicitação.

### De um servidor

Nesse caso, as Client Hints devem ser encaminhadas manualmente do navegador para o [!DNL Target] na solicitação da API de entrega.

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
