---
keywords: targetPageParamsAll, targetpageparamsall, PageParamsAll, pageparamsall, parâmetros da página, parâmetros da página, at.js, funções, função, targetPageParamsAll0
description: Use a função [!UICONTROL targetPageParamsAll()] da biblioteca JavaScript [!DNL Adobe Target] at.js para anexar parâmetros a todas as mboxes de fora do código da solicitação.
title: Como usar a função [!UICONTROL targetPageParamsAll()]?
feature: at.js
exl-id: 32045e60-6904-42a1-bf71-fd7e167a829f
TQID: https://experienceleague.adobe.com/A2sZYp7CeE3-zGcqfbvgo32auAtXBKN0dYNa84grs1Q
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 171
ht-degree: 54%

---

# [!UICONTROL targetPageParamsAll()]

Este método permite anexar parâmetros a todos os mboxes de fora do código da solicitação.

Isso é muito útil para incluir o mesmo conjunto de parâmetros em múltiplas chamadas da mbox. A função precisa ser definida pelo cliente. Ela deve retornar uma matriz de parâmetros que serão transmitidos a todas as solicitações de mbox na página. Esta função pode ser definida antes que a at.js seja carregada ou em **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Edição]** > **[!UICONTROL Configurações de Código]** > **[!UICONTROL Cabeçalho da Biblioteca]**.

Você pode transmitir parâmetros para target-global-mbox usando a função [!UICONTROL targetPageParamsAll()] de qualquer uma das seguintes maneiras:

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


