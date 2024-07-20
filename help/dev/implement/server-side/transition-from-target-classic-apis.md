---
keywords: api, adobe i/o, classic, console do desenvolvedor da adobe
description: Saiba como fazer a transição de  [!DNL Adobe Target Classic] APIs para  [!DNL Target] APIs em  [!DNL Adobe Developer Console].
title: Como fazer a transição de  [!DNL Target Classic] APIs para  [!DNL Target] APIs no [!DNL Adobe Developer Console]?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# Transição de [!DNL Target Classic] APIs para [!DNL Target] APIs no [!DNL Adobe Developer Console]

Informações para ajudá-lo a fazer a transição das APIs do [!DNL Target Classic] para as APIs do [!DNL Target] no [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Com a desativação do [!DNL Adobe Target Classic], as APIs conectadas à sua conta do [!DNL Target Classic] também ficaram indisponíveis. Este artigo ajudará você a fazer a transição das suas integrações baseadas em APIs do [!DNL Target Classic] para as APIs do [!DNL Target] alimentadas pelo [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Para obter mais informações sobre [!DNL Target] APIs, consulte [[!DNL Target] APIs](/help/dev/before-administer/target-api-overview.md). Para obter mais informações sobre os [!DNL Target] SDKs, consulte [[!DNL Target] Implementação no lado do servidor](/help/dev/implement/server-side/server-side-overview.md)

## Terminologia

| Termo | Descrição |
|--- |--- |
| API clássica | APIs vinculadas à sua conta do [!DNL Target Classic]. Essas chamadas de API são baseadas em um nome de usuário e uma autenticação por senha e usam o nome de host `testandtarget.omniture.com`. Se suas chamadas de API contiverem um nome de usuário e senha na URL da solicitação, você deverá fazer a transição para as APIs [!DNL Adobe Developer Console]. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | O [!DNL Adobe Developer Console] é o gateway para [!DNL Target] APIs. Essas APIs estão conectadas à sua conta do [!DNL Target Standard/Premium]. As APIs [!DNL Target] no [!DNL Adobe Developer Console] usam uma [autenticação baseada em JWT](../../before-administer/configure-authentication.md), que é o padrão do setor para APIs corporativas seguras. |

## Linha do tempo 

As seguintes APIs foram descontinuadas quando [!DNL Target Classic] foi descontinuado:

| Data | Detalhes |
|--- |--- |
| 17 de outubro de 2017 | Todos os métodos da API que executam uma operação de gravação (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent`e `setCampaignState`) foram descontinuados.<P>Esta é a mesma data em que todas as contas de usuário do [!DNL Target Classic] foram definidas para o status de somente leitura. |
| 14 de novembro de 2017 | As APIs restantes foram desativadas. Esta é a data em que a interface do usuário [!DNL Target Classic] foi desativada |

[!DNL Recommendations Classic] APIs não foram afetadas por esta linha do tempo.

## Métodos equivalentes 

A tabela a seguir lista os métodos de API [!DNL Adobe Developer Console] equivalentes para os métodos de API Clássica. As APIs [!DNL Adobe Developer Console] retornam JSON, enquanto as APIs Clássicas retornam XML.

Os métodos da API [!DNL Adobe Developer Console] estão vinculados à seção correspondente no site da documentação da API. Um exemplo é fornecido para cada método de API. Você também pode usar a Coleção de Postman da API de Administração [!DNL Target], que contém exemplos de chamadas de API para todos os métodos de API de Adobe no [!DNL Adobe Developer Console].

| Grupos | Método da API clássica | Método API [!DNL Adobe Developer Console] | Notas |
|--- |--- |--- |--- |
| Campanha/Atividade | Criação de campanha | [Criar atividade AB](https://developers.adobetarget.com/api/#create-ab-activity)<P>[Criar atividade XT](https://developers.adobetarget.com/api/#create-xt-activity) | As novas APIs fornecem métodos de criação separados para AB e XT |
|  | Atualização da campanha | [Atualização de atividade AB](https://developers.adobetarget.com/api/#update-ab-activity)<P>[Atualização de atividade XT](https://developers.adobetarget.com/api/#update-xt-activity) |  |
|  | Copiar campanha | N/A | Usar APIs de criação de atividade |
|  | Lista de campanhas | [Listar atividades](https://developers.adobetarget.com/api/#list-activities) |  |
|  | Estado da campanha | [Atualizar estado da atividade](https://developers.adobetarget.com/api/#update-activity-state) |  |
|  | Exibição de campanha | [Obter atividade AB por ID](https://developers.adobetarget.com/api/#get-ab-activity-by-id)<P>[Obter atividade XT por ID](https://developers.adobetarget.com/api/#get-xt-activity-by-id) |  |
|  | ID de campanha de terceiros | N/A | Se estiver usando thirdpartyID, os métodos de Atividade relevantes podem ser usados |
| Ofertas | Criação de oferta | [Criar oferta](https://developers.adobetarget.com/api/#create-offer) |  |
|  | Obtenção de oferta | [Obter oferta por ID](https://developers.adobetarget.com/api/#get-offer-by-id) |  |
|  | Lista de ofertas | [Listar ofertas](https://developers.adobetarget.com/api/#list-offers) |  |
|  | Lista de pastas | N/A | Não há suporte para pastas em [!DNL Target Standard/Premium] |
| Relatório | Relatório de desempenho da campanha | [Relatório de desempenho AB](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[Relatório de desempenho XT](https://developers.adobetarget.com/api/#get-xt-performance-report) |  |
|  | Relatório de auditoria | [Obter Relatório de Auditoria](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | Relatório de conteúdo 1-1 | [Obter relatório de desempenho AP](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| Configurações da conta | Obter grupos de Hosts | [Listar ambientes](https://developers.adobetarget.com/api/#list-environments) |  |

## Exceções

Se você precisar de uma exceção, entre em contato com o seu Gerente de sucesso do cliente.

## Ajuda 

Entre em contato com [!DNL Adobe Target Client Care] (tt-support@adobe.com) se tiver dúvidas ou precisar de ajuda na transição das APIs Classic para as APIs [!DNL Target] no [!DNL Adobe Developer Console].
