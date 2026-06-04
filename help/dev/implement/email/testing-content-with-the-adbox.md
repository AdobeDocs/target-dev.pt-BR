---
keywords: Implementação, não javascript, mbox, adbox
description: Use uma AdBox para fornecer imagens em uma implementação externa usando o  [!DNL Adobe Target]. Uma AdBox é como uma mbox, mas é controlada por um URL em vez do JavaScript.
title: Como criar uma AdBox para uma imagem?
feature: Implement Email
exl-id: ad1eb6c4-7a16-4054-ae76-57971261e931
TQID: https://experienceleague.adobe.com/OPo9T2Eb7afF8Ir8PAlY62OX83zhxtruUMKWCfUthxY
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: c94a34eb-b51c-4dd1-a6a4-46b0d84ccccd
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 337
ht-degree: 67%

---

# Criar uma AdBox para uma imagem

Use uma AdBox para fornecer imagens em uma implementação externa usando o [!DNL Adobe Target].

Uma AdBox é como uma mbox, mas é controlada por um URL, em vez de um JavaScript. AdBoxes são criadas com um URL AdBox especial que carrega uma mbox de &quot;anúncio&quot; (ou AdBox) na conta da Adobe. Use a AdBox no lugar de uma mbox em suas atividades. Use o URL da AdBox em vez de uma referência direta da imagem em um email ou outras implementações não-JavaScript.

Para obter ajuda para selecionar a configuração correta, consulte [Implementações não baseadas em JavaScript](/help/dev/implement/email/overview.md).

1. Criar o URL AdBox:

   ```
   https://myClientCode.tt.omtrdc.net/m2/myClientCode/ubox/
   image?mbox=emailHeroImage123_320x200&
   mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif
   ```

   * Onde `myClientCode` é o código de cliente da sua empresa. O código de cliente de sua empresa tem todos os caracteres em minúsculas e sem caracteres especiais.

     O código de cliente está disponível na parte superior da página **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** da interface [!DNL Target].

   * Onde `image` é o tipo de chamada. Nesse caso, uma imagem.

   * Onde `emailHeroImage123_320x200` é o nome da AdBox.

   * Onde `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif` é o conteúdo padrão da mbox. Isso deve ser uma imagem.

     Isso deve ser codificado no URL e uma referência absoluta. Você pode usar a [Referência de codificação de URL do HTML](https://www.w3schools.com/tags/ref_urlencode.asp) para codificar rapidamente suas URLs.

1. Crie [Ofertas de redirecionamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html) para cada imagem alternativa.

   >[!NOTE]
   >
   >As AdBoxes devem ser carregadas com uma Oferta de redirecionamento ou com a oferta de conteúdo padrão. Outros tipos de ofertas não funcionarão. Como a AdBox é um URL, ela só pode exibir os URLs que recebe, portanto, apenas a Oferta de redirecionamento funciona.

1. Crie a atividade.

   Consulte [Implementações não baseadas em JavaScript](/help/dev/implement/email/overview.md) para a configuração correta para atingir suas metas.

1. Faça o controle de qualidade da atividade.

   Como prática recomendada, crie uma página de teste e verifique se todas as experiências, o conteúdo padrão e os relatórios estão funcionando corretamente em todos os tipos de navegadores, para todos os seus ambientes.

1. Inicie a atividade.
