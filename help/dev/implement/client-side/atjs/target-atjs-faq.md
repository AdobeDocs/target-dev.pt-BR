---
keywords: perguntas frequentes da at.js, perguntas frequentes da at.js, perguntas frequentes, cintilação, carregador, carregador de página, domínio cruzado, tamanho do arquivo, tamanho do arquivo, domínio x, at.js e mbox.js, somente x, domínio cruzado, safari, aplicativo de página única, seletores ausentes, seletores, aplicativo de página única, tt.omtrdc.net, spa, Adobe Experience Manager, AEM, endereço ip, httponly, HttpOnly, seguro, ip, cookie domínio
description: Leia respostas das perguntas frequentes sobre o [!DNL Adobe Target] Biblioteca JavaScript at.js.
title: Quais são as perguntas e respostas comuns sobre a at.js?
feature: at.js
exl-id: 362ccc5b-8731-46c0-bc52-3e55c273e216
source-git-commit: 448c43c0c10e22ad054f4ee98bfc282f8c96cdcb
workflow-type: tm+mt
source-wordcount: '2938'
ht-degree: 66%

---

# Perguntas frequentes sobre at.js

Respostas às perguntas frequentes sobre a biblioteca de JavaScript at.js do [!DNL Adobe Target].

## Quais as vantagens de usar a at.js versus a mbox.js?

A biblioteca da at.js substitui a mbox.js. A biblioteca mbox.js não é mais suportada. No entanto, para a maioria das pessoas, a at.js fornece vantagens em relação à mbox.js.

Entre outros benefícios, a at.js melhora os tempos de carregamento de página de implementações da Web, melhora a segurança e fornece opções de implementações melhores para aplicativos de página única.

O diagrama a seguir ilustra o desempenho do carregamento de página usando a mbox.js versus a at.js.

(Clique na imagem para expandir até a largura total.)

![Diagrama de desempenho da página que compara a mbox.js com a at.js](/help/dev/implement/client-side/atjs/assets/atjs_versus_mboxjs.png "Diagrama de desempenho da página que compara a mbox.js com a at.js"){zoom=&quot;yes&quot;}

Como ilustrado acima, ao usar a mbox.js, o conteúdo da página não inicia o carregamento até que a chamada do [!DNL Target] seja concluída. Usando a at.js, o conteúdo da página inicia o carregamento ao iniciar a chamada do [!DNL Target] e não espera até que ela seja concluída.

## Qual é o impacto da at.js e da mbox.js nos tempos de carregamento de página?

Muitos clientes e consultores querem saber o impacto da at.js e da mbox.js nos tempos de carregamento de página, especialmente no contexto de usuários novos e recorrentes. Infelizmente, é difícil medir e fornecer números concretos sobre como a at.js ou a mbox.js influenciam o tempo de carregamento de página devido à implementação de cada cliente.

No entanto, se a API de visitante estiver presente na página, [!DNL Target] O pode entender melhor como a at.js e a mbox.js influenciam o tempo de carregamento de página.

>[!NOTE]
>
>A API do visitante e a at.js ou mbox.js têm um impacto no tempo de carregamento de página somente quando você está usando a mbox global (por causa da técnica de ocultação do corpo). As mboxes regionais não são afetadas pela integração da API do visitante.

As seções a seguir descrevem a sequência de ações para visitantes novos e recorrentes:

### Novos visitantes

1. A API do visitante é carregada, analisada e executada.
1. A at.js / mbox.js é carregada, analisada e executada.
1. Se a criação automática da mbox global estiver acionada, a biblioteca JavaScript do [!DNL Target]:

   * Iniciará o objeto do visitante.
   * A variável [!DNL Target] A biblioteca do tenta recuperar os dados de ID de visitante do Experience Cloud.
   * Como esse é um novo visitante, a API de visitante irá disparar uma solicitação de domínio cruzado para demdex.net.
   * Depois que os dados de ID de visitante do Experience Cloud forem recuperados, uma solicitação para [!DNL Target] foi acionado.

### Visitantes que retornam

1. A API do visitante é carregada, analisada e executada.
1. A at.js / mbox.js é carregada, analisada e executada.
1. Se a criação automática da mbox global estiver acionada, a biblioteca JavaScript do [!DNL Target]:

   * Iniciará o objeto do visitante.
   * A variável [!DNL Target] A biblioteca do tenta recuperar os dados de ID de visitante do Experience Cloud.
   * A API de visitante recuperará os dados dos cookies.
   * Depois que os dados de ID de visitante do Experience Cloud forem recuperados, uma solicitação para [!DNL Target] foi acionado.

>[!NOTE]
>
>Para novos visitantes, quando a API de visitante estiver presente, [!DNL Target] precisa transmitir as informações várias vezes para garantir que [!DNL Target] contêm dados de ID de visitante do Experience Cloud. Para os visitantes recorrentes, o [!DNL Target] transmitirá as informações apenas para o [!DNL Target] recuperar o conteúdo personalizado.

## Por que parece que vejo tempos de resposta mais lentos após a atualização de uma versão anterior da at.js para a versão 1.0.0?

A at.js versão 1.0.0 e posteriores acionam todas as solicitações paralelamente. As versões anteriores executam as solicitações sequencialmente, o que significa que elas são colocadas em uma fila e o [!DNL Target] aguarda até que a primeira seja concluída antes de passar para a próxima solicitação.

A forma como as versões anteriores da at.js executam as solicitações é susceptível ao chamado &quot;bloqueio do topo da linha&quot;. Em at.js 1.0.0 e posterior, [!DNL Target] alternado para execução de solicitação paralela.

Por exemplo, se você verificar a cascata da guia de rede para a at.js 0.9.1, verá que a próxima [!DNL Target] A solicitação do não é iniciada até que a anterior tenha terminado. Isso não ocorre com a at.js 1.0.0 e posteriores, pois nestas versões as solicitações são iniciadas basicamente ao mesmo tempo.

Da perspectiva de tempo de resposta, matematicamente, essa sequência pode ser resumida assim

<ul class="simplelist"> 
 <li> at.js 0.9.1: tempo de resposta de todos [!DNL Target] solicitações = soma do tempo de resposta das solicitações </li> 
 <li> at.js 1.0.0 e posteriores: tempo de resposta de todos [!DNL Target] solicitações = tempo máximo de resposta das solicitações </li> 
</ul>

A versão 1.0.0 da biblioteca at.js conclui as solicitações mais rapidamente. Além disso, as solicitações da at.js são assíncronas, [!DNL Target] O não bloqueia a renderização da página. Mesmo que as solicitações levem alguns segundos para serem concluídas, você ainda verá a página renderizada, mas apenas algumas partes da página ficarão em branco até que o [!DNL Target] receba uma resposta da borda do [!DNL Target].

## Posso carregar a biblioteca do [!DNL Target] de forma assíncrona?

A versão 1.0.0 da at.js permite carregar a biblioteca do [!DNL Target] de forma assíncrona.

Para carregar a at.js de forma assíncrona:

* A abordagem recomendada é por meio de tags na Adobe Experience Platform.
* Também é possível carregar a at.js de forma assíncrona, adicionando o atributo async à tag do script que carrega a at.js. Use algo assim:

  ```
  <script src="<URL to at.js>" async></script>
  ```

* Você também pode carregar a at.js de forma assíncrona usando este código:

  ```
  var script = document.createElement('script'); 
  script.async = true; 
  script.src = "<URL to at.js>"; 
  document.head.appendChild(script);
  ```

Carregar a at.js de forma assíncrona é uma ótima maneira de evitar o bloqueio de renderização do navegador. No entanto, essa técnica pode levar à cintilação na página da Web.

Você pode evitar a cintilação usando um snippet de pré-ocultação que oculta a página (ou partes especificadas), exibindo-a após o carregamento completo da at.js e da solicitação global. O trecho deve ser adicionado antes de carregar a at.js.

Se estiver implantando a at.js por meio de uma interface [!UICONTROL Adobe Experience Platform] implementação, certifique-se de incluir o trecho pré-ocultação diretamente nas páginas, antes da opção Implementar [!DNL Target] usar [!UICONTROL Adobe Experience Platform] Incorporar código.

Se estiver implantando a at.js por meio de uma implementação DTM síncrona, o snippet de pré-ocultação pode ser adicionado por uma regra de Carregamento de página acionada na parte superior da página.

Para obter mais informações, consulte [Como o at.js gerencia a cintilação](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

## A at.js é compatível com a integração do [!DNL Adobe Experience Manager] (Experience Manager)?

[!DNL Adobe Experience Manager] O 6.2 com FP-11577 (ou posterior) agora é compatível com implementações da at.js com o [!UICONTROL Adobe Target Cloud Service] integração.

## Como posso evitar a cintilação de carregamento de página usando a at.js?

[!DNL Target] O fornece várias maneiras de evitar a cintilação de carregamento de página. Para obter mais informações, consulte [Como evitar a cintilação com o at.js](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

## Qual é o tamanho do arquivo da at.js?

O arquivo da at.js tem aproximadamente 109 KB quando baixado. No entanto, como a maioria dos servidores compacta automaticamente os arquivos para diminuir os tamanhos, a at.js fica com aproximadamente 34 KB quando é compactada (usando GZIP ou outro método) em seu servidor e é carregada conforme os usuários visitam o site. As configurações de compactação no servidor onde a at.js foi instalada determinam o seu tamanho compactado real.

## Por que o at.js é maior que o mbox.js?

As implementações da at.js usam uma única biblioteca ( at.js), enquanto as implementações de mbox.js na verdade usam duas bibliotecas ( mbox.js e target.js). Por isso, uma comparação mais justa seria de at.js versus mbox.js *e* `target.js`. Comparação entre os tamanhos gzipped das duas versões, a at.js versão 1.2 tem 34 KB e a mbox.js versão 63 tem 26.2 KB. ``

A at.js é maior, pois realiza muito mais análise de DOM em comparação à mbox.js. Isso é necessário porque a at.js recebe dados &quot;brutos&quot; na resposta JSON e precisa entender isso. A mbox.js usava o `document.write()` e todas as análises eram realizadas pelo navegador.

Embora o tamanho do arquivo seja maior, nossos testes indicam que as páginas carregam mais rápido com a at.js versus a mbox.js. Além disso, em questão de segurança, a at.js é superior, pois não carrega arquivos adicionais dinamicamente ou usa o `document.write`.

## A at.js contém um jQuery? Posso remover essa parte da at.js já que tenho o jQuery no meu site?

Atualmente, a at.js usa partes do jQuery e, consequentemente, você verá a notificação de licença do MIT na parte superior da at.js. O jQuery não está exposto e não interfere na biblioteca do jQuery que já existe na sua página, que pode ser de uma versão diferente. A remoção do código do jQuery na at.js não é suportado.

## A at.js é compatível com o Safari e com o domínio cruzado definido como somente x?

Não, se o domínio cruzado estiver definido como somente x e o Safari tiver cookies de terceiros desativados, a mbox.js e a at.js vão definir um cookie desativado e nenhuma solicitação de mbox será executada para o domínio desse cliente específico.

Para auxiliar os visitantes do Safari, um Domínio X melhor seria &quot;desativado&quot; (define apenas um cookie primário) ou &quot;ativado&quot; (define apenas um cookie primário no Safari, enquanto define cookies primários e de terceiros em outros navegadores).

## Posso usar o Target [!UICONTROL Visual Experience Composer] (VEC) nos meus aplicativos de página única?

Sim, você pode usar o VEC para aplicativos de página única se utilizar a at.js 2.x. Para obter mais informações, consulte [Aplicativo de página única (SPA) no Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/spa-visual-experience-composer.html).

## Posso usar o depurador da Adobe Experience Cloud com implementações da at.js?

Sim. Também é possível usar a mboxTrace para fins de depuração ou as Ferramentas de desenvolvedor do navegador para inspecionar as solicitações da rede, filtrando como &quot;mbox&quot;, a fim de isolar as chamadas da mbox.

## Posso usar caracteres especiais em nomes de mbox com a at.js?

Sim, o mesmo que ocorre com a mbox.js.

## Por que as mboxes não estão sendo acionadas nas minhas páginas da Web?

Os [!DNL Target] clientes do, às vezes, usam instâncias baseadas em nuvem com o [!DNL Target] para testes ou fins de prova de conceito simples. Esses domínios e muitos outros fazem parte da [Lista de sufixos públicos](https://publicsuffix.org/list/public_suffix_list.dat).

Se estiver usando esses domínios, os navegadores modernos não salvarão os cookies, a menos que você personalize a configuração de `cookieDomain` usando targetGlobalSettings(). Para obter mais informações, consulte [Usar instâncias baseadas em nuvem com o [!DNL Target]](/help/dev/implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md).

## Os endereços IP podem ser usados como o domínio de cookie ao usar a at.js?

Sim, se estiver usando [a at.js versão 1.2 ou posterior](/help/dev/implement/client-side/atjs/target-atjs-versions.md). No entanto, a Adobe recomenda que você se mantenha atualizado com a versão mais recente.

>[!NOTE]
>
>Os seguintes exemplos não são necessários se estiver usando a at.js versão 1.2 ou posterior.

Dependendo de como você usa [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md), talvez seja necessário fazer modificações adicionais no código depois de baixar a at.js. Por exemplo, se você precisava de configurações ligeiramente diferentes para as implementações do [!DNL Target] em vários sites e não pode defini-las dinamicamente usando o JavaScript personalizado, faça essas personalizações manualmente depois de baixar o arquivo e antes de fazer upload para os respectivos sites.

Os exemplos a seguir permitem usar a função `targetGlobalSettings()` at.js para inserir um trecho de código para suportar endereços IP:

Este exemplo é para um único endereço IP:

```
if (window.location.hostname === '123.456.78.9') { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

Este exemplo é para uma série de endereços IP:

```
if (/^123\.456\.78\..*/g.test(window.location.hostname)) { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

## Por que vejo mensagens de aviso, como &quot;ações com seletores ausentes&quot;? 

Essas mensagens não estão relacionadas à funcionalidade da at.js. A biblioteca at.js tenta informar tudo que não pode ser encontrado no DOM.

Caso veja esta mensagem de aviso, as possíveis causas raiz podem ser as seguintes:

* A página está sendo criada dinamicamente e a at.js não consegue encontrar o elemento.
* A página está sendo criada lentamente (devido a uma rede lenta) e a at.js não consegue encontrar o seletor no DOM.
* A estrutura de página em que a atividade está sendo executada foi alterada. Se você reabrir a atividade no Visual Experience Composer (VEC), deverá receber uma mensagem de aviso. Atualize a atividade para que todos os elementos necessários possam ser encontrados.
* A página subjacente faz parte de um Aplicativo de página única (SPA) ou a página contém elementos que são exibidos mais abaixo e o &quot;mecanismo de buscas do seletor&quot; da at.js não consegue encontrá-los. Aumentar o `selectorsPollingTimeout` pode ajudar. Para obter mais informações, consulte [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
* Todas as métricas de rastreamento de cliques tentam se adicionar a cada página, independentemente do URL em que a métrica foi configurada. Embora inofensiva, essa situação faz com que muitas dessas mensagens sejam exibidas.

  Para obter melhores resultados, baixe e use o [versão mais recente da at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md). Para obter mais informações sobre como baixar a at.js, consulte a [Baixe a at.js usando o [!DNL Target] interface](how-to-deployatjs/implement-target-without-a-tag-manager.md#download-atjs-using-the-target-interface) na seção [*Como implantar a at.js* > *Implementar [!DNL Target] sem um gerenciador de tags*](how-to-deployatjs/implement-target-without-a-tag-manager.md) artigo.

## O que é o domínio tt.omtrdc.net para o qual as chamadas de servidor do [!DNL Target] são direcionadas?

tt.omtrdc.net é o nome de domínio para a rede Adobe EDGE, usada para receber todas as chamadas de servidor para [!DNL Target].

## Por que a at.js nem sempre usa os sinalizadores de cookies HttpOnly e Seguro?

HttpOnly pode ser definido somente pelo código do lado do servidor. [!DNL Target]Os cookies do, como mbox, são criados e salvos pelo código JavaScript, para que o não possa usar o sinalizador de [!DNL Target] cookies HttpOnly. O [!DNL Target] usa o conjunto HttpOnly para cookies de terceiros definidos pelo lado do servidor quando o domínio cruzado está ativado.

Seguro pode ser definido somente por JavaScript, quando a página tiver sido carregada por HTTPS. Se a página inicialmente carregar por meio de HTTP, o JavaScript não poderá definir esse sinalizador. Além disso, se o sinalizador Seguro for usado, o cookie estará disponível somente nas páginas HTTPS. Para páginas carregadas por HTTPS, o [!DNL Target] define os atributos Secure e SameSite=None.

Para garantir que o [!DNL Target] possa rastrear os usuários adequadamente e, como os cookies são gerados no lado do cliente, o [!DNL Target] não usa nenhum desses sinalizadores, exceto nas situações mencionadas acima.

## Como a at.js lida com problemas de segurança como ataques XSS e MITM?

A comunicação com a rede do Adobe Edge, habilitada pela at.js, acontece somente por HTTPS, desde que a `secureOnly` está definida como true na função targetGlobalSettings() ([targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)), caso contrário, a at.js poderá alternar entre HTTP e HTTPS com base no protocolo da página.

Os seguintes cabeçalhos são aplicados por padrão:
* HTTP Strict Transport Security (HSTS)
* Proteção X-XSS
* X Opções de Tipo de Conteúdo
* Referenciador-Política

Todos os cabeçalhos já usados nas páginas do cliente podem ser aplicados. Uma maneira comum de fazer isso é por meio da &quot;Autorização de cabeçalho de solicitação HTTP&quot;. O Atendimento ao cliente do Adobe pode fornecer mais recomendações sobre os melhores métodos e práticas.

Além disso, as solicitações à Rede Adobe Edge são públicas (já que são projetadas para serem feitas a partir dos navegadores dos visitantes) e não contêm detalhes visíveis do visitante (contêm apenas uma ID do visitante). Essas solicitações fornecem experiências aos visitantes e contêm detalhes sobre o que um visitante deve ver na página.

Observe que para tokens de resposta e IDs de sessão transmitidos nessas solicitações:

* Eles rastreiam sessões de comunicação
* Eles são compostos de caracteres aleatórios
* As IDs de sessão são válidas por 30 minutos
* Os tokens de resposta podem ser desativados ([Tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html))
* Eles são úteis somente no ambiente de soluções Adobe.

Espera-se que o `Access-Control-Allow-Origin` cabeçalho com valor &quot;*&quot; nas solicitações at.js, como são públicas, a autenticação não é necessária e a Rede Adobe Edge precisa ser acessada de qualquer domínio por meio de chamadas JavaScript.

No entanto, a Política de segurança de conteúdo (CSP) precisa ser aplicada na página. Para obter mais informações sobre os requisitos da CSP para a at.js, consulte [Política de segurança de conteúdo](/help/dev/before-implement/privacy/content-security-policy.md) e [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Com que frequência a at.js dispara uma solicitação de rede? 

O [!DNL Target] executa todas as suas decisões no lado do servidor. Isso significa que a at.js dispara uma solicitação de rede sempre que a página é recarregada ou uma API pública da at.js é chamada.

## Na melhor das hipóteses, podemos esperar que o usuário não tenha nenhum efeito visível no carregamento da página relacionado à ocultação, substituição e exibição de conteúdo?

A at.js tenta evitar pré-ocultar o HTML BODY ou outros elementos DOM por um longo período de tempo, mas isso depende das condições da rede e da configuração da atividade. O at.js fornece [configurações](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) que você pode usar para personalizar o estilo CSS de ocultação do BODY, de modo que, em vez de esvaziar todo o HTML BODY, você possa pré-ocultar apenas algumas partes da página. A expectativa é que essas partes contenham elementos DOM que precisam ser &quot;personalizados&quot;.

## Qual é a sequência de eventos em um cenário médio em que um usuário se qualifica para uma atividade? 

A solicitação da at.js é uma `XMLHttpRequest` assíncrona, para a execução das seguintes etapas:

1. A página é carregada.
1. A at.js pré-oculta o HTML BODY. Há uma configuração para pré-ocultar um determinado contêiner em vez do HTML BODY.
1. A solicitação da at.js é disparada.
1. Depois que a resposta do [!DNL Target] é recebida, o [!DNL Target] extrai os seletores de CSS.
1. Usando seletores CSS, o [!DNL Target] cria tags STYLE para pré-ocultar os elementos DOM que serão personalizados.
1. O HTML BODY que pré-oculta o STYLE é removido.
1. O [!DNL Target] inicia a pesquisa de elementos DOM.
1. Se um elemento DOM for encontrado, o [!DNL Target] aplicará as alterações do DOM e o STYLE que está pré-ocultando elementos será removido.
1. Se os elementos DOM não forem encontrados, um tempo limite global volta a exibir os elementos para evitar uma página interrompida.

## Com que frequência o conteúdo da página é totalmente carregado e visível quando a at.js finalmente exibe o elemento que a atividade está alterando?

Considerando o cenário acima, com que frequência o conteúdo da página é totalmente carregado e visível quando a at.js finalmente exibe o elemento que a atividade está alterando? Em outras palavras, a página é totalmente visível, exceto pelo conteúdo da atividade, que é revelado um pouco após o restante do conteúdo.

A at.js não bloqueia a renderização da página. Um usuário pode notar algumas regiões em branco na página, que representam elementos a serem personalizados pelo [!DNL Target]. Se o conteúdo a ser aplicado não tiver muitos recursos remotos, como SCRIPTs ou IMGs, tudo deverá ser renderizado rapidamente.

## Como uma página totalmente armazenada em cache afetaria o cenário acima? Seria mais provável que o conteúdo da atividade se tornasse visível depois que o restante do conteúdo da página fosse carregado? 

Se uma página for armazenada em cache em um CDN próximo à localização do usuário, mas não próximo à borda do [!DNL Target], esse usuário poderá ver alguns atrasos. As bordas do [!DNL Target] são bem distribuídas em todo o mundo, portanto, isso não é um problema na maioria das vezes.

## É possível que uma imagem herói seja exibida e depois removida após um pequeno atraso? 

Considere o seguinte cenário:

O tempo limite do [!DNL Target] é de cinco segundos. Um usuário carrega uma página que possui uma atividade para personalizar uma imagem herói. A at.js envia a solicitação para determinar se há uma atividade a ser aplicada, mas não há resposta inicial. Suponha que o usuário veja o conteúdo regular da imagem principal, porque nenhuma resposta foi recebida do [!DNL Target] sobre alguma atividade associada. Após quatro segundos, o [!DNL Target] retorna uma resposta com o conteúdo da atividade.

Nessa etapa, seria possível mostrar a versão alternativa? Então, depois de quatro segundos, a imagem herói pode ser removida e o usuário pode perceber essa troca de imagem?

Inicialmente, o elemento DOM da imagem herói está oculto. Depois que uma resposta do [!DNL Target] é recebida, a at.js aplica as alterações do DOM, como a substituição do IMG e a exibição da imagem principal personalizada.

## Qual doctype HTML é exigido pela at.js?

A at.js exige o doctype HTML 5.

Esta sintaxe é:

`<!DOCTYPE html>`

O doctype HTML 5 garante que a página carregue no modo padrão. Ao carregar no modo quirks, algumas APIs de JS das quais a at.js depende são desativadas. O [!DNL Target] desativa a at.js no modo quirks.

## A at.js funciona em um ambiente de aplicativo Iônico.

Essa implementação nunca foi testada, pois a at.js não tinha a intenção de funcionar em um ambiente que não fosse da Web. [!DNL Adobe] recomenda que [SDKs para implementações móveis](/help/dev/implement/mobile/overview.md).
