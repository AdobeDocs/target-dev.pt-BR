---
keywords: lado do servidor, lado do servidor, sdk, sdks, no dispositivo, decisão, no dispositivo, ondevice, latência zero, latência, próximo a zero, node.js, lado do servidor3
description: Saiba como usar o [!UICONTROL on-device decisioning] para armazenar em cache suas [!DNL Target] atividades A/B e MVT no servidor para executar a decisão na memória com latência próxima de zero.
title: O que é a Decisão no dispositivo?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: ff0becf3fe3a6fd6694e13243b6a93b910316434
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 9%

---

# Visão geral da decisão no dispositivo

Os [!DNL Adobe Target] SDKs da próxima geração agora oferecem o [!UICONTROL on-device decisioning], que fornece a capacidade de armazenar em cache suas campanhas A/B e de Direcionamento de experiência (XT) em seu servidor e tomar decisões na memória com latência próxima de zero, sem bloquear solicitações de rede para o Edge Network do [!DNL Adobe Target].

O [!DNL Adobe Target] também oferece a flexibilidade de fornecer a experiência mais relevante e atualizada de suas campanhas de experimentação e personalização orientadas por aprendizado de máquina por meio de uma chamada de servidor em tempo real. Em outras palavras, quando o desempenho é mais importante, você pode optar por utilizar o [!UICONTROL on-device decisioning], mas quando a experiência mais relevante e atualizada for necessária, uma chamada de servidor poderá ser feita. Consulte [quando usar a decisão no dispositivo vs. a decisão na borda](../../sdk-guides/on-device-decisioning/supported-features.md) para saber mais sobre os casos de uso que garantem o uso de uma sobre a outra.

>[!NOTE]
>
>A decisão no dispositivo está disponível para implementações do lado do cliente e do lado do servidor. Este artigo descreve o [!UICONTROL on-device decisioning] para o lado do servidor. Para obter informações sobre [!UICONTROL on-device decisioning] para o lado do cliente, consulte a documentação de implementação do lado do cliente [aqui](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## Como funciona?

Quando você instala e inicializa um SDK do [!DNL Adobe Target] com o [!UICONTROL on-device decisioning] habilitado, um *artefato de regra* é baixado e armazenado em cache localmente no seu servidor, do CDN da Akamai mais próximo ao seu servidor. Quando uma solicitação para recuperar uma experiência do [!DNL Adobe Target] é feita no aplicativo do lado do servidor, a decisão sobre qual conteúdo retornar é tomada na memória, com base nos metadados codificados no artefato de regra em cache, que define todas as suas atividades A/B e XT do [!UICONTROL on-device decisioning].

O diagrama a seguir mostra a arquitetura [!UICONTROL on-device decisioning]. Clique em para expandir a imagem.

(Clique na imagem para expandir até a largura total.)

![Diagrama da arquitetura de decisão no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "Diagrama da arquitetura de decisão no dispositivo"){zoomable="yes"}

## Quais são os benefícios?

* **Fornecer decisões de latência quase zero.** O particionamento e a decisão são executados na memória e no dispositivo para evitar o bloqueio de solicitações de rede.
* **Aprimorar o desempenho do aplicativo.** Execute experimentos e forneça personalização aos seus clientes e usuários sem comprometer as experiências do usuário final.
* **Melhore A Pontuação De Qualidade Do Site Do Google.** Com as decisões ocorrendo na memória e no lado do servidor, melhore a pontuação da Qualidade do site do Google de sua empresa online para torná-la mais detectável pelos consumidores.
* **Aprenda com a análise em tempo real.** Obtenha insights do desempenho da sua atividade em tempo real através dos relatórios do [!DNL Adobe Target] ou do A4T, permitindo que você dinamize a sua estratégia em momentos críticos.

## Funcionalidade compatível

### Atividades

A decisão no dispositivo é compatível com os seguintes tipos de atividades criadas pelo [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=pt-BR):

* [!UICONTROL A/B Test]
* [!UICONTROL Experience Targeting] (XT)

### Método de Alocação

A decisão no dispositivo é compatível com o seguinte método de alocação:

* Manual

### Direcionamento de público

A decisão no dispositivo é compatível com as seguintes regras de público-alvo:

| Regra de público-alvo | Decisão no dispositivo |
| --- | --- |
| [Geografia](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=pt-BR) | Sim<P>Ao usar a decisão no dispositivo, os seguintes atributos geográficos são compatíveis:<ul><li>País/Região</li><li>Cidade</li><li>Latitude</li><li>Longitude</li></ul> |
| [Rede](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=pt-BR) | Não |
| [Móvel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=pt-BR) | Não |
| [Parâmetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=pt-BR) | Sim |
| [Sistema operacional](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=pt-BR) | Sim |
| [Páginas do site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=pt-BR) | Sim |
| [Navegador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=pt-BR) | Sim |
| [Perfil do visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=pt-BR) | Não |
| [Fontes de Tráfego](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=pt-BR) | Não |
| [Intervalo de tempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=pt-BR) | Sim |
| [Públicos-alvo do Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=pt-BR) (públicos-alvo do Adobe Audience Manager, Adobe Analytics e Adobe Experience Manager | Não |

## Como provisionar meu cliente para usar o [!UICONTROL on-device decisioning]?

A decisão no dispositivo está disponível para todos os clientes do [!DNL Adobe Target] que usam SDKs do lado do servidor do [!DNL Adobe Target]. Para habilitar este recurso, navegue até **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** na interface do usuário do [!DNL Adobe Target] e habilite a opção **[!UICONTROL On-Device Decisioning]**.

>[!NOTE]
>
>Você deve ter a *função de usuário* de Administrador ou Aprovador para habilitar ou desabilitar a [!UICONTROL On-Device Decisioning].

![alt imagem](assets/asset-odd-toggle.png)

Depois de habilitar a opção de Decisão no Dispositivo, o [!DNL Adobe Target] começará a gerar e propagar *artefatos de regras* para o seu cliente.

>[!NOTE]
>
>Habilite o botão de alternância antes de inicializar o SDK [!DNL Adobe Target] para usar [!UICONTROL on-device decisioning]. Os artefatos da regra precisarão primeiro ser gerados e propagados para os CDNs do Akamai para que o [!UICONTROL on-device decisioning] funcione.

### Incluir todas as [!UICONTROL on-device decisioning] atividades qualificadas existentes na alternância de artefato

Ative esta **em** quando desejar que todas as suas atividades [!DNL Target] ativas qualificadas para [!UICONTROL on-device decisioning] sejam incluídas automaticamente no artefato.

Sair desta **desativação** significa que você precisará recriar e ativar quaisquer atividades [!UICONTROL on-device decisioning] para que elas sejam incluídas no artefato de regras gerado.

## Como faço para saber se uma atividade tem capacidade para [!UICONTROL on-device decisioning]?

Após criar uma atividade, um rótulo chamado **[!UICONTROL Decisioning Method]**, visível na página de detalhes da atividade, indica se a atividade é compatível com [!UICONTROL on-device decisioning].

![alt imagem](assets/asset-odd9.png)

Você também pode ver todas as atividades [!UICONTROL on-device decisioning] compatíveis na página **[!UICONTROL Activities]** adicionando a coluna **[!UICONTROL Decisioning Method]** à lista de atividades.

![alt imagem](assets/asset-odd7.png)

>[!NOTE]
>
>Depois de criar e ativar uma atividade com capacidade para [!UICONTROL on-device decisioning], pode levar até 20 minutos para que ela seja incluída no artefato de regras gerado e propagado para os PoPs do Akamai CDN.

## Qual é o resumo das etapas que preciso seguir para garantir que minhas atividades do [!UICONTROL on-device decisioning] sejam entregues com êxito por meio do SDK do lado do servidor do [!DNL Adobe Target]?

1. Acesse a interface do usuário do [!DNL Adobe Target] e navegue até **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** para habilitar a alternância **[!UICONTROL On-Device Decisioning]**.
1. Habilite a alternância **[!UICONTROL Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact]**.
1. Crie e ative um tipo de atividade que seja suportado por [!UICONTROL on-device decisioning] e verifique se **[!UICONTROL Decisioning Method]** é **[!UICONTROL On-Device Decisioning]** para essa atividade.
1. Instale e inicialize o SDK [Node.js](../../node-js/overview.md) ou [Java](../../java/overview.md) com `decisioningMethod = on-device`.
1. Implemente `getOffers()` ou `getAttributes()` em seu código para recuperar uma experiência no dispositivo.
1. Implante seu código.

Para obter exemplos demonstrando como começar a usar as etapas 1 a 3 acima, consulte a seção [Introdução](../getting-started/getting-started.md).


## Recursos adicionais

### Webinário: Personalize e teste em latência zero com decisões no dispositivo do [!DNL Adobe Target]

Mais do que nunca, os profissionais de marketing, proprietários de produtos e desenvolvedores estão sendo incumbidos de otimizar a experiência geral do cliente em sites, aplicativos e em todos os outros lugares onde eles se conectam com seus clientes. Várias ferramentas com silos de dados e implementações complicadas são inadequadas.

Neste webinário gravado, os especialistas em produtos do [!DNL Adobe Target] discutem como mover as decisões de otimização de experiência crítica no dispositivo para execução local com latência próxima a zero pode abrir portas para novos casos de uso interessantes e, ao mesmo tempo, melhorar o desempenho do site para seus clientes.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### Tutorial: decisão no dispositivo

[!DNL Adobe Target] [!UICONTROL on-device decisioning] habilita a entrega de conteúdo de latência quase zero.

Este vídeo de 7 minutos:

* Descreve [!UICONTROL on-device decisioning], incluindo como ele se compara a outros métodos de implementação de [!DNL Target]
* Demonstra como habilitar [!UICONTROL on-device decisioning] no Target
* Examina uma amostra de atividade de compositor baseada em formulário que foi configurada com conteúdo JSON
* Mostra o exemplo de código SDK Node.JS contendo a configuração de chave necessária para [!UICONTROL on-device decisioning]
* Demonstra resultados em um navegador

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

Para obter mais vídeos e tutoriais, consulte os [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=pt-BR).

### Adobe Tech Blog — Parte 1: Execute o SDK NodeJS do [!DNL Adobe Target] para experimentação e personalização em plataformas de borda (Trabalhadores do Akamai Edge)

[Clique aqui para acessar a publicação do blog](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe Tech Blog — Parte 2: Execute o SDK NodeJS do [!DNL Adobe Target] para experimentação e personalização em plataformas de borda (AWS Lambda@Edge)

[Clique aqui para acessar a publicação do blog](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
