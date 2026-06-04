---
title: Introdução à API de entrega do Adobe Target
description: Como usar a [!UICONTROL API de entrega do Adobe Target]?
keywords: api de entrega
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/DC-YVq6VfAaqMU1utmIMw73gzp4PIJgQjaS0a8FQEO4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 132
ht-degree: 1%

---

# Introdução à [!UICONTROL API de entrega do Adobe Target]

Uma chamada da [!UICONTROL API de Entrega do Target] tem esta aparência:

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

O `clientCode` pode ser recuperado da interface do usuário [!DNL Target] navegando até **[!UICONTROL Administração]** > **[!UICONTROL Implementação]**.

Antes de fazer uma chamada da [!UICONTROL API de entrega do Target], siga estas etapas para garantir que uma resposta contenha a experiência relevante para mostrar aos usuários finais:

1. Crie uma atividade [!DNL Target] (A/B, XT, AP ou Recommendations) usando o [Criador baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=pt-BR) ou o [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=pt-BR).
1. Use a API de Entrega para obter uma resposta para as mboxes usadas na atividade [!DNL Target] criada na Etapa 2.
1. Apresente a experiência ao visitante.
