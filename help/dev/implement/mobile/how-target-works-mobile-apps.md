---
description: Saiba como usar o [!DNL Adobe Mobile SDK] para mostrar as experiências ideais aos visitantes do aplicativo móvel.
title: Como o [!DNL Target] Trabalhar em aplicativos móveis?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 34%

---

# Como [!DNL Target] funciona em aplicativos móveis

A variável [!DNL Adobe Mobile SDK] contata a [!DNL Target] servidor para obter o conteúdo junto com outros pontos de dados para mostrar a experiência correta ao usuário.

>[!IMPORTANT]
>
>Suporte para o [!DNL Adobe Mobile] versão 4.*x* Os SDKs terminaram em 31 de agosto de 2021 e não são mais recomendados para [!DNL Adobe Target] usuários de dispositivos móveis.
>
>A variável [Adobe Experience Platform SDK para aplicativos móveis](https://developer.adobe.com/client-sdks/documentation/){target=_blank} é a solução recomendada para [!DNL Adobe Experience Cloud] soluções e serviços em seus aplicativos móveis.

## [!DNL Target] locais e métricas de sucesso

Uma *localização direcionada* também é conhecida como uma  mbox. Uma localização identificada no aplicativo é ativada para teste ou personalização (por exemplo, mensagem de boas vindas na tela inicial). Essas localizações são identificadas durante o processo de criação de teste.

Um *[métrica de sucesso](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)* é uma ação realizada pelo usuário que identifica se uma atividade específica foi bem-sucedida (como se conectar, fazer uma compra, reservar uma passagem e assim por diante).

![imagem alt](assets/mobile-target-location.png)

* **[!DNL Target]localização:** O conteúdo que é exibido abaixo do botão Registrar.

  Esse usuário específico tem frete grátis até às 18h. Esse local pode ser reutilizado em vários [!DNL Target] para executar testes A/B e personalização.

* **Métrica de sucesso:** A ação executada pelo usuário em que o usuário toca no botão Registrar.

**Entenda como [!DNL Target] funciona no SDK**

![imagem alt](assets/how-target-mobile-works.png)
