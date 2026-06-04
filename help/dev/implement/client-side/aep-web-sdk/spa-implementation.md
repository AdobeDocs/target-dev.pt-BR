---
title: Implementação de Aplicativo de Página Única para o [!DNL Adobe Experience Platform Web SDK]
description: Saiba como criar uma implementação de aplicativo de página única (SPA) do [!DNL Adobe Experience Platform Web SDK]usando o [!DNL Target].
keywords: destino;adobe destino;exibições xdm; exibições;aplicativos de página única;SPA;ciclo de vida SPA;lado do cliente;teste AB;Direcionamento de experiência;XT;VEC
feature: AEP Web SDK
exl-id: 17e71e47-c7cc-421a-bc9c-53f45f587449
TQID: https://experienceleague.adobe.com/Kp5fxEhLaXUNi6GOXXnET-1ueGQVLC0tPFhYzShk0cQ
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1836
ht-degree: 2%

---

# Implementação de aplicativos de página única

O [!DNL Adobe Experience Platform Web SDK] fornece recursos avançados para sua empresa personalizar tecnologias de próxima geração no lado do cliente, como aplicativos de página única (SPAs).

Os sites tradicionais usavam modelos de navegação &quot;página para página&quot;, também chamados de Aplicativos de várias páginas. Nesses sites, os designs são totalmente vinculados aos URLs, e mover-se entre páginas exigia um carregamento de página completo.

Aplicativos da Web modernos, como aplicativos de página única, adotaram um modelo que impulsiona o uso rápido da renderização da interface do usuário do navegador, que geralmente é independente dos recarregamentos de página. Essas experiências são acionadas pelas interações do cliente, como rolagens, cliques e movimentos de cursor. À medida que os paradigmas da Web moderna evoluíram, a relevância dos eventos genéricos tradicionais, como um carregamento de página, para implantar a personalização e a experimentação não funciona mais.

![Diagrama mostrando o ciclo de vida de SPA comparado ao ciclo de vida de página tradicional.](/help/dev/implement/client-side/aep-web-sdk/assets/spa-vs-traditional-lifecycle.png)

## Benefícios do [!DNL Experience Platform Web SDK] para SPAs

Estes são alguns benefícios de usar o [!DNL Adobe Experience Platform Web SDK] para seus aplicativos de página única:

* Capacidade de armazenar em cache todas as ofertas no carregamento da página para reduzir várias chamadas do servidor a uma única chamada de servidor.
* Melhore a experiência do usuário no site, pois as ofertas são exibidas imediatamente pelo cache, sem o tempo de atraso introduzido pelas chamadas do servidor tradicional.
* Uma única linha de código e uma configuração de desenvolvedor única permitem que os profissionais de marketing criem e executem atividades de [!UICONTROL Teste A/B] e [!UICONTROL Direcionamento de experiência] (XT) por meio do [!UICONTROL Visual Experience Composer] (VEC) em seu SPA.

## Exibições XDM e aplicativos de página única

O VEC do [!UICONTROL Adobe Target] para SPAs aproveita um conceito chamado [!UICONTROL Exibições]: um grupo lógico de elementos visuais que, juntos, constituem uma experiência de SPA. Um aplicativo de página única pode, portanto, ser considerado como uma transição entre exibições, em vez de URLs, com base nas interações do usuário. Uma [!UICONTROL Exibição] geralmente pode representar um site inteiro ou elementos visuais agrupados dentro de um site.

Para explicar melhor o que são Exibições, o exemplo a seguir usa um site de comércio eletrônico online hipotético implementado em [!DNL React] para explorar o exemplo [!UICONTROL Exibições].

Depois de navegar para o site inicial, uma imagem principal promove uma venda de Páscoa e os produtos mais recentes disponíveis no site. Nesse caso, uma [!UICONTROL Exibição] pode ser definida para toda a tela inicial. Esta [!UICONTROL Exibição] pode simplesmente ser chamada de &quot;inicial&quot;.

![Imagem de exemplo de um aplicativo de página única em uma janela do navegador.](/help/dev/implement/client-side/aep-web-sdk/assets/example-views.png)

À medida que o cliente se torna mais interessado nos produtos que a empresa está vendendo, ele decide clicar no link **Produtos**. Assim como o site inicial, a totalidade do site de produtos pode ser definida como uma [!UICONTROL Visualização]. Esta [!UICONTROL Exibição] pode se chamar &quot;products-all&quot;.

![Imagem de exemplo de um aplicativo de página única em uma janela de navegador, com todos os produtos exibidos.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products-all.png)

Uma vez que uma [!UICONTROL Exibição] pode ser definida como um site inteiro ou um grupo de elementos visuais em um site. Os quatro produtos mostrados no site de produtos podem ser agrupados e considerados como uma [!UICONTROL Exibição]. Essa exibição pode se chamar &quot;produtos&quot;.

![Imagem de exemplo de um aplicativo de página única em uma janela de navegador, com produtos de exemplo exibidos.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products.png)

Quando o cliente decide clicar no botão **Carregar mais** para explorar mais produtos no site, a URL do site não é alterada nesse caso. No entanto, uma [!UICONTROL Exibição] pode ser criada aqui para representar apenas a segunda linha de produtos mostrados. O nome da [!UICONTROL Exibição] poderia ser &quot;products-page-2&quot;.

![Imagem de exemplo de um aplicativo de página única em uma janela de navegador, com produtos de exemplo exibidos em uma página adicional.](/help/dev/implement/client-side/aep-web-sdk/assets/example-load-more.png)

O cliente decide comprar alguns produtos do site e prossegue para a tela de finalização. No site de finalização da compra, o cliente recebe as opções para escolher a entrega normal ou a expressa. Uma [!UICONTROL Exibição] pode ser qualquer grupo de elementos visuais em um site, portanto, uma [!UICONTROL Exibição] pode ser criada para preferências de entrega e ser chamada de &quot;Preferências de Entrega&quot;.

![Imagem de exemplo de uma página de check-out de aplicativo de página única em uma janela do navegador.](/help/dev/implement/client-side/aep-web-sdk/assets/example-check-out.png)

O conceito de [!UICONTROL Exibições] pode ser estendido muito além deste cenário. Estes cenários são apenas alguns exemplos de [!UICONTROL Exibições] que podem ser definidas em um site.

## Implementando [!UICONTROL Exibições XDM]

As [!UICONTROL Exibições XDM] podem ser usadas no [!DNL Target] para permitir que profissionais de marketing executem testes A/B e XT em SPAs por meio do [!UICONTROL Visual Experience Composer]. Para fazer isso, é necessário executar as seguintes etapas para concluir uma configuração de desenvolvedor única:

1. Instale o [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview).
2. Determine todas as [!UICONTROL Exibições XDM] no aplicativo de página única que deseja personalizar.
3. Após definir as [!UICONTROL Exibições XDM], para entregar atividades A/B ou XT do VEC, implemente a função `sendEvent()` com `renderDecisions` definida como `true` e a [!UICONTROL Exibição XDM] correspondente no Aplicativo de página única. A [!UICONTROL Exibição XDM] deve ser passada em `xdm.web.webPageDetails.viewName`. Esta etapa permite que os profissionais de marketing aproveitem o [!UICONTROL Visual Experience Composer] para iniciar testes A/B e XT para esses XDM.

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>Na primeira chamada `sendEvent()`, todas as [!UICONTROL Exibições XDM] que devem ser renderizadas para o usuário final são buscadas e armazenadas em cache. As `sendEvent()` chamadas subsequentes com [!UICONTROL Exibições XDM] passadas são lidas do cache e renderizadas sem uma chamada de servidor.

## Exemplos de função `sendEvent()`

Esta seção descreve três exemplos mostrando como invocar a função `sendEvent()` no React para um SPA hipotético de comércio eletrônico.

### Exemplo 1: página inicial de teste A/B

A equipe de marketing deseja executar testes A/B em toda a página inicial.

![Imagem de exemplo de um aplicativo de página única em uma janela do navegador.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-1.png)

Para executar testes A/B em todo o site inicial, `sendEvent()` deve ser chamado com o XDM `viewName` definido como `home`:

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Exemplo 2: produtos personalizados

A equipe de marketing deseja personalizar a segunda linha de produtos alterando a cor do rótulo de preço para vermelho depois que um usuário clicar em **Carregar mais**.

![Imagem de exemplo de um aplicativo de página única em uma janela do navegador, mostrando ofertas personalizadas.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component's state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Exemplo 3: preferências de delivery do teste A/B

A equipe de marketing deseja executar um teste A/B para ver se a alteração da cor do botão de azul para vermelho quando a **Entrega expressa** é selecionada. A equipe acha que essa alteração pode aumentar as conversões (em vez de manter a cor do botão azul para ambas as opções de delivery).

![Imagem de exemplo de um aplicativo de página única em uma janela de navegador, com teste A/B.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-3.png)

Para personalizar o conteúdo no site, dependendo da preferência de entrega selecionada, uma [!UICONTROL Exibição] pode ser criada para cada preferência de entrega. Quando a opção **Entrega normal** está selecionada, a [!UICONTROL Exibição] pode ser chamada de &quot;check-out-normal&quot;. Se a **Entrega expressa** estiver selecionada, a [!UICONTROL Exibição] poderá ser chamada de &quot;checkout-express&quot;.

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Usando o [!UICONTROL Visual Experience Composer] para um SPA

Quando você terminar de definir suas [!UICONTROL Exibições XDM] e implementar o `sendEvent()` com essas [!UICONTROL Exibições XDM] passadas, o VEC poderá detectar essas [!UICONTROL Exibições] e permitir que os usuários criem ações e modificações para atividades A/B ou XT.

>[!NOTE]
>
>Para usar o VEC para SPA, instale e ative o [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou a [Extensão de assistente do Chrome VEC](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension).

### Painel [!UICONTROL Modificações]

O painel [!UICONTROL Modificações] captura as ações criadas para uma [!UICONTROL Exibição] específica. Todas as ações de uma [!UICONTROL Exibição] estão agrupadas nessa [!UICONTROL Exibição].

### Ações

Clicar em uma ação destaca o elemento no site onde essa ação é aplicada. Cada ação do VEC criada em uma [!UICONTROL Exibição] tem os seguintes ícones: **Informações**, **Editar**, **Clonar**, **Mover** e **Excluir**. Esses ícones são explicados com mais detalhes na tabela a seguir.

| Ícone | Descrição |
|---|---|
| Informações | Exibe os detalhes da ação. |
| Editar | Permite editar as propriedades da ação diretamente. |
| Clonar | Clona a ação a uma ou mais [!UICONTROL Exibições] existentes no painel [!UICONTROL Modificações] ou a uma ou mais [!UICONTROL Exibições] que você buscou e nas quais navegou no VEC. A ação não precisa existir necessariamente no painel [!UICONTROL Modificações].<br/><br/>**Observação:** depois que uma operação de clonagem for feita, você deverá navegar para a [!UICONTROL Exibição] no VEC via [!UICONTROL Procurar] para ver se a ação clonada foi uma operação válida. Se a ação não puder ser aplicada à [!UICONTROL Exibição], você verá um erro. |
| Mover | Move a ação para um [!UICONTROL Evento de Carregamento de Página] ou qualquer outro [!UICONTROL Modo de Exibição] que já exista no painel [!UICONTROL Modificações].<br/><br/>**Evento de carregamento de página:** qualquer ação correspondente ao evento de carregamento de página é aplicada no carregamento inicial da página no aplicativo da Web. <br/><br/>**Observação:** após a realização de uma operação de movimentação, navegue até a [!UICONTROL Exibição] do VEC via [!UICONTROL Procurar] para ver se a movimentação foi uma operação válida. Se a ação não puder ser aplicada à [!UICONTROL Exibição], consulte um erro. |
| Excluir | Exclui a ação. |

## Exemplos de uso do VEC para SPAs

Esta seção descreve três exemplos para usar o [!UICONTROL Visual Experience Composer] para criar ações e modificações para atividades A/B ou XT.

### Exemplo 1: atualizar a visualização &quot;inicial&quot;

Anteriormente neste artigo, uma [!UICONTROL Exibição] chamada &quot;inicial&quot; foi definida para todo o site inicial. Agora, a equipe de marketing quer atualizar a visualização &quot;inicial&quot; das seguintes maneiras:

* Altere os botões **Adicionar ao carrinho** e **Curtir** para um tom mais claro de azul. Essa alteração deve ocorrer durante o carregamento da página, pois envolve a alteração de componentes do cabeçalho.
* Altere o rótulo **Produtos mais recentes de 2026** para **Produtos de teste simples para 2026** e altere a cor do texto para violeta.

Para fazer essas atualizações no VEC, selecione **Compor** e aplique essas alterações à exibição &quot;inicial&quot;.

![página de exemplo do Visual Experience Composer.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-home.png)

### Exemplo 2: alterar rótulos de produto

Para a [!UICONTROL Exibição] de &quot;products-page-2&quot;, a equipe de marketing gostaria de alterar o rótulo **Preço** para **Preço de Venda** e alterar a cor do rótulo para vermelho.

Para fazer essas atualizações no VEC, as seguintes etapas são necessárias:

1. Selecione **Procurar** no VEC.
2. Selecione **Produtos** na navegação superior do site.
3. Selecione **Carregar Mais** uma vez para exibir a segunda linha de produtos.
4. Selecione **Compor** no VEC.
5. Aplique ações para alterar o rótulo do texto para **Preço de Venda** e a cor para vermelho.

![Página de exemplo do Visual Experience Composer com rótulos de produto.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-products-page-2.png)

### Exemplo 3: personalizar o estilo de preferência do delivery

As [!UICONTROL Exibições] podem ser definidas em nível granular, como um estado ou uma opção por meio de um botão de opção. Anteriormente neste artigo, [!UICONTROL As exibições] foram definidas para preferências de entrega, &quot;check-out-normal&quot; e &quot;check-out-express&quot;. A equipe de marketing deseja alterar a cor do botão para a exibição &quot;checkout-express&quot;.

Para fazer essas atualizações no VEC, as seguintes etapas são necessárias:

1. Selecione **Procurar** no VEC.
2. Adicione produtos ao carrinho no site.
3. Selecione o ícone do carrinho no canto superior direito do site.
4. Selecione **Checkout do pedido**.
5. Selecione o botão de opção **Entrega expressa** em **Preferências de entrega**.
6. Selecione **Compor** no VEC.
7. Altere a cor do botão **Pagar** para vermelho.

>[!NOTE]
>
>O &quot;checkout-express&quot; [!UICONTROL View] não aparece no painel [!UICONTROL Modificações] até que o botão de opção **Entrega expressa** seja selecionado. Isso ocorre porque a função `sendEvent()` é executada quando o botão de opção **Entrega expressa** é selecionado. Portanto, o VEC não está ciente da [!UICONTROL Exibição] &quot;check-out-express&quot; até que o botão de opção seja selecionado.

![Visual Experience Composer mostrando o seletor de preferências de entrega.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-delivery-preference.png)
