---
title: Como gerenciar o catálogo do Recommendations usando APIs
description: Etapas necessárias para usar APIs do Adobe Target para criar, atualizar, salvar, obter e excluir entidades no catálogo do Recommendations.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: aea82607-cde4-456a-8dfb-2967badce455
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Gerencie seu catálogo do Recommendations usando APIs

Ao garantir que você atenda aos [requisitos para usar a API de Recommendations](/help/dev/before-administer/recs-api/overview.md#prerequisites), você aprendeu a [gerar um token de acesso](/help/dev/before-administer/configure-authentication.md) usando o fluxo de autenticação JWT para usar as APIs de Administrador [!DNL Adobe Target] na [Adobe Developer Console](https://developer.adobe.com/console/home).

Agora você pode usar as [APIs do Recommendations](https://developer.adobe.com/target/administer/recommendations-api/) para adicionar, atualizar ou excluir itens do catálogo de recomendações. Assim como no restante das APIs de administrador do Adobe Target, as APIs do Recommendations exigem autenticação.

>[!NOTE]
>
>Envie a solicitação **[!UICONTROL IMS: JWT Generate + Auth via User Token]** sempre que precisar atualizar o token de acesso para autenticação, pois ela expira após 24 horas. Consulte [Configurar a autenticação da API do Adobe](../configure-authentication.md) para obter instruções.

![JWT3ff](assets/configure-io-target-jwt3ff.png)

Antes de continuar, obtenha a [coleção do Recommendations Postman](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman).

## Criação e atualização de itens com a API Salvar entidades

Para preencher o banco de dados de produtos do Recommendations usando a API em vez de um feed de produto CSV ou de solicitações do Target sendo acionadas nas páginas de produtos, use a [API Salvar Entidades](https://developer.adobe.com/target/administer/recommendations-api/#operation/saveEntities). Esta solicitação adiciona ou atualiza um item em um único ambiente do Target. A sintaxe é:

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

Por exemplo, Salvar Entidades pode ser usado para atualizar itens sempre que certos limites forem atingidos - como limites para estoque ou preço - para sinalizar esses itens e evitar que eles sejam recomendados.

1. Navegue até **[!UICONTROL Target]** > **[!UICONTROL Setup]** > **[!UICONTROL Hosts]** > **[!UICONTROL CONTROL Environments]** para obter a ID de Ambiente de Destino na qual você deseja adicionar ou atualizar um item.

   ![SaveEntities1](assets/SaveEntities01.png)

1. Verifique se `TENANT_ID` e `API_KEY` fazem referência às variáveis de ambiente do Postman estabelecidas anteriormente. Use a imagem abaixo para comparação. Se necessário, modifique os cabeçalhos e o caminho na solicitação de API para corresponder aos da imagem abaixo.

   ![SaveEntities3](assets/SaveEntities03.png)

1. Insira seu JSON como código **raw** no **Corpo**. Não se esqueça de especificar sua ID de ambiente, usando a variável `environment`. (No exemplo abaixo, a ID de ambiente é 6781.)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   Abaixo está um exemplo de JSON que adiciona o entity.id kit2001 com valores de entidade associados para um produto de Forno de torradeira, no ambiente 6781.

   ```
       {
       "entities": [{
               "name": "Toaster Oven",
               "id": "kit2001",
               "environment": 6781,
               "categories": [
                   "housewares:appliances"
               ],
               "attributes": {
                   "inventory": 77,
                   "margin": 23,
                   "message": "crashing helicopter",
                   "pageUrl": "www.foobar.foo.com/helicopter.html",
                   "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
               }
           }]
       }
   ```

1. Clique em **[!UICONTROL Send]**. Você deve receber a seguinte resposta.

   ![SaveEntities5.png](assets/SaveEntities05.png)

   O objeto JSON pode ser dimensionado para enviar vários produtos. Por exemplo, esse JSON especifica duas entidades.

   ```
       {
           "entities": [{
                   "name": "Toaster Oven",
                   "id": "kit2001",
                   "environment": 6781,
                   "categories": [
                       "housewares:appliances"
                   ],
                   "attributes": {
                       "inventory": 89,
                       "margin": 11,
                       "message": "Toaster Oven",
                       "pageUrl": "www.foobar.foo.com/helicopter.html",
                       "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                       "value": 102.5
                   }
               },
               {
                   "name": "Blender",
                   "id": "kit2002",
                   "environment": 6781,
                   "categories": [
                       "housewares:appliances"
                   ],
                   "attributes": {
                       "inventory": 36,
                       "margin": 5,
                       "message": "Blender",
                       "pageUrl": "www.foobar.foo.com/helicopter.html",
                       "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                       "value": 54.5
                   }
               }
           ]
       }
   ```

1. Agora é a sua vez! Use a API **[!UICONTROL Save Entities]** para adicionar os seguintes itens ao catálogo. Use a amostra JSON acima como ponto de partida. (Será necessário estender o JSON para incluir entidades adicionais.)

   ![SaveEntities6.png](assets/SaveEntities06.png)

Parece que esses dois últimos itens não pertencem. Vamos inspecioná-los usando a API **[!UICONTROL Get Entity]** e, se necessário, excluí-los usando a API **[!UICONTROL Delete Entities]**.

## Obter detalhes do item com a API Obter entidade

Para recuperar os detalhes de um item existente, use a [Obter API de Entidade](https://developer.adobe.com/target/administer/recommendations-api/#operation/getEntity). A sintaxe é:

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

Os detalhes da entidade só podem ser recuperados para uma única entidade de cada vez. Você pode usar Obter entidade para confirmar que as atualizações foram feitas no catálogo conforme esperado ou para auditar o conteúdo do catálogo de outra forma.

1. Na solicitação de API, especifique a ID da entidade, usando a variável `entityId`. O exemplo a seguir retornará detalhes para a entidade cuja entityId=kit2004.

   ![GetEntity1](assets/GetEntity1.png)

1. Verifique se `TENANT_ID` e `API_KEY` fazem referência às variáveis de ambiente do Postman estabelecidas anteriormente. Use a imagem abaixo para comparação. Se necessário, modifique os cabeçalhos e o caminho na solicitação de API para corresponder aos da imagem abaixo.

   ![GetEntity2](assets/GetEntity2.png)

1. Envie a solicitação.

   ![GetEntity3](assets/GetEntity3.png)
Se você receber um erro informando que a entidade não foi encontrada, como mostrado no exemplo acima, verifique se está enviando a solicitação para o ambiente correto do Target.



   >[!NOTE]
   >
   >Se nenhum ambiente for especificado explicitamente, Obter Entidade tentará obter a entidade somente do seu [ambiente padrão](https://experienceleague.adobe.com/docs/target/using/administer/environments.html?lang=pt-BR). Se quiser extrair de qualquer ambiente que não seja o ambiente padrão, especifique a ID do ambiente.

1. Se necessário, adicione o parâmetro `environmentId` e reenvie a solicitação.

   ![GetEntity4](assets/GetEntity4.png)

1. Envie outra solicitação **[!UICONTROL Get Entity]**, desta vez para inspecionar a entidade cuja entityId=kit2005.

   ![GetEntity5](assets/GetEntity5.png)

Suponha que você decida que essas entidades precisam ser removidas do catálogo. Vamos usar a API **[!UICONTROL Delete Entities]**.

## Exclusão de itens com a API Excluir entidades

Para remover itens do catálogo, use a [API de Exclusão de Entidades](https://developer.adobe.com/target/administer/recommendations-api/#operation/deleteEntities). A sintaxe é:

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
>
>A API Excluir entidades exclui entidades referenciadas pelas IDs especificadas. Se nenhuma ID de entidade for fornecida, todas as entidades em um determinado ambiente serão excluídas. Se nenhuma ID de ambiente for fornecida, as entidades serão excluídas de todos os ambientes. Use isso com cuidado!

1. Navegue até **[!UICONTROL Target]** > **[!UICONTROL Setup]** > **[!UICONTROL Hosts]** > **[!UICONTROL Environments]** para obter a ID de Ambiente de Destino da qual deseja excluir itens.

   ![ExcluirEntidades1](assets/SaveEntities01.png)

1. Na solicitação de API, especifique as IDs de entidade das entidades que deseja excluir, usando a sintaxe `&ids=[comma-delimited-entity-ids]` (um parâmetro de consulta). Ao excluir mais de uma entidade, separe as IDs usando vírgulas.

   ![ExcluirEntidades2](assets/DeleteEntities2.png)

1. Especifique a ID de ambiente, usando a sintaxe `&environment=[environmentId]`; caso contrário, as entidades em todos os ambientes serão excluídas.

   ![ExcluirEntidades3](assets/DeleteEntities3.png)

1. Verifique se `TENANT_ID` e `API_KEY` fazem referência às variáveis de ambiente do Postman estabelecidas anteriormente. Use a imagem abaixo para comparação. Se necessário, modifique os cabeçalhos e o caminho na solicitação de API para corresponder aos da imagem abaixo.

   ![ExcluirEntidades4](assets/DeleteEntities4.png)

1. Envie a solicitação.

   ![ExcluirEntidades5](assets/DeleteEntities5.png)

1. Verifique os resultados usando **[!UICONTROL Get Entity]**, que agora deve indicar que as entidades excluídas não foram encontradas.

   ![ExcluirEntidades6](assets/DeleteEntities6.png)

   ![ExcluirEntidades6](assets/DeleteEntities7.png)

Parabéns! Agora você pode usar as APIs do Recommendations para criar, atualizar, excluir e obter detalhes sobre as entidades no catálogo. Na próxima seção, você aprenderá a gerenciar critérios personalizados.

&lt;!— [Próximo &quot;Gerenciar Critérios Personalizados&quot; >](manage-custom-criteria.md) —>
