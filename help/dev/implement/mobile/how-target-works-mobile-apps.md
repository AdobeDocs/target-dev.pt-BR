---
description: Saiba como usar o  [!DNL Adobe Mobile SDK]  para mostrar as experiências ideais aos visitantes do aplicativo móvel.
title: Como o  [!DNL Target] funciona em aplicativos móveis?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
TQID: https://experienceleague.adobe.com/R3B-i9BFKaoTkbfzVLOU-j8VV2K-MpNrf0WTCkMceT8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 16%

---

# Como o [!DNL Target] funciona em aplicativos móveis

O [!DNL Adobe Mobile SDK] contata o servidor [!DNL Target] para obter o conteúdo junto com outros pontos de dados para mostrar a experiência correta ao usuário.

>[!IMPORTANT]
>
>O suporte para os SDKs [!DNL Adobe Mobile] versão 4.*x* terminou a partir de 31 de agosto de 2021 e não é mais recomendado para usuários móveis [!DNL Adobe Target].
>
>O [Adobe Experience Platform SDK para Aplicativos para Dispositivos Móveis](https://developer.adobe.com/client-sdks/documentation/){target=_blank} é a solução recomendada para habilitar soluções e serviços do [!DNL Adobe Experience Cloud] em seus aplicativos para dispositivos móveis.

## [!DNL Target] locais e métricas de sucesso

Um *local de destino* também é chamado de mbox. Uma localização identificada no aplicativo é ativada para teste ou personalização (por exemplo, mensagem de boas vindas na tela inicial). Essas localizações são identificadas durante o processo de criação de teste.

Uma *[métrica de sucesso](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)* é uma ação executada pelo usuário que identifica se uma atividade específica foi bem-sucedida (como se conectar, fazer uma compra, reservar uma passagem e assim por diante).

![alt imagem](assets/mobile-target-location.png)

* **[!DNL Target]local:** O conteúdo que aparece abaixo do botão de registro.

  Esse usuário específico tem frete grátis até às 18h. Este local pode ser reutilizado em várias atividades [!DNL Target] para executar testes A/B e personalização.

* **Métrica de sucesso:** a ação executada pelo usuário em que o usuário toca no botão Registrar.

**Entenda como o [!DNL Target] funciona na SDK**

![alt imagem](assets/how-target-mobile-works.png)
