---
title: Implementar a configuração de proxy no  [!DNL Adobe Target] Node.js SDK
description: Saiba como definir a configuração de proxy [!UICONTROL TargetClient] no SDK  [!DNL Adobe Target] Node.js.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
TQID: https://experienceleague.adobe.com/kaE-ZEOTteaVp5kWSHiVYCvEiHuQHSMqeWRq6r-mJaA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 102
ht-degree: 0%

---

# Configuração de proxy (Node.js)

Para configurar um proxy para as solicitações HTTP do Node SDK, substitua a API de busca usada pelo SDK durante a inicialização.

Este é um exemplo básico de como substituir `fetchApi` durante a inicialização de `TargetClient` para adicionar um proxy:

```javascript {line-numbers="true"}
const { ProxyAgent } = require("undici");

const proxyAgent = new ProxyAgent("your proxy address here");

const fetchImpl = (url, options) => {
  const fetchOptions = options;
  fetchOptions.dispatcher = proxyAgent;
  return fetch(url, fetchOptions);
};

client = TargetClient.create({
    ...,
    fetchApi: fetchImpl
});
```

Observe que isso só funciona para as versões de Nó 18.2+, em que `undici.fetch` é o padrão `fetch` para o nó.
Visite o [repositório de amostras do Nó SDK](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
para obter exemplos de configuração de proxy para versões mais antigas do nó e mais informações.
