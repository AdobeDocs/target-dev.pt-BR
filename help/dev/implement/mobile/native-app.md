---
keywords: aplicativo móvel,sdk aep,aplicativo nativo,exibições da web,nativo;swift,sdk móvel da adobe experience platform,sdk móvel,código nativo
description: Saiba como implementar o [!DNL Adobe Target] com o [!DNL AEP Mobile SDK] em um aplicativo nativo com visualizações da web.
title: Implementar [!DNL Adobe Target] em um aplicativo móvel que usa código nativo com visualizações da web
feature: Implement Mobile
role: Developer
source-git-commit: c0fda36cb5472d71438c47b8b484716003da4214
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---


# Implementar [!DNL Target] com o [!DNL AEP Mobile SDK] em um aplicativo nativo com visualizações da web

Este artigo compartilha as práticas recomendadas para implementação do [!DNL Adobe Target] em um aplicativo móvel que usa código nativo com visualizações da web usando o [!DNL Adobe Experience Platform Mobile SDK].

Este artigo usa um aplicativo iOS de exemplo usando o [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} and a [!DNL Target] integration written in [Swift from the GitHub repository](https://github.com/adobe/aep-sdk-app/){target=_blank}.

No mundo real, seu aplicativo corporativo provavelmente está usando visualizações da Web em seu aplicativo móvel. Uma exibição da Web é um container que carrega uma página da Web usando um URL. O contêiner é semelhante a uma janela do navegador sem controles. No iOS, o contêiner de visualização da Web funciona como um navegador Safari ao processar páginas da Web.

## Pré-requisitos

Para começar a usar o [!DNL Adobe Experience Platform Mobile SDK], é necessário executar algumas tarefas de pré-requisito.

Para obter mais informações, consulte [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in the [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank} documentação.

## Sincronizar código nativo com visualizações da Web

O desafio ao implementar [!DNL Target] em um aplicativo nativo com visualizações da web, o [!DNL Adobe Experience Platform Mobile SDK] já gerou todos os identificadores necessários para [!DNL Adobe] para funcionar perfeitamente. No entanto, os identificadores ainda não estão visíveis para as visualizações da Web porque esses identificadores não estão no ambiente de plataforma nativo. Portanto, você deve criar uma ponte para transmitir alguns identificadores do SDK para as visualizações da Web, de modo que a identidade do visitante persista no ambiente da Web. Se isso não for feito corretamente, as visitas serão duplicadas, afetando seus relatórios.

Felizmente, o [!DNL Adobe Experience Platform Mobile SDK] O fornece um método conveniente para gerar [!DNL Adobe] parâmetros necessários para que as exibições da web consumam e persistam para o mesmo visitante, mostrados no seguinte código de amostra:

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

Para obter mais informações sobre o `Identity.appendTo` e para ver um exemplo de como usar o método, consulte [Swift > Exemplo](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} no *Documentação do SDK móvel*.

Usar `Identity.appendTo`, este URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

transforma em:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Como você pode ver, há `adobe_mc` parâmetro anexado ao URL. Esse parâmetro contém valores codificados para:

* TS=1660667205: O carimbo de data e hora atual. Esse carimbo de data e hora garante que a exibição da Web não receba valores expirados.
* MCMID=69624092487065093697422606480535692677: A [!UICONTROL ID do Experience Cloud] (ECID). Também conhecida como MID ou [!UICONTROL ID DO MARKETING CLOUD] obrigatório para [!DNL Adobe] identificação de visitantes entre soluções.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: a [!UICONTROL ID da organização Adobe].

A variável `Identity.getUrlVariables` é uma alternativa [!DNL Adobe Experience Platform Mobile SDK] que retorna uma string formada adequadamente que contém a variável [!DNL Experience Cloud Identity Service] Variáveis de URL. Para obter mais informações, consulte [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} no *Referência da API de identidade*.

## Passe o [!DNL Target] ID de sessão para experiência de mesma sessão

É necessária uma etapa extra para tornar o [!DNL Target] o user jornada funciona perfeitamente nas visualizações nativas e da web. Esta etapa inclui extrair e passar o [!DNL Target] ID da sessão do [!DNL Adobe Experience Platform Mobile SDK] para as visualizações da web do aplicativo móvel.

A variável `Target.getSessionId` extrai a ID da sessão que pode ser passada para o URL de exibição da Web como um `mboxSession` parâmetro:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Testar nas visualizações da Web

Os links de visualização da Web são gerados no [!UICONTROL Detalhes da atividade] clicando no link [[!UICONTROL ADOBE QA] link](/help/dev/implement/mobile/target-mobile-preview.md) para exibir um pop-up para copiar cada link de visualização de experiência, semelhante ao seguinte:

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Os links de visualização da Web contêm informações adicionais `at_preview_index` e `at_preview_listed_activities_only` parâmetros. Copie esses parâmetros para criar links de visualização para dispositivos móveis com parâmetros de link da Web.

Por exemplo:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Depois de abrir o link em um navegador iOS Safari, seu aplicativo captura o URL em seu `AppDelegate` classe semelhante ao exemplo a seguir:

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
