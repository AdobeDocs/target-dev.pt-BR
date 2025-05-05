---
keywords: implementação, biblioteca javascript, js, atjs, decisão no dispositivo, decisão no dispositivo, recursos compatíveis, $8
description: Saiba quais recursos são compatíveis com o [!UICONTROL on-device decisioning].
title: Quais recursos são compatíveis com a Decisão no dispositivo?
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 12%

---

# Recursos com suporte para [!UICONTROL on-device decisioning]

O SDK JS do [!DNL Adobe Target] oferece aos clientes flexibilidade para escolher entre desempenho e atualização de dados para decisões. Em outras palavras, se o fornecimento do conteúdo personalizado mais relevante e envolvente por meio do aprendizado de máquina for mais importante para você, uma chamada de servidor em tempo real deverá ser feita. Mas quando o desempenho é mais crítico, uma decisão no dispositivo e na memória deve ser tomada. Para que o [!UICONTROL on-device decisioning] funcione, consulte as seções a seguir, que listam os recursos compatíveis.

## Tipos de atividades aceitas

A tabela a seguir indica quais [tipos de atividade](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=pt-BR) criados pelo [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=pt-BR) ou pelo [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=pt-BR) (VEC) têm ou não suporte para [!UICONTROL on-device decisioning].

| Tipo de atividade | Suportado? |
| --- | --- |
| [Teste A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=pt-BR) | Sim |
| [Alocação automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=pt-BR) | Não |
| [Direcionamento automático](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=pt-BR) ![Premium](../../../assets/premium.png) | Não |
| [Teste multivariado](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=pt-BR) (MVT) | Não |
| [Direcionamento de experiência](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=pt-BR) (XT) | Sim |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=pt-BR) ![Premium](../../../assets/premium.png) | Não |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=pt-BR) ![Premium](../../../assets/premium.png) | Não |
| [Atividades usando o Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=pt-BR&) (A4T) | Sim |

## Direcionamento de público

A tabela a seguir indica quais regras de público-alvo têm ou não suporte para [!UICONTROL on-device decisioning].

| Regra de público | Suportado? |
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
| Públicos da Adobe Experience Cloud<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager] e [!DNL Adobe Experience Manager]) | Não |

### Direcionamento geográfico para [!UICONTROL on-device decisioning]

Para manter uma latência mínima para atividades [!UICONTROL on-device decisioning] com públicos baseados em localização geográfica, a Adobe recomenda que você mesmo forneça os valores geográficos na chamada para [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). Defina o objeto Geo no contexto da solicitação. Isso significa no navegador uma maneira de determinar a localização de cada visitante. Por exemplo, você pode executar uma pesquisa de IP para Geo usando um serviço configurado por você. Alguns provedores de hospedagem, como a Google Cloud, fornecem essa funcionalidade por meio de cabeçalhos personalizados em cada `HttpServletRequest`.

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

No entanto, se você não conseguir realizar pesquisas de IP para Geografia no servidor, mas ainda quiser executar [!UICONTROL on-device decisioning] para solicitações de [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) que contêm públicos baseados em localização geográfica, isso também será suportado. A desvantagem dessa abordagem é que ela usa uma pesquisa remota de IP para Geo, o que adiciona latência a cada chamada `getOffers`. Essa latência deve ser menor que uma chamada `getOffers` com decisão do lado do servidor, pois atinge um CDN localizado próximo ao seu servidor. Forneça somente o campo &quot;ipAddress&quot; no objeto Geo no Contexto de sua solicitação para o SDK recuperar a localização geográfica do endereço IP do visitante. Se qualquer outro campo além de &quot;ipAddress&quot; for fornecido, o SDK [!DNL Target] não buscará os metadados de localização geográfica para resolução.

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

A tabela a seguir indica quais métodos de alocação têm ou não suporte para [!UICONTROL on-device decisioning].

| Método de alocação | Suportado? |
| --- | --- |
| Manual | Sim |
| [Alocar automaticamente para a melhor experiência](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=pt-BR) | Não |
| [Direcionamento automático para experiências personalizadas](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=pt-BR) | Não |
