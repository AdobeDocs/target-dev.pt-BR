---
title: Inicialize o SDK do Node.js usando o método de criação
description: Saiba como usar o método de criação para inicializar o SDK do Node.js e instanciar o [!DNL Target] cliente para fazer chamadas para [!DNL Adobe Target] para experimentos e experiências personalizadas.
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 19%

---

# Inicializar o SDK do Node.js

## Descrição

Use o `create` para inicializar o SDK do Node.js e instanciar o [!UICONTROL Target] cliente para fazer chamadas para [!DNL Adobe Target] para experimentos e experiências personalizadas.

## Método

**criar**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## Parâmetros

`options` tem a seguinte estrutura:

| Nome | Tipo | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- | --- |
| cliente | String | Sim | None | [!UICONTROL ID do cliente do Adobe Target] |
| organizationId | String | Sim | None | [!UICONTROL ID da organização Experience Cloud] |
| ambiente | String | Não | produção | Nome do ambiente de destino. No [!DNL Target] IU, [!UICONTROL Administração] > [!UICONTROL Ambientes]. |
| timeout | Número | Não | 3000 | Tempo limite em milissegundos |
| serverDomain | String | Não | `*client*.tt.omtrdc.net` | Substitui o nome de host padrão |
| seguro | Booleano | Não | true | Não definido para impor o esquema HTTP |
| logger | Objeto | Não | Agente NOOP | Substitui o logger NOOP padrão |
| targetLocationHint | String | Não | None | Dica de localização do Target |
| fetchApi | Função | Não | global.fetch ou window.fetch | [buscar](https://fetch.spec.whatwg.org/) é usado pelo SDK para solicitações http. Por padrão, é usada a busca por nó ou a implementação de busca no navegador. Mas uma implementação alternativa pode ser fornecida usando `fetchApi` |
| propertyToken | String | Não | None | **Token de propriedade de destino**. Se especificado aqui, todas as `getOffers` As chamadas do usarão esse valor. **Para decisões no dispositivo**, o SDK baixará somente o artefato que contém as atividades qualificadas para o token de propriedade definido em `propertyToken` |
| decisioningMethod | String | Não | lado do servidor | Determina que método de decisão usar ([no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), lado do servidor, híbrido) |
| pollingInterval | Número | Não | 300000 (5 minutos) | Intervalo de sondagem para o [artefato da regra de decisão no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (em milissegundos) |
| artifactLocation | String | Não | None | Um url totalmente qualificado para o [artefato da regra de decisão no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Substitui o local determinado internamente. |
| artifactPayload | Objeto | Não | None | A carga JSON do [artefato da regra de decisão no dispositivo](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Se especificado, é usado em vez de solicitar um de um URL. |
| [events](sdk-events.md) | Objeto&lt;string function=&quot;&quot;> | Não | None | Um objeto opcional com chaves de nome de evento e valores de função de retorno de chamada |
| telemetryEnabled | Booleano | Não | true | Quando habilitado, o Adobe coletará os dados de uso de recursos do SDK e de telemetria de desempenho. Os dados pessoais não são coletados. |

## Exemplo

### Node.js

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    events: {clientReady: targetClientReady }
};

const targetClient = TargetClient.create(CONFIG);

function targetClientReady() {
    // make calls to Adobe Target
}
```
