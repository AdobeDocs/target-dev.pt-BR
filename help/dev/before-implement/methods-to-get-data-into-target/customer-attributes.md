---
keywords: implementar, implementar, configurar, configurar, atributos do cliente
description: Obter dados em  [!DNL Target] usando atributos do cliente.
title: Como obtenho dados no  [!DNL Target] usando atributos do cliente?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 14%

---

# Atributos do cliente

Os atributos do cliente permitem carregar dados de perfil do visitante via FTP para o [!DNL Adobe Experience Cloud]. Depois de carregado, use os dados em [!DNL Adobe Analytics] e [!DNL Adobe Target].

Os clientes da Target Standard podem aplicar cinco atributos, [!DNL Target Premium] os clientes podem aplicar 200 atributos.

## Formato

Um arquivo .csv com [!DNL Experience Cloud] IDs (ECIDs) e pares de nome/valor de atributo é carregado via FTP ou manualmente na interface do usuário do Experience Cloud.

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
