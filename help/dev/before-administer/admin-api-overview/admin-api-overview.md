---
title: Visão geral da API de administração do Adobe Target
description: Visão geral do  [!DNL Adobe Target Admin API]
exl-id: 1168d376-c95b-4c5a-b7a2-c7815799a787
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 2%

---

# Visão geral da API de administração do Target

Este artigo fornece uma visão geral das informações de referência necessárias para entender e usar o [!DNL Adobe Target Admin API]s com êxito. O conteúdo a seguir pressupõe que você entende como [configurar a autenticação](../configure-authentication.md) para [!DNL Adobe Target Admin API]s.

>[!NOTE]
>
>Se você deseja administrar [!DNL Target] por meio da interface, consulte a [seção de administração do *Guia do Profissional de Negócios do Adobe Target*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=pt-BR).
>
>As APIs de administrador e APIs de perfil geralmente são mencionadas coletivamente (&quot;APIs de administrador e perfil&quot;), mas também podem ser mencionadas separadamente (&quot;APIs de administrador&quot; e &quot;APIs de perfil&quot;). A API do Recommendations é uma implementação específica de uma API de administração [!DNL Target].

## Antes de começar 

Em todos os exemplos de código fornecidos para as [APIs de administrador](../../administer/admin-api/admin-api-overview-new.md), substitua {tenant} pelo seu valor de locatário, `your-bearer-token` pelo token de acesso gerado com seu JWT e `your-api-key` pela sua chave de API da [Adobe Developer Console](https://developer.adobe.com/console/home). Para obter mais informações sobre locatários e JWTs, consulte o artigo sobre como [configurar a autenticação](../configure-authentication.md) para APIs de administrador do Adobe [!DNL Target].

## Controle de versão

Todas as APIs têm uma versão associada. É importante fornecer a versão correta da API que você deseja usar.

Se a solicitação tiver uma carga (POST ou PUT), o cabeçalho `Content-Type` da solicitação será usado para especificar a versão.

Se a solicitação não contiver uma carga (GET, DELETE ou OPTIONS), o cabeçalho `Accept` será usado para especificar a versão.

Se uma versão não for fornecida, a chamada assumirá V1 como padrão (application/vnd.adobe.target.v1+json).

>[!NOTE]
>
>Se a versão correta não for especificada — por exemplo, se você usar uma carga V2, mas não especificar o cabeçalho Content-Type — a API responderá com um erro não suportado se a API não for compatível com versões anteriores.

Mensagem de erro para recursos sem suporte

```
{
    "httpStatus": 406,
    "requestId": "8752b736-cf71-4d81-86c3-94be2b5ae648",
    "requestTime": "2018-02-02T21:39:06.405Z",
    "errors": [
        {
            "errorCode": "Unsupported.Feature",
            "message": "Unsupported features detected"
        }
    ]
}
```

Admin Postman Collection

O Postman é um aplicativo que facilita o acionamento de chamadas de API. Esta [Coleção do Postman da API de administração do Target](https://developers.adobetarget.com/api/#admin-postman-collection) contém todas as chamadas da API de administração do Target que exigem autenticação usando Atividades, Públicos, Ofertas, Relatórios, Mboxes e Ambientes

## Códigos de resposta

Estes são os códigos de resposta comuns para as APIs de administrador do Target.

| Status | Significado | Descrição |
| --- | --- | --- |
| 200 | [OK](https://www.rfc-editor.org/rfc/rfc7231#section-6.3.1) | OK |  |
| 400 | [Solicitação inválida](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.1) | Solicitação inválida. Provavelmente, os dados fornecidos na solicitação são inválidos. |  |
| 401 | [Não autorizado](https://www.rfc-editor.org/rfc/rfc7235#section-3.1) | O usuário não tem permissão para executar esta operação. |  |
| 403 | [Proibido](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.3) | O acesso a este recurso é proibido. |  |
| 404 | [Não encontrado](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.4) | O recurso referenciado não foi encontrado. |  |

## Atividades

Uma atividade permite testar ou personalizar o conteúdo para seus usuários. As atividades podem ser de um dos seguintes tipos:

* [A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=pt-BR)
* [Direcionamento de experiência (XT)](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=pt-BR)
* [Recommendations](https://experienceleague.adobe.com/docs/target/using/activities/recommendations-activity.html?lang=pt-BR)
* [Personalização automatizada](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=pt-BR)
* [Teste multivariado (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=pt-BR)

## Atualizações em lote

Várias APIs de administrador podem ser executadas como uma única solicitação em lote.

### Executar chamadas em lote

`POST /{tenant}/target/batch`

Empilhe várias chamadas de API e execute-as em um único lote.

O agrupamento em lotes permite passar instruções para várias operações em uma única solicitação HTTP. Você também pode especificar dependências entre operações relacionadas (descritas em uma seção abaixo). O TNT processará cada uma de suas operações independentes (possivelmente em paralelo) e processará suas operações dependentes sequencialmente. Depois que todas as operações forem concluídas, uma resposta consolidada será enviada de volta e a conexão HTTP será fechada.

A API de lote recebe uma matriz de solicitações HTTP lógicas representadas como matrizes JSON - cada solicitação tem um método (correspondente ao método HTTP GET/PUT/POST/DELETE etc.), um relativeUrl (a parte do URL após admin/rest/), matriz de cabeçalhos opcionais (correspondente a cabeçalhos HTTP) e um corpo opcional (para solicitações POST e PUT). A API de lote retorna uma matriz de respostas HTTP lógicas representadas como matrizes JSON - cada resposta tem um código de status, uma matriz de cabeçalhos opcionais e um corpo opcional (que é uma cadeia de caracteres codificada em JSON). Para fazer solicitações em lote, crie um objeto JSON que descreve cada operação individual a ser executada. O número máximo de operações permitidas é de 256 (de 0 a 255).

Especificando dependências entre operações na solicitação Por padrão, as operações especificadas na solicitação da API em lote são independentes - elas podem ser executadas em ordem arbitrária no servidor e um erro em uma operação não afeta a execução de outras operações.

Geralmente, as operações na solicitação são dependentes - por exemplo, a saída de uma operação pode ser usada na entrada da próxima operação. Por exemplo, a oferta criada em operationId=0 precisa ser usada na criação da campanha operationId=1.

Para vincular duas operações em lote, especifique na operação dependente a ID da operação necessária, por exemplo: &quot;dependsOnOperationId&quot; : 5. Além disso, as IDs de recursos criados por meio de solicitações POST de operações em lote podem ser usadas em operações dependentes, em &quot;relativeUrl&quot; e &quot;body&quot;.

#### Permissões e limitação

Para executar ações de API em lote, o usuário subjacente deve ter pelo menos direitos de &quot;editor&quot; (para cada operação individual, caso sejam necessários direitos adicionais, em vez de o usuário ter, a operação individual falhará). As estratégias de limitação comuns são aplicadas em ações de API em lote como se cada operação tivesse sido executada individualmente.

O processamento em lote é concluído quando todas as operações são concluídas. Uma operação pode ser bem-sucedida (2xx statusCode), com falha (4xx, 5xx status code) ou ignorada porque uma operação de dependência falhou ou foi ignorada.

#### Parâmetros do objeto de solicitação

| Atributo | Descrição | Limites | Padrão |
| --- | --- | --- | --- |
| corpo | corpo para operação em lote de HTTP. será ignorado para todas as ações, exceto POST e PUT. pode fazer referência a IDs de ações em lote anteriores, por exemplo: &quot;offerId&quot;: &quot;{operationIdResponse:0}&quot;, &quot;segmentId&quot;: &quot;{operationIdResponse:1}&quot; | deve ser um JSON válido; caso faça referência a um operationIdResponse, a resposta do operationId referenciada deve ser um ID válido e o método dessa ação deve ser POST | objeto vazio {} |  |
| dependsOnOperationIds | lista de IDs de restrição que garantirá que a operação atual será executada somente se as operações especificadas forem concluídas com êxito. Pode ser usado para encadear operações. | são permitidas no máximo 255 operações; somente valores únicos são permitidos; deve apontar para uma operationId válida na matriz; dependências cíclicas não são permitidas |  |  |
| cabeçalhos | matriz de cabeçalhos de valor-chave a serem enviados com uma operação específica. Caso a autenticação para a API em lote tenha sido executada por meio do cabeçalho de Autorização, ela também será copiada para operações individuais. | o número máximo de cabeçalhos na matriz permitida é 50 | Tipo de conteúdo: application/json |  |
| cabeçalhos->nome | nome do cabeçalho | deve ser exclusivo entre outros nomes de cabeçalho. os cabeçalhos não diferenciam maiúsculas de minúsculas por rfc, caso contrário, os valores se substituirão. |  |  |
| cabeçalhos->valor | valor do cabeçalho | N/A | cadeia de caracteres vazia |  |
| método | Método HTTP a ser usado. Opções disponíveis: GET, POST, PUT, PATCH, DELETE | são permitidos apenas os métodos GET, POST, PUT, PATCH, DELETE |  |  |
| operationId | ID da operação usada para identificar uma operação entre outras operações para respostas e resultados de referência. | exclusivo entre outras operações; valores de 0 a 255 |  |  |
| operações | lista de operações a serem executadas em um lote. não é pertinente. | são permitidas no máximo 256 operações |  |  |
| relativeUrl | URL relativo da API rest do administrador, a parte após &quot;/admin/rest/&quot;. Pode conter parâmetros da sequência de consulta como: &quot;/v2/campaigns?limit=10&amp;offset=10&quot;. pode se referir a URLs com IDs de ações em lote anteriores, por exemplo: &quot;/v1/offers/{operationIdResponse:0}&quot;. Caso os parâmetros de consulta sejam enviados, eles devem ser codificados por URL. | deve começar com / (ser relativo); somente novas APIs JSON válidas são compatíveis; no caso de relativeURL inválido, uma resposta 404 para uma operação específica será retornada; no caso de fazer referência a uma operationIdResponse, a resposta da operationId referenciada deve ser uma ID válida e o método nessa ação deve ser POST |  |  |

#### Exemplo de objeto de solicitação

```
{
  "operations": [
    {
      "operationId": 1,
      "dependsOnOperationIds~": [0],
      "method": "POST",
      "relativeUrl": "/v1/offers",
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json"
        }
      ],
      "body~": {
        "key": "value"
      }
    }
  ]
}
```

#### Parâmetros do Objeto de Resposta

| Parâmetro | Descrição |
| --- | --- |
| operationId | ID de operação usada para identificar uma operação entre outras operações, a mesma ID que foi enviada na solicitação POST. |  |
| ignorado | sinalizador booleano para marcar se a operação foi executada ou ignorada. Será verdadeiro caso a operação atual dependa de uma operação que falhou (retornou um valor de statusCode diferente de 2xx). |  |
| statusCode | retornado, todas as operações dependentes serão ignoradas (não executadas). |  |
| cabeçalhos | matriz de cabeçalhos de valor-chave a ser enviada como resposta para uma operação específica. |  |
| cabeçalhos->nome | nome do cabeçalho |  |
| cabeçalhos->valor | valor do cabeçalho |  |
| corpo | corpo para operação de resposta em lote HTTP |  |

#### Exemplo de objeto de resposta

```
{
  "results": [
    {
      "operationId": 1,
      "skipped~": false,
      "statusCode~": 200,
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json; charset=UTF-8"
        }
      ],
      "body~": {
        "id": 5
      }
    }
  ]
}
```
