---
keywords: diagrama de sistema, cintilação, at.js, implementação, biblioteca javascript, js, atjs, $8
description: Conheça as  [!DNL Target]  funções da biblioteca JavaScript at.js, incluindo diagramas de sistema, que ajudam você a entender o fluxo de trabalho quando as páginas são carregadas.
title: Como funciona a biblioteca JavaScript at.js?
feature: at.js
exl-id: 9183797c-857b-4b7f-a573-6bb1d583f7b1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 74%

---

# Como a at.js funciona

Para implementar a [!DNL Adobe Target] no lado do cliente, você deve usar a biblioteca JavaScript at.js.

Em uma implementação no lado do cliente do [!DNL Adobe Target], o [!DNL Target] fornece as experiências associadas a uma atividade diretamente para o navegador do cliente. O navegador decide qual experiência será exibida e realiza a ação. Com uma implementação no lado do cliente, você pode usar um editor WYSIWYG, o [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) ou uma interface não visual, o [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para criar experiências de teste e personalização.

## O que é a at.js?

A at.js é a biblioteca de implementação para implementação no lado do cliente do [!DNL Adobe Target]. A biblioteca at.js melhora os tempos de carregamento de página de implementações da Web e fornece opções de implementações melhores para aplicativos de página única. A at.js é a biblioteca de implementação recomendada e é atualizada frequentemente com novos recursos. Recomendamos que todos os clientes implementem ou migrem para a   [última versão da at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

Para obter mais informações, consulte [Bibliotecas de JavaScript do Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#libraries).

No [!DNL Target]ilustrada abaixo, as seguintes soluções da Adobe Experience Cloud são implementadas: [!DNL Analytics], Target e [!DNL Audience Manager]. Além disso, as seguintes [!DNL Experience Cloud] os principais serviços estão implementados: [!DNL Adobe Experience Platform], [!UICONTROL Públicos-alvo], e [!UICONTROL Serviço de ID de visitante].

## Qual é a diferença entre os diagramas de fluxo de trabalho at.js 1 *x* e at.js 2.x tem fluxo de trabalho de diagramas?

Consulte [Atualização da at.js 1.x para at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md) para obter mais informações sobre as diferenças introduzidas na versão 2.0 em relação à 1.*x*.

A partir de uma exibição de alto nível, há algumas diferenças entre as duas versões:

* A at.js 2.x não tem um conceito global de solicitação de mbox, mas sim uma solicitação de carregamento de página. Uma solicitação de carregamento de página pode ser visualizada como uma solicitação para recuperar o conteúdo que deve ser aplicado no carregamento da página inicial do site.
* A at.js 2.x gerencia conceitos chamados [!UICONTROL Visualizações], que são usados para Aplicativos de página única (SPA). at.js 1.*x* não está ciente deste conceito.

## diagramas at.js 2.x

Os diagramas a seguir ajudam a entender o fluxo de trabalho da at.js 2.x com [!UICONTROL Visualizações] e como isso melhora a integração do SPA. Para obter uma mais detalhes sobre os conceitos usados na Noções básicas sobre o funcionamento da at.js 2.x, consulte [Implementação de aplicativos de página única](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Clique na imagem para expandir até a largura total.)

![Fluxo do Target com a at.js 2.x](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "Fluxo do Target com a at.js 2.x"){zoom=&quot;yes&quot;}

| Etapa | Detalhes |
| --- | --- |
| 1 | A chamada retorna o [!UICONTROL ID do Experience Cloud] se o usuário estiver autenticado; outra chamada sincroniza a ID do cliente. |
| 2 | A biblioteca at.js é carregada de modo síncrono e oculta o corpo do documento.<br />O at.js também pode ser carregado de forma assíncrona com uma opção que oculta previamente o trecho implementado na página. |
| 3 | Uma solicitação de carregamento de página é feita, incluindo todos os parâmetros configurados (MCID, SDID e ID do cliente). |
| 4 | Os scripts de perfil executam e, em seguida, fazem o feed na [!UICONTROL Loja de perfis]. O pontosolicita novamente públicos qualificados da [!UICONTROL Biblioteca de público-alvo] (por exemplo, públicos-alvo compartilhados de [!DNL Adobe Analytics], [!DNL Audience Manager], etc.).<br />[!UICONTROL Os atributos do cliente são enviados à Loja de perfis em um processo em lote.] |
| 5 | Com base nos parâmetros de solicitação de URL e dados de perfil, [!DNL Target] decide quais atividades e experiências retornarão ao visitante para a página atual e para as exibições futuras. |
| 6 | O conteúdo direcionado é enviado de volta para a página, incluindo, opcionalmente, valores de perfil para personalização adicional.<br />O conteúdo direcionado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.<br />Conteúdo direcionado para exibições que são mostradas como resultado das ações do usuário em um SPA, que é armazenado em cache no navegador para que possa ser aplicado instantaneamente, sem uma chamada de servidor adicional, quando as exibições forem acionadas por meio do `triggerView()`. |
| 7 | Os dados do Analytics são enviados para [!UICONTROL Coleta de dados] servidores. |
| 8 | Os dados direcionados correspondem aos dados do Analytics por meio da SDID e são processados na [!DNL Analytics] armazenamento de relatórios.<br />[!DNL Analytics]Os dados podem ser exibidos no [!DNL Analytics] e no [!DNL Target] pelos relatórios do  (A4T). |

Agora, onde quer `triggerView()` que seja implementada em seu SPA, as Exibições e as ações são recuperadas do cache e mostradas ao usuário, sem uma chamada de servidor. `triggerView()` também faz uma solicitação de notificações ao backend [!DNL Target] para aumentar e registrar contagens de impressão. Para obter mais informações sobre o at.js para SPAs com Exibições, consulte [Implementação de aplicativos de página única](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Clique na imagem para expandir até a largura total.)

![Fluxo do Target com a at.js 2.x triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Fluxo do Target com a at.js 2.x triggerView"){zoom=&quot;yes&quot;}

| Etapa | Detalhes |
| --- | --- |
| 1 | `triggerView()`[!UICONTROL  é chamado no SPA para renderizar a Exibição e aplicar ações para modificar elementos visuais.] |
| 2 | O conteúdo direcionado para a exibição é lido do cache. |
| 3 | O conteúdo direcionado é revelado o mais rápido possível sem oscilação do conteúdo padrão. |
| 4 | A solicitação de notificação é enviada para a [!DNL Target] Loja de perfil para contar o visitante nas métricas de atividade e incremento. |
| 5 | [!DNL Analytics] dados enviados para o [!UICONTROL Servidores de coleta de dados]. |
| 6 | Os dados do [!DNL Target] são correspondidos aos dados do [!DNL Analytics] pela SDID, e processados no armazenamento de relatório do [!DNL Analytics]. [!DNL Analytics] os dados podem ser exibidos em [!DNL Analytics] e [!DNL Target] pelos relatórios do A4T. |

### Vídeo - diagrama de arquitetura da at.js 2.x

A at.js 2.x aprimora o suporte do Adobe Target para SPAs e integra-se com outras soluções da Experience Cloud. Este vídeo explica como tudo se une.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Consulte [Noções básicas sobre o funcionamento da at.js 2.x](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html) para obter mais informações.

## diagrama do at.js 1.x

Os diagramas a seguir ajudam a entender o fluxo de trabalho da at.js 1.x.

(Clique na imagem para expandir até a largura total.)

![Fluxo do Target com a at.js 1.x](/help/dev/implement/client-side/assets/target-flow.png "Fluxo do Target com a at.js 1.x"){zoom=&quot;yes&quot;}

| Etapa | Descrição | Chama | Descrição |
|--- |--- |--- |--- |
| 1 | A chamada retornará a Experience Cloud ID (MCID) se o usuário estiver autenticado; outra chamada sincroniza a ID do cliente. | 2 | A biblioteca at.js é carregada de modo síncrono e oculta o corpo do documento. |
| 3 | Uma solicitação mbox global é feita, incluindo todos os parâmetros configurados, MCID, SDID e ID do cliente (opcional). | 4 | Os scripts de perfil executam e, em seguida, fazem o feed na Loja do perfil. A Loja solicita públicos qualificados da Biblioteca de público-alvo (por exemplo, públicos-alvo compartilhados de Adobe Analytics, Audience Manager, etc.).<br />Os atributos do cliente são enviados à Loja de perfis em um processo em lote. |
| 5 | Com base no URL, nos parâmetros mbox e nos dados do perfil, o [!DNL Target] decide quais atividades e experiências são retornadas ao visitante. | 6 | O conteúdo direcionado é retornado à página, opcionalmente incluindo os valores de perfil para personalização adicional.<br />A experiência é revelada o mais rápido possível sem cintilação do conteúdo padrão. |
| 7 | Os dados do Analytics são enviados ao servidores de Coleção de dados. | 8 | Os dados do Target são correspondidos aos dados do Analytics pela SDID, e processados no armazenamento de relatório do Analytics.Em seguida, os dados do <br />Analytics podem ser visualizados no Analytics e no [!DNL Target] pelos relatórios do [!UICONTROL Analytics for Target] (A4T). |

### Vídeo - Horário comercial: dicas e visão geral da at.js (26 de junho de 2019)

Este vídeo é uma gravação de &quot;No expediente&quot;, uma iniciativa da [!UICONTROL Atendimento ao cliente Adobe] equipe.

* Os benefícios da utilização da at.js
* As configurações da at.js
* O tratamento de cintilação
* Depuração do at.js
* Problemas conhecidos
* Perguntas frequentes

>[!VIDEO](https://video.tv.adobe.com/v/27959/?quality=12)

## Como o at.js renderiza ofertas com conteúdo HTML

Ao renderizar ofertas com conteúdo HTML, o at.js aplica o seguinte algoritmo:

1. As imagens são pré-carregadas (se houver tags do `<img>` no conteúdo HTML).

1. O conteúdo HTML é anexado ao nó DOM.

1. Os scripts embutidos são executados (código delimitado nas tags do `<script>`).

1. Os scripts remotos são carregados de forma assíncrona e executados (tags do `<script>` com `src` atributos).

Observações importantes:

* O at.js não oferece garantia na ordem de execução dos scripts remotos, pois são carregados de forma assíncrona.
* Os scripts embutidos não devem ter dependências nos scripts remotos, pois são carregados e executados posteriormente.
