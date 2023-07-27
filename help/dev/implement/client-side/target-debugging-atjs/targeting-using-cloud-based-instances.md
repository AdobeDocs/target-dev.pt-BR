---
keywords: instâncias de nuvem, lista de sufixos públicos, sufixo público, cookie, cookie próprio, cookie próprio, cookie próprio, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, herokuapp.com, firebaseapp.com,, targetGlobalSettings, cookieDomain, instâncias de nuvem5, instâncias de nuvem6, instâncias de nuvem7, instâncias de nuvem8, instâncias de nuvem9, lista de sufixos públicos0, lista de sufixos públicos1, lista de sufixos públicos2, lista de sufixos públicos3, lista de sufixos públicos4, lista de sufixos públicos5
description: Explore problemas (com soluções) que os clientes enfrentam ao usar as instâncias baseadas em nuvem para testar [!DNL Adobe Target] ou para fins de prova de conceito.
title: Posso usar [!DNL Target] com Instâncias baseadas em nuvem?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 49%

---

# Usar instâncias baseadas em nuvem com o [!DNL Target]

Informações sobre problemas que os clientes enfrentam ao usar as instâncias baseadas em nuvem para testar o [!DNL Adobe Target].

Os [!DNL Target] clientes do, às vezes, usam instâncias baseadas em nuvem com o [!DNL Target] para testes ou fins de prova de conceito simples. Essas instâncias podem incluir os seguintes domínios:

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com` ou `firebaseapp.com`

Esses domínios e muitos outros fazem parte da [Lista de sufixos públicos](https://publicsuffix.org/list/public_suffix_list.dat).

**Problema:** os navegadores modernos não salvam cookies, se você estiver usando esses domínios.

A biblioteca JavaScript at.js do usa cookies para rastrear usuários, garantindo que o [!DNL [!DNL Target]] sempre apresenta uma experiência consistente. Se a variável [!DNL Target] A biblioteca do JavaScript do não pode salvar cookies, as solicitações do Target estão desativadas.

**Solução:** como prática recomendada, se você pretende usar instâncias baseadas em nuvem com domínios incluídos na Lista de sufixos públicos, certifique-se de personalizar a configuração do `cookieDomain`. Para obter mais informações, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
