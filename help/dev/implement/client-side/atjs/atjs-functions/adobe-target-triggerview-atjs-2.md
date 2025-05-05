---
keywords: adobe.target.triggerView, triggerView, triggerview, acionar exibição, at.js, funções, função, viewName, viewname, nome da exibição, adobe.target.triggerView1
description: Use a função adobe.target.triggerView() da biblioteca de JavaScript do  [!DNL Adobe Target] at.js para usar em Aplicativos de página única (SPA). (at.js 2.x)
title: Como usar a função adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: fe4e607173c760f782035a10f52936d96e9db300
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 21%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

Essa função pode ser chamada sempre que uma nova página é carregada ou quando um componente em uma página é renderizado novamente. `adobe.target.triggerView()` deve ser implementado para aplicativos de página única (SPA) para usar o [!UICONTROL Visual Experience Composer] (VEC) para criar atividades do [!UICONTROL A/B Test] e [!UICONTROL Experience Targeting] (XT). Se `[!UICONTROL adobe.target.triggerView()]` não estiver implementado no site, o VEC não poderá ser usado para SPA. Para obter mais informações, consulte [Implementação do aplicativo de página única](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Essa função foi introduzida com o at.js 2.*x*. Essa função não está disponível para a at.js versão 1.*x*.

| Parâmetro | Tipo | Obrigatório? | Descrição |
| --- | --- | --- | --- |
| viewName | String | Sim | Transmita qualquer nome como um tipo de sequência de caracteres que você deseja representar sua exibição. Esse nome de exibição aparece no painel [!UICONTROL Modifications] do VEC para que os profissionais de marketing criem ações e executem suas atividades de XT [!UICONTROL A/B Test] e [!UICONTROL Experience Targeting]. |
| opções | Objeto | Não |  |
| opções > página | Booleano | Não | **TRUE:** O valor padrão da página é true. Quando page=true, as notificações são enviadas ao [!DNL Target] backend para aumentar a contagem de impressões.<P>Uma notificação é sempre enviada por padrão quando um `[!UICONTROL triggerView]` é chamado, exceto quando options > page é definido como false.<P>**FALSE:** quando page=false, as notificações não são enviadas para aumentar a contagem de impressões. Essa abordagem deve ser usada quando você deseja apenas renderizar novamente um componente em uma página com uma oferta.<P>**Observação**: as ofertas de código personalizado no VEC não são renderizadas novamente quando `[!UICONTROL triggerView()]` é chamado com `{page: false}` como a opção. |

## Exemplo: Verdadeiro

Chamada `[!UICONTROL triggerView()]` para enviar uma notificação para o back-end do [!DNL Target] para incrementar as impressões da atividade e outras métricas.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Exemplo: Falso

`[!UICONTROL triggerView()]` chamada para não ter notificações enviadas ao backend [!DNL Target] para contagem de impressões.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Exemplo: encadeamento de promessas com `getoffers()` e `applyOffers()`

Para executar `triggerView()` quando a promessa `getOffers()` for resolvida, é importante executar `triggerView()` no bloco final, conforme mostrado no exemplo abaixo. Isso é necessário para que o VEC detecte `Views` no modo de criação.

```javascript {line-numbers="true"}
adobe.target.getOffers({
    'request': {
        'prefetch': {
            'views': [{
                'parameters': {}
            }]
        }
    }
}).then(function(response) {
    // Apply Offers
    adobe.target.applyOffers({
        response: response
    });
}).catch(function(error) {
    console.log("AT: getOffers failed - Error", error);
}).finally(() => {
    // Trigger View call, assuming pageView is defined elsewhere
    adobe.target.triggerView(pageView, {
        page: true
    });
    console.log('AT: View triggered on : ' + pageView);
});
```

## Exemplo: Melhor compatibilidade de `triggerView()` com [!UICONTROL Adobe Visual Editing Helper extension]

Considere o seguinte ao usar a [extensão Auxiliar de Edição Visual do Adobe](https://experienceleague.adobe.com/pt-br/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}:

Devido às novas políticas de Manifesto V3 do [!DNL Googl]e para extensões do [!DNL Chrome], o [!UICONTROL Visual Editing Helper extension] deve aguardar o evento `DOMContentLoaded` antes de carregar as bibliotecas do [!DNL Target] no VEC. Esse atraso pode fazer com que as páginas da Web acionem a chamada `triggerView()` antes que as bibliotecas de criação estejam prontas, resultando no preenchimento da exibição ao carregar.

Para atenuar esse problema, use um ouvinte para o evento de página `load`.

Este é um exemplo de implementação:

```javascript
function triggerViewIfLoaded() {
    adobe.target.triggerView("homeView");
}

if (document.readyState === "complete") {
    // If the page is already loaded
    triggerViewIfLoaded();
} else {
    // If the page is not yet loaded, set up an event listener
    window.addEventListener("load", triggerViewIfLoaded);
}
```


