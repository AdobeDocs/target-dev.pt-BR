---
keywords: guia do desenvolvedor do target, visão geral
title: Guia do desenvolvedor do Adobe Target
description: Como implementar e administrar o  [!DNL Adobe Target]  e trabalhar com suas APIs e SDKs?
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: 063d0574ee380bf76130fb0f17db89cd09efdb7d
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 14%

---

# Guia do desenvolvedor do [!DNL Adobe Target]

**([Exibir [!DNL Target] atualizações de documentação](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html){target=_blank})**

Este *[!DNL Adobe Target]Guia do desenvolvedor* O fornece recursos e guias para [!DNL Target] desenvolvedores do, incluindo a documentação de API e SDK para implementar e administrar o [!DNL Target].

>[!NOTE]
>
>Além deste guia, as seguintes guias do [!DNL Adobe Target] também estão disponíveis:
>
>* [*[!DNL Adobe Target] Guia do profissional de negócios do *](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=pt-BR){target=_blank}
>
>* [*[!DNL Adobe Target] Tutorials *](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=pt-BR){target=_blank}
>
>Para obter informações sobre a versão, consulte [Notas de versão do Target (atual)](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html){target=_blank} no *[!DNL Adobe Target]Guia do profissional de negócios do*.

## Introdução à implementação

**[](/help/dev/before-implement/considerations-before-you-implement-target.md)** Antes da implementação: considerações que você deve fazer antes de implementar o [!DNL Adobe Target].

## Implementação do lado do cliente

[**Adobe Experience Platform Web SDK**](/help/dev/implement/client-side/aep-web-sdk.md): A variável [!DNL Adobe Experience Platform Web SDK] permite interagir com os vários serviços na [!DNL Experience Cloud] (incluindo [!DNL Target]) por meio da [!UICONTROL Rede de borda da Adobe Experience].

[**Biblioteca JavaScript at.js do Target**](/help/dev/implement/client-side/overview.md): A biblioteca JavaScript at.js do melhora os tempos de carregamento de página de implementações da Web, melhora a segurança e fornece opções de implementações melhores para aplicativos de página única.

## Implementação do lado do servidor

[**Visão geral do SDK do Target**](implement/server-side/server-side-overview.md): Introdução a [!DNL Adobe Target] SDKs, incluindo a Decisão no dispositivo.

[**SDK do Node.js**](implement/server-side/node-js/overview.md): como usar o [!DNL Target] SDK do Node.js.

[**SDK do Java**](implement/server-side/java/overview.md): como usar o [!DNL Target] SDK do Java.

[**SDK DO .NET**](implement/server-side/net/overview.md): como usar o [!DNL Target] .NET SDK.

[**Python SDK**](implement/server-side/python/overview.md): como usar o [!DNL Target] Python SDK.

## Implementação híbrida

[**Implantação híbrida**](implement/hybrid/hybrid-overview.md): Implementação [!DNL Target] usando uma combinação de implementação do lado do cliente e do lado do servidor.

## Implementação do Recommendations

[**Implementação do Recommendations**](implement/recommendations/recommendations.md): Planejar e implementar o [!DNL Adobe Target Recommendations].

## Implementação do aplicativo móvel

[**Visão geral do SDK do AEP Mobile**](implement/mobile/overview.md): visão geral de como implementar o [!DNL Adobe Target] com [!DNL Adobe Experience Platform] SDKs móveis.

[**Referência do SDK do AEP Mobile**](https://developer.adobe.com/client-sdks/documentation/): Implementação [!DNL Adobe Target] com [!DNL Adobe Experience Platform] SDKs móveis.

## Implementação de email

[**Visão geral do email**](implement/email/overview.md): visão geral de como implementar o [!DNL Adobe Target] nos emails.

## Guias da API

[**Introdução**](before-administer/target-api-overview.md): Visão geral do [!DNL Adobe Target] APIs.

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md): Use o [!DNL Adobe Target] APIs de entrega para fornecer experiências em canais da Web e móveis, bem como dispositivos IoT não baseados em navegador, como TV conectada, quiosque ou tela digital na loja.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md): Use o [!DNL Adobe Target] API de administração para gerenciar propriedades, atividades, públicos, ofertas, propriedades, relatórios, mboxes, hosts, ambientes e muito mais.

[**[!DNL Target Profile API]**](https://developers.adobetarget.com/api/#profiles): Recuperar [!DNL Adobe Target] informações de perfil do usuário.

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports): Recuperar [!UICONTROL Teste A/B] e [!UICONTROL Automated Personalization] dados do relatório de atividades.

[**[!DNL Target Recommendations API]**](http://developers.adobetarget.com/api/recommendations/): Use o [!DNL Target Recommendations] API.

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md)incluir na lista de bloqueios : Gerenciar classificações para definir os recursos usados no [!DNL Target] modelos de aprendizado de máquina.

[**APIs Admin Console**](https://developer.adobe.com/umapi/): gerencie usuários e direitos de produto por meio do Gerenciamento de usuários do Adobe e das APIs de sincronização de usuários.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html): Use o [!DNL Adobe Experience Platform Edge Network Server] API para diversos casos de uso de coleta de dados, personalização, publicidade e marketing.

## Recursos

* [repositório de código aberto do Adobe](https://github.com/adobe)
* [Origem do SDK JS do nó de destino](https://github.com/adobe/target-nodejs-sdk)
* [Exemplos de SDK JS do nó de destino do repositório](https://github.com/adobe/target-nodejs-sdk-samples)
* [Origem do SDK Java do Target](https://github.com/adobe/target-java-sdk)
* [Exemplo de repositório do SDK Java do Target](https://github.com/adobe/target-java-sdk-samples)
* [Implementação do Target](./before-implement/prepare-to-implement-target.md)
* [Administração do Target](./before-administer/target-api-overview.md)
* [Repositório GitHub do Adobe Target Dev Docs](https://github.com/AdobeDocs/target-developers)
* [Notas de versão do Adobe Target](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Guia do usuário empresarial do Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=pt-BR)

