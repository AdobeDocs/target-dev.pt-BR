---
keywords: implementar, implementar, configurar, configurar, atributos do cliente
description: Obter dados em  [!DNL Target] usando atributos do cliente.
title: Como obtenho dados no  [!DNL Target] usando atributos do cliente?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
TQID: https://experienceleague.adobe.com/bzK915y7fvjfZjTkSK2QWHDzmIN9SdAQiEguiUlc-r8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 216
ht-degree: 13%

---

# Atributos do cliente

Os atributos do cliente permitem carregar dados de perfil do visitante via FTP para o [!DNL Adobe Experience Cloud]. Depois de carregado, use os dados em [!DNL Adobe Analytics] e [!DNL Adobe Target].

Os clientes da Target Standard podem aplicar cinco atributos, [!DNL Target Premium] os clientes podem aplicar 200 atributos.

## Formato

Um arquivo .csv com [!DNL Experience Cloud] IDs (ECIDs) e pares de nome/valor do atributo é carregado via FTP ou manualmente na interface do usuário da Experience Cloud.

## Exemplo de casos de uso

Seu CRM ou outro sistema interno armazena informações importantes que você deseja compartilhar com o [!DNL Adobe Experience Cloud], incluindo [!DNL Target] e [!DNL Analytics].

## Benefícios do método

O carregamento de dados do cliente cria uma entrada de perfil para esse visitante no Target, mesmo que [!DNL Target] ainda não tenha visto o visitante.

Os mesmos dados estão disponíveis automaticamente em [!DNL Target] e [!DNL Analytics].

O FTP pode ser um método de implementação mais simples que a API.

## Avisos

Os clientes da Target Standard podem aplicar cinco atributos, [!DNL Target Premium] os clientes podem aplicar 200 atributos

Podem atualizar valores via Atributos do cliente, não nas páginas.

Requer a implementação da Experience Cloud ID (ECID).

## Exemplos de código

Detalhes podem ser encontrados em [Criar uma fonte de atributo do cliente e carregar o arquivo de dados](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).

### Links para informações relevantes

[Crie uma fonte de atributo do cliente e carrega o arquivo de dados](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).
