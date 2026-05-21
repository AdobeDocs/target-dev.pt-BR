---
keywords: implementar, implementar, configurar, configurar, api de atualização de perfil em massa
description: Obter dados em  [!DNL Target] usando o [!UICONTROL Bulk Profile Update API].
title: Como Obter Dados no  [!DNL Target] Usando o [!UICONTROL Bulk Profile Update API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
TQID: https://experienceleague.adobe.com/vBcIsBR6wwYr7MbRh7UJvt71ULDEq6iXVZ5spZlif-0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 221
ht-degree: 7%

---

# API de atualização de perfil em massa

O [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] permite atualizar perfis de usuário para vários visitantes de um site em massa usando um arquivo em lote.

Usando o [!UICONTROL Bulk Profile Update API], você pode enviar convenientemente dados detalhados do perfil do visitante na forma de parâmetros do perfil para muitos usuários para [!DNL Target] a partir de qualquer fonte externa. Fontes externas podem incluir os sistemas de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) ou POS (Point of Sale, ponto de venda), que normalmente não estão disponíveis em uma página da Web.

Compare [!UICONTROL Bulk Profile Update API] com [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Customer attributes] versus [!UICONTROL Bulk Profile Update API]

Esta opção é semelhante a [[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md), com algumas diferenças:

* [!UICONTROL Customer attributes] use um upload de FTP. O [!UICONTROL Target Bulk Profile Update API] usa uma API HTTP POST.
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