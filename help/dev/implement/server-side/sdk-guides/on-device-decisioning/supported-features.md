---
title: Quais recursos são compatíveis com a decisão no dispositivo?
description: Saiba como fornecer o conteúdo personalizado mais relevante e envolvente por meio do aprendizado de máquina usando uma chamada de servidor em tempo real.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 13%

---

# Visão geral dos recursos compatíveis

Os SDKs do lado do servidor do [!DNL Adobe Target] oferecem aos desenvolvedores flexibilidade para escolher entre desempenho e atualização de dados para decisões. Em outras palavras, se o fornecimento do conteúdo personalizado mais relevante e envolvente por meio do aprendizado de máquina for mais importante para você, uma chamada de servidor em tempo real deverá ser feita. Mas quando o desempenho é mais crítico, uma decisão no dispositivo deve ser tomada. Para que o [!UICONTROL on-device decisioning] funcione, consulte esta lista de recursos com suporte:

* Tipos de atividades
* Direcionamento de público
* Método de Alocação

## Tipos de atividades 

A tabela a seguir indica quais [tipos de atividades](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) criados com o [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?) têm suporte ou não têm suporte para [!UICONTROL on-device decisioning].

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

A tabela a seguir indica quais regras de público-alvo têm ou não suporte para [!UICONTROL on-device decisioning].

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
| [Públicos-alvo do Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (públicos-alvo do Adobe Audience Manager, Adobe Analytics e Adobe Experience Manager | Não |

### Direcionamento geográfico para [!UICONTROL on-device decisioning]

Para manter uma latência próxima de zero para atividades [!UICONTROL on-device decisioning] com públicos baseados em localização geográfica, a Adobe recomenda que você mesmo forneça os valores geográficos na chamada para `getOffers`. Faça isso definindo o objeto `Geo` no `Context` da solicitação. Isso significa que seu servidor precisará de uma maneira de determinar a localização de cada usuário final. Por exemplo, o servidor pode executar uma pesquisa de IP para Geo usando um serviço configurado por você. Alguns provedores de hospedagem, como a Google Cloud, fornecem essa funcionalidade por meio de cabeçalhos personalizados em cada `HttpServletRequest`.

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

No entanto, se você não tiver a capacidade de realizar pesquisas de IP para Geografia no servidor, mas ainda quiser executar [!UICONTROL on-device decisioning] para `getOffers` solicitações que contenham públicos com base geográfica, isso também será suportado. A desvantagem dessa abordagem é que ela usará uma pesquisa remota de IP para Geo, o que adicionará latência a cada chamada `getOffers`. Essa latência deve ser menor que uma chamada remota `getOffers`, pois atinge um CDN localizado próximo ao seu servidor. Você deve fornecer somente o campo `ipAddress` no objeto `Geo` no `Context` de sua solicitação para que o SDK recupere a localização geográfica do endereço IP do seu usuário. Se qualquer outro campo além de `ipAddress` for fornecido, o SDK [!DNL Target] não buscará os metadados de localização geográfica para resolução.


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

A tabela a seguir indica quais métodos de alocação têm ou não suporte para [!UICONTROL on-device decisioning].

| Método de Alocação | Suportado |
| --- | --- |
| Manual | Sim |
| [Alocar automaticamente para a melhor experiência](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Não |
| [Direcionamento automático para experiências personalizadas](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html) | Não |
