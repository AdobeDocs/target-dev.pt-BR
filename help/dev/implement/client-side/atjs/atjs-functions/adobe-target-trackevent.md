---
keywords: adobe.target.trackEvent, trackEvent, trackevent, rastrear evento, at.js, funções, função, preventDefault, preventdefault, impedir padrão, adobe.target.trackEvent
description: Use a função [!UICONTROL adobe.target.trackEvent()] da biblioteca JavaScript  [!DNL Adobe Target] at.js do para disparar uma solicitação para relatar ações do usuário, como cliques e conversões no site.
title: Como faço para usar a função [!UICONTROL adobe.target.trackEvent()]?
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
TQID: https://experienceleague.adobe.com/Jib9C5FvmsgIF6CA-0UbdMdnMiXxQCkU2-O3Zys3vrY
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 61%

---

# [!UICONTROL adobe.target.trackEvent(options)]

Essa função aciona uma solicitação para relatar ações do usuário, como cliques e conversões. Não entrega atividades na resposta.

Essa mbox de monitoramento de evento pode, então, ser usada para definir métricas em atividades. Para obter mais informações, consulte [Métricas de sucesso](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) e [Conversões de rastreamento](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions).

Veja os detalhes da API:

| Chave | Tipo | Obrigatório | Descrição |
|--- |--- |--- |--- |
| mbox | String | Sim | Nome da mbox<P>**Observação**: se uma chamada [!UICONTROL trackEvent()] for acionada com um nome de mbox que já tenha sido acionado na página, a SDID de [!UICONTROL trackEvent()] será redefinida e será diferente das chamadas [!DNL Target] na página. No entanto, disparar uma chamada [!UICONTROL trackEvent()] com um nome de mbox diferente mantém a SDID da chamada [!UICONTROL trackEvent()] consistente com as chamadas [!UICONTROL Page Load Request]/[!UICONTROL triggerView()] na página. |
| selector | String | Não | Seletores CSS usados para encontrar os elementos HTML. Os ouvintes do evento serão fixados aos elementos encontrados. |
| type | String | Não | Representa um tipo de evento registrado. Pode ser que ambos sejam elementos HTML conhecidos como: clique, mouse para baixo, etc., bem como eventos HTML. |
| preventDefault | Booleano | Não | Indica se usará `[!UICONTROL event.preventDefault()]` no retorno do ouvinte do evento. O padrão é false.<P>**Observação**: somente `[!UICONTROL form[submit]]` e `a[click]` são suportados. Outros cenários não são compatíveis devido à complexidade e à grande quantidade de cenários para suporte. |
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
