---
title: Implementar a configuração de proxy no SDK do  [!DNL Adobe Target] Node.js
description: Saiba como definir a configuração de proxy [!UICONTROL TargetClient] no SDK do  [!DNL Adobe Target] Node.js.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Configuração de proxy (Node.js)

Para configurar um proxy para as solicitações HTTP do SDK de nó, substitua a API de busca usada pelo SDK durante a inicialização.

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
Visite o [repositório de amostras do SDK do nó](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
para obter exemplos de configuração de proxy para versões mais antigas do nó e mais informações.
