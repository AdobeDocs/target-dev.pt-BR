---
keywords: lado do servidor, lado do servidor, sdk, sdks, no dispositivo, decisão, no dispositivo, ondevice, latência zero, latência, próximo a zero, node.js, lado do servidor3
description: Saiba como usar o [!UICONTROL [!UICONTROL decisão no dispositivo]] para armazenar em cache o [!DNL Target] Atividades A/B e MVT no servidor para executar a decisão na memória com latência próxima a zero.
title: O que é a Decisão no dispositivo?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 8%

---

# Visão geral da decisão no dispositivo

A próxima geração [!DNL Adobe Target] Os SDKs agora oferecem [!UICONTROL decisão no dispositivo], que oferece a capacidade de armazenar em cache suas campanhas A/B e de Direcionamento de experiência (XT) em seu servidor e executar decisões na memória com latência próxima a zero, sem bloquear solicitações de rede para [!DNL Adobe Target]Rede de borda da.

[!DNL Adobe Target] O também oferece a flexibilidade de fornecer a experiência mais relevante e atualizada de suas campanhas de experimentação e personalização orientadas por aprendizado de máquina por meio de uma chamada de servidor em tempo real. Em outras palavras, quando o desempenho é mais importante, você pode optar por utilizar o [!UICONTROL decisão no dispositivo], mas quando a experiência mais relevante e atualizada for necessária, uma chamada de servidor poderá ser feita. Consulte [quando usar a decisão no dispositivo e na borda](../../sdk-guides/on-device-decisioning/supported-features.md) para saber mais sobre casos de uso que justificam o uso de um em detrimento do outro.

>[!NOTE]
>
>A decisão no dispositivo está disponível para implementações do lado do cliente e do lado do servidor. Este artigo descreve [!UICONTROL decisão no dispositivo] para o lado do servidor. Para obter informações sobre [!UICONTROL decisão no dispositivo] para obter informações sobre o cliente, consulte a documentação de implementação do cliente. [aqui](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## Como funciona?

Ao instalar e inicializar um [!DNL Adobe Target] SDK com [!UICONTROL decisão no dispositivo] habilitado, uma *artefato de regra* O é baixado e armazenado em cache localmente no servidor, a partir do Akamai CDN mais próximo ao servidor. Quando uma solicitação para recuperar um [!DNL Adobe Target] A experiência do é tomada no aplicativo do lado do servidor, a decisão sobre qual conteúdo retornar é tomada na memória, com base nos metadados codificados no artefato de regra em cache, que define todas as [!UICONTROL decisão no dispositivo] Atividades A/B e XT.

O diagrama a seguir mostra as [!UICONTROL decisão no dispositivo] arquitetura. Clique em para expandir a imagem.

(Clique na imagem para expandir até a largura total.)

![Diagrama da arquitetura de decisão no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "Diagrama da arquitetura de decisão no dispositivo"){zoom=&quot;yes&quot;}

## Quais são os benefícios?

* **Fornecer decisões de latência quase zero.** O particionamento e a decisão são executados na memória e no dispositivo para evitar o bloqueio de solicitações de rede.
* **Melhorar o desempenho dos aplicativos.** Execute experimentos e forneça personalização aos seus clientes e usuários sem comprometer as experiências do usuário final.
* **Melhore A Pontuação De Qualidade Do Site Do Google.** Com as decisões acontecendo na memória e no lado do servidor, melhore a pontuação da Qualidade do site do Google de seu negócio online para torná-lo mais detectável pelos consumidores.
* **Aprenda com a análise em tempo real.** Obtenha insights sobre o desempenho da sua atividade em tempo real por meio do [!DNL Adobe Target] ou relatórios do A4T, permitindo que você dinamize sua estratégia em momentos críticos.

## Funcionalidade compatível

### Atividades

A decisão no dispositivo é compatível com os seguintes tipos de atividades criadas pelo [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html):

* [!UICONTROL Teste A/B]
* [!UICONTROL Direcionamento de experiência] (XT)

### Método de Alocação

A decisão no dispositivo é compatível com o seguinte método de alocação:

* Manual

### Direcionamento de público

A decisão no dispositivo é compatível com as seguintes regras de público-alvo:

| Regra de público-alvo | Decisão no dispositivo |
| --- | --- |
| [Geografia](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Sim<P>Ao usar a decisão no dispositivo, os seguintes atributos geográficos são compatíveis:<ul><li>País/Região</li><li>Cidade</li><li>Latitude</li><li>Longitude</li></ul> |
| [Rede](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Não |
| [Móvel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Não |
| [Parâmetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Sim |
| [Sistema operacional](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Sim |
| [Páginas do site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Sim |
| [Navegador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Sim |
| [Perfil do visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Não |
| [Fontes de Tráfego](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Não |
| [Intervalo de tempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Sim |
| [Públicos do Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Públicos-alvo da Adobe Audience Manager, Adobe Analytics e Adobe Experience Manager | Não |

## Como provisionar meu cliente para usar [!UICONTROL decisão no dispositivo]?

A decisão no dispositivo está disponível para todos [!DNL Adobe Target] clientes que usam [!DNL Adobe Target] SDKs do lado do servidor. Para ativar esse recurso, navegue até **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Detalhes da conta]** no [!DNL Adobe Target] e habilite a **[!UICONTROL Decisão no dispositivo]** alternar.

>[!NOTE]
>
>Você precisa ter um Administrador ou Aprovador *função do usuário* para ativar ou desativar o [!UICONTROL Decisão no dispositivo] alternar.

![imagem alt](assets/asset-odd-toggle.png)

Depois de ativar a opção On-Device Decisioning, [!DNL Adobe Target] começará a gerar e propagar *artefatos de regra* para o seu cliente.

>[!NOTE]
>
>Certifique-se de ativar o botão de alternância antes de inicializar o [!DNL Adobe Target] SDK a ser usado [!UICONTROL decisão no dispositivo]. Os artefatos da regra precisarão primeiro ser gerados e propagados para os CDNs do Akamai para que o [!UICONTROL decisão no dispositivo] para trabalhar.

### Incluir todos os existentes [!UICONTROL decisão no dispositivo] atividades qualificadas no alternador de artefato

Alternar este item **em** quando você quiser tudo em tempo real [!DNL Target] atividades qualificadas para [!UICONTROL decisão no dispositivo] para ser incluído automaticamente no artefato.

Deixando esta alternância **desligado** significa que será necessário recriar e ativar qualquer [!UICONTROL decisão no dispositivo] para que sejam incluídas no artefato de regras gerado.

## Como faço para saber se uma atividade está [!UICONTROL decisão no dispositivo] capaz?

Depois de criar uma atividade, um rótulo chamado **[!UICONTROL Método de decisão]**, visível na página de detalhes da atividade, indica se a atividade é [!UICONTROL decisão no dispositivo] capaz.

![imagem alt](assets/asset-odd9.png)

Você também pode ver todas as atividades [!UICONTROL decisão no dispositivo] capaz no **[!UICONTROL Atividades]** adicionando a coluna **[!UICONTROL Método de decisão]** à lista de atividades.

![imagem alt](assets/asset-odd7.png)

>[!NOTE]
>
>Depois de criar e ativar uma atividade que é [!UICONTROL decisão no dispositivo] Compatível, pode levar de 5 a 10 minutos antes de ser incluído no artefato de regras que é gerado e propagado para os PoPs do Akamai CDN.

## Qual é o resumo das etapas que preciso seguir para garantir minha [!UICONTROL decisão no dispositivo] As atividades do são entregues com sucesso através do [!DNL Adobe Target]SDK do lado do servidor do?

1. Acesse o [!DNL Adobe Target] e navegue até **[!UICONTROL Administração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Detalhes da conta]** para habilitar o **[!UICONTROL Decisão no dispositivo]** alternar.
1. Ativar o **[!UICONTROL Incluir todos os existentes [!UICONTROL decisão no dispositivo] atividades qualificadas no artefato]** alternar.
1. Crie e ative um tipo de atividade compatível com o [!UICONTROL decisão no dispositivo]e verificar se o **[!UICONTROL Método de decisão]** é **[!UICONTROL Decisão no dispositivo]** para essa atividade.
1. Instalar e inicializar o [Node.js](../../node-js/overview.md) ou [Java](../../java/overview.md) SDK com `decisioningMethod = on-device`.
1. Implementar `getOffers()` ou `getAttributes()` no código para recuperar uma experiência no dispositivo.
1. Implante seu código.

Para obter exemplos demonstrando como começar a usar as etapas 1 a 3 acima, consulte [Introdução](../getting-started/getting-started.md) seção.


## Recursos adicionais

### Webinário: Personalize e teste em latência zero com decisões no dispositivo do [!DNL Adobe Target]

Mais do que nunca, os profissionais de marketing, proprietários de produtos e desenvolvedores estão sendo incumbidos de otimizar a experiência geral do cliente em sites, aplicativos e em todos os outros lugares onde eles se conectam com seus clientes. Várias ferramentas com silos de dados e implementações complicadas são inadequadas.

Neste webinário gravado, [!DNL Adobe Target] especialistas em produtos discutem como mover as decisões de otimização de experiência crítica no dispositivo para execução local com latência próxima de zero pode abrir portas para novos casos de uso interessantes e, ao mesmo tempo, melhorar o desempenho do site para seus clientes.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### Tutorial: decisão no dispositivo

[!DNL Adobe Target] [!UICONTROL decisão no dispositivo] permite a entrega de conteúdo com latência próxima a zero.

Este vídeo de 7 minutos:

* Descreve [!UICONTROL decisão no dispositivo]incluindo a sua comparação com outros métodos de [!DNL Target] implementação
* Demonstra como ativar [!UICONTROL decisão no dispositivo] no Target
* Examina uma amostra de atividade de compositor baseada em formulário que foi configurada com conteúdo JSON
* Mostra o exemplo de código SDK Node.JS contendo a configuração de chave necessária para [!UICONTROL decisão no dispositivo]
* Demonstra resultados em um navegador

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

Para obter mais vídeos e tutoriais, consulte a [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=pt-BR).

### Blog técnico do Adobe - Parte 1: Executar [!DNL Adobe Target] SDK do NodeJS para experimentação e personalização em plataformas de borda (Trabalhadores do Akamai Edge)

[Clique aqui para acessar a publicação do blog](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe Tech Blog — Parte 2: Execute o SDK NodeJS do [!DNL Adobe Target] para experimentação e personalização em plataformas de borda (AWS Lambda@Edge)

[Clique aqui para acessar a publicação do blog](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
