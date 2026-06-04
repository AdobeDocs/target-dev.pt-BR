---
title: Gerenciar implantações para testes de recursos
description: Saiba como gerenciar implantações para testes de recursos usando a [!UICONTROL decisão no dispositivo].
feature: APIs/SDKs
exl-id: caa91728-6ac0-4583-a594-0c8fe616342d
TQID: https://experienceleague.adobe.com/soG8leVV3R4Y4FSns5oIJ43oziIhtOb2zJ5bkFYxeo0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 596
ht-degree: 1%

---

# Gerenciar implantações para testes de recursos

## Resumo das etapas

1. Habilitar a [!UICONTROL decisão no dispositivo] para sua organização
1. Criar uma atividade [!UICONTROL Teste A/B]
1. Definir as configurações de recurso e implantação
1. Implementar e renderizar o recurso em seu aplicativo
1. Implementar o rastreamento de eventos no aplicativo
1. Ativar atividade A/B
1. Ajuste a implantação e a alocação de tráfego conforme necessário

## &#x200B;1. Habilitar a [!UICONTROL decisão no dispositivo] para sua organização

A ativação da decisão no dispositivo garante que uma atividade A/B seja executada com latência próxima a zero. Para habilitar este recurso, navegue até **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Detalhes da conta]** em [!DNL Adobe Target] e habilite a opção **[!UICONTROL Decisão no Dispositivo]**.

![alt imagem](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Você deve ter a [função de usuário](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=pt-BR) de Administrador ou Aprovador para habilitar ou desabilitar a [!UICONTROL Decisão no Dispositivo].

Depois de habilitar a opção [!UICONTROL Decisão no Dispositivo], o [!DNL Adobe Target] começa a gerar *artefatos de regra* para o seu cliente.

## &#x200B;2. Criar uma atividade [!UICONTROL Teste A/B]

1. Em [!DNL Adobe Target], navegue até a página **[!UICONTROL Atividades]** e selecione **[!UICONTROL Criar atividade]** > **[!UICONTROL Teste A/B]**.

   ![alt imagem](assets/asset-ab.png)

1. No modal **[!UICONTROL Criar Atividade de Teste A/B]**, deixe a opção padrão **[!UICONTROL Web]** selecionada (1), selecione **[!UICONTROL Formulário]** como compositor de experiência (2), selecione **[!UICONTROL Workspace Padrão]** com **[!UICONTROL Sem Restrições de Propriedade]** (3) e clique em **[!UICONTROL Avançar]** (4).

   ![alt imagem](assets/asset-form.png)

## &#x200B;3. Definir as configurações de recurso e implantação

Na etapa **[!UICONTROL Experiências]** da criação da atividade, forneça um nome para a atividade (1). Digite o nome do local (2) no aplicativo onde deseja gerenciar implantações para o recurso. Por exemplo, `ondevice-rollout` ou `homepage-addtocart-rollout` são nomes de locais que indicam os destinos para o gerenciamento de implantações de recursos. No exemplo mostrado abaixo, `ondevice-rollout` é o local definido para a Experiência A. Opcionalmente, é possível adicionar refinamentos de Público-alvo (4) para restringir a qualificação à atividade.

![alt imagem](assets/asset-location-rollout.png)

1. Na seção **[!UICONTROL Conteúdo]** da mesma página, selecione **[!UICONTROL Criar Oferta JSON]** na lista suspensa (1), conforme mostrado.

   ![alt imagem](assets/asset-offer.png)

1. Na caixa de texto **[!UICONTROL Dados JSON]** exibida, digite a variável do sinalizador de recurso do recurso que você pretende implantar com esta atividade na Experiência A (1), usando um objeto JSON válido (2).

   ![alt imagem](assets/asset-json-a-rollout.png)

1. Clique em **[!UICONTROL Avançar]** (1) para avançar para a etapa **[!UICONTROL Direcionamento]** da criação da atividade.

   ![alt imagem](assets/asset-next-2-t-rollout.png)

1. Na etapa **[!UICONTROL Direcionamento]**, mantenha o público-alvo de **[!UICONTROL Todos os visitantes]** (1), para simplificar. Mas ajuste a alocação de tráfego (2) para 10%. Isso restringirá o recurso a apenas 10% dos visitantes do site. Clique em Avançar (3) para avançar para a etapa **[!UICONTROL Metas e configurações]**.

   ![alt imagem](assets/asset-next-2-g-rollout.png)

1. Na etapa **[!UICONTROL Metas e Configurações]**, escolha **[!UICONTROL Adobe Target]** (1) como a **[!UICONTROL Source de Relatórios]** para exibir os resultados da atividade na interface do usuário do [!DNL Adobe Target].

1. Escolha uma **[!UICONTROL Métrica de meta]** para medir a atividade. Neste exemplo, uma conversão bem-sucedida se baseia no fato de o usuário comprar um item, conforme indicado pelo fato de o usuário ter atingido o local orderConfirm (2).

1. Clique em **[!UICONTROL Salvar e fechar]** (3) para salvar a atividade.

   ![alt imagem](assets/asset-conv-rollout.png)

## &#x200B;4. Implementar e renderizar o recurso em seu aplicativo

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
targetClient.getAttributes(["ondevice-rollout"]).then(function(attributes) {
      const featureFlags = attributes.asObject("ondevice-rollout");

      // Your flag variables are now available in the featureFlags object variable.
      //If you failed to qualify for the Activity, you will have an empty object.
      console.log(featureFlags);
    });
```

>[!TAB Java]

```java {line-numbers="true"}
    Attributes attrs = targetJavaClient.getAttributes(targetDeliveryRequest, "ondevice-rollout");
    Map<String, Object> featureFlags = attrs.toMboxMap("ondevice-rollout");
​
    // Your flag variables are now available in the featureFlags object variable.
    //If you failed to qualify for the Activity, you will have an empty object.
    System.out.println(featureFlags);
```

>[!ENDTABS]

## &#x200B;5. Implementar o rastreamento de eventos no aplicativo

Depois de disponibilizar a variável do sinalizador de recurso no aplicativo, você pode usá-la para ativar qualquer recurso que já faça parte do aplicativo. Se um visitante não se qualificar para a atividade, significa que não foi incluído como parte do intervalo de 10% definido como o público-alvo.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

if(featureFlags.enable == "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}

// alternatively, the getValue method could be used on the Attributes object.

if(attributes.getValue("ondevice-rollout", "enable") === "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}
```

>[!TAB Java]

```java {line-numbers="true"}
//... Code removed for brevity
​
if("yes".equals(String.valueOf(featureFlags.get("enable")))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
​
// alternatively, the getString method could be used on the Attributes object.
​
if("yes".equals(attrs.getString("ondevice-rollout", "enable"))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
```

>[!ENDTABS]

## &#x200B;6. Ativar a atividade de implantação

![alt imagem](assets/asset-activate-rollout.png)

## &#x200B;7. Ajuste a implantação e a alocação de tráfego conforme necessário

Depois de ativar sua atividade, edite-a a qualquer momento para aumentar ou diminuir a alocação de tráfego, conforme necessário.

Aumento da alocação de tráfego de 10% para 50% devido ao sucesso da implantação inicial.

![alt imagem](assets/asset-adjust-rollout.png)
