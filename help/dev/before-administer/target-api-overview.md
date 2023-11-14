---
title: Visão geral da API do Adobe Target
description: Visão geral das diferentes APIs do Adobe Target, incluindo api de entrega, api de relatórios, api de administração, api de perfil, api de recomendações e links para coleções do Postman.
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# Visão geral da API do Target

Este artigo descreve as diferentes APIs do Target em geral, antes de se concentrar nos requisitos específicos das APIs de administrador e perfil. Se quiser administrar o Target por meio da interface, consulte a [seção de administração do *Guia do usuário empresarial do Adobe Target*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).

## Tipos de API

As APIs do Adobe Target são uma coleção de APIs que alimentam os produtos da Adobe Target, como o Adobe Recommendations. Essas APIs permitem a criação de interfaces de usuário ricas em dados que podem ser usadas para manipular e integrar dados.

As APIs do Adobe Target podem ser agrupadas de acordo com o tipo: Administração, Perfil, Entrega e Relatórios.

>[!NOTE]
>
>As APIs de administrador e APIs de perfil geralmente são mencionadas coletivamente (&quot;APIs de administrador e perfil&quot;), mas também podem ser mencionadas separadamente (&quot;APIs de administrador&quot; e &quot;APIs de perfil&quot;). A API do Recommendations é uma implementação específica de uma API de administração do Target.

| Tipo de API | O que ele permite que você faça | Link de download | Outros links úteis |
| --- | --- | --- |--- |
| [Admin](../administer/admin-api/admin-api-overview-new.md) | Crie, modifique e exclua atividades, públicos, ofertas e outros objetos (incluindo entidades, critérios, designs da Recommendations e assim por diante). As APIs do Recommendations são um tipo de API de administração). | <UL><li>[Coleção de Postman da API de administração do Target](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Coleção de Postman da API do Recommendations](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman)</li></UL> | [Uso de APIs do Recommendations](../before-administer/recs-api/overview.md) |
| Perfil | Recupere e modifique perfis de usuário armazenados no Adobe Target. | [Coleção de Postman da API do perfil do Target](https://developers.adobetarget.com/api/#profiles) |  |
| [Entrega](../implement/delivery-api/overview.md) | Recupere conteúdo otimizado e personalizado do Target para entrega a um usuário final. | [Coleção de Postman da API de entrega do Target](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman) |  |
| [Relatório](../administer/admin-api/admin-api-overview-new.md) | Exportar resultados da atividade e outros resultados do relatório. | As APIs de relatórios estão incluídas no [Coleção de Postman da API de administração do Target](https://developers.adobetarget.com/api/#admin-postman-collection). |  |
| [Modelos](../administer/models-api/models-api-overview.md) | Gerencie a lista de recursos que você deseja que o Target exclua de seus modelos de aprendizado de máquina (o &quot;incluo na lista de bloqueios de pesquisa&quot;). A API de modelos é um tipo de API de administração, mas é listada aqui separadamente devido às suas operações exclusivas em relação a objetos (incluis na lista de bloqueios) não acessíveis por meio da interface do usuário. |  |  |

## Diferenças da API

Há importantes distinções entre as APIs de administrador do Target (incluindo as APIs do Recommendations) e as APIs de entrega do Target:

* As APIs de administrador permitem configurar vários aspectos do Target que também podem ser configurados na interface do usuário do Target. A exceção a isso é a API de modelos, que permite configurar aspectos do Target não disponíveis na interface do usuário. Independentemente disso, **todas as APIs de administrador exigem autenticação.**

* As APIs de entrega permitem recuperar o conteúdo. As APIs de entrega não exigem autenticação.

Para usar as APIs de administrador do Target, você deve configurar a autenticação usando o [Console do Adobe Developer](https://developer.adobe.com/console/home). Para obter mais informações, consulte [Como configurar a autenticação](../before-administer/configure-authentication.md).
