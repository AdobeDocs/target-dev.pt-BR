---
keywords: implementar, implementar, configurar, configurar, atualização de perfil em massa
description: Obter dados em [!DNL Target] usando a API de atualização de perfil em massa.
title: Como posso obter dados no [!DNL Target] Usando a API de atualização de perfil em massa?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 3ae2391dea9994c0ddc1df39d74cccf6e067c1a4
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 59%

---

# API de atualização de perfil em massa

Pela API, envie um arquivo .csv para [!DNL Adobe Target] com atualizações de perfil de visitante para muitos visitantes. Cada perfil do visitante pode ser atualizado com vários atributos de perfil na página em uma chamada.

Essa opção é semelhante aos Atributos do cliente, com algumas diferenças:

* Os atributos do cliente usam um upload de FTP enquanto a [!UICONTROL API de atualização do perfil em massa do Target] usa uma API POST HTTP.
* Os dados de atributo do cliente podem ser compartilhados com o [!DNL Analytics]. [!UICONTROL A Atualização de perfil em massa é utilizável somente no Target.]
* Os atributos do cliente permitem criar um perfil para um usuário [!DNL Target] ainda não viu. A API de atualização de perfil em massa é atualizada [!DNL Target] somente perfis.
* Os atributos do cliente exigem o uso da ID de Experience Cloud (ECID) e o uso de uma ID de origem, como a ID de CRM ou a ID de fidelidade.
* A API de atualização do perfil em massa requer ID de TNT ou `mbox3rdPartyId`.
* Não é possível enviar os seguintes caracteres em `mbox3rdPartyID`: sinal de adição (+) e barra invertida (/).

## Formato

O arquivo .csv deve fazer referência a cada visitante por meio de [!DNL Target] PCID ou `mbox3rdPartyId`. A Experience Cloud ID (ECID) não é suportada. Todos os atributos/valores de perfil são criados e atualizados via API. Os detalhes de formato estão disponíveis na documentação da API.

## Exemplo de casos de uso

Seu CRM ou outro sistema interno armazena dados importantes sobre seus visitantes, que devem ser consistentemente atualizados no Target, sem expor os dados de perfil na implementação da página.

## Benefícios do método

Nenhum limite sobre o número de atributos de perfil.

Os atributos de perfil são enviados via site e podem ser atualizados pela API e vice-versa.

## Avisos

O tamanho do arquivo em lote deve ser menor que 50 MB. Além disso, o número total de linhas não deve ultrapassar 500.000 por carregamento.

As atualizações geralmente ocorrem em menos de uma hora, mas podem levar até 24 horas para serem refletidas

Não há limite em relação ao número ou linhas que você pode carregar em um período de 24 horas em lotes subsequentes. No entanto, o processo de ingestão pode ter o fluxo controlado em horário comercial, para garantir que outros processos sejam executados com eficiência.

As [chamadas de atualização em lote V2 consecutivas](https://developers.adobetarget.com/api/#updating-profiles) sem chamadas da mbox entre as mesmas thirdPartyIds substituindo as propriedades atualizadas na primeira chamada de atualização em lote.

## Exemplos de código

Consulte [Atualização de perfis](https://developers.adobetarget.com/api/#updating-profiles).

### Links para informações relevantes

[Atualizações de perfis](https://developers.adobetarget.com/api/#updating-profiles)
