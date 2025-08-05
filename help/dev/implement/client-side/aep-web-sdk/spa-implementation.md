---
title: Implementação de Aplicativo de Página Única para o [!DNL  Adobe Experience Platform Web SDK]
description: Saiba como criar uma implementação de aplicativo de página única (SPA) do [!DNL Adobe Experience Platform Web SDK]usando o [!DNL Target].
keywords: destino;adobe destino;exibições xdm; exibições;aplicativos de página única;SPA;ciclo de vida SPA;lado do cliente;teste AB;Direcionamento de experiência;XT;VEC
feature: AEP Web SDK
source-git-commit: f4e0e1b202863eb9fddb40836cf53d2df7cdbebe
workflow-type: tm+mt
source-wordcount: '1680'
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
* Uma única linha de código e uma configuração de desenvolvedor única permitem que os profissionais de marketing criem e executem atividades do [!UICONTROL A/B Test] e do [!UICONTROL Experience Targeting] (XT) por meio do [!UICONTROL Visual Experience Composer] (VEC) em seu SPA.

## Exibições XDM e aplicativos de página única

O [!UICONTROL Adobe Target] VEC for SPAs aproveita um conceito chamado [!UICONTROL Views]: um grupo lógico de elementos visuais que, juntos, constituem uma experiência de SPA. Um aplicativo de página única pode, portanto, ser considerado como uma transição entre exibições, em vez de URLs, com base nas interações do usuário. Um [!UICONTROL View] geralmente pode representar um site inteiro ou elementos visuais agrupados dentro de um site.

Para explicar melhor o que são Exibições, o exemplo a seguir usa um site de comércio eletrônico online hipotético implementado em [!DNL React] para explorar o exemplo [!UICONTROL Views].

Depois de navegar para o site inicial, uma imagem principal promove uma venda de Páscoa e os produtos mais recentes disponíveis no site. Nesse caso, um [!UICONTROL View] pode ser definido para toda a tela inicial. Este [!UICONTROL View] pode simplesmente ser chamado de &quot;inicial&quot;.

![Imagem de exemplo de um aplicativo de página única em uma janela do navegador.](/help/dev/implement/client-side/aep-web-sdk/assets/example-views.png)

À medida que o cliente se torna mais interessado nos produtos que a empresa está vendendo, ele decide clicar no link **Produtos**. Assim como o site inicial, a totalidade do site de produtos pode ser definida como um [!UICONTROL View]. Este [!UICONTROL View] pode se chamar &quot;products-all&quot;.

![Imagem de exemplo de um aplicativo de página única em uma janela de navegador, com todos os produtos exibidos.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products-all.png)

Já que um [!UICONTROL View] pode ser definido como um site inteiro ou um grupo de elementos visuais em um site. Os quatro produtos mostrados no site de produtos podem ser agrupados e considerados como um [!UICONTROL View]. Essa exibição pode se chamar &quot;produtos&quot;.

![Imagem de exemplo de um aplicativo de página única em uma janela de navegador, com produtos de exemplo exibidos.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products.png)

Quando o cliente decide clicar no botão **Carregar mais** para explorar mais produtos no site, a URL do site não é alterada nesse caso. No entanto, um [!UICONTROL View] pode ser criado aqui para representar apenas a segunda linha de produtos mostrados. O nome de [!UICONTROL View] poderia ser &quot;products-page-2&quot;.

![Imagem de exemplo de um aplicativo de página única em uma janela de navegador, com produtos de exemplo exibidos em uma página adicional.](/help/dev/implement/client-side/aep-web-sdk/assets/example-load-more.png)

O cliente decide comprar alguns produtos do site e prossegue para a tela de finalização. No site de finalização da compra, o cliente recebe as opções para escolher a entrega normal ou a expressa. Um [!UICONTROL View] pode ser qualquer grupo de elementos visuais em um site, portanto, um [!UICONTROL View] pode ser criado para preferências de entrega e ser chamado de &quot;Preferências de Entrega&quot;.

![Imagem de exemplo de uma página de check-out de aplicativo de página única em uma janela do navegador.](/help/dev/implement/client-side/aep-web-sdk/assets/example-check-out.png)

O conceito de [!UICONTROL Views] pode ser estendido muito além deste cenário. Estes cenários são apenas alguns exemplos de [!UICONTROL Views] que podem ser definidos em um site.

## Implementando [!UICONTROL XDM Views]

O [!UICONTROL XDM Views] pode ser aproveitado no [!DNL Target] para capacitar os profissionais de marketing a executar testes A/B e XT em SPAs por meio do [!UICONTROL Visual Experience Composer]. Para fazer isso, é necessário executar as seguintes etapas para concluir uma configuração de desenvolvedor única:

1. Instale o [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview).
2. Determine todos os [!UICONTROL XDM Views] no aplicativo de página única que deseja personalizar.
3. Após definir o [!UICONTROL XDM Views], para fornecer atividades A/B ou XT do VEC, implemente a função `sendEvent()` com `renderDecisions` definida como `true` e o [!UICONTROL XDM View] correspondente no Aplicativo de página única. O [!UICONTROL XDM View] deve ser passado em `xdm.web.webPageDetails.viewName`. Esta etapa permite que os profissionais de marketing aproveitem o [!UICONTROL Visual Experience Composer] para iniciar testes A/B e XT para esses XDM.

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
>Na primeira chamada `sendEvent()`, todos os [!UICONTROL XDM Views] que devem ser renderizados para o usuário final são buscados e armazenados em cache. As chamadas `sendEvent()` subsequentes de [!UICONTROL XDM Views] aprovadas são lidas do cache e renderizadas sem uma chamada de servidor.

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

Para personalizar o conteúdo no site, dependendo da preferência de entrega selecionada, um [!UICONTROL View] pode ser criado para cada preferência de entrega. Quando a opção **Entrega normal** está selecionada, a opção [!UICONTROL View] pode se chamar &quot;check-out-normal&quot;. Se a **Entrega expressa** estiver selecionada, o [!UICONTROL View] poderá se chamar &quot;checkout-express&quot;.

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

Quando você terminar de definir seu [!UICONTROL XDM Views] e implementar o `sendEvent()` com esses [!UICONTROL XDM Views] passados, o VEC poderá detectar esses [!UICONTROL Views] e permitir que os usuários criem ações e modificações para atividades A/B ou XT.

>[!NOTE]
>
>Para usar o VEC para SPA, instale e ative o [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou a [Extensão de assistente do Chrome VEC](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension).

### Painel [!UICONTROL Modifications]

O painel [!UICONTROL Modifications] captura as ações criadas para um [!UICONTROL View] específico. Todas as ações para um [!UICONTROL View] estão agrupadas sob esse [!UICONTROL View].

### Ações

Clicar em uma ação destaca o elemento no site onde essa ação é aplicada. Cada ação do VEC criada em um [!UICONTROL View] tem os seguintes ícones: **Informações**, **Editar**, **Clonar**, **Mover** e **Excluir**. Esses ícones são explicados com mais detalhes na tabela a seguir.

| Ícone | Descrição |
|---|---|
| Informações | Exibe os detalhes da ação. |
| Editar | Permite editar as propriedades da ação diretamente. |
| Clonar | Clona a ação a um ou mais [!UICONTROL Views] que existem no painel [!UICONTROL Modifications] ou a um ou mais [!UICONTROL Views] que você buscou e nos quais navegou no VEC. A ação não precisa existir necessariamente no painel [!UICONTROL Modifications].<br/><br/>**Observação:** após a realização de uma operação de clonagem, navegue até [!UICONTROL View] no VEC via [!UICONTROL Browse] para ver se a ação clonada foi uma operação válida. Se a ação não puder ser aplicada ao [!UICONTROL View], você verá um erro. |
| Mover  | Move a ação para [!UICONTROL Page Load Event] ou qualquer outro [!UICONTROL View] que já existe no painel [!UICONTROL Modifications].<br/><br/>**Evento de carregamento de página:** qualquer ação correspondente ao evento de carregamento de página é aplicada no carregamento inicial da página no aplicativo da Web. <br/><br/>**Observação:** após a realização de uma operação de movimentação, navegue até [!UICONTROL View] no VEC via [!UICONTROL Browse] para ver se a movimentação foi uma operação válida. Se a ação não puder ser aplicada ao [!UICONTROL View], consulte um erro. |
| Excluir | Exclui a ação. |

## Exemplos de uso do VEC para SPAs

Esta seção descreve três exemplos para usar o [!UICONTROL Visual Experience Composer] para criar ações e modificações para atividades A/B ou XT.

### Exemplo 1: atualizar a visualização &quot;inicial&quot;

Anteriormente neste artigo, um [!UICONTROL View] chamado &quot;página inicial&quot; foi definido para todo o site inicial. Agora, a equipe de marketing quer atualizar a visualização &quot;inicial&quot; das seguintes maneiras:

* Altere os botões **Adicionar ao carrinho** e **Curtir** para um tom mais claro de azul. Essa alteração deve ocorrer durante o carregamento da página, pois envolve a alteração de componentes do cabeçalho.
* Altere o rótulo **Produtos mais recentes de 2026** para **Produtos de teste simples para 2026** e altere a cor do texto para violeta.

Para fazer essas atualizações no VEC, selecione **Compor** e aplique essas alterações à exibição &quot;inicial&quot;.

![página de exemplo do Visual Experience Composer.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-home.png)

### Exemplo 2: alterar rótulos de produto

Para a [!UICONTROL View] &quot;products-page-2&quot;, a equipe de marketing quer alterar o rótulo **Price** para **Sale Price** e alterar a cor do rótulo para vermelho.

Para fazer essas atualizações no VEC, as seguintes etapas são necessárias:

1. Selecione **Procurar** no VEC.
2. Selecione **Produtos** na navegação superior do site.
3. Selecione **Carregar Mais** uma vez para exibir a segunda linha de produtos.
4. Selecione **Compor** no VEC.
5. Aplique ações para alterar o rótulo do texto para **Preço de Venda** e a cor para vermelho.

![Página de exemplo do Visual Experience Composer com rótulos de produto.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-products-page-2.png)

### Exemplo 3: personalizar o estilo de preferência do delivery

[!UICONTROL Views] pode ser definido em um nível granular, como um estado ou uma opção de um botão de opção. No início deste artigo, [!UICONTROL Views] foram definidos para preferências de entrega, &quot;check-out-normal&quot; e &quot;check-out-express&quot;. A equipe de marketing deseja alterar a cor do botão para a exibição &quot;checkout-express&quot;.

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
>O &quot;checkout-express&quot; [!UICONTROL View] não aparece no painel [!UICONTROL Modifications] até que o botão de opção **Entrega expressa** seja selecionado. Isso ocorre porque a função `sendEvent()` é executada quando o botão de opção **Entrega expressa** é selecionado. Portanto, o VEC não está ciente da [!UICONTROL View] &quot;check-out-express&quot; até que o botão de opção seja selecionado.

![Visual Experience Composer mostrando o seletor de preferências de entrega.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-delivery-preference.png)
