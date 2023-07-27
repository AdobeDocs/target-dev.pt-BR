---
keywords: mboxCreate, mboxcreate, mbox create, at.js, funções, função
description: Use o [!UICONTROL mboxCreate()] para a [!DNL Adobe Target] Biblioteca JavaScript at.js para aplicar ofertas ao DIV mais próximo com o nome de classe mboxDefault. (at.js 1.x)
title: Como usar o [!UICONTROL mboxCreate()] Função?
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 55%

---

# [!UICONTROL mboxCreate(mbox,params)] - at.js 1.x

Executa uma solicitação e aplica a oferta ao DIV mais próximo com o nome de classe mboxDefault.

>[!NOTE]
>
>Essa função está disponível para a at.js versão 1.somente *x*. Essa função foi descontinuada pelo lançamento da at.js 2.x. Ela retorna o conteúdo padrão se for usada com a 2.x.

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

* Certifique-se de ter uma `<div class="mboxDefault"></div>`antes de invocar `[!UICONTROL mboxCreate()]`, pois a at.js não adicionará um para você.

* Funções vazias no topo da página `[!UICONTROL mboxCreate()]` não são recomendadas como mbox global.

  A mbox global criada automaticamente no at.js é uma opção melhor, pois dispara do `<head>` e podem retornar conteúdo antecipadamente.
