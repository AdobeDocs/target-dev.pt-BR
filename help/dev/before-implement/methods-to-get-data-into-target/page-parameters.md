---
keywords: implementar, implementar, configurar, configurar, parâmetros de página
description: Obter dados em  [!DNL Target] usando parâmetros de página.
title: Como Obter Dados no  [!DNL Target] Usando Parâmetros de Página?
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
TQID: https://experienceleague.adobe.com/CYhZOFnli-DmREOOZGE2aGNn3x7BJ7uwGA2vfwUSnOk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 397
ht-degree: 31%

---

# Parâmetros da página

Parâmetros de página (também chamados de &quot;parâmetros de mbox&quot;) são pares de nome/valor passados diretamente pelo código da página que não são armazenados no perfil do visitante para uso futuro.

Parâmetros de página são úteis para enviar dados de página para [!DNL Adobe Target] que não precisam ser armazenados com o perfil do visitante para uso futuro do direcionamento. Esses valores são usados para descrever a página ou a ação que o usuário fez na página específica.

## Formato

Os parâmetros de página são passados para [!DNL Target] por meio de uma chamada de servidor como um par nome/valor da cadeia de caracteres. Os nomes e valores do parâmetro são personalizáveis (embora alguns sejam &quot;nomes reservados&quot; para usos específicos).

Estes são alguns exemplos de parâmetros de página

* `page=productPage`

* `categoryId=homeLoans`

## Exemplo de casos de uso

* **Páginas de produto**: envia as informações sobre o produto específico exibido (este método é o modo de funcionamento do Recommendations)
* **Detalhes do pedido**: envia a ID do pedido, orderTotal e assim por diante, para a coleção de pedidos
* **Afinidade de categorias**: envia informações visualizadas por categoria para [!DNL Target], gerando conhecimento da afinidade do usuário a determinadas categorias do site
* **Dados de terceiros**: envia informações de fontes de dados de terceiros, como provedores de definição de direcionamento meteorológico, dados de conta (por exemplo, DemandBase), dados demográficos (por exemplo, Experiência) e muito mais.

## Benefícios do método

Os dados são enviados para [!DNL Target] em tempo real e podem ser usados na mesma chamada de servidor que os dados recebidos.

## Avisos

* Precisa de atualização do código da página (diretamente ou por meio de um sistema de gerenciamento de tags).
* Se os dados precisarem ser usados para direcionamento em uma chamada de página/servidor subsequente, eles deverão ser convertidos em um script de perfil.
* As cadeias de consulta podem conter somente caracteres de acordo com o [padrão IETF (Internet Engineering Task Force)](https://www.ietf.org/rfc/rfc3986.txt).

  Além dos caracteres mencionados no site do IETF, [!DNL Target] permite os seguintes caracteres nas cadeias de caracteres de consulta:

  ```< > # % " { } | \ ^ [ ] ` ``` {line-numbers="true"}

  O restante deve ser codificado em url. O padrão especifica o seguinte formato ( [https://www.ietf.org/rfc/rfc1738.txt](https://www.ietf.org/rfc/rfc1738.txt) ), conforme ilustrado abaixo:

  ![alt imagem](assets/ietf1.png)

  Ou, a lista completa para simplicidade:

  ![alt imagem](assets/ietf2.png)

## Exemplos de código

targetPageParamsAll (anexa os parâmetros a todas as chamadas de mbox na página):

`function targetPageParamsAll() { return "param1=value1&param2=value2&p3=hello%20world";`

targetPageParams (anexa os parâmetros ao mbox global na página):

`function targetPageParams() { return "param1=value1&param2=value2&p3=hello%20world";`

## Links para informações relevantes

Recomendações: [implementação de acordo com o tipo de página](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=pt-BR)

Confirmação do pedido: [rastreia conversões](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

Afinidade de categorias: [afinidade de categorias](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=pt-BR)
