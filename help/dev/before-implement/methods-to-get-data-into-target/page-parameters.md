---
keywords: implementar, implementar, configurar, configurar, parâmetros de página
description: Obter dados em  [!DNL Target] usando parâmetros de página.
title: Como Obter Dados no  [!DNL Target] Usando Parâmetros de Página?
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 32%

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

* **Páginas do produto**: envia as informações sobre o produto específico exibido (este método é o modo de funcionamento do Recommendations)
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

  ```< > # % " { } | \ ^ [ ] ` ``` {line-numbers=&quot;true&quot;}

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

Recommendations: [implementação de acordo com o tipo de página](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=pt-BR)

Confirmação do pedido: [rastreia conversões](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

Afinidade de categorias: [afinidade de categorias](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=pt-BR)
