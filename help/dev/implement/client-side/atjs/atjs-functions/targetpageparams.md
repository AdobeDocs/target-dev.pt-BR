---
keywords: targetPageParams, targetpageparams, pageParams, pageparams, parâmetros da página, parâmetros da página, at.js, funções, função, targetPageParams0
description: Use o [!UICONTROL targetPageParams()] para a [!DNL Adobe Target] Biblioteca JavaScript at.js para anexar parâmetros à mbox global de fora do código da solicitação.
title: Como usar o [!UICONTROL targetPageParams()] Função?
feature: at.js
exl-id: 274e4d1f-843a-443b-ad98-7139dc4a13f8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 65%

---

# [!UICONTROL targetPageParams()]

Este método permite anexar parâmetros ao mbox global de fora do código da solicitação.

Esta função é muito útil para incluir o mesmo conjunto de parâmetros em múltiplas chamadas da mbox. A função precisa ser definida pelo cliente. Ela deve retornar uma matriz de parâmetros que serão transmitidos apenas à solicitação global da mbox. Essa função pode ser definida antes que a at.js seja carregada ou no **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Editar]** > **[!UICONTROL Cabeçalho da biblioteca]**.

Você pode transmitir parâmetros para target-global-mbox usando a função `[!UICONTROL targetPageParams()]` de qualquer uma das seguintes maneiras:

* Uma lista delimitada por ampersand
* Uma matriz
* Um objeto JSON

## Exemplos

Lista delimitada por ampersand (os valores devem ser codificados por URL):

```javascript {line-numbers="true"}
function targetPageParams() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Matriz (os valores não precisam ser codificados por URL):

```javascript {line-numbers="true"}
targetPageParams = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON (os valores não precisam ser codificados por URL):

```javascript {line-numbers="true"}
targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
        "age": 26, 
        "country": { 
          "city": "San Francisco" 
        } 
      } 
  }; 
};
```
