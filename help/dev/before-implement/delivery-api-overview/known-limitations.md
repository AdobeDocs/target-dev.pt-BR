---
title: Considerações sobre a API de entrega do Adobe Target e limitações conhecidas
description: Quais considerações e limitações conhecidas devo considerar ao usar o [!UICONTROL Adobe Target Delivery API]?
keywords: api de entrega
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 49acf92bbe06dbcee36fef2b7394acd7ce37baad
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 6%

---

# Considerações e limitações conhecidas

* Não há autenticação para [!DNL Target] APIs de Entrega.
* Ela não processa cookies ou redireciona chamadas.
* Os nomes de cabeçalho HTTP/1.1 e HTTP/2 não diferenciam maiúsculas de minúsculas; no entanto, HTTP/2 impõe nomes de cabeçalho em minúsculas. Para obter mais informações, consulte a [documentação do HTTP/2 (Hypertext Transfer Protocol Versão 2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Se você usar um endpoint que encaminha visitantes por meio de nossa nova infraestrutura de Balanceador de carga, suas conexões serão automaticamente atualizadas para HTTP/2. Esse processo de atualização converte cabeçalhos de solicitação em cabeçalhos em minúsculas para que eles não sejam considerados malformados.

  Esse problema pode ser um problema para os clientes se as bibliotecas forem configuradas para procurar cabeçalhos de solicitação/resposta que diferenciam maiúsculas e minúsculas (especificamente, não minúsculas).
