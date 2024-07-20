---
title: Direcionamento de público
description: Os públicos podem ser usados para direcionar suas atividades de experimentação e personalização.O  [!DNL Adobe Target] oferece suporte a vários recursos avançados de direcionamento de público-alvo prontos para uso.
exl-id: df1bd856-e848-452c-90a0-abf29e7a2313
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 26%

---

# Direcionamento de público

## Visão geral

Os públicos podem ser usados para direcionar suas atividades de experimentação e personalização. O [!DNL Adobe Target] oferece suporte a uma variedade de recursos avançados de direcionamento de público pronto para uso. Os seguintes atributos estão disponíveis para o [direcionamento de público](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/create-audience.html):

### Biblioteca [!DNL Target]

Para obter mais informações, consulte [[!DNL Target] Biblioteca](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-library.html).
&#x200B;
* Referenciado do Bing
* Chrome
* Firefox
* Referenciado do Google
* Internet Explorer
* Sistema operacional Linux
* Sistema operacional Mac OS
* Novos visitantes
* Visitantes que retornam
* Safari
* Dispositivo tablet
* Sistema operacional Windows
* Referenciado do Yahoo

### Geografia  

Para obter mais informações, consulte [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html).
&#x200B;&#x200B;
* País/Região
* Estado
* Cidade
* Código Postal
* Latitude
* Longitude
* DMA
* Operadora de celular

### Rede

Para obter mais informações, consulte [Rede](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html).

* ISP
* Nome do Domínio
* Velocidade de conexão

### Dispositivo móvel

Para obter mais informações, consulte [Dispositivo móvel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html).

* Nome de marketing do dispositivo
* Modelo do dispositivo
* Fornecedor do dispositivo
* É dispositivo móvel
* É celular
* É tablet
* SO
* Altura de tela (px)
* Largura de tela (px)

### Personalizado 

Para obter mais informações, consulte [Parâmetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html).

* qualquer par de chave/valor

### Sistema operacional

Para obter mais informações, consulte [Sistema Operacional](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html).

* Linux
* Macintosh
* Windows

### Páginas do site

Para obter mais informações, consulte [Páginas do site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html).

* Página atual
* Página anterior
* Página de aterrissagem
* Cabeçalho HTTP

### Navegador

Para obter mais informações, consulte [Navegador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html).

* Tipo
* Idioma 
* Versão 

### Perfil do visitante

Para obter mais informações, consulte [Perfil do visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html).

* qualquer par de chave/valor, que seja persistente

### Fontes de tráfego

Para obter mais informações, consulte [Fontes de tráfego](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html).

* Do Baidu
* Do Bing
* Do Google
* Do Yahoo
* Página de aterrissagem de referência: URL
* Página de aterrissagem de referência: domínio
* Página de aterrissagem de referência: consulta

### Intervalo de tempo

Para obter mais informações, consulte [Intervalo de tempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html).

* Data de Início / Data Final

## Client Hints

O [!DNL Adobe Target] requer Client Hints para a segmentação correta de atributos de Navegador, Sistema Operacional e Público-alvo móvel, bem como determinadas instâncias de Scripts de Perfil. Para obter mais informações de plano de fundo, consulte [User Agent e Client Hints](../../../client-side/atjs/user-agent-and-client-hints.md).

### Como passar as Client Hints para o [!DNL Adobe Target]

A partir do Node.js SDK v2.4.0 e do Java SDK v2.3.0, as Client Hints podem ser enviadas para [!DNL Target] por meio de chamadas `getOffers()`. As Client Hints devem ser incluídas no objeto `request.context`, juntamente com o Agente do Usuário.

>[!BEGINTABS]

>[!TAB SDK do Node.js]

```js {line-numbers="true"}
targetClient.getOffers({ 
    request: { 
        context: { 
            channel: "mobile" 
            userAgent: "Mozilla/5.0 (Linux; Android 12; Pixel 4a) AppleWebKit/537.36 (KHTML, like Gecko) Mobile Safari/537.36", 
            clientHints: { 
                mobile: "true", 
                platform: "Linux", 
                platformVersion: "12.1", 
                model: "Pixel 4a", 
                browserUAWithMajorVersion: "\"Not A;Brand\";v=\"98\", \"Chromium\";v=\"98\", \"Google Chrome\";v=\"98\"", 
                browserUAWithFullVersion: "\" Not A;Brand\";v=\"98.0.0.0\", \"Chromium\";v=\"98.0.4844.83\", \"Google Chrome\";v=\"98.0.4758.101\"", 
                bitness: "64", 
                architecture: "x86" 
            } 
        }, 
        execute: { 
            mboxes: [{ 
                name: "home", 
                index: 1 
            }] 
        } 
    } 
});
```

>[!TAB SDK Java]

```javascript {line-numbers="true"}
import com.adobe.target.delivery.v1.model.ClientHints; 
import com.adobe.target.delivery.v1.model.Context; 
import com.adobe.target.delivery.v1.model.ExecuteRequest; 
import com.adobe.target.edge.client.model.TargetDeliveryRequest; 

 
ClientHints clientHints = new ClientHints(); 
clientHints.setMobile(true); 
clientHints.setPlatform("macOS"); 
clientHints.setArchitecture("x86"); 
clientHints.setPlatformVersion("11.3.1"); 
clientHints.setBrowserUAWithMajorVersion( 
  "\" Not A;Brand\";v=\"99\", \"Chromium\";v=\"99\", \"Google Chrome\";v=\"99\""); 
String userAgent = 
  "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36"; 

 
TargetDeliveryRequest request = TargetDeliveryRequest.builder() 
        .execute(new ExecuteRequest().pageLoad(pageLoad)) 
        .context(new Context().clientHints(clientHints).userAgent(userAgent)) 
        .build(); 
```

>[!ENDTABS]

## Decisão no dispositivo

A tabela a seguir indica quais regras de público-alvo são ou não compatíveis com a decisão no dispositivo.

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

### Direcionamento geográfico para decisão no dispositivo

Para manter uma latência próxima de zero para atividades de decisão no dispositivo com públicos baseados em localização geográfica, a Adobe recomenda que você mesmo forneça os valores geográficos na chamada para `getOffers`. Faça isso definindo o objeto `Geo` no `Context` da solicitação. Isso significa que seu servidor precisará de uma maneira de determinar a localização de cada usuário final. Por exemplo, o servidor pode executar uma pesquisa de IP para Geo usando um serviço configurado por você. Alguns provedores de hospedagem, como a Google Cloud, fornecem essa funcionalidade por meio de cabeçalhos personalizados em cada `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB SDK do Node.js]

```js {line-numbers="true"}
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

>[!TAB SDK Java]

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

No entanto, se você não tiver a capacidade de executar pesquisas de IP para Geografia no servidor, mas ainda quiser executar decisões no dispositivo para solicitações `getOffers` que contenham públicos com base geográfica, isso também será suportado. A desvantagem dessa abordagem é que ela usará uma pesquisa remota de IP para Geo, o que adicionará latência a cada chamada `getOffers`. Essa latência deve ser menor que uma chamada remota `getOffers`, pois atinge um CDN localizado próximo ao seu servidor. Você deve **somente** fornecer o campo `ipAddress` no objeto `Geo` em `Context` de sua solicitação para que o SDK recupere a localização geográfica do endereço IP de seu usuário. Se qualquer outro campo além de `ipAddress` for fornecido, o SDK [!DNL Target] não buscará os metadados de localização geográfica para resolução.

>[!BEGINTABS]

>[!TAB SDK do Node.js]

```js {line-numbers="true"}
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

>[!TAB SDK Java]

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

## Decisão do lado do servidor

A tabela a seguir indica quais regras de público-alvo são ou não compatíveis com a decisão do lado do servidor.

| Regra de público-alvo | Decisão do lado do servidor |
| --- | --- |
| [Geografia](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Sim |
| [Rede](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Sim |
| [Móvel](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Sim |
| [Parâmetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Sim |
| [Sistema operacional](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Sim |
| [Páginas do site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Sim |
| [Navegador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Sim |
| [Perfil do visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Sim |
| [Fontes de Tráfego](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Sim |
| [Intervalo de tempo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Sim |
| [Públicos-alvo do Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (públicos-alvo do Adobe Audience Manager, Adobe Analytics e Adobe Experience Manager | Sim |
