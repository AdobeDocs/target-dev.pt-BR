---
keywords: implementar, implementar, configurar, configurar, atributos do cliente
description: Obter dados em [!DNL Target] usando atributos do cliente.
title: Como posso obter dados no [!DNL Target] Está usando os atributos do cliente?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 24%

---

# Atributos do cliente

Os atributos do cliente permitem que você carregue os dados de perfil do visitante via FTP à [!DNL Adobe Experience Cloud]. Após feito o upload, utilize os dados em [!DNL Adobe Analytics] e [!DNL Adobe Target].

Os clientes do Target Standard podem aplicar cinco atributos, [!DNL Target Premium] os clientes podem aplicar 200 atributos.

## Formato

Um arquivo .csv com [!DNL Experience Cloud] IDs (ECIDs) e pares de nome/valor do atributo são carregados via FTP ou manualmente na interface do usuário do Experience Cloud.

## Exemplo de casos de uso

Seu CRM ou outro sistema interno armazena informações valiosas que você deseja compartilhar [!DNL Adobe Experience Cloud], incluindo [!DNL Target] e [!DNL Analytics].

## Benefícios do método

Fazer upload dos dados do cliente cria uma entrada de perfil para esse visitante no Target, mesmo que [!DNL Target] ainda não viu o visitante.

Os mesmos dados são disponibilizados automaticamente no [!DNL Target] e [!DNL Analytics].

O FTP pode ser um método de implementação mais simples que a API.

## Avisos

Os clientes do Target Standard podem aplicar cinco atributos, [!DNL Target Premium] os clientes podem aplicar 200 atributos

Podem atualizar valores via Atributos do cliente, não nas páginas.

Requer a implementação da Experience Cloud ID (ECID).

## Exemplos de código

Os detalhes podem ser encontrados em [Crie uma fonte de atributo do cliente e faça upload do arquivo de dados](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).

### Links para informações relevantes

[Crie uma fonte de atributo do cliente e faça upload do arquivo de dados](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).
