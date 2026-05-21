---
keywords: adobe.target.applyOffer, applyOffer, applyoffer, aplicar oferta, at.js, funções, função, $8
description: Use a função [!UICONTROL adobe.target.applyOffer()] da biblioteca de JavaScript  [!DNL Adobe Target] at.js do para aplicar o conteúdo da resposta.
title: Como faço para usar a função [!UICONTROL adobe.target.applyOffer()]?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
TQID: https://experienceleague.adobe.com/lrjsIl-gKu1SnrZapxYcoDObvUCGG2ht58QtWbQkYts
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
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 169
ht-degree: 67%

---

# [!UICONTROL adobe.target.applyOffer(options)]

Esta função aplica o conteúdo de resposta com [!DNL Adobe Target].

>[!NOTE]
>
>`applyOffer` exige o `mbox` parâmetro. Se não houver nome de mbox definido, um erro ocorrerá.

O parâmetro de opções é obrigatório e tem a seguinte estrutura:

| Chave | Tipo | Obrigatório | Descrição |
|--- |--- |--- |--- |
| mbox | String | Sim | Nome da mbox<br />Com a at.js 1.3.0 (e posteriores), o Target exige que a tecla mbox seja usada. Essa chave era exigida anteriormente, mas o Target agora a aplica para garantir que tenha a validação adequada e que os clientes estejam usando a função corretamente. |
| selector | String ou elemento DOM | Não | Elemento HTML ou seletor CSS usado para identificar o elemento HTML onde o Target deve posicionar o conteúdo da oferta. Se o seletor não for fornecido, o Target presume que o elemento HTML deve usar o HTML HEAD. |
| Oferta | Matriz | Sim | Uma ação de matriz que deve ser aplicada ao elemento. |

## Exemplo

O exemplo a seguir mostra como usar `[!UICONTROL getOffer]` e `[!UICONTROL applyOffer]` juntos:

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "mbox",   
  "success": function(offers) {           
        adobe.target.applyOffer( {  
           "mbox": "mbox", 
           "offer": offers  
        } ); 
  },   
  "error": function(status, error) {           
      if (console && console.log) { 
        console.log(status); 
        console.log(error); 
      } 
  }, 
 "timeout": 5000 
}); 
```
