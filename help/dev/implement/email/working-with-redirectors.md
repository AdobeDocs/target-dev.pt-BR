---
keywords: Implementação, mbox.js sem JavaScript, redirecionador, custos por clique, receita por clique
description: Saiba como usar Redirecionadores em implementações de email, de forma semelhante a como você usa uma mbox em suas atividades de  [!DNL Adobe Target] .
title: Como trabalho com redirecionadores?
feature: Implement Email
exl-id: 072368ff-9f17-4709-ac2d-c9e1f0d888bb
TQID: https://experienceleague.adobe.com/3SUsZl1y9tk97sWgdB3iB7wrAXNb2LfN3hObJM14caE
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: c94a34eb-b51c-4dd1-a6a4-46b0d84ccccd
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 689
ht-degree: 63%

---

# Trabalhar com redirecionadores

Utilize o Redirecionador de forma similar a uma mbox em seus testes.

Redirecionadores são criados com um URL de Redirecionador especial, que carrega a mbox do Redirecionador na conta. Utilize o Redirecionador de forma similar a uma mbox em seus testes. Envie o URL de Redirecionador para sua Rede de publicidade como o link de destino do anúncio.

Use o redirecionador para fazer o seguinte:

* Acompanhar cliques dos seus anúncios de exibição para o seu site
* Criar um relatório único e centralizado para rastrear os cliques para exibir anúncios em várias redes de anúncios
* Variar os destinos de anúncio de exibição

  Por exemplo, o mesmo banner pode acessar sua página inicial, de categoria e produto.

* Descobrir qual página de aterrissagem leva ao maior número de conversões

Para obter ajuda para decidir a configuração correta, consulte [Implementações não baseadas em JavaScript](/help/dev/implement/email/overview.md).

## Criar um redirecionador

Antes de utilizar um redirecionador, você deve criá-lo.

1. Determine as variações de destino do anúncio, incluindo o destino padrão.
1. Crie o redirecionador de URL.

   ```
   https://<your_testandtarget_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox
   /​page?mbox=redirectorlink_456
   &mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm
   ```

   * Onde `yourclientcode` é o código de cliente da sua empresa. O código de cliente de sua empresa tem todos os caracteres em minúsculas e sem caracteres especiais.

     O código de cliente está disponível na parte superior da página **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** da interface [!DNL Target].

   * `redirectorlink_456` é o nome do Redirecionador mbox que aparece em sua conta para ser usado em campanhas e testes.

     Redirecionadores funcionam de forma diferente das outras mboxes, mas são exibidas como qualquer outra mbox em sua conta. Identifique o redirecionador de uma forma que seja fácil diferenciá-lo das mboxes de tipo padrão em sua conta.  Como prática recomendada, comece o nome da mbox com &quot;redirectorlink&quot;.

   * Onde `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm` é o destino padrão.

     Isso deve ser codificado no URL e uma referência absoluta. Você pode usar a [Referência de codificação de URL do HTML](https://www.w3schools.com/tags/ref_urlencode.asp) para codificar rapidamente suas URLs.

   >[!WARNING]
   >
   >Observe que, com o Redirecionador, você pode ser exposto ao risco de uma vulnerabilidade de redirecionamento aberto. Para evitar o uso não autorizado de links redirecionadores por terceiros, a Adobe recomenda que você use &quot;hosts autorizados&quot; para incluir na lista de permissões os domínios de URL de redirecionamento padrão. [!DNL Target] usa hosts para incluir na lista de permissões domínios aos quais você deseja permitir redirecionamentos. Para obter mais informações, consulte [Criar Incluis na lista de permissões que especificam hosts autorizados a enviar chamadas de mbox para  [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) em *Hosts*.

1. Valide o redirecionador.
   1. *Prática recomendada de segurança*: certifique-se de que o domínio usado no Redirecionador seja ativado, conforme indicado acima. Se você usar um domínio que não esteja classificado, a Adobe bloqueará qualquer chamada para esse domínio a fim de impedir que agentes mal-intencionados usem o Redirecionador para redirecionar para domínios potencialmente mal-intencionados.
   2. Insira o URL do redirecionador no navegador e atualize a página.
   3. Efetue logon em sua conta, atualize a lista de mbox e verifique se o novo redirecionador está indicado como uma mbox.
1. Se você vai testar destinos diferentes para um anúncio, crie [Ofertas de redirecionamento](https://experienceleague.adobe.com/docs/target/using/experiences/vec/redirect-offer.html) para cada versão.
1. Crie uma campanha.

   Consulte [Implementações não baseadas em JavaScript](/help/dev/implement/email/overview.md) para a configuração correta para atingir seus objetivos.
1. Faça o controle de qualidade da campanha.

   Crie uma página de testes com um `<a href>` contendo o URL Redirecionador. Exemplo:

   ```
   <a href=https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=
   
   redirectorlink_456&mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2F​usualdestination%2Ehtm>
   ```

1. Verifique se todos as experiências, o conteúdo padrão e os relatórios estão funcionando corretamente em todos os tipos de navegadores, para todos os seus ambientes.

   >[!NOTE]
   >
   >Redirecionadores não são suportados pela Visualização de oferta ou Procurar por mbox. Visualize as experiências diretamente em um navegador. Além disso, `mboxDebug` não funciona com Redirecionadores.

1. Envie o URL completo do Redirecionador para sua rede de publicidade como destino do anúncio.

## Use o redirecionador para enviar Custos por clique e Receita por clique

Informações sobre o uso de um redirecionador para transmitir os custos por clique e a receita por clique.

### Enviar custo por clique

Use o redirecionador para passar os custos por clique.

>[!NOTE]
>
>A prática recomendada é determinar o valor de custo usando a métrica de envolvimento **[!UICONTROL Score per visit]**.

Adicione `&mboxPageValue=-value` à URL. Observe o valor negativo.

Exemplo: Para um custo de 10 centavos por clique:

```
https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=redirectorlink_456
&mboxPageValue=-0.1&mboxDefault=​https://www.yourcompany.com/usualdestination.htm
```

### Enviar receita por clique

Use o redirecionador para passar a receita por clique.

>[!NOTE]
>
>A prática recomendada é determinar o valor de receita usando a métrica de envolvimento **[!UICONTROL Score per visit]**.

Adicione `&mboxPageValue=value` à URL.

Exemplo: Para uma receita de 10 centavos por clique.

```
https://<​your_clientcode>​​​​.tt​​.omtrdc​.net/​​m2/​yourclientcode/​ubox/​​​page?mbox=redirectorlink_456
&mboxPageValue=0.1​&mbox​Default=​​http%3A%2F%2Fwww%2E​yourcompany%2Ecom​%2Fusualdestination%2Ehtm
```
