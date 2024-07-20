---
keywords: adobe.target.applyOffer, applyOffer, applyoffer, aplicar oferta, at.js, funções, função, $8
description: Use a função [!UICONTROL adobe.target.applyOffer()] da biblioteca de JavaScript  [!DNL Adobe Target] at.js do para aplicar o conteúdo da resposta.
title: Como faço para usar a função [!UICONTROL adobe.target.applyOffer()]?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '172'
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
| selector | String ou elemento DOM | Não | Elemento HTML ou seletor CSS usado para identificar o elemento HTML onde o Target deve posicionar o conteúdo da oferta. Se o seletor não for fornecido, o Target presume que o elemento HTML deve usar HTML HEAD. |
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
