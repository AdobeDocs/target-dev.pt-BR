---
title: Executar testes A/B com sinalizadores de recursos e decisão no dispositivo
description: Execute testes A/B com sinalizadores de recursos usando a decisão no dispositivo.
feature: APIs/SDKs
exl-id: abf66e00-742d-4d40-9b6e-9bd71638c31a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Executar testes A/B com sinalizadores de recursos

## Resumo das etapas

1. Habilitar [!UICONTROL on-device decisioning] para sua organização
1. Criar uma atividade [!UICONTROL A/B Test]
1. Defina seus A e B
1. Adicionar um público
1. Definir alocação de tráfego
1. Definir a distribuição do tráfego para variações
1. Configurar relatórios
1. Adicionar métricas para KPIs de rastreamento
1. Implementar código para executar testes A/B com sinalizadores de recursos
1. Ativar o teste A/B com sinalizadores de recursos

>[!NOTE]
>
>Suponha que você queira determinar se o novo design com tema de outono da sua página inicial seria bem recebido pelos seus usuários. Você decide testá-lo executando um experimento A/B em [!DNL Adobe Target]. Você também quer garantir que o experimento seja entregue com ótimo desempenho para que uma experiência do usuário negativa ou lenta não distorça os resultados.

## 1. Habilitar [!UICONTROL on-device decisioning] para sua organização

A ativação da decisão no dispositivo garante que uma atividade A/B seja executada com latência próxima a zero. Para habilitar este recurso, navegue até **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** em [!DNL Adobe Target] e habilite a alternância **[!UICONTROL On-Device Decisioning]**.

&lt;!— Inserir image-ímpar4.png —>
![alt imagem](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Você deve ter a [função de usuário](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=pt-BR) de Administrador ou Aprovador para habilitar ou desabilitar a opção On-Device Decisioning.

Depois de habilitar a alternância **[!UICONTROL On-Device Decisioning]**, [!DNL Adobe Target] começa a gerar artefatos de regra para o seu cliente.

## 2. Criar uma atividade [!UICONTROL A/B Test]

Em [!DNL Adobe Target], navegue até a página **[!UICONTROL Activities]** e selecione **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**.

![alt imagem](assets/asset-ab.png)

No modal **[!UICONTROL Create A/B Test Activity]**, deixe a opção padrão **[!UICONTROL Web]** selecionada (1), selecione **[!UICONTROL Form]** como compositor de experiência (2), selecione **[!UICONTROL Default Workspace]** sem **[!UICONTROL Property Restrictions]** (3) e clique em **[!UICONTROL Next]** (4).

![alt imagem](assets/asset-form.png)

## 3. Defina seus A e B

1. Na etapa de criação da atividade **[!UICONTROL Experiences]**, forneça um nome para a atividade (1) e adicione uma segunda experiência, Experiência B, clicando no botão **[!UICONTROL Add Experience]** (2). Informe o nome do local (3) no aplicativo em que deseja executar o teste A/B. No exemplo mostrado abaixo, a página inicial é o local definido para a Experiência A. (Também é o local definido para a Experiência B.)

   A Experiência A define o controle, que é o design da página inicial atual.

   ![alt imagem](assets/asset-exp-a.png)

   A Experiência B define o desafiante, que representará uma página inicial reprojetada. Clique em para alterar o conteúdo padrão (1).

   ![alt imagem](assets/asset-exp-b.png)

1. Na Experiência B, clique para alterar o conteúdo de **[!UICONTROL Default Content]** para o conteúdo reprojetado selecionando **[!UICONTROL Create JSON Offer]** como mostrado abaixo (1).

   ![alt imagem](assets/asset-offer.png)

1. Defina o JSON com atributos que serão utilizados como sinalizadores para permitir que sua lógica comercial renderize a página inicial recém-reprojetada, em vez da página inicial atual em produção.


   >[!NOTE]
   >
   >Quando [!DNL Adobe Target] agrupa um usuário para ver a Experiência B (a página inicial reprojetada), o JSON com os atributos definidos no exemplo será retornado. Em seu código, você precisará verificar os valores do atributo para decidir se executa a lógica de negócios para renderizar a página inicial reprojetada. Você pode definir os nomes, os valores e o número de atributos nesta resposta JSON.

   ![alt imagem](assets/asset-homepage.png)

## 4. Adicionar um público-alvo

Suponha que você queira primeiro testar o redesign em seus clientes fiéis, que você pode identificar com base em se eles estão ou não conectados.

1. Na etapa **[!UICONTROL Targeting]**, clique em para substituir o público-alvo **[!UICONTROL All Visitors]**, conforme mostrado.

   ![alt imagem](assets/asset-all-audiences.png)

1. No modal **[!UICONTROL Create Audience]**, defina uma regra personalizada onde `logged-in = true`. Isso define o grupo de usuários que estão conectados. Use esse público-alvo na sua atividade.

   ![alt imagem](assets/asset-audience.png)

## 5. Definir a alocação de tráfego

Defina a porcentagem de usuários conectados com base na qual você deseja testar o novo design da página inicial. Em outras palavras, para que porcentagem de seus usuários você deseja implantar esse teste? Neste exemplo, para implantar este teste para todos os usuários conectados, mantenha a alocação de tráfego em 100%.

![alt imagem](assets/asset-allocation.png)

## 6. Definir a distribuição do tráfego para variações

Defina a porcentagem de usuários conectados que visualizarão o design atual da página inicial ou o novo design. Neste exemplo, mantenha a distribuição do tráfego dividida em 50/50 entre as Experiências A e B.

![alt imagem](assets/asset-traffic-distribution.png)

## 7. Configurar relatórios

Na etapa **[!UICONTROL Goals & Settings]**, escolha **[!UICONTROL Adobe Target]** como **[!UICONTROL Reporting Source]** para exibir os resultados da atividade na interface do usuário [!DNL Adobe Target], ou **[!UICONTROL Adobe Analytics]** para exibi-los na interface do usuário do Adobe Analytics.

![alt imagem](assets/asset-reporting.png)

## 8. Adicionar métricas para rastrear KPIs

Escolha um **[!UICONTROL Goal Metric]** para medir o teste A/B. Neste exemplo, uma conversão bem-sucedida se baseia no fato de o usuário chegar à parte inferior da página, indicando engajamento. Portanto, **[!UICONTROL Conversion]** é determinado com base no fato de o usuário ter visualizado o local chamado fim da página.

## 9. Implemente o código para executar testes A/B com sinalizadores de recursos no aplicativo

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const options = {
  client: "testClient",
  organizationId: "ABCDEF012345677890ABCDEF0@AdobeOrg",
  decisioningMethod: "on-device",
  events: {
    clientReady: targetClientReady
  }
};
const targetClient = TargetClient.create(options);

function targetClientReady() {
  return targetClient.getAttributes(["homepage"]).then(function(attributes) {
    const flag = attributes.getValue("homepage", "feature-flag");
    // ...
  });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

ClientConfig config = ClientConfig.builder()
    .client("testClient")
    .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
    .build();
TargetClient targetClient = TargetClient.create(config);
MboxRequest mbox = new MboxRequest().name("homepage").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "homepage");
String flag = attributes.getString("homepage", "feature-flag");
```

>[!ENDTABS]

## 10. Ative o teste A/B com o sinalizador de recurso

![alt imagem](assets/asset-activate.png)
