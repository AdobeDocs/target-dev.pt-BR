---
keywords: apple, ITP, prevenção inteligente de rastreamento, experience cloud id, ecid, itp
description: Saiba mais sobre o  [!DNL Adobe Target] e o impacto da iniciativa Apple Intelligent Tracking Prevention (ITP) que busca proteger a privacidade dos usuários do Safari.
title: Como o  [!DNL Target] Lida com o Suporte ITP da Apple?
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 30%

---

# Apple Intelligent Tracking Prevention (ITP) 2.x

Intelligent Tracking Prevention (ITP) é a iniciativa da Apple para proteger a privacidade dos usuários do Safari. A primeira versão da ITP, que foi em 2017, direcionava o uso de cookies de terceiros. Na verdade, a Apple bloqueou completamente os cookies de terceiros, o que, por sua vez, causou um grande problema para empresas de tecnologia de marketing e publicidade, pois os cookies de terceiros geralmente são usados para rastrear visitantes e coletar dados do visitante. Agora, a Apple está prestes a colocar limitações e restrições em como cookies próprios são usados no Safari.

Essas versões da ITP incluem as seguintes restrições:

| Versão | Detalhes |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | Cookies limitados do lado do cliente que são colocados no navegador usando a `document.cookie` API até um prazo de sete dias.<br />Lançado em 21 de fevereiro de 2019. |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | Redução drástica do limite de validade de sete dias para um dia.<br />Lançado em 24 de abril de 2019. |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/) | Foram eliminadas várias soluções alternativas, como empregar o localStorage ou usar o JavaScript `Document.referrer property`.<br />Lançado em 23 de setembro de 2019.<br />Recurso de defesa de cloaking CNAME para ITP lançado no Safari 14, macOS Big Sur, Catalina, Mojave, iOS 14 e iPadOS 14. Todos os cookies criados por uma resposta HTTP encoberta por CNAME de terceiros serão definidos para expirar em sete dias.<br />Anunciado em 12 de novembro de 2020. |

## Qual é o impacto para mim como cliente do [!DNL Target]?

O Target fornece bibliotecas JavaScript para você implantar em suas páginas para que o [!DNL Target] possa oferecer personalização em tempo real aos seus visitantes. Há três [!DNL Target] bibliotecas JavaScript at.js 1.*x*, at.js 2.*x*, o [!DNL Adobe Experience Cloud Web SDK] que coloca cookies do lado do cliente [!DNL Target] nos navegadores de seus visitantes por meio da API `document.cookie`. Como resultado, os cookies [!DNL Target] são afetados pela ITP 2.1, 2.2 e 2.3 da Apple e expirarão após sete dias (com a ITP 2.1) e após um dia (com a ITP 2.2 e a ITP 2.3).

O Apple ITP 2.x afeta [!DNL Target] nas seguintes áreas:

| Impacto | Detalhes |
| --- | --- |
| Aumento potencial das contagens de visitantes únicos | Como a janela de expiração está sendo definida como sete dias (com a ITP 2.1) e um dia (com a ITP 2.2 e a ITP 2.3), você pode ver um aumento de visitantes únicos vindos dos navegadores do Safari. Se os visitantes revisitarem seu domínio após sete dias (ITP 2.1) ou um dia (ITP 2.2 e ITP 2.3), o [!DNL Target] será forçado a colocar um novo cookie [!DNL Target] em seu domínio, no lugar do cookie expirado. O novo [!DNL Target] cookie indica um novo visitante único, mesmo que o usuário seja o mesmo. |
| Redução nos períodos de pesquisa para [!DNL Target] atividades | Os perfis de visitante para [!DNL Target] atividades podem ter um período de lookback reduzido para a tomada de decisão. Os [!DNL Target] cookies são usados para identificar um visitante e armazenar atributos de perfil do usuário para personalização. Considerando que os cookies do [!DNL Target] podem ser expirados no Safari após sete dias (ITP 2.1) ou um dia (ITP 2.2 e 2.3), os dados de perfil do usuário vinculados ao cookie [!DNL Target] removido não podem ser usados para a tomada de decisão. |
| Scripts de perfil com base em 3rdPartyID | Como a janela de expiração está sendo definida como sete dias (com ITP 2.1) e um dia (com ITP 2.2 e ITP 2.3), os [scripts de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=pt-BR) baseados no cookie 3rdPartyID deixarão de funcionar após a expiração. |
| URLs de controle de qualidade/visualização em dispositivos iOS | Como a janela de expiração está sendo definida como sete dias (com ITP 2.1) e um dia (com ITP 2.2 e ITP 2.3), os [URLs de controle de qualidade/visualização](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=pt-BR) deixarão de funcionar após a expiração porque os URLs são baseados no cookie 3rdPartyID. |

## Minha implementação atual do [!DNL Target] será afetada?

Se você estiver usando a biblioteca da Experience Cloud ID (ECID), além da biblioteca do JavaScript [!DNL Target], sua implementação será afetada pelas formas listadas neste artigo: [Impacto da ITP 2.1 do Safari nos clientes da Adobe Experience Cloud e da Experience Platform](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
