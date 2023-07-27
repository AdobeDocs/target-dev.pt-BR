---
keywords: implementar, implementação, configuração, configuração, parâmetro de página, tomcat, url codificado, atributo de perfil na página, parâmetro mbox, atributos de perfil na página, atributo de perfil de script, API de atualização de perfil em massa, API de atualização de arquivo único, atributos do cliente, implementar5, implementar6, implementar7, implementar8, implementar0, implementar1, implementar2, implementar3, implementar4, implementar5, provedores de dados, provedor de dados, provedor de dados
description: Obter dados em [!DNL Target] (parâmetros de página, atributos de perfil, atributos de perfil de script, provedores de dados, APIs de atualização de perfil único e em massa, atributos do cliente).
title: Como coloco os dados no Target?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 52%

---

# Visão geral dos métodos

Informações sobre os diferentes métodos que você pode usar para inserir dados no Adobe Target.

Os métodos disponíveis incluem:

| Método | Detalhes |
| --- | --- |
| [Parâmetros de página](page-parameters.md)<br />(Também chamado de &quot;parâmetros de mbox&quot;) | Os parâmetros de página são pares de nome/valor enviados diretamente pelo código de página que não são armazenados no perfil do visitante para uso futuro.<br />Os parâmetros de página são úteis para enviar dados de página para o [!DNL Target] que não precisam ser armazenadas com o perfil do visitante para uso futuro do target. Esses valores são usados para descrever a página ou a ação que o usuário fez na página específica. |
| [Atributos de perfil na página](in-page-profile-attributes.md)<br />(Também chamado de &quot;atributos de perfil in-mbox&quot;) | Os atributos de perfil na página são pares de nome/valor enviados diretamente pelo código de página que são armazenados no perfil do visitante para uso futuro.<br />Os atributos de perfil na página permitem que os dados específicos do usuário sejam armazenados no perfil do Target para direcionamento e segmentação posteriores. |
| [Atributos de perfil de script](script-profile-attributes.md) | Os atributos do perfil de script são pares de nome/valor definidos no [!DNL Target] solução. O valor é determinado na execução de um snippet do JavaScript no servidor Target, a cada chamada do servidor.<br />Os usuários gravam pequenos snippets de código que são executados de acordo com a chamada de mbox e antes de um visitante ser avaliado para associação de público-alvo e atividade. |
| [Provedores de dados](data-providers.md) | Os provedores de dados permitem que você passe dados de terceiros facilmente para o Target. |
| [API de atualização de perfil em massa](bulk-profile-update-api.md) | Pela API, envie um arquivo .csv para [!DNL Target] com atualizações de perfil de visitante para muitos visitantes. Cada perfil do visitante pode ser atualizado com vários atributos de perfil na página em uma chamada. |
| [API de atualização de perfil único](single-profile-update-api.md) | Quase idêntica à API de atualização de perfil em massa, mas um perfil de visitante é atualizado por vez, alinhada à chamada de API em vez de um arquivo .csv. |
| [Atributos do cliente](customer-attributes.md) | Os atributos do cliente permitem que você carregue os dados de perfil do visitante via FTP à Experience Cloud. Após feito o upload, use os dados no Adobe Analytics e no Adobe Target. |
