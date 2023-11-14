---
title: O que é a API do Adobe Recommendations?
description: Este guia orienta os desenvolvedores na prática usando as APIs do Adobe Target Recommendations para configurar e gerenciar catálogos e critérios personalizados do Recommendations, além de usar a API de entrega para recuperar o conteúdo das recomendações.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# Visão geral da API do Adobe Recommendations

As APIs relevantes para o Recommendations incluem [APIs de administrador](../../before-administer/target-api-overview.md) que permitem:

* Gerencie seu catálogo de produtos ou conteúdo recomendáveis
* Gerencie algoritmos e atividades do Recommendations

Uso do Target [API de entrega](../../implement/delivery-api/overview.md) com o Recommendations, também é possível:

* Recupere recomendações em objetos JSON, HTML ou XML para que elas possam ser exibidas na Web, em dispositivos móveis, em emails, na Internet das Coisas (IOT) e em outros canais.

## Descrição

Este guia sobre as APIs do Recommendations orienta os desenvolvedores na prática usando as APIs do Recommendations para configurar e gerenciar catálogos do Recommendations e critérios personalizados, bem como usando a API de entrega para recuperar o conteúdo das recomendações. Ao final, você poderá:

* Configurar e gerenciar entidades usando a API do Recommendations
* Configurar e gerenciar critérios personalizados usando a API do Recommendations
* Entenda como usar o Recommendations com a API de entrega para usar os resultados das recomendações em dispositivos não HTML

## Público-alvo

Este guia destina-se a desenvolvedores novatos nas APIs do Target ou nas APIs do Recommendations.

## Pré-requisitos {#prerequisites}

As APIs de administrador do Target exigem [configuração da autenticação Adobe](../configure-authentication.md). Verifique se isso está configurado antes de usar a API do Recommendations.

## Recursos

Observe os seguintes recursos, que são necessários para entender este guia e segui-lo com êxito:

| Recurso | Detalhes |
| --- | --- |
| Postman | Obtenha o [aplicativo Postman](https://www.postman.com/downloads/) para o seu sistema operacional. O Postman Basic é gratuito com a criação da conta. Embora não seja necessário para usar as APIs do Adobe Target em geral, o Postman facilita os fluxos de trabalho da API, e a Adobe Target fornece várias coleções do Postman para ajudar a executar suas APIs e saber como elas operam. O restante deste guia pressupõe conhecimento prático do Postman. Para obter ajuda, consulte o [Documentação do Postman](https://learning.getpostman.com/). |
| Referências | Familiaridade com os seguintes recursos é presumida no restante deste guia:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentação da API de administrador e perfil do Target](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Documentação da API do Recommendations](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
