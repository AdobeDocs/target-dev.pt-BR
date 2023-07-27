---
keywords: aplicativo móvel, local de aplicativo móvel, aplicativo móvel target, métricas de sucesso no aplicativo móvel
description: Visualize exemplos de código para ajudá-lo a saber como criar locais e métricas de sucesso em aplicativos iOS para que você possa usar [!DNL Adobe Target] para personalizar e otimizar seu aplicativo.
title: Como criar [!DNL Target] Locais e métricas de sucesso em um aplicativo iOS?
feature: Implement Mobile
exl-id: 755c8b26-5c60-48fc-9e7e-5e97a25edb78
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 67%

---

# iOS - criar um [!DNL Target] localização e métrica de sucesso

Para usar [!DNL Target] no aplicativo móvel, crie um local e métrica de sucesso.

>[!IMPORTANT]
>
>Suporte para o [!DNL Adobe Mobile] versão 4.*x* Os SDKs terminaram em 31 de agosto de 2021 e não são mais recomendados para [!DNL Adobe Target] usuários de dispositivos móveis.
>
>A variável [Adobe Experience Platform SDK para aplicativos móveis](https://developer.adobe.com/client-sdks/documentation/){target=_blank} é a solução recomendada para [!DNL Adobe Experience Cloud] soluções e serviços em seus aplicativos móveis.

Esta seção inclui amostras de código que podem ser usadas como molde para seu aplicativo. As amostras nesta seção contém código para o iOS. Os mesmos padrões se aplicam ao Android. Sintaxe específica para Android pode ser encontrada no guia de soluções [](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/target-main.html)Android SDK 4.x para Experience Cloud.

>[!NOTE]
>
>Consulte a [Documentação para dispositivos móveis](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-target-methods.html) para obter uma lista de todos os [!DNL Target] métodos.

Para criar um [!DNL Target] no aplicativo e fazer uma solicitação, há dois métodos principais:

* `targetCreateRequestWithName`
* `targetLoadRequest`

1. Criar um [!DNL Target] localização.

   Este é um exemplo de chamada para criar uma solicitação:

   ```
   // make your request 
   ADBTargetLocationRequest *myRequest = [ADBMobile targetCreateRequestWithName:@"heroBanner" 
                                                    defaultContent:@"default.png" 
                                                    parameters:nil];
   ```

   | Parâmetro | Descrição |
   |---|---|
   | `ADBTargetLocationRequest *myRequest` | Substitua `myRequest` com o nome de seu `targetLocation` no aplicativo. |
   | `targetCreateRequestWithName:@"heroBanner"` | Substitua `heroBanner` com o nome de seu `targetLocation` no Target. Este é o mesmo nome da mbox. Este banner herói aparece na interface do Target. |
   | `defaultContent:@"default.png"` | Substitua `default.png` com o valor que o aplicativo usa se o Target não responder. |
   | `parameters:nil` | Especifique os parâmetros de perfil ou mbox. Veja mais informações na seção &quot;Passando dados personalizados&quot;. |

   Este é um exemplo de chamada para carregar a solicitação:

   ```
   // load your request 
   [ADBMobile targetLoadRequest:myRequest callback:^(NSString *content) { 
                                        // do something with content 
                                        heroImage.image = [UIImage imageNamed:content]; 
   }];
   ```

   | Parâmetro | Descrição |
   |---|---|
   | `targetLoadRequest:myRequest` | Substitua `myRequest` com o nome de seu `targetLocation` no aplicativo. |
   | `NSString *content` | Substitua content com o conteúdo real retornando da Adobe. A cadeia de caracteres pode ser XML, JSON ou uma cadeia de caracteres simples. Use esta seção do código para definir variáveis, caminhos de imagem, ver fluxos de controlador, pontos de transação ou qualquer outra coisa que queira fazer. O Target irá retornar o conteúdo inserido na interface do usuário no exato mesmo formato. |
   | `heroImage.image = [UIImage imageNamed:content];` | Por exemplo: obtém o conteúdo e define o caminho para a imagem herói. |

1. Criar uma métrica de sucesso.

   O método `targetCreateOrderConfirmRequestWithName` pode ser usado para rastrear uma métrica de conversão/sucesso no seu aplicativo.

   ```
   ADBTargetLocationRequest *req = [ADBMobile targetCreateOrderConfirmRequestWithName: "orderConfirm" 
                                              orderId: orderId 
                                              orderTotal: @"39.95" 
                                              productPurchasedId: _galleryItem.title 
                                              parameters: nil]; 
   [ADBMobile targetLoadRequest: req callback: nil];
   ```

   | Parâmetro | Descrição |
   |---|---|
   | `orderId` | Substitua com uma variável dinâmica representando uma ID de pedido única. |
   | `@"39.95"` | Substitua com uma variável dinâmica representando um total de pedido único. |
   | `_galleryItem.title` | Substitua com uma variável dinâmica representando uma lista delimitada por vírgula de produtos comprados. |
   | `parameters: nil` | Dicionário opcional de parâmetros adicionais. |

1. Compile o aplicativo.

   Resultado da etapa Após criar o local de definição com sucesso e marcar uma métrica de sucesso, crie um teste A/B. A atividade pode ser criada usando o compositor de experiência baseado em formulários.
