---
keywords: Recommendations, configurações, preferências, vertical do setor, critérios incompatíveis com o filtro, grupo de hosts padrão, url de base em miniatura, token de api do recommendations, $9
description: Saiba como implementar o [!UICONTROL Recommendations] atividades no [!DNL Adobe Target].
title: Como implementar o [!UICONTROL Recommendations] Atividades?
feature: Recommendations
exl-id: af1e8b60-6dbb-451b-aa4f-e167d1800d1c
source-git-commit: 777c8b9aeb866e1b20ec24e85532a99f57d1fe72
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 25%

---

# Planejar e implementar [!UICONTROL Recommendations]

Informações para ajudá-lo a planejar e implementar [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Para além deste artigo, a [Guia do profissional de negócios do Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=pt-BR){target=_blank} contém informações detalhadas sobre [Recommendations do Target](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html){target=_blank}.

Antes de configurar seu primeiro [!UICONTROL Recommendations] atividade no [!DNL Adobe Target], conclua as seguintes etapas:

1. [Implementar [!UICONTROL Target]](#implement-target) na Web e nas superfícies de aplicativos móveis que você deseja usar para capturar o comportamento do usuário e fornecer recomendações.
1. [Configure seu [!UICONTROL Recommendations] catálogo](#set-up-your-recommendations-catalog) de produtos ou conteúdo que deseja recomendar aos usuários.
1. [Transmitir informações comportamentais e contexto](#pass-behavioral-information-and-context) para [!DNL Target Recommendations] para permitir que ele forneça recomendações personalizadas.
1. [Configurar exclusões globais](#configure-global-exclusions).
1. [Configurar [!UICONTROL Recommendations] configurações](#configure-recommendations-settings).
1. (Opcional) [Administrar [!UICONTROL Recommendations] uso de APIs de administrador](#administer-recommendations-using-admin-apis).

## 1. Implementar [!UICONTROL Target]

[!DNL Target Recommendations] O requer a implementação do Adobe Experience Platform Web SDK ou da at.js 0.9.2 (ou posterior). Consulte a [[!UICONTROL Target] guias de implementação do lado do cliente](../client-side/overview.md) para obter mais informações.

## 2. Configure seu [!UICONTROL Recommendations] catálogo

Para fornecer recomendações de alta qualidade, [!UICONTROL Target] O deve saber sobre os produtos ou conteúdo que deseja recomendar. Os catálogos normalmente incluem três tipos de informações sobre itens recomendados. Suponha que você esteja recomendando filmes. Inclua o seguinte:

1. Os dados que você deseja exibir para o usuário que recebe a recomendação. Por exemplo, é possível exibir o nome do filme e um URL para uma imagem em miniatura do pôster do filme.
1. Dados úteis para aplicar controles de marketing e merchandising. Por exemplo, você pode exibir a classificação do filme para que não recomende filmes NC-17.
1. Dados úteis para determinar a similaridade dos itens com outros itens. Por exemplo, é possível exibir o gênero do filme e o diretor do filme.

[!UICONTROL Target] O oferece várias opções de integração para preencher o catálogo. Essas opções podem ser usadas em combinação para atualizar diferentes itens no catálogo ou atualizar diferentes atributos de item em diferentes frequências.

| Método | O que é | Quando usar | Informações adicionais |
| --- | --- | --- | --- |
| Feed do catálogo | Programe um feed (CSV, XML do produto do Google ou Classificações do produto Analytics) para ser carregado e assimilado diariamente. | Para enviar informações sobre vários itens de cada vez. Para enviar informações que são alteradas com pouca frequência. | Consulte [Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html). |
| API de entidades | Chame uma API para enviar atualizações de minuto para um único item. | Para enviar atualizações que ocorrem sobre um item de cada vez. Para enviar informações que mudam com frequência (por exemplo, preço, nível de estoque/estoque). | Consulte a [Documentação do desenvolvedor da API de entidades](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Enviar atualizações na página | Envie atualizações de minuto a minuto para um único item usando JavaScript na página ou usando a API de entrega. | Para enviar atualizações que ocorrem sobre um item de cada vez. Para enviar informações que mudam com frequência (por exemplo, preço, nível de estoque/estoque). | Consulte [Exibições de item/páginas de produto](#item-views-or-product-pages) abaixo. |

A maioria dos clientes deve implementar pelo menos um feed. Em seguida, você pode optar por complementar seu feed com atualizações para atributos ou itens alterados com frequência usando a API de entidades ou o método na página.

## 3. Transmitir informações comportamentais e contexto

As informações comportamentais e o contexto que você deve transmitir para [!UICONTROL Target] depende da ação que seu visitante está tomando, o que geralmente está associado ao tipo de página com a qual seu visitante está interagindo.

### Exibições de item ou páginas de produto

Nas páginas em que um visitante está visualizando um único item, como uma página de detalhes do produto, você deve transmitir a identidade do item que o visitante está visualizando. Você também deve passar a categoria mais granular do item que o visitante está visualizando, para permitir a filtragem de recomendações para a categoria atual.

Você também pode transmitir determinados atributos que mudam rapidamente na própria página do produto. Por exemplo, você pode passar o preço (`value`) e nível de estoque/estoque.

#### Transmitir preço e estoque

```js {line-numbers="true"}
<script type="text/javascript">
function targetPageParams() { 
   return { 
      "entity": { 
         "id": "32323", 
         "categoryId": "running-shoes", 
         "value": 119.99, 
         "inventory": 329 
      } 
   } 
}
</script>
```

### Visualizações de categoria/páginas de categoria

Em uma página de categoria, é provável que você queira restringir suas recomendações a produtos ou conteúdo dentro dessa categoria. Para fazer isso, transmita a identidade da categoria visualizada atualmente.

#### Passar categoria atual

```js {line-numbers="true"}
function targetPageParams() { 
   return { 
      "entity": { 
         "categoryId": "running-shoes" 
      } 
   } 
}
```

### Páginas de inclusão do carrinho/exibição do carrinho/check-out

Em uma página de carrinho, você pode recomendar itens com base no conteúdo do carrinho atual do visitante. Para fazer isso, passe as IDs de todos os itens no carrinho atual do visitante usando o parâmetro especial `cartIds`.

#### Envio de itens atualmente no carrinho

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Para obter mais informações sobre as recomendações baseadas em carrinho, consulte [Baseado em carrinho](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based) no *[!DNL Adobe Target]Guia do profissional de negócios do*.

### Excluir itens que já estão no carrinho do visitante

Nas páginas de todo o site, você pode excluir alguns itens das recomendações. Por exemplo, talvez você não queira recomendar itens que já estejam no carrinho atual do visitante. Para fazer isso, passe as IDs de todos os itens que deseja excluir usando o parâmetro especial `excludedIds`.

#### Enviar itens para exclusão

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Páginas de compras/confirmação de pedido

Quando ocorrer um evento de compra, transmitir a identidade do(s) item(ns) comprado(s). Consulte [Rastrear conversões](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) no [Como implantar a at.js > Implementar [!UICONTROL Target] sem um gerenciador de tags](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) artigo.

## 4. Configurar exclusões globais

Exclua todos os itens em um nível global que você nunca deseja recomendar a um visitante. Consulte [Exclusões](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/exclusions.html) no *[!DNL Adobe Target]Guia do profissional de negócios do*.

## 5. Configurar [!UICONTROL Recommendations] configurações

Use as configurações para gerenciar a sua implementação do [!UICONTROL Recommendations].

Para acessar o **[!UICONTROL Recommendations Settings]** opções, abra o Target na [!DNL Adobe Experience Cloud]e, em seguida, clique em **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]**.

![Página Configurações do Recommendations](/help/dev/implement/recommendations/assets/recs_settings.png)

As opções disponíveis são as seguintes:

| Configuração | Descrição |
|--- |--- |
| Mbox global personalizada | (Opcional) especifique a mbox personalizada global usada para atender às atividades do [!UICONTROL Target]. Por padrão, a mbox global usada por [!UICONTROL Target] é usado para [!UICONTROL Recommendations].<P>Observação: essa opção é definida na guia [!UICONTROL Target] **[!UICONTROL Administration]** página. Abertura [!UICONTROL Target]e, em seguida, clique em **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]**. |
| Vertical do setor | O vertical do setor é usado para ajudar a categorizar os critérios de recomendação. Essas informações ajudam os membros da equipe a encontrar critérios que fazem sentido para uma página específica, como critérios melhores para a página do carrinho de compras ou para uma página de mídia. |
| Filtrar critérios incompatíveis | Ative essa opção para mostrar apenas os critérios pelos quais a página selecionada passa os dados solicitados. Nem todos os critérios são executados corretamente em cada página. A página ou mbox deve passar no `entity.id` ou `entity.categoryId` para que as recomendações do item atual/categoria atual sejam compatíveis. Em geral, é melhor mostrar apenas critérios compatíveis. No entanto, se você desejar que critérios incompatíveis estejam disponíveis para a atividade, desmarque essa opção.<P>É recomendável desativar esta opção se estiver usando uma solução de gerenciamento de tags.<P>Para obter mais informações sobre essa opção, consulte [[!UICONTROL Recommendations] Perguntas frequentes](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html) no *[!DNL Adobe Target]Guia do profissional de negócios do*. |
| Grupo de host padrão | Selecione seu grupo de hosts padrão.<P>O grupo de hosts pode ser usado para separar os itens disponíveis no catálogo para usos diferentes. Por exemplo, você pode usar grupos de hosts para os ambientes de Desenvolvimento e Produção, para diferentes marcas ou diferentes regiões. Por padrão, os resultados de visualização na Pesquisa no catálogo, nas Coleções e nas Exclusões estão baseados no grupo de hosts padrão. (Também é possível selecionar um grupo de hosts diferente para visualizar os resultados, usando o filtro Ambiente.) Por padrão, os itens recém adicionados ficam disponíveis em todos os grupos de hosts, a menos que uma ID de ambiente seja especificada ao criar ou atualizar o item. As recomendações entregues dependem do grupo de hosts especificado na solicitação.<P>Se você não visualiza seus produtos, certifique-se de que você esteja usando o grupo correto de hosts. Por exemplo, se você configurar sua recomendação para usar um ambiente de preparo e você definir o grupo de hosts para Armazenamento temporário, você pode necessitar recriar suas coleções no ambiente de preparo para serem mostradas pelos produtos. Para ver quais produtos estão disponíveis em cada ambiente, use a Pesquisa de catálogo com cada ambiente. Também é possível visualizar o conteúdo de [!UICONTROL Recommendations] coleções e exclusões para um ambiente selecionado (grupo de hosts).<P>**Nota:** Depois de alterar o ambiente selecionado, clique em Pesquisar para atualizar os resultados retornados.<P> **[!UICONTROL The Environment]** O filtro está disponível nos seguintes locais na interface do usuário do Target:<ul><li>Pesquisa no catálogo (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)</li><li>Caixa de diálogo Criar coleção (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create New]**)</li><li>Caixa de diálogo Atualizar coleção (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)</li><li>Caixa de diálogo Criar exclusão (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create New]**)</li><li>Caixa de diálogo Atualizar exclusão (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)</li></ul>Para obter mais informações, consulte [Hosts](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) no *[!DNL Adobe Target]Guia do profissional de negócios do*. |
| URL de base de miniatura | Definir um URL base para o seu catálogo de produtos possibilita o uso de URLs relativos ao especificar miniaturas dos produtos ao enviar no seu URL em miniatura.<P>Por exemplo:<P>`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`<P>define um URL relativo à URL de base de miniatura. |
| [!UICONTROL Recommendations] Token de API | Usar este token no [!UICONTROL Recommendations] Chamadas de API, como Baixar API. |

## 6. (Opcional) Administrar [!UICONTROL Recommendations] uso de APIs de administrador

Consulte a [Uso [!UICONTROL Recommendations] APIs](../../before-administer/recs-api/overview.md) guia prático para saber como configurar e usar o [!UICONTROL Target] APIs de administração e entrega para [!UICONTROL Recommendations].
