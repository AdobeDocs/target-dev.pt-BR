---
title: Executar testes A/B com sinalizadores de recursos e decisão no dispositivo
description: Execute testes A/B com sinalizadores de recursos usando a decisão no dispositivo.
feature: APIs/SDKs
exl-id: abf66e00-742d-4d40-9b6e-9bd71638c31a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Executar testes A/B com sinalizadores de recursos

## Resumo das etapas

1. Ativar [!UICONTROL decisão no dispositivo] para sua organização
1. Criar um [!UICONTROL Teste A/B] atividade
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
>Suponha que você queira determinar se o novo design com tema de outono da sua página inicial seria bem recebido pelos seus usuários. Você decide testá-lo executando um experimento A/B no [!DNL Adobe Target]. Você também quer garantir que o experimento seja entregue com ótimo desempenho para que uma experiência do usuário negativa ou lenta não distorça os resultados.

## 1. Ativar [!UICONTROL decisão no dispositivo] para sua organização

A ativação da decisão no dispositivo garante que uma atividade A/B seja executada com latência próxima a zero. Para ativar esse recurso, navegue até **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Detalhes da conta]** in [!DNL Adobe Target]e habilite o **[!UICONTROL Decisão no dispositivo]** alternar.

&lt;!— Inserir image-ímpar4.png —>
![imagem alt](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Você precisa ter um Administrador ou Aprovador [função do usuário](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) para ativar ou desativar a opção Decisão no dispositivo.

Depois de ativar o **[!UICONTROL Decisão no dispositivo]** alternar, [!DNL Adobe Target] O começa a gerar artefatos de regra para o seu cliente.

## 2. Criar um [!UICONTROL Teste A/B] atividade

Entrada [!DNL Adobe Target], navegue até o **[!UICONTROL Atividades]** e selecione **[!UICONTROL Criar atividade]** > **[!UICONTROL Teste A/B]**.

![imagem alt](assets/asset-ab.png)

No **[!UICONTROL Criar atividade de teste A/B]** modal, deixe o padrão **[!UICONTROL Web]** selecionada (1), selecione **[!UICONTROL Formulário]** como compositor de experiências (2), selecione **[!UICONTROL Espaço de trabalho padrão]** com Não **[!UICONTROL Restrições de propriedade]** (3) e clique em **[!UICONTROL Próxima]** (4).

![imagem alt](assets/asset-form.png)

## 3. Defina seus A e B

1. No **[!UICONTROL Experiências]** etapa de criação da atividade, forneça um nome para a atividade (1) e adicione uma segunda experiência, Experiência B, clicando no link **[!UICONTROL Adicionar experiência]** (2) botão. Informe o nome do local (3) no aplicativo em que deseja executar o teste A/B. No exemplo mostrado abaixo, a página inicial é o local definido para a Experiência A. (Também é o local definido para a Experiência B.)

   A Experiência A define o controle, que é o design da página inicial atual.

   ![imagem alt](assets/asset-exp-a.png)

   A Experiência B define o desafiante, que representará uma página inicial reprojetada. Clique em para alterar o conteúdo padrão (1).

   ![imagem alt](assets/asset-exp-b.png)

1. Na Experiência B, clique para alterar o conteúdo de **[!UICONTROL Conteúdo padrão]** ao conteúdo reprojetado selecionando **[!UICONTROL Criar oferta JSON]** conforme indicado abaixo (1).

   ![imagem alt](assets/asset-offer.png)

1. Defina o JSON com atributos que serão utilizados como sinalizadores para permitir que sua lógica comercial renderize a página inicial recém-reprojetada, em vez da página inicial atual em produção.


   >[!NOTE]
   >
   >Quando [!DNL Adobe Target] agrupa um usuário para ver a Experiência B (a página inicial reprojetada), o JSON com os atributos definidos no exemplo será retornado. Em seu código, você precisará verificar os valores do atributo para decidir se executa a lógica de negócios para renderizar a página inicial reprojetada. Você pode definir os nomes, os valores e o número de atributos nesta resposta JSON.

   ![imagem alt](assets/asset-homepage.png)

## 4. Adicionar um público-alvo

Suponha que você queira primeiro testar o redesign em seus clientes fiéis, que você pode identificar com base em se eles estão ou não conectados.

1. No **[!UICONTROL Direcionamento]** clique em para substituir a variável **[!UICONTROL Todos os visitantes]** público-alvo, conforme mostrado.

   ![imagem alt](assets/asset-all-audiences.png)

1. No **[!UICONTROL Criar público-alvo]** modal, defina uma regra personalizada onde `logged-in = true`. Isso define o grupo de usuários que estão conectados. Use esse público-alvo na sua atividade.

   ![imagem alt](assets/asset-audience.png)

## 5. Definir a alocação de tráfego

Defina a porcentagem de usuários conectados com base na qual você deseja testar o novo design da página inicial. Em outras palavras, para que porcentagem de seus usuários você deseja implantar esse teste? Neste exemplo, para implantar este teste para todos os usuários conectados, mantenha a alocação de tráfego em 100%.

![imagem alt](assets/asset-allocation.png)

## 6. Definir a distribuição do tráfego para variações

Defina a porcentagem de usuários conectados que visualizarão o design atual da página inicial ou o novo design. Neste exemplo, mantenha a distribuição do tráfego dividida em 50/50 entre as Experiências A e B.

![imagem alt](assets/asset-traffic-distribution.png)

## 7. Configurar relatórios

No **[!UICONTROL Metas e configurações]** etapa, escolha **[!UICONTROL Adobe Target]** como o **[!UICONTROL Fonte dos relatórios]** para exibir os resultados da atividade no [!DNL Adobe Target] ou escolha **[!UICONTROL Adobe Analytics]** para visualizá-los na interface do usuário do Adobe Analytics.

![imagem alt](assets/asset-reporting.png)

## 8. Adicionar métricas para rastrear KPIs

Escolha um **[!UICONTROL Métrica de objetivo]** para medir o teste A/B. Neste exemplo, uma conversão bem-sucedida se baseia no fato de o usuário chegar à parte inferior da página, indicando engajamento. Por conseguinte, **[!UICONTROL Conversão]** é determinado com base no fato de o usuário ter visualizado o local chamado de final da página.

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

![imagem alt](assets/asset-activate.png)
