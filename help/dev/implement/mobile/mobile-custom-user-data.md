---
keywords: aplicativo móvel, enviar dados aplicativo móvel, aplicativo móvel target, dados de usuários personalizados móveis, dados personalizados de aplicativo móvel
description: Saiba como enviar informações adicionais sobre a localização ou o usuário para o [!DNL Adobe Target] como pares nome-valor para ajudar você a criar públicos-alvo personalizados.
title: Como enviar dados personalizados do usuário em um aplicativo do iOS?
feature: Implement Mobile
exl-id: 9cf8e8fd-1898-43b1-b339-d7a21cb35d57
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 62%

---

# iOS - Enviar dados do usuário personalizados

É possível enviar informações adicionais sobre a localização ou o usuário para [!DNL Target] como pares nome-valor.

>[!IMPORTANT]
>
>Suporte para o [!DNL Adobe Mobile] versão 4.*x* Os SDKs terminaram em 31 de agosto de 2021 e não são mais recomendados para [!DNL Adobe Target] usuários de dispositivos móveis.
>
>A variável [Adobe Experience Platform SDK para aplicativos móveis](https://developer.adobe.com/client-sdks/documentation/){target=_blank} é a solução recomendada para [!DNL Adobe Experience Cloud] soluções e serviços em seus aplicativos móveis.

Essa informação pode ser usada para construir públicos-alvo personalizados (por exemplo, usuários com mais de 25.000 milhas) e em relatórios.

Há dois tipos de parâmetros que você pode enviar com um [!DNL Target] ligue para:

* **parâmetros de mbox**: os parâmetros da mbox não são persistentes entre as sessões.
* **Parâmetros de perfil**: os parâmetros do perfil são armazenados no armazenamento de perfil do visitante e são mantidos em todas as sessões. Os parâmetros da mbox não persistem. Enquanto algumas chaves são reservadas, tanto os parâmetros de perfil e de mbox podem ser pares de valores chave personalizados.

Embora algumas chaves são reservadas, tanto os parâmetros de perfil e de mbox podem conter pares de valores chave personalizados.

1. Crie um dicionário.

   Primeiro, crie um dicionário com os valores que você quer passar para o [!DNL Target]. Por conveniência, adicione isso dentro do método `welcomeMessageCampaign` para que você não tenha que se preocupar com o alcance.

   A seguir está uma amostra de dicionário. Você pode cipar e colar isto dentro de `(void)welcomeMessageCampaign`. Os valores para chaves como `userLevel` e `userMiles` são codificados neste exemplo. No geral, você passa nas variáveis correspondentes.

   ```
   NSDictionary *targetParams = [[NSDictionary alloc] initWithObjectsAndKeys: 
                                 @"platinum",@"userLevel", 
                                 @26500,@"userMiles", 
                                 @"1067007",@"entity.id", 
                                 @"dealsapp.qa", @"host", 
                                 @"fashion",@"entity.categoryId", 
                                 @"millenial", @"profile.persona", 
                                 @"cohort_5", @"profile.cohort", 
                                 nil];
   ```

   * Chaves com o prefixo profile (por exemplo, `profile.persona`) são armazenadas no perfil do usuário.

     Estes atributos e perfil podem ser usados entre diferentes atividades e canais.

   * Chaves que não possuem nenhum perfil (por exemplo, `userMiles`) são parâmetros mbox.

     Estes parâmetros só estão disponíveis durante a sessão.

   * Chaves com o prefixo entity (por exemplo, `entity.category.id`) são usadas para recomendações de produto.

1. Verifique os dados.
   1. Na aplicação `didFinishLaunchingWithOptions`, exclua o comentário ou adicione `[ADBMobile setDebugLogging:YES];`.

      Isso imprime relatórios detalhados de depuração.
   1. Compile o aplicativo.
   1. Verifique se os parâmetros foram passados na chamada de definição.

      Procure pelo seu nome de local de definição no seu console de depuração. Você verá uma chamada para `YOUR-CLIENT-CODE.tt.omtrdc.net` com todos parâmetros que você acabou de passar.

      (Clique na imagem para expandir até a largura total.)

      ![Local do Target no console de depuração](/help/dev/implement/mobile/assets/mobile-debug.png "Local do Target no console de depuração"){zoom=&quot;yes&quot;}

   Você pode construir audiência e restringir ou definir a exibição de conteúdo usando estes parâmetros no [!DNL Target].
