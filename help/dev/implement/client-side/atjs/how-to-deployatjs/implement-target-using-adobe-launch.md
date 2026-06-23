---
keywords: implementar, implementação, implementação, adobe launch, launch, raça, redirecionamento, experience platform launch, platform launch, tags, adobe platform, implement2
description: Saiba como implementar a biblioteca at.js do  [!DNL Adobe Target] usando o  [!DNL Adobe Experience Platform], o método preferido para implementar o Target.
title: Como implementar o  [!DNL Target]  usando a  [!DNL Adobe Experience Platform]?
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
TQID: https://experienceleague.adobe.com/5dXJlXYYvlu5sskrNED2j55SNmeggtWTb1jLgXRXAEo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 61%

---

# Implementar o [!DNL Target]usando a [!DNL Adobe Experience Platform]

As tags na [!DNL Adobe Experience Platform] são a próxima geração de recursos de gerenciamento de tags da [!DNL Adobe]. As tags oferecem aos clientes uma forma simples de implantar e gerenciar as tags de análise, marketing e anúncios necessárias para potencializar experiências relevantes do cliente.

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleção de dados no [!DNL Adobe Experience Platform]. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?) para obter uma referência consolidada das alterações de terminologia.

A tabela a seguir lista as diversas fontes para obter mais informações:

| Recurso | Detalhes |
|--- |--- |
| [Adicionar Adobe Target](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html?lang=pt-BR#implement-solutions) | Esse tutorial fornece o passo a passo para implementar o [!DNL Target] em um site com tags na [!DNL Adobe Experience Platform]. Os tópicos incluem a adição da biblioteca do JavaScript at.js, o acionamento da mbox global, a adição de parâmetros e a integração com outras soluções. Este artigo faz parte de um tutorial maior que mostra como implementar o Adobe Experience Platform e outras soluções da Adobe Experience Cloud. |
| [Guia de início rápido](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html?lang=pt-BR) | Informações sobre implantação e gerenciamento das tags de análise, marketing e anúncio para potencialização de experiências relevantes do cliente. |
| [Visão geral da extensão da Adobe  [!DNL Target] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=pt-BR) | Informações sobre como implementar o [!DNL Target] usando a [!DNL Adobe Experience Platform]. |

## Vantagens de implementar a at.js utilizando a extensão do [!DNL Target]

As seguintes vantagens se aplicam apenas se você usar tags na [!DNL Adobe Experience Platform] para implementar a at.js. Por isso, a Adobe recomenda que você use tags no [!DNL Adobe Experience Platform], em vez de implementar manualmente a at.js.

* **Soluciona a condição de corrida do [!DNL Adobe Analytics] e do [!DNL Target]:** visto que a chamada do [!DNL Analytics] pode ser disparada antes da chamada do [!DNL Target], a chamada do [!DNL Target] não é anexada à chamada do [!DNL Analytics]. Este sequenciamento pode levar a dados incorretos. A extensão do [!DNL Target] garante que a chamada de sinal do [!DNL Analytics] espere até que a chamada do [!DNL Target] seja concluída, com ou sem êxito. Usar tags na [!DNL Adobe Experience Platform] resolve a inconsistência de dados que pode ocorrer com os clientes ao implementar manualmente.

  >[!NOTE]
  >
  >Use a ação Enviar Sinal na extensão [!DNL Adobe Analytics] para que a chamada [!DNL Analytics] aguarde a chamada [!DNL Target]. Se você chamar `s.t()` ou `s.tl()` diretamente, usando um código personalizado, as chamadas do [!DNL Analytics] não irão esperar até que as chamadas do [!DNL Target] sejam concluídas.

* **Impede o tratamento incorreto da oferta de redirecionamento:** Se você tiver [!DNL Target] e [!DNL Analytics] na página e uma oferta de redirecionamento for executada pelo Target, você poderá se deparar com uma situação em que o rastreador [!DNL Analytics] dispara uma solicitação quando não deveria (porque o usuário está sendo redirecionado para uma URL diferente). Se você implementar o [!DNL Target] e o [!DNL Analytics] por meio de tags no [!DNL Adobe Experience Platform], você não experienciará esse problema. Ao usar tags na [!DNL Adobe Experience Platform], o [!DNL Target] instrui o [!DNL Analytics] a suspender a solicitação de sinal do [!DNL Analytics].

