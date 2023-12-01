---
keywords: implementar, implementar, configurar, configurar, api de atualização de perfil em massa
description: Obter dados em [!DNL Target] usando o [!UICONTROL API de atualização de perfil em massa].
title: Como posso obter dados no [!DNL Target] Usar o [!UICONTROL API de atualização de perfil em massa]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 5%

---

# API de atualização de perfil em massa

A variável [!DNL Adobe Target] [!UICONTROL API de atualização de perfil em massa] permite atualizar perfis de usuário para vários visitantes de um site em massa usando um arquivo em lote.

Usar o [!UICONTROL API de atualização de perfil em massa], você pode enviar dados detalhados do perfil do visitante na forma de parâmetros do perfil para muitos usuários para o [!DNL Target] de qualquer fonte externa. Fontes externas podem incluir os sistemas de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) ou POS (Point of Sale, ponto de venda), que normalmente não estão disponíveis em uma página da Web.

Compare o [!UICONTROL API de atualização de perfil em massa] com o [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Atributos do cliente] versus [!UICONTROL API de atualização de perfil em massa]

Essa opção é semelhante a [[!UICONTROL atributos do cliente]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) com algumas diferenças:

* [!UICONTROL Atributos do cliente] usar um upload do FTP. A variável [!UICONTROL API de atualização do perfil em massa do Target] usa uma API POST HTTP.
* [!UICONTROL Atributo do cliente] os dados podem ser compartilhados com [!DNL Analytics]. A variável [!UICONTROL Atualização de perfil em massa] é utilizável somente em [!DNL Target].
* [!UICONTROL Atributos do cliente] suporte à criação de um perfil para um usuário [!DNL Target] ainda não viu.
   * [!UICONTROL API de atualização de perfil em massa] v2: Não é necessário especificar todos os valores de parâmetro para cada `pcId`. Perfis são criados para qualquer `pcId` ou `mbox3rdPartyId` que não é encontrado em [!DNL Target].
   * [!UICONTROL API de atualização de perfil em massa] v1: O [!UICONTROL API de atualização de perfil em massa] atualizações existentes [!DNL Target] somente perfis. Se você estiver usando a v1, os perfis não serão criados para ausentes `pcIds` ou `mbox3rdPartyIds`.
* [!UICONTROL Atributos do cliente] Exigir a utilização do [!UICONTROL ID do Experience Cloud] (ECID) e o uso de uma ID de origem, como a ID do CRM ou a ID de fidelidade.
* A variável [!UICONTROL API de atualização de perfil em massa] exige a ID de TNT ou a `mbox3rdPartyId`.
* Não é possível enviar os seguintes caracteres em `mbox3rdPartyID`: sinal de adição (+) e barra invertida (/).

## Recursos

Para obter mais informações, consulte:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)