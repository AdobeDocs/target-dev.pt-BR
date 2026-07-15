---
keywords: eventos personalizados, at.js, falha de solicitação, solicitação com êxito, falha na renderização de conteúdo, renderização de conteúdo com êxito, biblioteca carregada, início da solicitação, início da renderização de conteúdo, renderização de conteúdo não há ofertas, redirecionamento de renderização de conteúdo, eventos personalizados2
description: Use eventos personalizados para que a biblioteca de JavaScript da at.js [!DNL Adobe Target] seja notificada quando uma solicitação de mbox ou oferta falhar ou for bem-sucedida.
title: Como usar os eventos personalizados da at.js?
feature: at.js
exl-id: a4baed9a-9eb8-4343-9834-709b03e44ca2
TQID: https://experienceleague.adobe.com/gCjLJ-XBlMe-GE-gaTJ2wHkn1jmal6Ftbs1GDb0zURA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: a1af9d2c909d9b3d506dd4875d1bd75149dbf636
workflow-type: tm+mt
source-wordcount: 661
ht-degree: 70%

---

# Eventos personalizados da at.js

Informações sobre `at.js custom events`, que informam quando uma solicitação ou oferta de mbox falha ou é bem-sucedida.

Historicamente, a mbox.js (descontinuada) não permitiu que outro código do JavaScript executado na página saiba o que acontece nos bastidores. Com o avanço da at.js, tivemos uma oportunidade única de corrigir este problema.

De acordo com nossos clientes, há vários cenários dos quais eles gostariam de ser notificados, incluindo:

* Uma falha em uma solicitação da mbox devido ao tempo limite, código do status incorreto, erro de análise do JSON, etc.
* Uma solicitação da mbox foi bem-sucedida.
* Falha na renderização da oferta devido à ausência do elemento da mbox de encapsulamento, não foi possível encontrar o seletor, etc.
* Renderização de oferta bem-sucedida. As alterações de DOM foram aplicadas.

Os eventos predefinidos têm uma estrutura que permite que você extraia os dados necessários conforme o tipo de evento.

Para certificar-se de que os eventos possam ser usados em diferentes cenários, os eventos personalizados têm um objeto de carga que é atribuído à propriedade detalhada do objeto do evento (que é transmitido ao manipulador). Para evitar, também, transmitir sequências de caracteres como nomes de evento, os eventos são expostos como constantes usando o namespace `adobe.target.event`.

## Estrutura

| Chave | Tipo | Descrição |
|--- |--- |--- |
| type | String | Há vários cenários em que você gostaria de receber notificações para ajudar com o rastreamento, depuração e personalização da interação com a at.js.<p>Cada evento personalizado listado abaixo tem dois formatos: um &quot;constante&quot; e um &quot;valor em sequência&quot;.<ul><li>**Constantes**: Prefixado com `adobe.target.event.`, apresentado em todas as maiúsculas e contém caracteres sublinhados. Para se inscrever em eventos personalizados *após* o carregamento da at.js, mas *antes* de receber a resposta da mbox, use o constante.</li><li>**Valores da string**: Minúsculas e contêm hifens. Para se inscrever em eventos personalizados *antes* do carregamento da at.js, use os valores em sequência.</li></ul>**Solicitação com Falha**<p>Constante: `adobe.target.event.REQUEST_FAILED`<p>Valor da cadeia de caracteres: `at-request-failed`<p>Descrição: Uma falha em uma solicitação da mbox devido ao tempo limite, código do status incorreto, erro de análise do JSON, etc.<p>**Solicitação bem-sucedida**<p>Constante: `adobe.target.event.REQUEST_SUCCEEDED`<p>Valor da Cadeia: `at-request-succeeded`<p>Descrição: Uma solicitação da mbox foi bem-sucedida.<p>**Falha na renderização do conteúdo**<p>Constante: `adobe.target.event.CONTENT_RENDERING_FAILED`<p>Valor da Cadeia: `at-content-rendering-failed`<p>Descrição: Falha na renderização da oferta devido à ausência do elemento da mbox de encapsulamento, não foi possível encontrar o seletor, etc.<p>**Renderização do conteúdo bem-sucedida**<p>Constante: `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`<p>Valor da Cadeia: `at-content-rendering-succeeded`<p>Descrição: A renderização da oferta foi bem-sucedida. As alterações de DOM foram aplicadas.<p>**Biblioteca carregada**<p>Constante: `adobe.target.event.LIBRARY_LOADED`<p>Valor da Cadeia: `at-library-loaded`<p>Descrição: este evento é ideal para monitorar quando a at.js tiver sido totalmente carregada. Você pode usar este evento para personalizar a execução da mbox global. Você também pode usar este evento para desativar a mbox global e depois ouvir este evento disparar a mbox global posteriormente.<p>**Início da solicitação**<p>Constante: `adobe.target.event.REQUEST_START`<p>Valor da Cadeia: `at-request-start`<p>Descrição: este evento é disparado antes que uma solicitação HTTP seja executada. Você pode usar este evento para avaliações de desempenho usando a API do Resource Timing.<p>**Início da renderização do conteúdo**<p>Constante: `adobe.target.event.CONTENT_RENDERING_START`<p>Valor da Cadeia: `at-content-rendering-start`<p>Descrição: este é evento é disparado antes que a pesquisa do seletor seja iniciada e o conteúdo seja renderizado para a página. Você pode usar este evento para monitorar o progresso da renderização de conteúdo.<p>**Renderização do conteúdo sem ofertas**<p>Constante: `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`<p>Valor da Cadeia: `at-content-rendering-no-offers`<p>Descrição: Este evento é disparado quando não há retorno de ofertas.<p>**Redirecionamento da renderização do conteúdo**<p>Constante: `adobe.target.event.CONTENT_RENDERING_REDIRECT`<p>Valor da Cadeia: `at-content-rendering-redirect`<p>Descrição: Esse evento é disparado quando uma oferta é redirecionada e [!DNL Target] redirecionará para uma URL diferente. |
| mbox | String | nome da mbox |
| message | String | Contém descrição para leitura humana, como o que aconteceu, mensagem de erro, etc. |
| rastreamento | Objeto | Contém o `sessionId` e `deviceId`. Em alguns casos, o `deviceId` pode estar ausente, porque o [!DNL Target] não foi capaz de recuperá-lo do servidor do Edge. |
| type | String | **Artefato de decisão no dispositivo bem-sucedido**<p>Constante:<p>`adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`<p>Valor da cadeia de caracteres: `artifactDownloadSucceeded`<p>Descrição: chamado quando o artefato de decisão no dispositivo é baixado com êxito.<p>**Falha no artefato de decisão no dispositivo**<p>Constante: `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`<p>Valor da Cadeia: `artifactDownloadFailed`<p>Descrição: chamado quando ocorria uma falha no download do artefato de decisão no dispositivo. |

## Uso

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(event) { 
  console.log('Event', event); 
});
```

## Vídeo de treinamento: tokens de resposta e os eventos personalizados da at.js ![Selo do tutorial](../../../assets/tutorial.png)

Assista ao vídeo a seguir para saber como usar Tokens de resposta e Eventos personalizados de at.js para compartilhar informações de perfil do [!DNL Target] com sistemas de terceiros.

>[!VIDEO](https://video.tv.adobe.com/v/33346/?captions=por_br&quality=12)



