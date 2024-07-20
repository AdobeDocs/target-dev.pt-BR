---
title: Práticas recomendadas para usar a decisão no dispositivo
description: Saiba mais sobre as práticas recomendadas ao usar o [!UICONTROL on-device decisioning] no [!DNL Adobe Target]
feature: Implement Server-side
exl-id: a0ca014d-ad9f-4ecc-961d-cb7ba236507f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Práticas recomendadas

O [!DNL Adobe] recomenda as seguintes práticas recomendadas ao usar o [!UICONTROL on-device decisioning]:

## Práticas recomendadas quando o método de decisão for &quot;no dispositivo&quot;

Ao usar &quot;no dispositivo&quot; como o método de decisão, o artefato é baixado quando o visitante carrega a página da Web pela primeira vez. Qualquer qualificação de atividade que precise ocorrer no primeiro carregamento de página (sem cache) ocorre somente após o artefato ser totalmente baixado. Há certas práticas recomendadas que você pode seguir para garantir que as qualificações de atividade ocorram rapidamente para um novo visitante anônimo.

* Desative as atividades compatíveis &quot;No dispositivo&quot; que não devem estar no artefato.
* Se você tiver o Target Premium, poderá usar [propriedades/espaços de trabalho](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=pt-BR) para criar arquivos de artefatos diferentes para espaços de trabalho diferentes.
* Se os arquivos de artefato se tornarem muito grandes por motivos legítimos, você poderá usar o método de decisão &quot;híbrido&quot;. Esse método permite baixar o artefato em paralelo e todas as chamadas de API do Target transmitirão as informações até que o artefato seja baixado. Leia a seção de práticas recomendadas sobre o modo de decisão &quot;Híbrido&quot; abaixo para saber mais sobre essa abordagem.
* Se você tiver um aplicativo de página única (SPA), o [!DNL Adobe] recomenda carregar e inicializar a at.js antes de carregar o arquivo JavaScript principal do aplicativo durante o primeiro carregamento da página. Essa abordagem inicia o download do artefato muito antes, fornecendo uma renderização de experiência mais rápida.

## Práticas recomendadas quando o método de decisão for &quot;híbrido&quot;

Ao usar &quot;híbrido&quot; como o método de decisão, o artefato é baixado em paralelo. Até que o artefato seja baixado, qualquer chamada de API do [!DNL Target] transmitirá as informações mesmo que os &quot;locais&quot; sejam compatíveis no dispositivo. Esse comportamento é o padrão para todas as chamadas `getOffers()` e fornece o melhor desempenho na maioria das situações. Se você alterar o comportamento padrão de `getOffers()` definindo `decisioningMethod` como `on-device`, siga estas práticas recomendadas para evitar erros e garantir o melhor desempenho.

* Se você decidir chamar `getOffers()` com `decisioningMethod` como `on-device` quando a página for carregada pela primeira vez, faça isso dentro do manipulador de eventos &quot;ARTIFACT_DOWNLOAD_SUCCEEDED&quot; at.js para evitar erros. Se o artefato for muito grande, todos os &quot;locais&quot; que usam essa abordagem serão renderizados somente após o download completo do artefato, o que pode atrasar a renderização da experiência. A [!DNL Adobe] recomenda que você raramente use essa abordagem. Siga as práticas recomendadas para reduzir o tamanho do artefato na seção de práticas recomendadas &quot;No dispositivo&quot; acima ao usar essa abordagem.
