---
keywords: adobe.target.trackEvent, trackEvent, trackevent, rastrear evento, at.js, funções, função, preventDefault, preventdefault, impedir padrão, adobe.target.trackEvent
description: Use o [!UICONTROL adobe.target.trackEvent()] para a [!DNL Adobe Target] Biblioteca JavaScript at.js do para disparar uma solicitação para relatar ações do usuário, como cliques e conversões no site.
title: Como usar o [!UICONTROL adobe.target.trackEvent()] Função?
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 59%

---

# [!UICONTROL adobe.target.trackEvent(options)]

Essa função aciona uma solicitação para relatar ações do usuário, como cliques e conversões. Não entrega atividades na resposta.

Essa mbox de monitoramento de evento pode, então, ser usada para definir métricas em atividades. Para obter mais informações, consulte [Métricas de sucesso](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) e [Conversões de rastreamento](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions).

Veja os detalhes da API:

| Chave | Tipo | Obrigatório | Descrição |
|--- |--- |--- |--- |
| mbox | String | Sim | Nome da mbox<P>**Nota**: Se um [!UICONTROL trackEvent()] é acionada com um nome de mbox que já foi acionado na página, a SDID de [!UICONTROL trackEvent()] é redefinido e será diferente da variável [!DNL Target] chamadas na página. No entanto, o acionamento de um [!UICONTROL trackEvent()] a chamada com um nome de mbox diferente mantém o [!UICONTROL trackEvent()] SDID da chamada de acordo com a variável [!UICONTROL Solicitação de carregamento de página]/[!UICONTROL triggerView()] chamadas na página. |
| selector | String    | Não | Seletores CSS usados para encontrar os elementos HTML. Os ouvintes do evento serão fixados aos elementos encontrados. |
| type | String | Não | Representa um tipo de evento registrado. Pode ser que ambos sejam elementos HTML conhecidos como: clique, mouse para baixo, etc., bem como eventos HTML. |
| preventDefault | Booleano | Não | Indica se usará `[!UICONTROL event.preventDefault()]` no retorno do ouvinte do evento. O padrão é false.<P>**Nota**: Somente `[!UICONTROL form[submit]]` e `a[click]` são compatíveis. Outros cenários não são compatíveis devido à complexidade e à grande quantidade de cenários para suporte. |
| params | Objeto | Não | Parâmetros de mbox. Um objeto de pares de valores-chave que tem a seguinte estrutura:<P>`{ "param1": "value1", "param2": "value2"}` |
| timeout | Número | Não | Tempo limite em milissegundos.<P>Se não especificado, o valor padrão é utilizado:<P>`...timeoutInSeconds: 0.15...}` |
| success | Função | Não | Uma função de retorno de chamada usada para sinalizar que o evento foi relatado. |
| error | Função | Não | Uma função de retorno de chamada usada para sinalizar que não foi possível relatar o evento. |

## Exemplo

```javascript {line-numbers="true"}
<a href="https://asite.com">click me!</a> 
```

Além do código JavaScript para atribuição de `trackEvent`:

```javascript {line-numbers="true"}
<script> 
$('a').click(function(event){ 
  adobe.target.trackEvent({'mbox':'homePageHero'}) 
}); 
</script> 
```

Ou:

```javascript {line-numbers="true"}
adobe.target.trackEvent({ 
    "mbox": "clicked-cta", 
    "params": { 
        "param1": "value1" 
    } 
});
```

>[!WARNING]
>
>Se os campos obrigatórios não estiverem definidos, nenhuma solicitação será executada e um erro será lançado.
