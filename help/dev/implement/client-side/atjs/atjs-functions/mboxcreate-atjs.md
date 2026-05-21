---
keywords: mboxCreate, mboxcreate, mbox create, at.js, funções, função
description: Use a função [!UICONTROL mboxCreate()] da biblioteca de JavaScript at.js  [!DNL Adobe Target]  para aplicar ofertas ao DIV mais próximo com o nome de classe mboxDefault. (at.js 1.x)
title: Como faço para usar a função [!UICONTROL mboxCreate()]?
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
TQID: https://experienceleague.adobe.com/hCEKL9RPtqIbMVEouzObjU6dc7TKl1hBtKZ1jEdicRE
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 211
ht-degree: 41%

---

# [!UICONTROL mboxCreate(mbox,params)] - at.js 1.x

Executa uma solicitação e aplica a oferta ao DIV mais próximo com o nome de classe mboxDefault.

>[!NOTE]
>
>Esta função está disponível somente para a at.js versão 1.*x*. Essa função foi substituída pelo lançamento da at.js 2.x. Essa função retorna o conteúdo padrão se for usada com a at.js 2.x.

Essa função está incorporada na at.js, principalmente para facilitar a transição da mbox.js (descontinuada) para a at.js. Uma alternativa mais nova para `[!UICONTROL mboxCreate()]` é `[!UICONTROL adobe.target.getOffer()]`/ `[!UICONTROL adobe.target.applyOffer()]` ou a diretiva Angular.

## Exemplo

```javascript {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  mboxCreate('mboxName','param1=value1','param2=value2'); 
</script>
```

## Notas

`mboxCreate()` agora usa o terminal &quot;json&quot; ao invés de &quot;standard&quot; e dispara de maneira assíncrona. Por esse motivo:

* [Depuração](/help/dev/implement/client-side/target-debugging-atjs/target-debugging-atjs.md) é diferente.
* Evite oferecer código que exija chamadas bloqueio sincrônicas.

  Por exemplo, ofertas que definem variáveis de JavaScript que são usadas para código do site ou outras mboxes posteriores na página.

* Certifique-se de ter um `<div class="mboxDefault"></div>`antes de invocar `[!UICONTROL mboxCreate()]`, pois at.js não adicionará um para você.

* Funções vazias no topo da página `[!UICONTROL mboxCreate()]` não são recomendadas como mbox global.

  A mbox global criada automaticamente no at.js é uma opção melhor, pois dispara do `<head>` e pode retornar conteúdo antecipadamente.
