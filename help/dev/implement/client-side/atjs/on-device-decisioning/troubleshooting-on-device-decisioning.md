---
keywords: implementação, biblioteca javascript, js, atjs, decisão no dispositivo, decisão no dispositivo, at.js, no dispositivo, no dispositivo, solução de problemas, solução de problemas, implementação2
description: Saiba como solucionar problemas [!UICONTROL decisão no dispositivo] com a biblioteca at.js do.
title: Como solucionar problemas da decisão no dispositivo com a biblioteca JavaScript at.js do?
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Solução de problemas [!UICONTROL decisão no dispositivo] para at.js

Conclua as etapas a seguir para solucionar problemas [!UICONTROL decisão no dispositivo] in [!UICONTROL Adobe Target] com a biblioteca at.js de JavaScript do:

## Etapa 1: ativar o log do console para at.js

Anexação do parâmetro de URL `mboxDebug=1` O permite que a at.js imprima mensagens no console do navegador.

Todas as mensagens contêm um prefixo &quot;AT:&quot; para obter uma visão geral conveniente. Para garantir que um artefato tenha sido carregado com êxito, o log do console deve conter mensagens semelhantes às seguintes:

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

A ilustração a seguir mostra essas mensagens no log do console:

(Clique na imagem para expandir até a largura total.)

![Log do console com mensagens de artefato](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "Log do console com mensagens de artefato"){zoom=&quot;yes&quot;}

## Etapa 2: verifique o download do artefato da regra na guia Rede do navegador

Abra a guia Rede do navegador.

Por exemplo, para abrir DevTools no Google Chrome:

1. Pressione Control+Shift+J (Windows) ou Command+Option+J (Mac).
1. Navegue até a guia Rede.
1. Filtre suas chamadas com a palavra-chave &quot;rules.json&quot; para garantir que somente o arquivo de regras de artefato seja exibido.

   Além disso, você pode filtrar por &quot;/delivery|rules.json/&quot; para exibir todas as chamadas do Target e o artifact rules.json.

   ![Guia Rede no Google Chrome](assets/rule-json.png)

## Etapa 3: verificar o download de artefato de regra usando eventos personalizados at.js

A biblioteca at.js do envia dois novos eventos personalizados para oferecer suporte [!UICONTROL decisão no dispositivo].

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
