---
keywords: implementar, implementação, configuração, configuração, parâmetro de página, tomcat, url codificado, atributo de perfil na página, parâmetro mbox, atributos de perfil na página, atributo de perfil de script, API de atualização de perfil em massa, API de atualização de arquivo único, atributos do cliente, implementar5, implementar6, implementar7, implementar8, implementar0, implementar1, implementar2, implementar3, implementar4, implementar5, provedores de dados, provedor de dados, provedor de dados
description: Obter dados em  [!DNL Target] (parâmetros de página, atributos de perfil, atributos de perfil de script, provedores de dados, APIs de atualização de perfil único e em massa, Atributos do cliente).
title: Como coloco os dados no Target?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
TQID: https://experienceleague.adobe.com/pmlPWRHb9tnrdSFm7s5OZ-RRsJJOxw-ntBY5AeswIcM
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 377
ht-degree: 27%

---

# Visão geral dos métodos

Informações sobre os diferentes métodos que você pode usar para inserir dados no Adobe Target.

Os métodos disponíveis incluem:

| Método | Detalhes |
| --- | --- |
| [Parâmetros da página](page-parameters.md)<br />(Também chamados de &quot;parâmetros mbox&quot;) | Os parâmetros de página são pares de nome/valor enviados diretamente pelo código de página que não são armazenados no perfil do visitante para uso futuro.<br />Os parâmetros de página são úteis para enviar dados de página para [!DNL Target] que não precisam ser armazenados com o perfil do visitante para uso futuro do direcionamento. Esses valores são usados para descrever a página ou a ação que o usuário fez na página específica. |
| [Atributos de perfil na página](in-page-profile-attributes.md)<br />(Também chamados de &quot;atributos de perfil in-mbox&quot;) | Os atributos de perfil na página são pares de nome/valor passados diretamente pelo código da página e armazenados no perfil do visitante para uso futuro.<br />Os atributos de perfil na página permitem que dados específicos do usuário sejam armazenados no perfil do Target para direcionamento e segmentação posteriores. |
| [Atributos de perfil de script](script-profile-attributes.md) | Os atributos do perfil de script são pares de nome/valor definidos na solução [!DNL Target]. O valor é determinado na execução de um snippet do JavaScript no servidor Target, a cada chamada do servidor.<br />Os usuários gravam pequenos trechos de código que são executados por chamada mbox e antes que um visitante seja avaliado quanto à associação de público-alvo e atividade. |
| [Provedores de dados](data-providers.md) | Os provedores de dados permitem que você passe dados de terceiros facilmente para o Target. |
| [API de atualização de perfil em massa](bulk-profile-update-api.md) | Pela API, envie um arquivo .csv para [!DNL Target] com atualizações de perfil de visitante para muitos visitantes. Cada perfil do visitante pode ser atualizado com vários atributos de perfil na página em uma chamada. |
| [API de atualização de perfil único](single-profile-update-api.md) | Quase idêntico à API de atualização de perfil em massa, mas um perfil de visitante é atualizado de cada vez, em linha na chamada da API em vez de com um arquivo .csv. |
| [Atributos do cliente](customer-attributes.md) | Os atributos do cliente permitem que você carregue os dados de perfil do visitante via FTP à Experience Cloud. Após feito o upload, use os dados no Adobe Analytics e no Adobe Target. |
