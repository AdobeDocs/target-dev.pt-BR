---
keywords: implementar, implementar, configurar, configurar, api de atualização de perfil em massa
description: Obter dados em  [!DNL Target] usando o [!UICONTROL Bulk Profile Update API].
title: Como Obter Dados no  [!DNL Target] Usando o [!UICONTROL Bulk Profile Update API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 7%

---

# API de atualização de perfil em massa

O [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] permite atualizar perfis de usuário para vários visitantes de um site em massa usando um arquivo em lote.

Usando o [!UICONTROL Bulk Profile Update API], você pode enviar convenientemente dados detalhados do perfil do visitante na forma de parâmetros do perfil para muitos usuários para [!DNL Target] a partir de qualquer fonte externa. Fontes externas podem incluir os sistemas de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) ou POS (Point of Sale, ponto de venda), que normalmente não estão disponíveis em uma página da Web.

Compare [!UICONTROL Bulk Profile Update API] com [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Customer attributes] versus [!UICONTROL Bulk Profile Update API]

Esta opção é semelhante a [[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md), com algumas diferenças:

* [!UICONTROL Customer attributes] use um upload de FTP. O [!UICONTROL Target Bulk Profile Update API] usa uma API POST HTTP.
* [!UICONTROL Customer attribute] dados podem ser compartilhados com [!DNL Analytics]. O [!UICONTROL Bulk Profile Update] é utilizável somente em [!DNL Target].
* O suporte do [!UICONTROL Customer attributes] à criação de um perfil para um usuário [!DNL Target] ainda não foi visto.
   * [!UICONTROL Bulk Profile Update API] v2: Você não precisa especificar todos os valores de parâmetro para cada `pcId`. Perfis são criados para qualquer `pcId` ou `mbox3rdPartyId` que não seja encontrado em [!DNL Target].
   * [!UICONTROL Bulk Profile Update API] v1: O [!UICONTROL Bulk Profile Update API] atualiza apenas os perfis [!DNL Target] existentes. Se você estiver usando a v1, os perfis não serão criados para `pcIds` ou `mbox3rdPartyIds` ausentes.
* [!UICONTROL Customer attributes] exigem o uso de [!UICONTROL Experience Cloud ID] (ECID) e o uso de uma ID de origem, como a ID do CRM ou a ID de Fidelidade.
* O [!UICONTROL Bulk Profile Update API] requer ID de TNT ou `mbox3rdPartyId`.
* Não é possível enviar os seguintes caracteres em `mbox3rdPartyID`: sinal de adição (+) e barra invertida (/).

## Recursos

Para obter mais informações, consulte:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)