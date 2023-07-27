---
keywords: adobe.target.getOffer, getOffer, getoffer, obter oferta, at.js, funções, função, $8
description: Use o [!UICONTROL adobe.target.getOffer()] e suas opções para a função [!DNL Adobe Target] Biblioteca at.js para disparar solicitações para obter um [!DNL Target] oferta.
title: Como usar o [!UICONTROL adobe.target.getOffer()] Função?
feature: at.js
exl-id: 7b917d42-06e8-4838-a09d-0c4872c9beaa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 81%

---

# [!DNL adobe.target.getOffer(options)]

Esta função envia uma solicitação para obter uma [!DNL Target] oferta.

Use com `[!UICONTROL adobe.target.applyOffer()]` para processar a resposta ou use sua própria manipulação de sucesso. O parâmetro de opções é obrigatório e tem a seguinte estrutura:

| Chave | Tipo | Obrigatório | Descrição |
|--- |--- |--- |--- |
| mbox | String | Sim | Nome da mbox |
| params | Objeto | Não | Parâmetros de mbox. Um objeto de pares de valores-chave que tem a seguinte estrutura:<P>`{ "param1": "value1", "param2": "value2"}` |
| success | Função | Sim | Retorno de chamada para execução quando recebemos uma resposta do servidor. A função de retorno de chamada bem-sucedida receberá um único parâmetro que represente uma variedade de objetos em oferta. Este é um exemplo de retorno de chamada:<P>`function handleSuccess(response){......}`<P>Veja as respostas abaixo para obter mais informações. |
| error | Função | Sim | Retorno de chamada para execução quando recebemos um erro. Há alguns casos que são considerados errôneos:<ul><li>Código do status de HTTP diferente de 200 OK</li><li>Não foi possível analisar a resposta. Por exemplo, nós mal construímos JSON ou HTML ao invés de JSON.</li><li>A resposta contém a tecla &quot;erro&quot;. Por exemplo, uma exceção foi lançada no Edge e não foi possível processar a solicitação apropriadamente. Podemos receber um erro quando uma mbox está bloqueada e não é possível recuperar o conteúdo dela, etc. A função de retorno de chamada de erro receberá dois parâmetros: status e erro. Veja um exemplo de retorno de chamada de erro:  `function handleError(status, error){......}`</li></ul>Veja as respostas com erro abaixo para obter mais informações. |
| timeout | Número | Não | Tempo limite em milissegundos. Se não especificado, o tempo limite padrão em at.js será utilizado.<P>O tempo limite padrão pode ser definido no [!DNL Target] IU em [!UICONTROL Administração] > [!UICONTROL Implementação]. |

## Exemplos

Adicionar parâmetros com [!UICONTROL getOffer()] e usando [!UICONTROL applyOffer()] para manipulação bem-sucedida:

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "target-global-mbox", 
  "params": { 
     "a": 1, 
     "b": 2 
  }, 
  "success": function(offer) {           
        adobe.target.applyOffer( {  
           "mbox": "target-global-mbox", 
           "offer": offer  
        } ); 
  },   
  "error": function(status, error) {           
      console.log('Error', status, error); 
  } 
});
```

Adicionar parâmetros e parâmetros de perfil com o [!UICONTROL getOffer()] e usando [!UICONTROL applyOffer()] para manipulação bem-sucedida:

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "target-global-mbox", 
  "params": { 
     "a": 1, 
     "b": 2, 
     "profile.age": 27, 
     "profile.gender": "male" 
  }, 
  "success": function(offer) {           
        adobe.target.applyOffer( {  
           "mbox": "target-global-mbox", 
           "offer": offer  
        } ); 
  },   
  "error": function(status, error) {           
      console.log('Error', status, error); 
  } 
});
```

Usar tempo limite personalizado e manipulação personalizada de sucesso com o [!UICONTROL getOffer()]:

&quot;YOUR_OWN_CUSTOM_HANDLING_FUNCTION&quot; é um placeholder para uma função que o cliente definiria.

```javascript {line-numbers="true"}
adobe.target.getOffer({     
  "mbox": "target-global-mbox",   
  "success": function(offer) { 
    YOUR_OWN_CUSTOM_HANDLING_FUNCTION(offer);   
  }, 
  "error": function(status, error) {                 
    console.log('Error', status, error);   
  },   
  "timeout": 2000 
});
```

## Respostas 

O parâmetro de resposta passado para o retorno de chamada de sucesso será uma variedade de ações. Uma ação é um objeto que geralmente tem o seguinte formato:

| Nome | Tipo | Descrição |
|--- |--- |--- |
| action | String | Tipo de ação a ser aplicada ao elemento identificado. |
| selector | Sequência | Representa um seletor do Sizzle. |
| cssSelector | String | Seletor nativo DOM, usado para pré-ocultação de elemento. |
| content | String | O conteúdo a ser aplicado ao elemento identificado. |

## Exemplo

```javascript {line-numbers="true"}
{ 
    "sessionId": "1444512212156-384616", 
    "tntId": "1444512212156-384616.17_35", 
    "offers": [{ 
        "plugins": ["<script type=\"text/javascript\">\r\n/*mboxHighlight+ (1of2) v1 ==> Response Plugin*/\r\nwindow.ttMETA=(typeof(window.ttMETA)!='undefined')?window.ttMETA:[];window.ttMETA.push({'mbox':'target-global-mbox','campaign':'at: redirect ootb','experience':'Experience B','offer':'/at_redirect_ootb/experiences/1/pages/0/1442082890250'});window.ttMBX=function(x){var mbxList=[];for(i=0;i<ttMETA.length;i++){if(ttMETA[i].mbox==x.getName()){mbxList.push(ttMETA[i])}}return mbxList[x.getId()]}\r\n</script>"], 
        "actions": { 
            "content": [{ 
                "passMboxSession": false, 
                "selector": "body", 
                "action": "redirect", 
                "url": "https://example.com/04.html", 
                "includeAllUrlParameters": true 
            }] 
        } 
    }] 
}
```

## Respostas de erro

Os parâmetros &quot;status&quot; e &quot;erro&quot; passados para o retorno de chamada de erro terão o seguinte formato:

| Nome | Tipo | Descrição |
|--- |--- |--- |
| status | String | Representa o status do erro. Este parâmetro pode ter os seguintes valores:<ul><li>timeout: Indica que o tempo limite para a solicitação foi excedido.</li><li>parseerror: Indica que a resposta não pôde ser analisada, por exemplo, se recebermos um texto HTML ou sem formatação em vez de JSON.</li><li>error: Indica um erro geral, como o recebimento do status HTTP diferente de 200 OK</li></ul> |
| error | String | Contém dados adicionais, como mensagem de exceção ou qualquer outra coisa que possa ser útil para solução de problemas. |
