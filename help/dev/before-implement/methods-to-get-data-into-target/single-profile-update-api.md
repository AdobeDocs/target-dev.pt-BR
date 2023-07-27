---
keywords: implementar, implementar, configurar, configurar, atualização de perfil único
description: Obter dados em [!DNL Target] usando a API de atualização de perfil único.
title: Como posso obter dados no [!DNL Target] Usando a API de atualização de perfil único?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 35%

---

# API de atualização de perfil único

Quase idêntico ao [!UICONTROL API de atualização de perfil em massa] in [!DNL Adobe Target], mas um perfil de visitante é atualizado de cada vez, em linha na chamada da API, em vez de com um arquivo .csv.

## Formato

O visitante deve ser identificado por meio do valor [!DNL Target]mboxPC do ou valor de `mbox3rdPartyId`. A Experience Cloud ID (ECID) não é suportada.

## Exemplo de casos de uso

Você deseja atualizar o perfil de um único visitante que executa alguma ação offline. As ações podem incluir alcançar uma central de atendimento, um empréstimo é financiado, usar um cartão de fidelidade na loja, acessar um quiosque e assim por diante.

## Benefícios do método

Nenhum limite sobre o número de atributos de perfil.

Os atributos de perfil são enviados via site e podem ser atualizados pela API e vice-versa.

## Avisos

Limite de 1.000.000 de chamadas de API (1 milhão) por 24 horas

Perfis de atualização somente. Não é possível criar um perfil para um usuário potencial [!DNL Target] ainda não viu.

As atualizações geralmente ocorrem em menos de 1 hora, mas podem levar até 24 horas para serem refletidas.

## Exemplos de código

Suporte a GET e POST. 

```
https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr1=0&profile.attr2=1...
```

## Recursos

* [Atualizações de perfis](https://developers.adobetarget.com/api/#updating-profiles)
