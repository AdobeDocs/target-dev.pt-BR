---
title: API de atualização de perfil em massa do Adobe Target
description: Saiba como usar o [!DNL Adobe Target] [!UICONTROL API de atualização de perfil em massa] para enviar os dados de perfil de vários visitantes para [!DNL Target] para uso no direcionamento.
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: 3d90616b0a920abea380d4cfcd1227eafde86adb
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 8%

---

# [!DNL Adobe Target Bulk Profile Update API]

A variável [!DNL Adobe Target] [!UICONTROL API de atualização de perfil em massa] permite atualizar perfis de usuário para vários visitantes de um site em massa usando um arquivo em lote.

Usar o [!UICONTROL API de atualização de perfil em massa], você pode enviar dados detalhados do perfil do visitante na forma de parâmetros do perfil para muitos usuários para o [!DNL Target] de qualquer fonte externa. Fontes externas podem incluir os sistemas de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) ou POS (Point of Sale, ponto de venda), que normalmente não estão disponíveis em uma página da Web.

| Versão  | Exemplo de URL | Recursos |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | Suporte somente para atualização de perfil em massa. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Caso não seja encontrado, criar perfil.</li><li>Atualização de status por linha.</li></ul> |

>[!NOTE]
>
>A versão 2 (v2) do [!UICONTROL API de atualização de perfil em massa] é a versão atual. No entanto, [!DNL Target] ainda suporta a versão 1 (v1).

## Benefícios da API de atualização do perfil em massa

* Nenhum limite sobre o número de atributos de perfil.
* Os atributos de perfil enviados pelo site podem ser atualizados por meio da API e do oposto.

## Avisos

* O tamanho do arquivo em lote deve ser menor que 50 MB. Além disso, o número total de linhas não deve ultrapassar 500.000 por carregamento.
* As atualizações geralmente ocorrem em menos de uma hora, mas podem levar até 24 horas para serem refletidas.
* Não há limite para o número ou as linhas que você pode fazer upload por um período de 24 horas em lotes subsequentes. No entanto, o processo de ingestão pode ter o fluxo controlado em horário comercial, para garantir que outros processos sejam executados com eficiência.
* As chamadas de atualização em lote v2 consecutivas sem chamadas da mbox entre as mesmas thirdPartyIds substituindo as propriedades atualizadas na primeira chamada de atualização em lote.
* [!DNL Adobe] A não garante que 100% dos dados do perfil do lote sejam integrados e retidos no Target e, portanto, estejam disponíveis para uso no direcionamento. No design atual, há a possibilidade de uma pequena porcentagem de dados (até 0,1% de grandes lotes de produção) não ser integrada ou retida.

## Arquivo em lote

Para atualizar os dados do perfil em massa, crie um arquivo em lote. O arquivo de lote é um arquivo de texto com valores separados por vírgulas semelhante ao seguinte arquivo de amostra.

``````
batch=pcId, param1, param2, param3, param4 123, value1 124, value1,,, value4 125,, value2 126, value1, value2, value3, value4
``````

Você faz referência a esse arquivo na chamada de POST para [!DNL Target] servidores para processar o arquivo. Ao criar o arquivo de lote, considere o seguinte:

* A primeira linha do arquivo deve especificar cabeçalhos de coluna.
* O primeiro cabeçalho deve ser um `pcId` ou `thirdPartyId`. A variável [!UICONTROL ID de visitante do Marketing Cloud] não é compatível. [!UICONTROL pcId] é um [!DNL Target]visitorID gerado pelo. `thirdPartyId` é uma ID especificada pelo aplicativo cliente, que é passada para [!DNL Target] por meio de uma chamada mbox como `mbox3rdPartyId`. Deve ser aqui referido como `thirdPartyId`.
* Os parâmetros e valores especificados no arquivo de lote devem ser codificados por URL usando UTF-8 por motivos de segurança. Os parâmetros e valores podem ser encaminhados para outros nós de borda para processamento por meio de solicitações HTTP.
* Os parâmetros devem estar no formato `paramName` somente. Os parâmetros são exibidos em [!DNL Target] as `profile.paramName`.
* Se você estiver usando [!UICONTROL API de atualização de perfil em massa] v2, não é necessário especificar todos os valores de parâmetro para cada `pcId`. Perfis são criados para qualquer `pcId` ou `mbox3rdPartyId` que não é encontrado em [!DNL Target]. Se você estiver usando a v1, os perfis não serão criados para pcIds ou mbox3rdPartyIds ausentes.
* O tamanho do arquivo em lote deve ser menor que 50 MB. Além disso, o número total de linhas não deve exceder 500 mil. Esse limite garante que os servidores não sejam inundados com muitas solicitações.
* Você pode enviar vários arquivos. No entanto, a soma total das linhas de todos os arquivos enviados em um dia não deve exceder um milhão para cada cliente.
* Não há limite para o número de atributos que você carrega. No entanto, o tamanho geral de um perfil, incluindo dados do sistema, não deve exceder 2000 KB. [!DNL Adobe] A recomenda que você use menos de 1000 KB de armazenamento para atributos de perfil.
* Os parâmetros e valores diferenciam maiúsculas de minúsculas.

## solicitação POST do HTTP

Fazer uma solicitação POST HTTP para [!DNL Target] servidores de borda para processar o arquivo. Este é um exemplo de solicitação HTTP POST para o arquivo batch.txt usando o comando curl:

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``````

Em que:

BATCH.TXT é o nome do arquivo. CLIENTCODE é o [!DNL Target] código de cliente.

Se você não souber o código de cliente, no campo [!DNL Target] clique na interface do usuário **[!UICONTROL Administração]** > **[!UICONTROL Implementação]**. O código de cliente é mostrado no [!UICONTROL Detalhes da conta] seção.

### Inspect a resposta

A API de perfis retorna o status de envio do lote para processamento, juntamente com um link em &quot;batchStatus&quot; para um URL diferente que mostra o status geral do trabalho em lote específico.

### Exemplo de resposta da API

O código a seguir recortado é um exemplo de uma resposta da API de perfis:

```
<response>
    <success>true</success>
    <batchStatus>http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383</batchStatus>
    <message>Batch submitted for processing</message>
</response>
```

Se houver um erro, a resposta conterá `success=false` e uma mensagem detalhada para o erro.

### Resposta de status de lote padrão

Uma resposta padrão bem-sucedida quando o parâmetro acima `batchStatus` O link do URL clicado é semelhante ao seguinte:

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

Os valores esperados para os campos de status são:

| Status | Detalhes |
| --- | --- |
| [!UICONTROL complete] | A solicitação de atualização do lote de perfis foi concluída com êxito. |
| [!UICONTROL incompleto] | A solicitação de atualização do lote de perfis ainda está sendo processada e não foi concluída. |
| [!UICONTROL paralisado] | A solicitação de atualização do lote de perfis está paralisada e não pôde ser concluída. |

### Resposta detalhada do URL de status do lote

Uma resposta mais detalhada pode ser obtida ao passar um parâmetro `showDetails=true` para o `batchStatus` url acima.

Por exemplo:

```
http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383&showDetails=true
```

#### Resposta detalhada

```
<response>
    <batchId>demo4-1701473848678-13029383</batchId>
    <status>complete</status>
    <batchSize>1</batchSize>
    <consumedCount>1</consumedCount>
    <successfulUpdates>1</successfulUpdates>
    <profilesNotFound>0</profilesNotFound>
    <failedUpdates>0</failedUpdates>
</response>
```
