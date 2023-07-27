---
keywords: implementação, biblioteca javascript, js, atjs, decisão no dispositivo, decisão no dispositivo, recursos compatíveis, $8
description: Saiba quais recursos são compatíveis com o [!UICONTROL decisão no dispositivo].
title: Quais recursos são compatíveis com a Decisão no dispositivo?
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 9%

---

# Recursos compatíveis com o [!UICONTROL decisão no dispositivo]

A variável [!DNL Adobe Target] O JS SDK oferece aos clientes a flexibilidade para escolher entre o desempenho e a atualização dos dados para as decisões. Em outras palavras, se o fornecimento do conteúdo personalizado mais relevante e envolvente por meio do aprendizado de máquina for mais importante para você, uma chamada de servidor em tempo real deverá ser feita. Mas quando o desempenho é mais crítico, uma decisão no dispositivo e na memória deve ser tomada. Para [!UICONTROL decisão no dispositivo] para funcionar, consulte as seguintes seções que listam os recursos compatíveis.

## Tipos de atividades aceitas

A tabela a seguir indica quais [tipos de atividades](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) criado pela [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) ou [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) são ou não compatíveis com o [!UICONTROL decisão no dispositivo].

| Tipo de atividade | Suportado? |
| --- | --- |
| [Teste A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Sim |
| [Alocação automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Não |
| [Direcionamento automático](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![Premium](../../../assets/premium.png) | Não |
| [Teste multivariado](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Não |
| [Direcionamento de experiência](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Sim |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | Não |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![Premium](../../../assets/premium.png) | Não |
| [Atividades que usam o Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | Sim |

## Direcionamento de público

A tabela a seguir indica quais regras de público-alvo são ou não compatíveis com o [!UICONTROL decisão no dispositivo].

| Regra de público | Suportado? |
| --- | --- |
| [Geografia](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Sim |
| [Rede](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Não |
| [Móvel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Não |
| [Parâmetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Sim |
| [Sistema operacional](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Sim |
| [Páginas do site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Sim |
| [Navegador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Sim |
| [Perfil do visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Não |
| [Fontes de Tráfego](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Não |
| [Intervalo de tempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Sim |
| Públicos da Adobe Experience Cloud<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager], e [!DNL Adobe Experience Manager]) | Não |

### Direcionamento geográfico para [!UICONTROL decisão no dispositivo]

Para manter a latência mínima para [!UICONTROL decisão no dispositivo] atividades com públicos baseados em geografia, a Adobe recomenda que você forneça os valores geográficos na chamada para [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). Defina o objeto Geo no contexto da solicitação. Isso significa no navegador uma maneira de determinar a localização de cada visitante. Por exemplo, você pode executar uma pesquisa de IP para Geo usando um serviço configurado por você. Alguns provedores de hospedagem, como o Google Cloud, fornecem essa funcionalidade por meio de cabeçalhos personalizados em cada `HttpServletRequest`.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                city: "SAN FRANCISCO", 
                countryCode: "US", 
                stateCode: "CA", 
                latitude: 37.75, 
                longitude: -122.4 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

No entanto, se você não conseguir realizar pesquisas de IP para Geografia no servidor, mas ainda quiser realizar [!UICONTROL decisão no dispositivo] para [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) que contêm públicos com base geográfica, isso também é compatível. A desvantagem dessa abordagem é que ela usa uma pesquisa remota de IP para geografia, o que adiciona latência a cada `getOffers` chame. Essa latência deve ser menor que um `getOffers` chame com a decisão do lado do servidor, pois ela atinge um CDN localizado próximo ao seu servidor. Forneça somente o campo &quot;ipAddress&quot; no objeto Geo no Contexto de sua solicitação para o SDK recuperar a localização geográfica do endereço IP do visitante. Se qualquer outro campo além de &quot;ipAddress&quot; for fornecido, a variável [!DNL Target] O SDK não buscará os metadados de localização geográfica para resolução.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                ipAddress: "127.0.0.1" 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

### Método de alocação

A tabela a seguir indica quais métodos de alocação são ou não compatíveis com [!UICONTROL decisão no dispositivo].

| Método de alocação | Suportado? |
| --- | --- |
| Manual | Sim |
| [Alocar automaticamente para a melhor experiência](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Não |
| [Direcionamento automático para experiências personalizadas](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Não |
