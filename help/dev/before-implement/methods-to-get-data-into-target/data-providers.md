---
keywords: implementar, implementar, configurar, configurar, provedores de dados
description: Obter dados em  [!DNL Target] usando provedores de dados.
title: Como Obter Dados no  [!DNL Target] Usando Provedores de Dados?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 55%

---

# Provedores de dados

Os provedores de dados são um recurso que permite passar dados de terceiros facilmente para o [!DNL Adobe Target].

>[!NOTE]
>
>Os provedores de dados exigem o at.js 1.3 ou posterior.

## Formato

A configuração `window.targetGlobalSettings.dataProviders` é uma matriz de provedores de dados.

Para obter mais informações sobre a estrutura de cada provedor de dados, consulte [Provedores de dados](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Exemplo de casos de uso

Colete dados de terceiros, como um serviço meteorológico, um DMP ou até mesmo seu próprio serviço da Web. É possível então usar esses dados para criar públicos-alvo, conteúdo de direcionamento e enriquecer o perfil do visitante.

## Benefícios do método

Essa configuração permite que clientes reúnam dados de provedores de dados de terceiros, como Demandbase, BlueKai e serviços personalizados, além de enviar os dados para [!DNL Target] como parâmetros da mbox na solicitação global da mbox.

Ela é compatível com a coleta de dados de múltiplos provedores via solicitações síncronas e assíncronas.

Usar esta abordagem facilita o gerenciamento de cintilação ou conteúdo padrão da página, enquanto inclui tempos limites independentes para cada provedor para limitar o impacto sobre o desempenho da página

## Avisos

Se os provedores de dados adicionados a `window.targetGlobalSettings.dataProviders` forem assíncronos, serão executados em paralelo. A solicitação da API de Visitante é executada em paralelo com funções adicionadas a `window.targetGlobalSettings.dataProviders` para permitir um tempo mínimo de espera.

A at.js não tenta armazenar os dados em cache. Se o provedor de dados obtiver os dados apenas uma vez, deverá certificar-se de que os dados estão armazenados em cache e, quando a função de provedor for invocada, servir os dados do cache para a segunda invocação.

## Exemplos de código

Vários exemplos podem ser encontrados em [Provedores de dados](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Links para informações relevantes

Documentação: [Provedores de dados](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## Vídeos de treinamento:

* [Uso de provedores de dados do Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Implementação de provedores de dados no Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
