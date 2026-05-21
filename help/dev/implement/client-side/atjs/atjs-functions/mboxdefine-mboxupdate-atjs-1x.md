---
keywords: mboxDefine, mboxdefine, mbox define, mboxUpdate, mboxupdate, atualização da mbox, at.js, funções, função, mboxDefine0
description: Use as funções [!UICONTROL mboxDefine()] e [!UICONTROL mboxUpdate()] da biblioteca JavaScript  [!DNL Adobe Target] at.js do para definir ou atualizar uma mbox. (at.js 1.x)
title: Como faço para usar as funções [!UICONTROL mboxDefine()] e [!UICONTROL mboxUpdate()]?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
TQID: https://experienceleague.adobe.com/Fn-Ej8jk2AMEn79tOtRoP9GQc36Ugy6FtXyn6x7jkmA
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
source-wordcount: 202
ht-degree: 47%

---

# [!UICONTROL mboxDefine()] e [!UICONTROL mboxUpdate()] - at.js 1.x

Defina e atualize uma mbox no [!DNL Adobe Target].

>[!NOTE]
>
>Essas funções estão disponíveis somente para a at.js versão 1.*x*. Essas funções foram descontinuadas com o lançamento da at.js 2.*x*. Essas funções retornam o conteúdo padrão se usadas com a at.js 2.*x*.

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
