---
title: API de atualização de perfil único do Adobe Target
description: Saiba como usar o  [!DNL Adobe Target] [!UICONTROL Single Profile Update API] para enviar dados de perfil de um único visitante para o  [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
TQID: https://experienceleague.adobe.com/HEjGkrgixufe9wQvaPAljSlZRSaF-idgwKYWs3cuoJ0
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 361
ht-degree: 4%

---

# [!DNL Adobe Target Single Profile Update API]

O [!DNL Adobe Target] [!UICONTROL Single Profile Update API] permite enviar uma atualização de perfil para um único usuário. O [!UICONTROL Single Profile Update API] é quase idêntico ao [!UICONTROL Bulk Profile Update API], mas um perfil de visitante é atualizado de cada vez, em linha com a chamada de API em vez de com um arquivo .cvs.

O [!UICONTROL Single Profile Update API] e geralmente é usado quando uma atualização deve ocorrer em relação a uma transação que ocorre em um canal que não implementou o [!DNL Target]. Por exemplo, você deseja atualizar o perfil de um único visitante que executa alguma ação offline. As ações podem incluir alcançar uma central de atendimento, um empréstimo é financiado, usar um cartão de fidelidade na loja, acessar um quiosque e assim por diante.

Os benefícios da [!UICONTROL Single Profile Update API] incluem:

* Nenhum limite sobre o número de atributos de perfil.
* Os atributos de perfil enviados pelo site podem ser atualizados por meio da API e do oposto.

## Avisos

* O [!UICONTROL Single Profile Update API] está limitado a executar 1 milhão de atualizações em qualquer período contínuo de 24 horas.
* As atualizações geralmente ocorrem em menos de uma hora, mas podem levar até 24 horas para serem refletidas.

  Se você precisar enviar mais atualizações ou solicitar que elas sejam processadas em prazos mais curtos, considere enviar atualizações de perfil transacional por atualização do lado do cliente (preferencial) ou pela [!DNL Adobe Target] [API de entrega](/help/dev/implement/delivery-api/overview.md) do lado do servidor.

* O [!UICONTROL Single Profile Update API] é uma API de servidor para servidor e não foi projetado para funcionar em uma página da Web. Para atualizar um perfil de visitante na sua página da Web, você pode usar a função [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) ou a [API de Entrega](/help/dev/implement/delivery-api/overview.md).

## Formato

Especifique os parâmetros do perfil no formato `profile.paramName=value`.

Para atualizar o perfil de `pcId`, use:

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

Para atualizar o perfil de um `mbox3rdPartyId`, use:

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

O [!UICONTROL Single Profile Update API] é somente para atualizações. Se nada for encontrado, um perfil não será criado.

## Notas

* Os parâmetros e valores devem ser codificados em URL usando UTF-8.
* O formato do parâmetro é `profile.paramName`.
* Nem todos os valores de parâmetro devem existir para todas as pcIds e mbox3rdPartyIds.
* Os parâmetros e valores diferenciam maiúsculas de minúsculas.
* Há suporte para GET e POST.
* O limite de tamanho atual é de 8 KB para GET e 60 KB para POST.

## Resposta

Um exemplo de resposta para as solicitações acima tem esta aparência:

`trueRequest successfully submitted`

Essa resposta indica que a resposta foi enviada e será processada em breve.
