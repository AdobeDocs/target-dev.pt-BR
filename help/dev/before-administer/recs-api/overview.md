---
title: O que é a API do Adobe Recommendations?
description: Este guia orienta os desenvolvedores na prática usando as APIs do Adobe Target Recommendations para configurar e gerenciar catálogos e critérios personalizados do Recommendations, além de usar a API de entrega para recuperar o conteúdo das recomendações.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail:
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
TQID: 'https://experienceleague.adobe.com/-bWsxWNZK7LXp0VvKZmsZc68jXcit57v7Wki9hR3wH4'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
    internal-label: Administration and configuration
  - id: f69bc5f1-ebdb-4306-a281-f2e77daf734c
    internal-label: Activities and tests
subfeature_v2:
  - id: ed58f4a1-16eb-4c8c-b505-be9da766a9ec
    internal-label: Recommendations
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
    internal-label: Overview
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 3%
---
# Visão geral da API do Adobe Recommendations

As APIs relevantes para o Recommendations incluem [APIs de administrador](../../before-administer/target-api-overview.md) que permitem:

* Gerencie seu catálogo de produtos ou conteúdo recomendáveis
* Gerencie suas atividades e algoritmos do Recommendations

Usando a [API de entrega](../../implement/delivery-api/overview.md) do Target com o Recommendations, você também pode:

* Recupere recomendações em objetos JSON, HTML ou XML para que elas possam ser exibidas na Web, em dispositivos móveis, em emails, na Internet das Coisas (IOT) e em outros canais.

## Descrição

Este guia sobre as APIs do Recommendations orienta os desenvolvedores sobre práticas práticas usando as APIs do Recommendations para configurar e gerenciar catálogos e critérios personalizados do Recommendations, além de usar a API de entrega para recuperar o conteúdo das recomendações. Ao final, você poderá:

* Configurar e gerenciar entidades usando a API do Recommendations
* Configurar e gerenciar critérios personalizados usando a API do Recommendations
* Entenda como usar o Recommendations com a API de entrega para usar os resultados das recomendações em dispositivos que não sejam HTML

## Público-alvo

Este guia tem como objetivo desenvolvedores novatos nas APIs do Target ou nas APIs do Recommendations.

## Pré-requisitos {#prerequisites}

As APIs de administrador do Target exigem [configuração de autenticação do Adobe](../configure-authentication.md). Verifique se isso está configurado antes de usar a API do Recommendations.

## Recursos

Observe os seguintes recursos, que são necessários para entender este guia e segui-lo com êxito:

| Recurso | Detalhes |
| --- | --- |
| Postman | Obtenha o [aplicativo Postman](https://www.postman.com/downloads/) para seu sistema operacional. O Postman Basic é gratuito com a criação da conta. Embora não seja necessário para usar as APIs do Adobe Target em geral, o Postman facilita os fluxos de trabalho da API, e a Adobe Target fornece várias coleções do Postman para ajudar a executar suas APIs e saber como elas operam. O restante deste guia pressupõe conhecimento prático do Postman. Para obter ajuda, consulte a [documentação do Postman](https://learning.getpostman.com/). |
| Referências | Familiaridade com os seguintes recursos é presumida no restante deste guia:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentação da API de perfil e de administrador do Target](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Documentação da API do Recommendations](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
