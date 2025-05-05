---
description: Saiba como usar o  [!DNL Adobe Mobile SDK]  para mostrar as experiências ideais aos visitantes do aplicativo móvel.
title: Como o  [!DNL Target] funciona em aplicativos móveis?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 17%

---

# Como o [!DNL Target] funciona em aplicativos móveis

O [!DNL Adobe Mobile SDK] contata o servidor [!DNL Target] para obter o conteúdo junto com outros pontos de dados para mostrar a experiência correta ao usuário.

>[!IMPORTANT]
>
>Suporte para o [!DNL Adobe Mobile] versão 4.Os SDKs do *x* terminaram em 31 de agosto de 2021 e não são mais recomendados para usuários móveis do [!DNL Adobe Target].
>
>O [Adobe Experience Platform SDK para Aplicativos para Dispositivos Móveis](https://developer.adobe.com/client-sdks/documentation/){target=_blank} é a solução recomendada para habilitar soluções e serviços do [!DNL Adobe Experience Cloud] em seus aplicativos para dispositivos móveis.

## [!DNL Target] locais e métricas de sucesso

Um *local de destino* também é chamado de mbox. Uma localização identificada no aplicativo é ativada para teste ou personalização (por exemplo, mensagem de boas vindas na tela inicial). Essas localizações são identificadas durante o processo de criação de teste.

Uma *[métrica de sucesso](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=pt-BR)* é uma ação executada pelo usuário que identifica se uma atividade específica foi bem-sucedida (como se conectar, fazer uma compra, reservar uma passagem e assim por diante).

![alt imagem](assets/mobile-target-location.png)

* **[!DNL Target]local:** O conteúdo que aparece abaixo do botão de registro.

  Esse usuário específico tem frete grátis até às 18h. Este local pode ser reutilizado em várias atividades [!DNL Target] para executar testes A/B e personalização.

* **Métrica de sucesso:** a ação executada pelo usuário em que o usuário toca no botão Registrar.

**Entenda como o [!DNL Target] funciona no SDK**

![alt imagem](assets/how-target-mobile-works.png)
