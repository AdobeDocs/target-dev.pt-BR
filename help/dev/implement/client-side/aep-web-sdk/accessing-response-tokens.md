---
title: Acesso aos tokens de resposta usando o Adobe Experience Platform Web SDK
description: Saiba como acessar tokens de resposta com o  [!DNL Adobe Experience Platform Web SDK].
keywords: personalization;target;adobe target;renderDecisions;sendEvent;decisionScopes;result.decision,response tokens;
feature: AEP Web SDK
source-git-commit: f010ca54aac3c2a644a77fb2f88aff1996f6ddfe
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Acesso aos tokens de resposta

O conteúdo do Personalization retornado de [!DNL Adobe Target] inclui [tokens de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que são detalhes sobre a atividade, a oferta, a experiência, o perfil do usuário, as informações geográficas e muito mais. Esses detalhes podem ser compartilhados com ferramentas de terceiros ou usados para depuração. Os tokens de resposta podem ser configurados na interface do usuário [!DNL Target].

Para acessar qualquer conteúdo de personalização, forneça uma função de retorno de chamada ao enviar um evento. Esse retorno de chamada é chamado depois que o SDK recebe uma resposta bem-sucedida do servidor. Seu retorno de chamada recebe um objeto `result`, que pode conter uma propriedade `propositions` contendo qualquer conteúdo de personalização retornado. Veja abaixo um exemplo de como fornecer uma função de retorno de chamada.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

Neste exemplo, `result.propositions`, se existir, é uma matriz contendo propostas de personalização relacionadas ao evento. Consulte [Renderização do conteúdo de personalização](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content) para obter mais informações sobre o conteúdo de `result.propositions.`

Suponha que você queira coletar todos os nomes de atividade de todas as propostas que foram renderizadas automaticamente pelo SDK da Web e enviá-las para uma única matriz. Em seguida, você pode enviar o array único para terceiros. Neste caso:

1. Extrair apresentações do objeto `result`.
1. Execute um loop em cada proposta.
1. Determine se o SDK renderizou a proposta.
1. Nesse caso, percorra cada item na proposta.
1. Recupere o nome da atividade da propriedade `meta`, que é um objeto que contém tokens de resposta.
1. Transfira o nome da atividade para um storage.
1. Envie os nomes da atividade para terceiros.

Seu código seria semelhante ao seguinte:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
