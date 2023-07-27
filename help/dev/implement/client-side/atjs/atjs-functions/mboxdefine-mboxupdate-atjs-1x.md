---
keywords: mboxDefine, mboxdefine, mbox define, mboxUpdate, mboxupdate, atualização da mbox, at.js, funções, função, mboxDefine0
description: Use o [!UICONTROL mboxDefine()] e [!UICONTROL mboxUpdate()] funções para o [!DNL Adobe Target] Biblioteca JavaScript at.js para definir ou atualizar uma mbox. (at.js 1.x)
title: Como usar o [!UICONTROL mboxDefine()] E [!UICONTROL mboxUpdate()] Funções?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 52%

---

# [!UICONTROL mboxDefine()] e [!UICONTROL mboxUpdate()] - at.js 1.x

Definir e atualizar uma mbox no [!DNL Adobe Target].

>[!NOTE]
>
>Essas funções estão disponíveis para a at.js versão 1.somente *x*. Essas funções foram descontinuadas com o lançamento da at.js 2.*x*. Essas funções retornam o conteúdo padrão se usadas com a at.js 2.*x*.

`[!UICONTROL mboxDefine()]` e `[!UICONTROL mboxCreate()]` estão vinculados a elementos HTML DIV onde a oferta deve ser exibida. Esses elementos HTML DIV devem ter a classe `mboxDefault`. Se os elementos HTML não tiverem essa classe anexada, você pode observar alguma cintilação perceptível.

## mboxDefine

Cria um mapeamento interno entre um nodeId e um nome de mbox, mas não executa a solicitação. Usado em conjunto com `[!UICONTROL mboxUpdate()]`. Incorporada na at.js, principalmente para facilitar a transição da mbox.js (descontinuada) para a at.js.

## mboxUpdate

Executa a solicitação e aplica a oferta ao elemento identificado pelo `nodeId` em `mboxDefine()`. Também pose ser usada para atualizar uma mbox iniciada por `[!UICONTROL mboxCreate]`. Incorporada na at.js, principalmente para facilitar a transição da mbox.js (descontinuada) para a at.js. `mboxDefine()`/ `mboxUpdate()` pode ser substituído por [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) e [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) usando a opção do seletor.

## Exemplo

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```
