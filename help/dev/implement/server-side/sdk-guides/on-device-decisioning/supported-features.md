---
title: Quais recursos são compatíveis com a decisão no dispositivo?
description: Saiba como fornecer o conteúdo personalizado mais relevante e envolvente por meio do aprendizado de máquina usando uma chamada de servidor em tempo real.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
TQID: https://experienceleague.adobe.com/Fgwu8Nh90i-tS1aCUVmQReGz6DYBP2GHdcNM7z17BSk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 731
ht-degree: 9%

---

# Visão geral dos recursos compatíveis

Os SDKs do lado do servidor do [!DNL Adobe Target] oferecem aos desenvolvedores flexibilidade para escolher entre desempenho e atualização de dados para decisões. Em outras palavras, se o fornecimento do conteúdo personalizado mais relevante e envolvente por meio do aprendizado de máquina for mais importante para você, uma chamada de servidor em tempo real deverá ser feita. Mas quando o desempenho é mais crítico, uma decisão no dispositivo deve ser tomada. Para que a [!UICONTROL decisão no dispositivo] funcione, consulte esta lista de recursos com suporte:

* Tipos de atividades
* Direcionamento de público
* Método de Alocação

## Tipos de atividades

A tabela a seguir indica quais [tipos de atividade](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=pt-BR) criados com o [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=pt-BR&) têm ou não suporte para a [!UICONTROL decisão no dispositivo].

| Tipo de atividade | Suportado |
| --- | --- |
| [Teste A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=pt-BR) | Sim |
| [Alocação automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=pt-BR) | Não |
| [Direcionamento automático](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=pt-BR) | Não |
| [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=pt-BR) (A4T) | Sim |
| [Teste multivariado](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=pt-BR) (MVT) | Não |
| [Direcionamento de experiência](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=pt-BR) (XT) | Sim |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=pt-BR) (AP) | Não |
| [Recomendações](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=pt-BR) | Não |


## Direcionamento de público

A tabela a seguir indica quais regras de público-alvo são suportadas ou não para a [!UICONTROL decisão no dispositivo].

| Regra de público-alvo | Decisão no dispositivo |
| --- | --- |
| [Geografia](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=pt-BR) | Sim |
| [Rede](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=pt-BR) | Não |
| [Móvel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=pt-BR) | Não |
| [Parâmetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=pt-BR) | Sim |
| [Sistema operacional](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=pt-BR) | Sim |
| [Páginas do site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=pt-BR) | Sim |
| [Navegador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=pt-BR) | Sim |
| [Perfil do visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=pt-BR) | Não |
| [Fontes de Tráfego](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=pt-BR) | Não |
| [Intervalo de tempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=pt-BR) | Sim |
| [Públicos-alvo da Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=pt-BR) (públicos-alvo da Adobe Audience Manager, Adobe Analytics e Adobe Experience Manager) | Não |

### Direcionamento geográfico para [!UICONTROL decisão no dispositivo]

Para manter uma latência próxima de zero para atividades de [!UICONTROL decisão no dispositivo] com públicos baseados em localização geográfica, a Adobe recomenda que você forneça os valores geográficos você mesmo na chamada para `getOffers`. Faça isso definindo o objeto `Geo` no `Context` da solicitação. Isso significa que seu servidor precisará de uma maneira de determinar a localização de cada usuário final. Por exemplo, o servidor pode executar uma pesquisa de IP para Geo usando um serviço configurado por você. Alguns provedores de hospedagem, como a Google Cloud, fornecem essa funcionalidade por meio de cabeçalhos personalizados em cada `HttpServletRequest`.

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

No entanto, se você não tiver a capacidade de executar pesquisas de IP para Geografia no servidor, mas ainda quiser executar a [!UICONTROL decisão no dispositivo] para solicitações `getOffers` que contêm públicos com base geográfica, isso também é suportado. A desvantagem dessa abordagem é que ela usará uma pesquisa remota de IP para Geo, o que adicionará latência a cada chamada `getOffers`. Essa latência deve ser menor que uma chamada remota `getOffers`, pois atinge um CDN localizado próximo ao seu servidor. Você só deve fornecer o campo `ipAddress` no objeto `Geo` no `Context` de sua solicitação para que o SDK recupere a localização geográfica do endereço IP de seu usuário. Se qualquer outro campo além de `ipAddress` for fornecido, o SDK [!DNL Target] não buscará os metadados de localização geográfica para resolução.


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

A tabela a seguir indica quais métodos de alocação têm ou não suporte para a [!UICONTROL decisão no dispositivo].

| Método de Alocação | Suportado |
| --- | --- |
| Manual | Sim |
| [Alocar automaticamente para a melhor experiência](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=pt-BR) | Não |
| [Direcionamento automático para experiências personalizadas](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html?lang=pt-BR) | Não |
