---
title: Introdução à API de entrega do Adobe Target
description: Como usar o [!UICONTROL Adobe Target Delivery API]?
keywords: api de entrega
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Introdução ao [!UICONTROL Adobe Target Delivery API]

Uma chamada de [!UICONTROL Target Delivery API] tem esta aparência:

```
curl -X POST \
  'https://`clientCode`.tt.omtrdc.net/rest/v1/delivery?client=`clientCode`&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

O `clientCode` pode ser recuperado da interface do usuário do [!DNL Target] navegando até **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

Antes de fazer uma chamada [!UICONTROL Target Delivery API], siga estas etapas para garantir que uma resposta contenha a experiência relevante para mostrar aos usuários finais:

1. Crie uma atividade [!DNL Target] (A/B, XT, AP ou Recommendations) usando o [Criador baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=pt-BR) ou o [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=pt-BR).
1. Use a API de Entrega para obter uma resposta para as mboxes usadas na atividade [!DNL Target] criada na Etapa 2.
1. Apresente a experiência ao visitante.
