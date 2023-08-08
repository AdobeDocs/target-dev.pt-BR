---
title: Como buscar o Recommendations com a API de entrega
description: Este artigo orienta os desenvolvedores sobre as etapas necessárias para buscar conteúdo das recomendações usando a API de entrega do Adobe Target.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 9b391f42-2922-48e0-ad7e-10edd6125be6
source-git-commit: ba53161b2ec51af3d90994773034790feb51099c
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 1%

---

# Busca do Recommendations com a API de entrega

As APIs do Adobe Target e do Adobe Target Recommendations podem ser usadas para fornecer respostas a páginas da Web, mas também podem ser usadas em experiências não baseadas em HTML, incluindo aplicativos, telas, consoles, emails, quiosques e outros dispositivos de exibição. Em outras palavras, quando bibliotecas do Target e JavaScript não puderem ser usadas, a variável [API de entrega do Target](/help/dev/implement/delivery-api/overview.md) O ainda permite o acesso à gama completa de funcionalidades do Target, para fornecer experiências personalizadas.

>[!NOTE]
>
>Ao solicitar conteúdo contendo recomendações reais (produtos ou itens recomendados), use a API de entrega do Target.

Para recuperar recomendações, envie uma chamada de POST da API de entrega do Adobe Target com as informações contextuais apropriadas, que podem incluir uma ID de usuário (para uso com recomendações específicas do perfil, como os itens visualizados recentemente pelo usuário), nome da mbox relevante, parâmetros da mbox, parâmetros do perfil ou outros atributos. A resposta incluirá entity.ids recomendado (e pode incluir outros dados de entidade) no formato JSON ou HTML, que pode então ser exibido no dispositivo.

A variável [API de entrega](/help/dev/implement/delivery-api/overview.md) Para o Adobe Target, expõe todos os recursos existentes que uma solicitação padrão do Target fornece.

A API de entrega:

* Permite recuperar experiências ou ofertas para um local e um público-alvo de maneira RESTful.
* Não requer autenticação.
* Somente POSTs.
* Não processa cookies ou chamadas de redirecionamento.
* Não exige ou reconhece &quot;funções de usuário&quot;. Ele simplesmente busca conteúdo ou relata eventos para os servidores do Target Edge.

Para usar a API de entrega para fornecer experiências do Target, incluindo recomendações, siga estas etapas:

1. Crie uma atividade do Target (A/B, XT, AP ou Recommendations) usando o Criador baseado em formulário (não o Visual Experience Composer).
1. Use a API de entrega para obter uma resposta para as solicitações geradas pela atividade do Target que você acabou de criar.

&lt;!— P: Por que ambas as etapas são necessárias para isso? Se você tiver uma recomendação baseada em formulário definida para uma mbox, qual é o ponto/benefício de TAMBÉM ter a etapa da API de entrega na para recuperar resultados? Por que você não pode apenas ter o Rec baseado em formulário entregar os resultados no dispositivo de destino...? R: Veja o caso de uso abaixo... é quando você deseja &quot;interceptar&quot; os resultados pendentes para fazer mais coisas antes de exibir os resultados. Coisas como comparações em tempo real com níveis de inventário. --->

## Criar uma recomendação usando o Experience Composer baseado em formulário

Para criar recomendações que podem ser usadas com a API de entrega, use o [Compositor baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

1. Primeiro, crie e salve um design baseado em JSON para usar em sua recomendação. Para obter exemplos de JSON, mais informações de segundo plano sobre como as respostas JSON podem ser retornadas ao configurar uma atividade baseada em formulário, consulte a documentação em [Criação de Designs de Recomendação](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html). Neste exemplo, o design é nomeado como *JSON simples.*
   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

1. No Target, navegue até **[!UICONTROL Atividades]** > **[!UICONTROL Criar atividade]** > **[!UICONTROL Recommendations]** e selecione **[!UICONTROL Formulário]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

1. Selecione uma Propriedade e clique em **[!UICONTROL Próxima]**.
1. Defina o local em que você deseja que os usuários recebam a resposta da recomendação. O exemplo abaixo usa um local chamado *api_charter*. Selecione o design baseado em JSON, criado anteriormente, chamado *JSON simples.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
1. Salve e ative a recomendação. Ele gerará resultados. [Quando os resultados estiverem prontos](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), você pode usar a API de entrega para recuperá-los.

## Usar a API de entrega

A sintaxe para a variável [API de entrega](/help/dev/implement/delivery-api/overview.md) é:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Observe que o código de cliente é obrigatório. Como lembrete, o código de cliente pode ser encontrado no Adobe Target navegando até **[!UICONTROL Recommendations]** > **[!UICONTROL Configurações]**. Observe que **Código do cliente** valor no **Token da API de recomendação** seção.
   ![client-code.png](assets/client-code.png)
1. Depois de ter o código de cliente, crie a chamada da API de entrega. O exemplo abaixo começa com **[!UICONTROL Chamada da API de entrega de mboxes em lote na Web]** fornecido na [Coleção de Postman da API de entrega](../../implement/delivery-api/overview.md/#section/Getting-Started/Postman-Collection), fazendo as modificações relevantes. Por exemplo:
   * o **navegador** e **endereço** objetos foram removidos do **Corpo**, já que não são necessários para casos de uso que não sejam de HTML
   * *api_charter* está listado como o nome do local neste exemplo
   * entity.id está especificada, pois esta recomendação se baseia na Similaridade de Conteúdo, que requer que uma chave de item atual seja passada para o Target.
     ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
Lembre-se de configurar os parâmetros de consulta corretamente. Por exemplo, especifique `{{CLIENT_CODE}}` conforme necessário. &lt;!— P: Na sintaxe de chamada atualizada, entity.id é listado como um profileParameter em vez de um mboxParameter como nas versões mais antigas. ---> &lt;!— Q: Imagem antiga ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Antigo texto de acompanhamento: &quot;Observe que esta recomendação se baseia nos produtos Content Similares baseados no entity.id enviado via mboxParameters.&quot; —>
     ![client-code3](assets/client-code3.png)
1. Envie a solicitação. Isso é executado em relação ao *api_charter* O local, que tem uma recomendação ativa em execução, definido com seu design JSON que gerará uma lista de entidades recomendadas.
1. Receba uma resposta com base no design JSON.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
A resposta inclui a ID de chave, bem como as IDs de entidade das entidades recomendadas.

Usar a API de entrega com o Recommendations dessa maneira permite executar etapas adicionais antes de exibir recomendações para o visitante no dispositivo não HTML. Por exemplo, você pode obter a resposta da API de entrega para executar uma pesquisa adicional em tempo real dos detalhes do atributo da entidade (inventário, preço, classificação e assim por diante) de outro sistema (como um CMS, PIM ou plataforma de comércio eletrônico), antes de exibir os resultados finais.

Usando a abordagem descrita neste guia, você pode obter qualquer aplicativo para aproveitar a resposta do Target e fornecer recomendações personalizadas.

## Exemplo de implementações

Os recursos a seguir fornecem exemplos de várias implementações não focadas em HTML. Lembre-se de que cada implementação será única, devido ao sistema e aos dispositivos envolvidos.

| Recurso | Detalhes |
| --- | --- |
| [Adobe Target em qualquer lugar - Implementar o Server Side ou na IoT](https://expleague.azureedge.net/labs/L733/index.html) | Laboratório Adobe Summit 2019 que oferece experiência prática para um aplicativo React que usa APIs do lado do servidor Adobe Target. |
| [Adobe Target em um aplicativo móvel sem o SDK do Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Este guia mostra como configurar o Adobe Target no aplicativo móvel sem instalar o SDK do Adobe. Essa solução usa a visualização da Web do SDK do Tealium e o módulo de Comandos remotos para enviar e receber solicitações para a API de visitante do Adobe (Experience Cloud) e para a API do Adobe Target. |
| [Configuração da extensão do Target no Experience Platform Launch e implementação das APIs do Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/) | Etapas para configurar a extensão do Target no Experience Platform Launch, adicionar a extensão do Target ao seu aplicativo e implementar APIs do Target para solicitar atividades, realizar uma busca prévia por ofertas e entrar no modo de visualização visual. |
| [Cliente de nó Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | SDK v1.0 da Target Node.js de código aberto |
| [Visão geral do lado do servidor](../../implement/server-side/server-side-overview.md) | Informações sobre APIs de entrega do lado do servidor do Adobe Target, APIs de entrega em lote do servidor, SDK do Node.js e APIs do Adobe Target Recommendations. |
| [Recommendations de conteúdo do Adobe Campaign no email](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog que descreve como aproveitar as recomendações de conteúdo em emails por meio do Adobe Target e do Adobe I/O Runtime no Adobe Campaign. |

## Gerenciamento da configuração do Recommendations com APIs

Na maioria das vezes, as recomendações são configuradas na interface do usuário do Adobe Target e, em seguida, usadas ou acessadas por meio das APIs do Target, por motivos como os mencionados nas seções acima. Essa coordenação UI-API é comum. No entanto, às vezes os usuários podem querer executar todas as ações por meio das APIs, tanto a configuração quanto o uso dos resultados. Embora seja muito menos comum, os usuários podem configurar, executar e *e* Aproveite os resultados das recomendações totalmente usando as APIs.

Aprendemos em um [seção anterior](manage-catalog.md) como gerenciar entidades do Adobe Target Recommendations e fornecê-las no lado do servidor. Do mesmo modo, a [Console do Adobe Developer](https://developer.adobe.com/console/home) O permite gerenciar critérios, promoções, coleções e modelos de design sem precisar fazer logon no Adobe Target. Uma lista completa de todas as APIs do Recommendations pode ser encontrada [aqui](http://developers.adobetarget.com/api/recommendations/), mas aqui está um resumo para referência.

| Recurso | Detalhes |
| --- | --- |
| [Coleções](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Liste, crie, obtenha, edite e exclua coleções. |
| [Critérios](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Listar e obter critérios. |
| [Designs](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Liste, crie, obtenha, edite, exclua e valide designs. |
| [Entidades](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Salvar, excluir e obter entidades. |
| [Promoções](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Liste, crie, obtenha, edite e exclua promoções. |
| [Critérios da categoria](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Liste, crie, obtenha, edite e exclua critérios de categoria. |
| [Critérios personalizados](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Liste, crie, obtenha, edite e exclua critérios personalizados. |
| [Critérios de item](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Listar, criar, obter, editar e excluir critérios de item. |
| [Critério de popularidade](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Liste, crie, obtenha, edite e exclua critérios de popularidade. |
| [Critérios de atributo de perfil](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Liste, crie, obtenha, edite e exclua critérios de atributo de perfil. |
| [Critério recente](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Listar, criar, obter, editar e excluir critérios recentes. |
| [Critérios de sequência](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Liste, crie, obtenha, edite e exclua critérios de sequência. |

## Documentação de referência

* [Documentação da API de entrega do Adobe Target](/help/dev/implement/delivery-api/overview.md)
* [Integração do Recommendations ao email](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Resumo e revisão

Parabéns! Ao concluir este guia, você aprendeu a:
* [Gerencie seu catálogo usando a API do Recommendations](manage-catalog.md)
* [Gerenciar critérios personalizados usando a API do Recommendations](manage-custom-criteria.md)
* [Usar a API de entrega com o Recommendations](fetch-recs-server-side-delivery-api.md)
