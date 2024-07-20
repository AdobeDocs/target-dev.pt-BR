---
keywords: aplicativo móvel,sdk aep,aplicativo nativo,exibições da web,nativo;swift,sdk móvel da adobe experience platform,sdk móvel,código nativo
description: Saiba como implementar o [!DNL Adobe Target] com o [!DNL AEP Mobile SDK] em um aplicativo nativo com exibições da Web.
title: Implementar [!DNL Adobe Target] em um aplicativo móvel que usa código nativo com exibições da Web
feature: Implement Mobile
role: Developer
exl-id: 3dd2e1d7-c744-4ba8-aaa4-6c2fe64d01fa
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Implementar o [!DNL Target] com o [!DNL AEP Mobile SDK] em um aplicativo nativo com exibições da Web

Este artigo compartilha as práticas recomendadas para implementação do [!DNL Adobe Target] em um aplicativo móvel que usa código nativo com exibições da Web usando o [!DNL Adobe Experience Platform Mobile SDK].

Este artigo usa um aplicativo iOS de exemplo usando o [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} e uma integração [!DNL Target] escrita em [Swift do repositório GitHub](https://github.com/adobe/aep-sdk-app/){target=_blank}.

No mundo real, seu aplicativo corporativo provavelmente está usando visualizações da Web em seu aplicativo móvel. Uma exibição da Web é um container que carrega uma página da Web usando um URL. O contêiner é semelhante a uma janela do navegador sem controles. No iOS, o contêiner de visualização da Web funciona como um navegador Safari ao processar páginas da Web.

## Pré-requisitos

Para começar a usar o [!DNL Adobe Experience Platform Mobile SDK], você deve executar algumas tarefas de pré-requisito.

Para obter mais informações, consulte [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} na documentação [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank}.

## Sincronizar código nativo com visualizações da Web

O desafio ao implementar o [!DNL Target] em um aplicativo nativo com exibições da Web é que o [!DNL Adobe Experience Platform Mobile SDK] já gerou todos os identificadores necessários necessários para que as soluções do [!DNL Adobe] funcionem perfeitamente. No entanto, os identificadores ainda não estão visíveis para as visualizações da Web porque esses identificadores não estão no ambiente de plataforma nativo. Portanto, você deve criar uma ponte para transmitir alguns identificadores do SDK para as visualizações da Web, de modo que a identidade do visitante persista no ambiente da Web. Se isso não for feito corretamente, as visitas serão duplicadas, afetando seus relatórios.

Felizmente, o [!DNL Adobe Experience Platform Mobile SDK] fornece um método conveniente para gerar [!DNL Adobe] parâmetros necessários para que as exibições da Web sejam consumidas e mantidas para o mesmo visitante, mostrados no seguinte código de exemplo:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  print("appendedURL \(String(describing: appendedURL))")
  // load the url with ECID on the main thread
  DispatchQueue.main.async {
    let request = NSMutableURLRequest(url: appendedURL!)
    self.webView.load(request as URLRequest)
  }
});
```

Para obter mais informações sobre o método `Identity.appendTo` e ver um exemplo de como usar o método, consulte [Swift > Exemplo](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} na *Documentação do SDK móvel*.

Usando `Identity.appendTo`, esta URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

transforma em:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Como você pode ver, há um parâmetro `adobe_mc` anexado à URL. Esse parâmetro contém valores codificados para:

* TS=1660667205: O carimbo de data e hora atual. Esse carimbo de data e hora garante que a exibição da Web não receba valores expirados.
* MCMID=69624092487065093697422606480535692677: O [!UICONTROL Experience Cloud ID] (ECID). Também conhecida como MID ou [!UICONTROL Marketing Cloud ID] necessária para a identificação de visitantes entre soluções de [!DNL Adobe].
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: O [!UICONTROL Adobe Organization ID].

O `Identity.getUrlVariables` é um método [!DNL Adobe Experience Platform Mobile SDK] alternativo que retorna uma cadeia de caracteres devidamente formada que contém as variáveis de URL [!DNL Experience Cloud Identity Service]. Para obter mais informações, consulte [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} na *Referência de API de identidade*.

## Passar a ID da sessão [!DNL Target] para a experiência da mesma sessão

Uma etapa extra é necessária para fazer com que a jornada de usuário [!DNL Target] funcione perfeitamente nas exibições nativas e da Web. Esta etapa inclui a extração e a passagem da ID de Sessão do [!DNL Target] do [!DNL Adobe Experience Platform Mobile SDK] para as exibições da Web do aplicativo móvel.

O `Target.getSessionId` extrai a ID da Sessão que pode ser passada para a URL de exibição da Web como um parâmetro `mboxSession`:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Testar nas visualizações da Web

Os links de visualização da Web são gerados na página [!UICONTROL Activity detail] clicando no link [[!UICONTROL Adobe QA]](/help/dev/implement/mobile/target-mobile-preview.md) para exibir um pop-up para copiar cada link de visualização de experiência, semelhante ao seguinte:

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Os links de visualização da Web contêm `at_preview_index` e `at_preview_listed_activities_only` parâmetros adicionais. Copie esses parâmetros para criar links de visualização para dispositivos móveis com parâmetros de link da Web.

Por exemplo:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Depois de abrir o link em um navegador iOS Safari, seu aplicativo captura a URL na classe `AppDelegate` semelhante ao seguinte exemplo:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

Agora que você capturou todos os parâmetros necessários no aplicativo, é possível passá-los para a Web quando necessário:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

A saída final do link de exibição da Web pode ser semelhante a:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
