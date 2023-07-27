---
title: Gerenciar implantações para testes de recursos
description: Saiba como gerenciar implantações para testes de recursos usando o [!UICONTROL decisão no dispositivo].
feature: APIs/SDKs
exl-id: caa91728-6ac0-4583-a594-0c8fe616342d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Gerenciar implantações para testes de recursos

## Resumo das etapas

1. Ativar [!UICONTROL decisão no dispositivo] para sua organização
1. Criar um [!UICONTROL Teste A/B] atividade
1. Definir as configurações de recurso e implantação
1. Implementar e renderizar o recurso em seu aplicativo
1. Implementar o rastreamento de eventos no aplicativo
1. Ativar atividade A/B
1. Ajuste a implantação e a alocação de tráfego conforme necessário

## 1. Ativar [!UICONTROL decisão no dispositivo] para sua organização

A ativação da decisão no dispositivo garante que uma atividade A/B seja executada com latência próxima a zero. Para ativar esse recurso, navegue até **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Detalhes da conta]** in [!DNL Adobe Target]e habilite o **[!UICONTROL Decisão no dispositivo]** alternar.

![imagem alt](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Você precisa ter um Administrador ou Aprovador [função do usuário](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) para ativar ou desativar o [!UICONTROL Decisão no dispositivo] alternar.

Depois de ativar o [!UICONTROL Decisão no dispositivo] alternar, [!DNL Adobe Target] começa a gerar *artefatos de regra* para o seu cliente.

## 2. Criar um [!UICONTROL Teste A/B] atividade

1. Entrada [!DNL Adobe Target], navegue até o **[!UICONTROL Atividades]** e selecione **[!UICONTROL Criar atividade]** > **[!UICONTROL Teste A/B]**.

   ![imagem alt](assets/asset-ab.png)

1. No **[!UICONTROL Criar atividade de teste A/B]** modal, deixe o padrão **[!UICONTROL Web]** selecionada (1), selecione **[!UICONTROL Formulário]** como compositor de experiências (2), selecione **[!UICONTROL Espaço de trabalho padrão]** com **[!UICONTROL Sem restrições de propriedade]** (3) e clique em **[!UICONTROL Próxima]** (4).

   ![imagem alt](assets/asset-form.png)

## 3. Definir as configurações de recurso e implantação

No **[!UICONTROL Experiências]** etapa de criação da atividade, forneça um nome para a atividade (1). Digite o nome do local (2) no aplicativo onde deseja gerenciar implantações para o recurso. Por exemplo,  `ondevice-rollout` ou `homepage-addtocart-rollout` são nomes de localização que indicam os destinos para o gerenciamento de implantações de recursos. No exemplo mostrado abaixo, `ondevice-rollout` é o local definido para a Experiência A. Opcionalmente, é possível adicionar refinamentos de Público-alvo (4) para restringir a qualificação à atividade.

![imagem alt](assets/asset-location-rollout.png)

1. No **[!UICONTROL Conteúdo]** na mesma página, selecione **[!UICONTROL Criar oferta JSON]** no menu suspenso (1), como mostrado.

   ![imagem alt](assets/asset-offer.png)

1. No **[!UICONTROL Dados JSON]** Na caixa de texto exibida, digite a variável do sinalizador de recurso do recurso que você pretende implantar com esta atividade na Experiência A (1), usando um objeto JSON válido (2).

   ![imagem alt](assets/asset-json-a-rollout.png)

1. Clique em **[!UICONTROL Próxima]** (1) Avançar para o **[!UICONTROL Direcionamento]** etapa de criação da atividade.

   ![imagem alt](assets/asset-next-2-t-rollout.png)

1. No **[!UICONTROL Direcionamento]** etapa, mantenha a **[!UICONTROL Todos os visitantes]** público-alvo (1), para simplificar. Mas ajuste a alocação de tráfego (2) para 10%. Isso restringirá o recurso a apenas 10% dos visitantes do site. Clique em Avançar (3) para avançar para a **[!UICONTROL Metas e configurações]** etapa.

   ![imagem alt](assets/asset-next-2-g-rollout.png)

1. No **[!UICONTROL Metas e configurações]** etapa, escolha **[!UICONTROL Adobe Target]** (1) Dado que a **[!UICONTROL Fonte dos relatórios]** para exibir os resultados da atividade no [!DNL Adobe Target] IU.

1. Escolha um **[!UICONTROL Métrica de objetivo]** para medir a atividade. Neste exemplo, uma conversão bem-sucedida se baseia no fato de o usuário comprar um item, conforme indicado pelo fato de o usuário ter atingido o local orderConfirm (2).

1. Clique em **[!UICONTROL Salvar e fechar]** (3) para salvar a atividade.

   ![imagem alt](assets/asset-conv-rollout.png)

## 4. Implementar e renderizar o recurso em seu aplicativo

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

## 5. Implementar o rastreamento de eventos no aplicativo

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

## 6. Ativar a atividade de implantação

![imagem alt](assets/asset-activate-rollout.png)

## 7. Ajuste a implantação e a alocação de tráfego conforme necessário

Depois de ativar sua atividade, edite-a a qualquer momento para aumentar ou diminuir a alocação de tráfego, conforme necessário.

Aumento da alocação de tráfego de 10% para 50% devido ao sucesso da implantação inicial.

![imagem alt](assets/asset-adjust-rollout.png)
