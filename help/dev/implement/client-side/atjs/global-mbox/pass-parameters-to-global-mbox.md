---
keywords: parâmetros de mbox global, targetPageParams, sequência de consulta, matriz, json, dtm
description: Saiba como usar a função [!UICONTROL targetPageParams] para passar informações adicionais de direcionamento ou contexto para a mbox global [!DNL Adobe Target] .
title: Como transfiro parâmetros para uma mbox global?
feature: at.js
exl-id: 2a6be3e4-a618-4812-9e87-b01789705c40
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 61%

---

# Envio de parâmetros para uma mbox global

A função `targetPageParams` do JavaScript é usada para passar parâmetros para a mbox global em [!DNL Adobe Target]. Isso é necessário em qualquer cenário em que informações adicionais de direcionamento/contexto sejam passadas para [!DNL Target].

Por exemplo, em uma atividade do Recommendations, use os parâmetros para representar o produto ou categoria atual que está sendo visualizada.

O código para chamar a função JavaScript deve vir antes da mbox global na página, independentemente de a mbox global ser acionada como parte da at.js ou incluída manualmente no código da página.

>[!NOTE]
>
>Se você quiser adicionar parâmetros a todas as mboxes na página, não apenas à mbox global, use a função [targetPageParamsAll()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md).

Você pode transmitir parâmetros para `target-global-mbox`usando a função `targetPageParams()`de qualquer uma das seguintes maneiras:

* Uma matriz
* Um objeto JSON
* Uma lista delimitada por ampersand

Use esses três métodos para verificar se os parâmetros estão sendo enviados corretament. Você também pode ser capaz de verificar o envio de parâmetros usando o [depurador da Adobe Experience Cloud](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html).

Você deve definir a função JavaScript antes de adicionar a mbox global à página. O nome deve ser `targetPageParams`.

## String de consulta

```
p1=v1&p2=v2&p3=hello%20world
```

* Nome: `targetPageParams`
* Valor de retorno: a &quot;&amp;&quot; parâmetros delimitados, com valores de parâmetro codificados por URL.

  Exemplo:

  Neste exemplo, p3 tem o valor `hello world`, que é codificado por URL.

Considere o exemplo de código de página a seguir:

```html {line-numbers="true"}
<html> 
  <head> 
    <title>Title here..</title> 
    <script type="text/javascript"> 
        function targetPageParams() { 
          return "p1=v1&p2=v2&p3=hello%20world";
        } 
    </script> 
    <script src="mbox.js" type="text/javascript"></script> 
  </head> 
  <body>Body here... 
  </body> 
</html>
```

Este exemplo envia os seguintes dados para a borda do mbox:

* p1=v1
* p2=v2
* p3=hello world

## Matriz

```javascript {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return ["a=1", "b=2", "c=hello world"]; 
}; 
```

Os valores não precisam ser codificados por URL. Por exemplo, se um valor tiver um espaço, não há necessidade de codificar o espaço.

Este exemplo envia os seguintes dados para a borda do mbox:

* a=1
* b=2
* c=hello world

## JSON

JSON é um modo poderoso de enviar os parâmetros. [!DNL Target] usa as chaves de objeto JSON para nivelar estruturas complicadas em parâmetros simples.

```json {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
                  "memberStatus": Gold, 
                  "country": { 
                                "city": "San Francisco" 
                            } 
              } 
  }; 
}; 
```

Os valores não precisam ser codificados por URL. Por exemplo, &quot;San Francisco&quot; não precisa de espaço para ser codificado. Um espaço é suficiente.

Este exemplo envia os seguintes dados para a borda do mbox:

* a=1
* b=2
* `profile.memberStatus`=Ouro
* `profile.country.city`=São Francisco
