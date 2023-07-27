---
title: Considerações sobre a API de entrega do Adobe Target e limitações conhecidas
description: Quais considerações e limitações conhecidas devo considerar ao usar o [!UICONTROL API de entrega do Adobe Target]?
keywords: api de entrega
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---

# Considerações e limitações conhecidas

* Não há autenticação para [!DNL Target] APIs de entrega.
* Ela não processa cookies ou redireciona chamadas.
* Suporte para [!UICONTROL Automated Personalization] (AP) e [!UICONTROL Recommendations] Atividades: essa API tem dois modos de busca de conteúdo: execução e modo de pré-busca. O modo de busca prévia só pode ser usado para [!UICONTROL Teste AB] e [!UICONTROL Direcionamento de experiência] (XT) Atividades. Não usar o modo de pré-busca para [!UICONTROL Automated Personalization] (AP), [!UICONTROL Alocação automática], [!UICONTROL Direcionamento automático]ou [!UICONTROL Recommendations] tipos de atividades.
* Os nomes de cabeçalho HTTP/1.1 e HTTP/2 não diferenciam maiúsculas de minúsculas; no entanto, HTTP/2 impõe nomes de cabeçalho em minúsculas. Para obter mais informações, consulte [Documentação do Hypertext Transfer Protocol versão 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  Se você usar um endpoint que encaminha visitantes por meio de nossa nova infraestrutura de Balanceador de carga, suas conexões serão automaticamente atualizadas para HTTP/2. Esse processo de atualização converte cabeçalhos de solicitação em cabeçalhos em minúsculas para que eles não sejam considerados malformados.

  Esse problema pode ser um problema para os clientes se as bibliotecas forem configuradas para procurar cabeçalhos de solicitação/resposta que diferenciam maiúsculas e minúsculas (especificamente, não minúsculas).
