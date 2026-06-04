---
keywords: implementação, biblioteca javascript, js, atjs, decisão no dispositivo, decisão no dispositivo, at.js, no dispositivo, no dispositivo, solução de problemas, solução de problemas, implementação2
description: Saiba como solucionar problemas da [!UICONTROL decisão no dispositivo] com a biblioteca at.js.
title: Como solucionar problemas da decisão no dispositivo com a biblioteca at.js de JavaScript?
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
TQID: https://experienceleague.adobe.com/Ji3jAHC0Ek7FrVnabEEMm-KCtxJLJ5rSz4uyi6sWpiE
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 281
ht-degree: 0%

---

# Solução de problemas da [!UICONTROL decisão no dispositivo] para at.js

Conclua as seguintes etapas para solucionar problemas da [!UICONTROL decisão no dispositivo] no [!UICONTROL Adobe Target] com a biblioteca at.js de JavaScript:

## Etapa 1: ativar o log do console para at.js

Anexar o parâmetro de URL `mboxDebug=1` permite que a at.js imprima mensagens no console do navegador.

Todas as mensagens contêm um prefixo &quot;AT:&quot; para obter uma visão geral conveniente. Para garantir que um artefato tenha sido carregado com êxito, o log do console deve conter mensagens semelhantes às seguintes:

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

A ilustração a seguir mostra essas mensagens no log do console:

(Clique na imagem para expandir até a largura total.)

![Log de console com mensagens de artefato](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "Log de console com mensagens de artefato"){zoomable="yes"}

## Etapa 2: verifique o download do artefato da regra na guia Rede do navegador

Abra a guia Rede do navegador.

Por exemplo, para abrir DevTools no Google Chrome:

1. Pressione Control+Shift+J (Windows) ou Command+Option+J (Mac).
1. Navegue até a guia Rede.
1. Filtre suas chamadas com a palavra-chave &quot;rules.json&quot; para garantir que somente o arquivo de regras de artefato seja exibido.

   Além disso, você pode filtrar por &quot;/delivery|rules.json/&quot; para exibir todas as chamadas do Target e o artifact rules.json.

   ![Guia Rede no Google Chrome](assets/rule-json.png)

## Etapa 3: verificar o download de artefato de regra usando eventos personalizados at.js

A biblioteca at.js despacha dois novos eventos personalizados para suportar a [!UICONTROL decisão no dispositivo].

* `adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`
* `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`

Você pode assinar para ouvir esses eventos personalizados no aplicativo para ação após o sucesso ou a falha no download do arquivo de regras de artefatos.

O exemplo a seguir mostra uma amostra de código ouvindo os eventos de sucesso e falha do download de artefatos:

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED, function(e) { 
  console.log("Artifact successfully downloaded", e.detail);
}, false);

document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_FAILED, function(e) { 
  console.log("Artifact failed to download", e.detail);
}, false);
```
