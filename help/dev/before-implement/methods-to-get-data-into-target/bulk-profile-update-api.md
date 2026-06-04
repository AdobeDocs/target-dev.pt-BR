---
keywords: implementar, implementar, configurar, configurar, api de atualização de perfil em massa
description: Obtenha dados em  [!DNL Target] usando a [!UICONTROL API de Atualização de Perfil em Massa].
title: Como obtenho dados no  [!DNL Target] usando a [!UICONTROL API de atualização de perfil em massa]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
TQID: https://experienceleague.adobe.com/vBcIsBR6wwYr7MbRh7UJvt71ULDEq6iXVZ5spZlif-0
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 284
ht-degree: 5%

---

# API de atualização de perfil em massa

A [!DNL Adobe Target] [!UICONTROL API de Atualização de Perfil em Massa] permite atualizar perfis de usuário para vários visitantes de um site em massa usando um arquivo em lote.

Usando a [!UICONTROL API de Atualização de Perfil em Massa], você pode enviar dados detalhados do perfil do visitante na forma de parâmetros do perfil de muitos usuários para [!DNL Target] de qualquer fonte externa. Fontes externas podem incluir os sistemas de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) ou POS (Point of Sale, ponto de venda), que normalmente não estão disponíveis em uma página da Web.

Compare a [!UICONTROL API de Atualização de Perfil em Massa] com a [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Atributos do cliente] versus a [!UICONTROL API de Atualização de Perfil em Massa]

Esta opção é semelhante aos [[!UICONTROL atributos do cliente]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md), com algumas diferenças:

* [!UICONTROL Os atributos do cliente] usam um upload de FTP. A [!UICONTROL API de Atualização do Perfil em Massa do Target] usa uma API HTTP POST.
* Os dados do [!UICONTROL Atributo do cliente] podem ser compartilhados com [!DNL Analytics]. A [!UICONTROL Atualização de Perfil em Massa] só pode ser usada em [!DNL Target].
* [!UICONTROL Os atributos do cliente] oferecem suporte à criação de um perfil para um usuário [!DNL Target] que ainda não foi visto.
   * [!UICONTROL API de Atualização de Perfil em Massa] v2: não é necessário especificar todos os valores de parâmetro para cada `pcId`. Perfis são criados para qualquer `pcId` ou `mbox3rdPartyId` que não seja encontrado em [!DNL Target].
   * [!UICONTROL API de Atualização de Perfil em Massa] v1: A [!UICONTROL API de Atualização de Perfil em Massa] atualiza apenas os [!DNL Target] perfis existentes. Se você estiver usando a v1, os perfis não serão criados para `pcIds` ou `mbox3rdPartyIds` ausentes.
* [!UICONTROL Os atributos do cliente] exigem o uso da [!UICONTROL Experience Cloud ID] (ECID) e o uso de uma ID de origem, como a ID do CRM ou a ID de Fidelidade.
* A [!UICONTROL API de Atualização de Perfil em Massa] requer ID de TNT ou `mbox3rdPartyId`.
* Não é possível enviar os seguintes caracteres em `mbox3rdPartyID`: sinal de adição (+) e barra invertida (/).

## Recursos

Para obter mais informações, consulte:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)