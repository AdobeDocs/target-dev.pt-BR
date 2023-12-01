---
title: API de atualização de perfil único do Adobe Target
description: Saiba como usar o [!DNL Adobe Target] [!UICONTROL API de atualização de perfil único] para enviar dados de perfil de um único visitante para o [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 6f7d9875e3b73352ead3a55e40a4b2f81f3d4400
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# [!DNL Adobe Target Single Profile Update API]

A variável [!DNL Adobe Target] [!UICONTROL API de atualização de perfil único] permite enviar uma atualização de perfil para um único usuário. A variável [!UICONTROL API de atualização de perfil único] e geralmente é usado quando uma atualização deve ocorrer em relação a uma transação que ocorre em um canal que não implementou [!DNL Target].

A variável [!UICONTROL API de atualização de perfil único] O está limitado à execução de 1 milhão de atualizações em qualquer período contínuo de 24 horas. As atualizações geralmente ocorrem em menos de uma hora, mas podem levar até 24 horas para serem refletidas. Se precisar enviar mais atualizações ou solicitar que as atualizações sejam processadas em prazos mais curtos, considere enviar atualizações de perfil transacional por atualização do lado do cliente (preferencial) ou pelo [!DNL Adobe Target] lado do servidor [API de entrega](/help/dev/implement/delivery-api/overview.md).

Especificar os parâmetros do perfil no formato `profile.paramName=value`.

Para atualizar o perfil de um `pcId`, use:

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

Para atualizar o perfil de um `mbox3rdPartyId`, use:

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

A variável [!UICONTROL API de atualização de perfil único] é somente para atualizações. Se nada for encontrado, um perfil não será criado.

## Notas

* Os parâmetros e valores devem ser codificados em URL usando UTF-8.
* O formato do parâmetro é `profile.paramName`.
* Nem todos os valores de parâmetro devem existir para todas as pcIds e mbox3rdPartyIds.
* Os parâmetros e valores diferenciam maiúsculas de minúsculas.
* O GET e o POST são compatíveis.
* O limite de tamanho atual é de 8 KB para o GET e 60 KB para o POST.

## Resposta

Um exemplo de resposta para as solicitações acima tem esta aparência:

`trueRequest successfully submitted`

Essa resposta indica que a resposta foi enviada e será processada em breve.