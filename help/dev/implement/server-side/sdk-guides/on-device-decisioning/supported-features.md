---
title: Quais recursos são compatíveis com a decisão no dispositivo?
description: Saiba como fornecer o conteúdo personalizado mais relevante e envolvente por meio do aprendizado de máquina usando uma chamada de servidor em tempo real.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 10%

---

# Visão geral dos recursos compatíveis

[!DNL Adobe Target]Os SDKs do lado do servidor da oferecem aos desenvolvedores flexibilidade para escolher entre desempenho e atualização de dados para decisões. Em outras palavras, se o fornecimento do conteúdo personalizado mais relevante e envolvente por meio do aprendizado de máquina for mais importante para você, uma chamada de servidor em tempo real deverá ser feita. Mas quando o desempenho é mais crítico, uma decisão no dispositivo deve ser tomada. Para [!UICONTROL decisão no dispositivo] para funcionar, consulte a seguinte lista de recursos compatíveis:

* Tipos de atividades
* Direcionamento de público
* Método de Alocação

## Tipos de atividades 

A tabela a seguir indica quais [tipos de atividades](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) criado usando o [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?) são compatíveis ou não com o [!UICONTROL decisão no dispositivo].

| Tipo de atividade | Suportado |
| --- | --- |
| [Teste A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Sim |
| [Alocação automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Não |
| [Direcionamento automático](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Não |
| [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T) | Sim |
| [Teste multivariado](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Não |
| [Direcionamento de experiência](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Sim |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) | Não |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) | Não |


## Direcionamento de público

A tabela a seguir indica quais regras de público-alvo são ou não compatíveis com o [!UICONTROL decisão no dispositivo].

| Regra de público-alvo | Decisão no dispositivo |
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
| [Públicos do Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Públicos-alvo da Adobe Audience Manager, Adobe Analytics e Adobe Experience Manager | Não |

### Direcionamento geográfico para [!UICONTROL decisão no dispositivo]

Para manter uma latência próxima de zero para [!UICONTROL decisão no dispositivo] atividades com públicos baseados em geografia, a Adobe recomenda que você forneça os valores geográficos na chamada para `getOffers`. Faça isso configurando o `Geo` objeto no `Context` do pedido. Isso significa que seu servidor precisará de uma maneira de determinar a localização de cada usuário final. Por exemplo, o servidor pode executar uma pesquisa de IP para Geo usando um serviço configurado por você. Alguns provedores de hospedagem, como o Google Cloud, fornecem essa funcionalidade por meio de cabeçalhos personalizados em cada `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(ipToGeoLookup(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

    public static Geo ipToGeoLookup(String ip) {
        GeoResult geoResult = geoLookupService.lookup(ip);
        return new Geo()
            .city(geoResult.getCity())
            .stateCode(geoResult.getStateCode())
            .countryCode(geoResult.getCountryCode());
    }

}
```

>[!ENDTABS]

No entanto, se você não tiver a capacidade de realizar pesquisas de IP para Geo no servidor, mas ainda quiser realizar [!UICONTROL decisão no dispositivo] para `getOffers` que contêm públicos com base geográfica, isso também é compatível. A desvantagem dessa abordagem é que ela usará uma pesquisa remota de IP para Geo, o que adicionará latência a cada `getOffers` chame. Essa latência deve ser menor que uma latência remota `getOffers` chamada, já que ela atinge um CDN localizado próximo ao seu servidor. Você só deve fornecer o `ipAddress` no campo `Geo` objeto no `Context` de sua solicitação, para que o SDK recupere a localização geográfica do endereço IP do usuário. Se qualquer outro campo além do campo `ipAddress` for fornecida, a variável [!DNL Target] O SDK não buscará os metadados de localização geográfica para resolução.


>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(new Geo().ipAddress(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

}
```

>[!ENDTABS]

## Método de alocação

A tabela a seguir indica quais métodos de alocação são ou não compatíveis com [!UICONTROL decisão no dispositivo].

| Método de Alocação | Suportado |
| --- | --- |
| Manual | Sim |
| [Alocar automaticamente para a melhor experiência](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Não |
| [Direcionamento automático para experiências personalizadas](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html) | Não |
