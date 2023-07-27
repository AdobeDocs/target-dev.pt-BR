---
keywords: targetPageParamsAll, targetpageparamsall, PageParamsAll, pageparamsall, parâmetros da página, parâmetros da página, at.js, funções, função, targetPageParamsAll0
description: Use o [!UICONTROL targetPageParamsAll()] para a [!DNL Adobe Target] Biblioteca JavaScript at.js para anexar parâmetros a todas as mboxes de fora do código da solicitação.
title: Como usar o [!UICONTROL targetPageParamsAll()] Função?
feature: at.js
exl-id: 32045e60-6904-42a1-bf71-fd7e167a829f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 55%

---

# [!UICONTROL targetPageParamsAll()]

Este método permite anexar parâmetros a todos os mboxes de fora do código da solicitação.

Isso é muito útil para incluir o mesmo conjunto de parâmetros em múltiplas chamadas da mbox. A função precisa ser definida pelo cliente. Ela deve retornar uma matriz de parâmetros que serão transmitidos a todas as solicitações de mbox na página. Essa função pode ser definida antes que a at.js seja carregada ou no **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Editar]** > **[!UICONTROL Configurações de código]** > **[!UICONTROL Cabeçalho da biblioteca]**.

Você pode transmitir parâmetros para target-global-mbox usando o [!UICONTROL targetPageParamsAll()] função de qualquer uma das seguintes maneiras:

* Uma lista delimitada por ampersand
* Uma matriz
* Um objeto JSON

## Exemplos

Lista delimitada por ampersand (os valores devem ser codificados por URL):

```javascript {line-numbers="true"}
function targetPageParamsAll() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Matriz (os valores não precisam ser codificados por URL):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON (os valores não precisam ser codificados por URL):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
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
