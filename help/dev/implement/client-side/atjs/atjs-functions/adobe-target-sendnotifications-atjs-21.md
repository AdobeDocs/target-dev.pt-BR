---
keywords: adobe.target.sendNotifications, sendNotifications, sendnotifications, enviar notificações, notificações, at.js, funções, função, $9
description: Use o [!UICONTROL adobe.target.sendNotifications()] for at.js para enviar notificações ao  [!DNL Target] edge quando uma experiência for renderizada sem usar o [!UICONTROL applyOffer]. (at.js.2.1 +)
title: Como usar a função adobe.target.sendNotifications()?
feature: at.js
exl-id: 1a08da10-31a0-4b0b-af7d-91ed7d32c308
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 83%

---

# [!UICONTROL adobe.target.sendNotifications(options)]

Esta função envia uma notificação para a borda [!DNL Target] quando uma experiência é renderizada sem usar `[!UICONTROL adobe.target.applyOffer()]` ou `[!UICONTROL adobe.target.applyOffers()]`.

>[!NOTE]
>
>Esta função foi introduzida na at.js 2.1.0 e estará disponível para todas as versões a partir da 2.1.0.

| Chave | Tipo | Obrigatório? | Descrição |
| --- | --- | --- | --- |
| consumerId | String | Não | O valor padrão é a mbox global do cliente se não for fornecida. Essa chave é usada para gerar a ID de dados complementares usada para integração A4T. |
| Solicitação | Objeto | Sim | Consulte Tabela de solicitações abaixo. |
| timeout | Número | Não | Tempo limite da solicitação. Se não for especificado, o tempo limite padrão da at.js será usado. |

## Solicitação

| Nome do campo | Tipo | Obrigatório? | Limitação | Descrição |
| --- | --- | --- | --- | --- |
| Request > notifications | Matriz de objetos | Sim |  | Notificações para o conteúdo exibido, seletores clicados e/ou exibições ou mboxes visitadas. |
| Request > notifications > address | Objeto | Não |  |  |
| Request > notifications > address > url | String | Não |  | URL de onde a notificação foi disparada. |
| Request > notifications > address > referringUrl | String | Não |  | O URL de referência do qual a notificação foi disparada. |
| Request > notifications > parameters | String | Não | Os seguintes nomes não são permitidos para parâmetros:<ul><li>orderId</li><li>orderTotal</li><li>productPurchasedIds</li></ul>Considere o seguinte:<ul><li>Limite máximo de 50 parâmetros.</li><li>O nome do parâmetro não pode ficar em branco.</li><li>Extensão máx. do nome do parâmetro: 128.</li><li>O nome do parâmetro não pode começar com &quot;perfil&quot;.</li><li>Extensão máx. do valor do parâmetro: 5000.</li></ul> |  |
| Request > notifications > profileParameters | String | Não | Os seguintes nomes não são permitidos para parâmetros:<ul><li>orderId</li><li>orderTotal</li><li>productPurchasedIds</li></ul>Considere o seguinte:<ul><li>Limite máximo de 50 parâmetros.</li><li>O nome do parâmetro não pode ficar em branco.</li><li>Extensão máx. do nome do parâmetro: 128.</li><li>O nome do parâmetro não pode começar com &quot;perfil&quot;.</li><li>Extensão máx. do valor do parâmetro: 5000.</li></ul> |  |
| Request > notifications > order | Objeto | Não |  | Objeto que descreve os detalhes da ordem. |
| Request > notifications > order > id | String | Não | `<=` 250 caracteres. | ID do pedido. |
| Request > notifications > order > total | String | Não | `>=` 0 | Total do pedido. |
| Request > notifications > order > purchasedProductIds | Matriz de string | Não | <ul><li>Valores em branco não são permitidos.</li><li>Comprimento máx. da ID de produto: 50.</li><li>IDs de produto, separadas por vírgulas e concatenadas, o comprimento total não pode exceder 250.</li></ul> | Identificações de produto da ordem. |
| Request > notifications > product | Objeto | Não |  |  |
| Request > notifications > product > id | String | Não | `<=` 128 caracteres; não pode ficar em branco. | Identificação do produto. |
| Request > notifications > product > categoryId | String | Não | `<=` 128 caracteres; não pode ficar em branco. | Identificação da categoria. |
| Request > notifications > id | String | Sim | `<=` 200 caracteres. | A ID da notificação será retornada em resposta e indicará que a notificação foi processada com sucesso. |
| Request > notifications > impressionId | String | Não | `<= 128` caracteres. | A ID da impressão é usada para unir (vincular) a notificação atual com uma notificação anterior ou executar a solicitação. Caso as duas correspondam, a segunda e as solicitações subsequentes não gerarão uma nova impressão para a atividade ou experiência. |
| Solicitação > notificações > tipo | String | Sim | &quot;click&quot; ou &quot;display&quot; são suportados. | Tipo de notificação. |
| Request > notifications > timestamp | Número`<int64>` | Sim |  | O carimbo de data e hora da notificação em milissegundos decorridos desde a época UNIX. |
| Request > notifications > tokens | Matriz de string | Sim |  | Uma lista de tokens para o conteúdo exibido ou para os seletores clicados, com base no tipo de notificação. |
| Request > notifications > mbox | Objeto | Não |  | Notificações para a mbox. |
| Request > notifications > mbox > name | String | Não | Valores em branco não são permitidos.<p>Caracteres permitidos: consulte a observação após a tabela. | nome da mbox. |
| Request > notifications > mbox > state | String | Não |  | token de estado da mbox. |
| Request > notifications > view | Objeto | Não |  |  |
| Request > notifications > view > id | Número inteiro `<int64>` | Não |  | Identificação de exibição. A identificação atribuída à exibição quando ela foi criada por meio da API de exibição. |
| Request > notifications > view > name | String | Não | `<= 128` caracteres. | Nome da exibição. |
| Request > notifications > view > key | String | Não | `<=` 512 caracteres. | Chave da exibição. A chave definida para a exibição por meio da API. |
| Request > notifications > view > state | String | Não |  | Token de estado da exibição. |

**Observação**: os seguintes caracteres *não* são permitidos para `Request > notifications > mbox > name`:

```
- '-, ./=`:;&!@#$%^&*()+|?~[]{}'
```

## chamada sendNotifications() após renderizar mboxes buscadas previamente

```javascript {line-numbers="true"}
function createTokens(options) {
  return options.map(e => e.eventToken);
}

function createNotification(mbox, type, tokens) {
  const id = 11111; // here we should use a random ID like UUID
  const timestamp = Date.now();
  const { name, state, parameters, profileParameters, order, product } = mbox;
  const result = {
    id,
    type,
    timestamp,
    parameters,
    profileParameters,
    order,
    product
  };

  result.mbox = { name, state };
  result.tokens = tokens;

  return result;
}

adobe.target.getOffers({
  request: {
    prefetch: {
      mboxes: [
        {
          index: 0,
          name: "a1-serverside-ab"
        }
      ]
    }
  }
})
.then(response => {
  const mboxes = response.prefetch.mboxes;
  const notifications = mboxes.map(mbox => {
    const type = "display";
    const tokens = createTokens(mbox.options);

    return createNotification(mbox, type, tokens);
  });
  
  adobe.target.sendNotifications({
    request: { notifications }
  });
})
```

>[!NOTE]
>
>Se você estiver usando [!DNL Adobe Analytics], `[!UICONTROL getOffers()]` com busca prévia somente e `[!UICONTROL sendNotifications()]`, a solicitação [!DNL Analytics] deverá ser disparada após a execução de `[!UICONTROL sendNotifications()]`. A finalidade disso é garantir que a SDID gerada por `[!UICONTROL sendNotifications()]` corresponda à SDID enviada para [!DNL Analytics] e [!DNL Target].
