---
keywords: apple, ITP, prevenção inteligente de rastreamento, experience cloud id, ecid, itp
description: Saiba mais sobre [!DNL Adobe Target] e o impacto da iniciativa Apple Intelligent Tracking Prevention (ITP) que busca proteger a privacidade dos usuários do Safari.
title: Como o [!DNL Target] Lidar com o suporte de ITP da Apple?
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 32%

---

# Apple Intelligent Tracking Prevention (ITP) 2.x

Intelligent Tracking Prevention (ITP) é a iniciativa da Apple para proteger a privacidade dos usuários do Safari. A primeira versão da ITP, que foi em 2017, direcionava o uso de cookies de terceiros. Na verdade, a Apple bloqueou completamente os cookies de terceiros, o que, por sua vez, causou um grande problema para empresas de tecnologia de marketing e publicidade, pois os cookies de terceiros geralmente são usados para rastrear visitantes e coletar dados do visitante. Agora, a Apple está prestes a colocar limitações e restrições em como cookies próprios são usados no Safari.

Essas versões da ITP incluem as seguintes restrições:

| Versão | Detalhes |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | Cookies limitados do lado do cliente que são colocados no navegador usando a `document.cookie` API até um prazo de sete dias.<br />Lançado em 21 de fevereiro de 2019. |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | Redução drástica do prazo de validade de sete dias para um dia.<br />Lançado em 24 de abril de 2019. |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-3-2/) | Eliminação de várias soluções alternativas, como empregar o localStorage ou usar o JavaScript `Document.referrer property`.<br />Lançado em 23 de setembro de 2019.<br />Recurso de defesa de camuflagem CNAME para ITP lançado no Safari 14, macOS Big Sur, Catalina, Mojave, iOS 14 e iPadOS 14. Todos os cookies criados por uma resposta HTTP encoberta por CNAME de terceiros serão definidos para expirar em sete dias.<br />Anunciado em 12 de novembro de 2020. |

## Qual é o impacto para mim como um [!DNL Target] cliente?

O Target fornece bibliotecas JavaScript para você implantar em suas páginas para que [!DNL Target] O pode fornecer personalização em tempo real aos seus visitantes. Há três [!DNL Target] Bibliotecas de JavaScript do at.js 1.*x*, at.js 2.*x*, o [!DNL Adobe Experience Cloud Web SDK] que colocam o lado do cliente [!DNL Target] cookies nos navegadores de seus visitantes por meio do `document.cookie` API. Como resultado, [!DNL Target] Os cookies do são afetados pela ITP 2.1, 2.2 e 2.3 da Apple e expirarão após sete dias (com a ITP 2.1) e após um dia (com a ITP 2.2 e a ITP 2.3).

Impactos do Apple ITP 2.x [!DNL Target] nas seguintes áreas:

| Impacto | Detalhes |
| --- | --- |
| Aumento potencial das contagens de visitantes únicos | Como a janela de expiração está sendo definida como sete dias (com a ITP 2.1) e um dia (com a ITP 2.2 e a ITP 2.3), você pode ver um aumento de visitantes únicos vindos dos navegadores do Safari. Se os visitantes revisitarem seu domínio após sete dias (ITP 2.1) ou um dia (ITP 2.2 e ITP 2.3), [!DNL Target] é forçado a colocar um novo [!DNL Target] cookie no domínio em vez do cookie expirado. O novo [!DNL Target] cookie indica um novo visitante único, mesmo que o usuário seja o mesmo. |
| Redução nos períodos de pesquisa para [!DNL Target] atividades | Os perfis de visitante para [!DNL Target] atividades podem ter um período de lookback reduzido para a tomada de decisão. Os [!DNL Target] cookies são usados para identificar um visitante e armazenar atributos de perfil do usuário para personalização. Tendo em conta [!DNL Target] Os cookies do podem ser expirados no Safari após sete dias (ITP 2.1) ou um dia (ITP 2.2 e 2.3), os dados de perfil do usuário vinculados ao [!DNL Target] cookie não pode ser usado para a tomada de decisão. |
| Scripts de perfil com base em 3rdPartyID | Como a janela de expiração está sendo definida como sete dias (com a ITP 2.1) e um dia (com a ITP 2.2 e a ITP 2.3), [scripts de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html) com base no cookie 3rdPartyID deixará de funcionar após a expiração. |
| URLs de controle de qualidade/visualização em dispositivos iOS | Como a janela de expiração está sendo definida como sete dias (com a ITP 2.1) e um dia (com a ITP 2.2 e a ITP 2.3), [URLs de controle de qualidade/visualização](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) O deixará de funcionar após a expiração porque os URLs se baseiam no cookie 3rdPartyID. |

## Minha implementação atual do [!DNL Target] será afetada?

Se você estiver usando a biblioteca Experience Cloud ID (ECID), além da biblioteca [!DNL Target] Biblioteca JavaScript, sua implementação será afetada pelas formas listadas neste artigo: [Impacto do Safari ITP 2.1 nos clientes do Adobe Experience Cloud e do Experience Platform](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
