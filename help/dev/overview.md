---
keywords: guia do desenvolvedor do target, visão geral, página inicial
title: Guia do desenvolvedor do Adobe Target
description: Como implementar e administrar o  [!DNL Adobe Target] e trabalhar com suas APIs e SDKs?
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: dadc3804da4592dba4ad88b8c5c9f804c56e232b
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 5%

---

# Guia do desenvolvedor do [!DNL Adobe Target]

**([Exibir [!DNL Target] atualizações de documentação](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html){target=_blank})**

Este *[!DNL Adobe Target]Guia do Desenvolvedor* fornece recursos e guias para desenvolvedores do [!DNL Target], incluindo a documentação de API e SDK para implementar e administrar o [!DNL Target].

>[!NOTE]
>
>Além deste guia, as seguintes guias do [!DNL Adobe Target] também estão disponíveis:
>
>* [*[!DNL Adobe Target] Guia do profissional de negócios *](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=pt-BR){target=_blank}
>
>* [*[!DNL Adobe Target] Tutorials *](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=pt-BR){target=_blank}
>
>Para obter informações sobre a versão, consulte as [Notas de versão do Target (atual)](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html){target=_blank} no *[!DNL Adobe Target]Guia do Profissional de Negócios*.

## Introdução à implementação

**[Antes de implementar](/help/dev/before-implement/considerations-before-you-implement-target.md)**: considerações que você deve fazer antes de implementar o [!DNL Adobe Target].

## Implementação do lado do cliente

[**SDK da Web do Adobe Experience Platform**](/help/dev/implement/client-side/aep-web-sdk.md): o [!DNL Adobe Experience Platform Web SDK] permite que você interaja com os vários serviços no [!DNL Experience Cloud] (incluindo o [!DNL Target]) até o [!UICONTROL Adobe Experience Edge Network].

[**Biblioteca de JavaScript at.js do Target**](/help/dev/implement/client-side/overview.md): a biblioteca de JavaScript at.js melhora os tempos de carregamento de página de implementações da Web, melhora a segurança e fornece opções de implementações melhores para aplicativos de página única.

## Implementação do lado do servidor

[**Visão geral do SDK do Target**](implement/server-side/server-side-overview.md): Introdução aos [!DNL Adobe Target] SDKs, incluindo a Decisão no dispositivo.

[**SDK do Node.js**](implement/server-side/node-js/overview.md): como usar o SDK do Node.js [!DNL Target].

[**SDK Java**](implement/server-side/java/overview.md): como usar o SDK Java [!DNL Target].

[**.NET SDK**](implement/server-side/net/overview.md): como usar o [!DNL Target] .NET SDK.

[**Python SDK**](implement/server-side/python/overview.md): como usar o [!DNL Target] Python SDK.

## Implementação híbrida

[**Implantação híbrida**](implement/hybrid/hybrid-overview.md): implemente [!DNL Target] usando uma combinação de implementação do lado do cliente e do lado do servidor.

## Implementação do Recommendations

[**Implementação do Recommendations**](implement/recommendations/recommendations.md): planejar e implementar [!DNL Adobe Target Recommendations].

## Implementação do aplicativo móvel

[**Visão geral do SDK do AEP Mobile**](implement/mobile/overview.md): visão geral de como implementar o [!DNL Adobe Target] com [!DNL Adobe Experience Platform] SDKs móveis.

[**Referência de SDK do AEP Mobile**](https://developer.adobe.com/client-sdks/documentation/): implemente [!DNL Adobe Target] com [!DNL Adobe Experience Platform] SDKs móveis.

## Implementação de email

[**Visão geral do email**](implement/email/overview.md): visão geral de como implementar o [!DNL Adobe Target] nos emails.

## Guias da API

[**Introdução**](before-administer/target-api-overview.md): visão geral de [!DNL Adobe Target] APIs.

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md): Use as APIs de Entrega do [!DNL Adobe Target] para fornecer experiências em canais móveis e da Web, bem como dispositivos IoT não baseados em navegador, como TV conectada, quiosque ou tela digital na loja.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md): Use a API de Administração [!DNL Adobe Target] para gerenciar propriedades, atividades, públicos, ofertas, propriedades, relatórios, mboxes, hosts, ambientes e muito mais.

[**[!DNL Target Profile API]**](/help/dev/administer/profile-api/profiles-api.md): Recuperar informações de perfil de usuário [!DNL Adobe Target].

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports): Recuperar [!UICONTROL A/B Test] e [!UICONTROL Automated Personalization] dados do relatório de atividades.

[**[!DNL Target Recommendations API]**](https://developer.adobe.com/target/administer/recommendations-api/): Use a API [!DNL Target Recommendations].

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md): Gerenciar incluis na lista de bloqueios para definir os recursos usados em modelos de aprendizado de máquina do [!DNL Target].

[**APIs de Admin Console**](https://developer.adobe.com/umapi/): gerencie usuários e direitos de produto por meio das APIs de Sincronização de Usuários e Gerenciamento de Usuários de Adobe.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html): Use a API [!DNL Adobe Experience Platform Edge Network Server] para uma variedade de casos de uso de coleta de dados, personalização, publicidade e marketing.

## Recursos

* [repositório de código aberto do Adobe](https://github.com/adobe)
* [Source do SDK JS do Nó de Destino](https://github.com/adobe/target-nodejs-sdk)
* [Repo de Exemplos de SDK JS do Nó de Destino](https://github.com/adobe/target-nodejs-sdk-samples)
* [Source do SDK Java do Target](https://github.com/adobe/target-java-sdk)
* [Exemplo de repositório do SDK Java do Target](https://github.com/adobe/target-java-sdk-samples)
* [Implementação do Target](./before-implement/prepare-to-implement-target.md)
* [Administração do Target](./before-administer/target-api-overview.md)
* [Repositório GitHub do Adobe Target Dev Docs](https://github.com/AdobeDocs/target-developers)
* [Notas de versão do Adobe Target](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Guia do Usuário do Adobe Target Business](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=pt-BR)

