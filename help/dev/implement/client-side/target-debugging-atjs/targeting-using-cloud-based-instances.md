---
keywords: instâncias de nuvem, lista de sufixos públicos, sufixo público, cookie, cookie próprio, cookie próprio, cookie próprio, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, herokuapp.com, firebaseapp.com,, targetGlobalSettings, cookieDomain, instâncias de nuvem5, instâncias de nuvem6, instâncias de nuvem7, instâncias de nuvem8, instâncias de nuvem9, lista de sufixos públicos0, lista de sufixos públicos1, lista de sufixos públicos2, lista de sufixos públicos3, lista de sufixos públicos4, lista de sufixos públicos5
description: Explore os problemas (com soluções) que os clientes enfrentam ao usar as instâncias baseadas em nuvem para testar o [!DNL Adobe Target] ou para fins de prova de conceito.
title: Posso usar  [!DNL Target]  com instâncias baseadas em nuvem?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
TQID: https://experienceleague.adobe.com/df63sTQxukCfa4pYc1X6FRvxV3cY2UG-ixk5v9Fqh-c
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 929e1f10bc5dd0741f0fe28cd46435e680a4a308
workflow-type: tm+mt
source-wordcount: 203
ht-degree: 46%

---

# Usar instâncias baseadas em nuvem com [!DNL Target]

Informações sobre problemas que os clientes enfrentam ao usar as instâncias baseadas em nuvem para testar o [!DNL Adobe Target].

Os [!DNL Target] clientes do, às vezes, usam instâncias baseadas em nuvem com o [!DNL Target] para testes ou fins de prova de conceito simples. Essas instâncias podem incluir os seguintes domínios:

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com` ou `firebaseapp.com`

Esses domínios e muitos outros fazem parte da [Lista de sufixos públicos](https://publicsuffix.org/list/public_suffix_list.dat).

**Problema:** os navegadores modernos não salvam cookies, se você estiver usando esses domínios.

A biblioteca JavaScript da at.js usa cookies para rastrear usuários, para garantir que o [!DNL [!DNL Target]] sempre apresente uma experiência consistente. Se a biblioteca JavaScript do [!DNL Target] não puder salvar cookies, as solicitações do Target serão desabilitadas.

**Solução:** como prática recomendada, se você pretende usar instâncias baseadas em nuvem com domínios incluídos na Lista de sufixos públicos, certifique-se de personalizar a configuração do `cookieDomain`. Para obter mais informações, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

