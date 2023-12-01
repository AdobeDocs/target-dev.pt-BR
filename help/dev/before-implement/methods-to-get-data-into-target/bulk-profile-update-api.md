---
keywords: implementar, implementar, configurar, configurar, api de atualização de perfil em massa
description: Obter dados em [!DNL Target] usando o [!UICONTROL API de atualização de perfil em massa].
title: Como posso obter dados no [!DNL Target] Usar o [!UICONTROL API de atualização de perfil em massa]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 24%

---

# API de atualização de perfil em massa

Pela API, envie um arquivo .csv para [!DNL Adobe Target] com atualizações de perfil de visitante para muitos visitantes. Cada perfil do visitante pode ser atualizado com vários atributos de perfil na página em uma chamada.

Essa opção é semelhante a [!UICONTROL atributos do cliente] com algumas diferenças:

* [!UICONTROL Atributos do cliente] usar um upload do FTP. A variável [!UICONTROL API de atualização do perfil em massa do Target] usa uma API POST HTTP.
* [!UICONTROL Atributo do cliente] os dados podem ser compartilhados com [!DNL Analytics]. A Atualização de perfil em massa é utilizável somente no [!DNL Target].
* [!UICONTROL Atributos do cliente] suporte à criação de um perfil para um usuário [!DNL Target] ainda não viu.
   * [!UICONTROL API de atualização de perfil em massa] v2: Não é necessário especificar todos os valores de parâmetro para cada `pcId`. Perfis são criados para qualquer `pcId` ou `mbox3rdPartyId` que não é encontrado em [!DNL Target].
   * [!UICONTROL API de atualização de perfil em massa] v1: O [!UICONTROL API de atualização de perfil em massa] atualizações existentes [!DNL Target] somente perfis. Se você estiver usando a v1, os perfis não serão criados para ausentes `pcIds` ou `mbox3rdPartyIds`.
* [!UICONTROL Atributos do cliente] Exigir a utilização do [!UICONTROL ID do Experience Cloud] (ECID) e o uso de uma ID de origem, como a ID do CRM ou a ID de fidelidade.
* A variável [!UICONTROL API de atualização de perfil em massa] exige a ID de TNT ou a `mbox3rdPartyId`.
* Não é possível enviar os seguintes caracteres em `mbox3rdPartyID`: sinal de adição (+) e barra invertida (/).

## Formato

O arquivo .csv deve fazer referência a cada visitante por meio de [!DNL Target] PCID ou `mbox3rdPartyId`. A variável [!UICONTROL ID do Experience Cloud] (ECID) não é compatível. Todos os atributos/valores de perfil são criados e atualizados via API. Os detalhes de formato estão disponíveis na documentação da API.

## Exemplo de casos de uso

Seu CRM ou outro sistema interno armazena dados valiosos sobre seus visitantes que você deseja atualizar consistentemente para [!DNL Target], sem expor os dados do perfil na implementação da página.

## Benefícios do método

* Nenhum limite sobre o número de atributos de perfil.
* Os atributos de perfil enviados pelo site podem ser atualizados por meio da API e do oposto.

## Avisos

* O tamanho do arquivo em lote deve ser menor que 50 MB. Além disso, o número total de linhas não deve ultrapassar 500.000 por carregamento.
* As atualizações geralmente ocorrem em menos de uma hora, mas podem levar até 24 horas para serem refletidas.
* Não há limite para o número ou as linhas que você pode fazer upload por um período de 24 horas em lotes subsequentes. No entanto, o processo de ingestão pode ter o fluxo controlado em horário comercial, para garantir que outros processos sejam executados com eficiência.
* Chamadas de atualização em lote V2 consecutivas sem chamadas da mbox entre elas para o mesmo `thirdPartyIds` substitua as propriedades atualizadas na primeira chamada de atualização de lote.

## Recursos

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)