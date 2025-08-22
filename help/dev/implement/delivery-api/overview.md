---
title: Visão geral da API de entrega do Adobe Target
description: Visão geral da API de entrega do Adobe Target
keywords: api de entrega
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
source-git-commit: ccc27e66207e58dcd33865e5d28a51644e8e1931
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Visão geral da API de entrega

O [!DNL Adobe Target Delivery API] é baseado em REST. Esta documentação descreve os recursos que compõem o [!DNL Adobe Target] [!DNL Delivery API]. Os métodos HTTP são utilizados para executar operações nesses recursos.

Usando o [!UICONTROL Adobe Target's Delivery API], você pode:

* Ofereça experiências na Web, incluindo SPAs e canais móveis, bem como dispositivos IoT não baseados em navegador, como TV conectada, quiosque ou tela digital na loja.
* Fornecer experiências de qualquer plataforma ou aplicativo do lado do servidor que possa fazer chamadas HTTP/s.
* Ofereça experiências consistentes e personalizadas a um usuário, independentemente do canal ou dos dispositivos que o usuário tenha envolvido em sua empresa.
* Armazene em cache experiências de um usuário em uma sessão no seu servidor, para que várias chamadas de API possam ser evitadas e, como resultado, alcançar um desempenho melhor.
* Integre facilmente com [!DNL Adobe Experience Cloud] produtos, como [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] e o [!DNL Experience Cloud ID Service] a partir do lado do servidor.

>[!IMPORTANT]
>
>Tenha cuidado ao atualizar o [!DNL Recommendations] [!UICONTROL Catalog] via [!DNL Delivery API]. O [!DNL Delivery API] é público, portanto, evite usá-lo para preencher itens clicáveis no catálogo de recomendações. Isso pode apresentar conteúdo invalidado e poluir seu catálogo.
>
>Práticas recomendadas:
>
>Use o [!DNL Delivery API] somente para atualizar atributos de catálogo que:
>* Mude com frequência (por exemplo, preço, nível de estoque).
>* Siga um formato predefinido que possa ser facilmente validado no seu site.
>* Não o use para adicionar ou modificar itens clicáveis ou outro conteúdo não verificado.
>
>Se necessário, você pode solicitar ao suporte ao cliente que desative as atualizações de catálogo por meio da API de entrega.

Para obter mais informações, consulte a documentação de [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}.

>[!NOTE]
>
>Você ainda pode acessar a [documentação da API /v1/mbox herdada e /v2/batchmbox](https://developers.adobetarget.com/api/legacy-api/index.html). No entanto, os recursos serão desenvolvidos na API de entrega (conforme documentado aqui), que não terá suporte para as APIs herdadas.
