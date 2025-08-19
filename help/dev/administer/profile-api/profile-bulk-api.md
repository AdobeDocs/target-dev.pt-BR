---
title: API de atualização de perfil em massa do Adobe Target
description: Saiba como usar o  [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] para enviar os dados de perfil de vários visitantes para o  [!DNL Target] para uso no direcionamento.
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: 39f0ab4a6b06d0b3415be850487552714f51b4a2
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 7%

---

# [!DNL Adobe Target Bulk Profile Update API]

O [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] permite atualizar perfis de usuário para vários visitantes de um site em massa usando um arquivo em lote.

Usando o [!UICONTROL Bulk Profile Update API], você pode enviar convenientemente dados detalhados do perfil do visitante na forma de parâmetros do perfil para muitos usuários para [!DNL Target] a partir de qualquer fonte externa. Fontes externas podem incluir os sistemas de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) ou POS (Point of Sale, ponto de venda), que normalmente não estão disponíveis em uma página da Web.

| Versão  | Exemplo de URL | Recursos |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | Suporte somente para atualização de perfil em massa. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Caso não seja encontrado, criar perfil.</li><li>Atualização de status por linha.</li></ul> |

>[!NOTE]
>
>A versão 2 (v2) de [!DNL Bulk Profile Update API] é a versão atual. No entanto, [!DNL Target] continua a oferecer suporte à versão 1 (v1).
>
>* **Implementações autônomas que não dependem do `PCID`, use a Versão 2**: se a sua implementação do [!DNL Target] usar o [!DNL Experience Cloud ID] (ECID) como um dos identificadores de perfil para visitantes anônimos, você não deverá usar `pcId` como a chave em um arquivo em lotes da Versão 2 (v2). O uso de `pcId` com a Versão 2 de [!DNL Bulk Profile Update API] destina-se a implementações [!DNL Target] independentes que não dependem de `ECID`.
>
>* **Implementações que dependem de `thirdPartID`, usam a Versão 1**: implementações que usam `ECID` para identificação de perfil devem usar a Versão 1 (v1) da API se você quiser usar `pcId` como chave no arquivo de lote. Se sua implementação usar `thirdPartyId` para identificação de perfil, a Versão 2 (v2) será recomendada com `thirdPartyId` como chave.

## Benefícios do [!UICONTROL Bulk Profile Update API]

* Nenhum limite sobre o número de atributos de perfil.
* Os atributos de perfil enviados pelo site podem ser atualizados por meio da API e do oposto.

## Avisos

* O tamanho do arquivo em lote deve ser menor que 50 MB. Além disso, o número total de linhas não deve ultrapassar 500.000 por carregamento.
* As atualizações geralmente ocorrem em menos de uma hora, mas podem levar até 24 horas para serem refletidas.
* Não há limite para o número ou as linhas que você pode fazer upload por um período de 24 horas em lotes subsequentes. No entanto, o processo de ingestão pode ter o fluxo controlado em horário comercial, para garantir que outros processos sejam executados com eficiência.
* As chamadas de atualização em lote v2 consecutivas sem chamadas da mbox entre as mesmas thirdPartyIds substituindo as propriedades atualizadas na primeira chamada de atualização em lote.
* [!DNL Adobe] não garante que 100% dos dados do perfil de lote sejam incorporados e retidos no Target e, portanto, estejam disponíveis para uso no direcionamento. No design atual, há a possibilidade de uma pequena porcentagem de dados (até 0,1% de grandes lotes de produção) não ser integrada ou retida.

## Arquivo em lote

Para atualizar os dados do perfil em massa, crie um arquivo em lote. O arquivo de lote é um arquivo de texto com valores separados por vírgulas semelhante ao seguinte arquivo de amostra.

``` ```
batch=pcId,param1,param2,param3,param4
123,value1
124,value1,,,value4
125,,value2
126,value1,value2,value3,value4
``` ```

>[!NOTE]
>
>O parâmetro `batch=` é obrigatório e deve ser especificado no início do arquivo.

Você faz referência a este arquivo na chamada POST para [!DNL Target] servidores para processar o arquivo. Ao criar o arquivo de lote, considere o seguinte:

* A primeira linha do arquivo deve especificar cabeçalhos de coluna.
* O primeiro cabeçalho deve ser um `pcId` ou `thirdPartyId`. Não há suporte para [!UICONTROL Marketing Cloud visitor ID]. [!UICONTROL pcId] é um visitorID gerado por [!DNL Target]. `thirdPartyId` é uma ID especificada pelo aplicativo cliente, que é passada para [!DNL Target] através de uma chamada de mbox como `mbox3rdPartyId`. Deve ser chamado aqui de `thirdPartyId`.
* Os parâmetros e valores especificados no arquivo de lote devem ser codificados por URL usando UTF-8 por motivos de segurança. Os parâmetros e valores podem ser encaminhados para outros nós de borda para processamento por meio de solicitações HTTP.
* Os parâmetros devem estar somente no formato `paramName`. Os parâmetros são exibidos em [!DNL Target] como `profile.paramName`.
* Se você estiver usando [!UICONTROL Bulk Profile Update API] v2, não precisará especificar todos os valores de parâmetro para cada `pcId`. Perfis são criados para qualquer `pcId` ou `mbox3rdPartyId` que não seja encontrado em [!DNL Target]. Se você estiver usando a v1, os perfis não serão criados para pcIds ou mbox3rdPartyIds ausentes.
* O tamanho do arquivo em lote deve ser menor que 50 MB. Além disso, o número total de linhas não deve exceder 500 mil. Esse limite garante que os servidores não sejam inundados com muitas solicitações.
* Você pode enviar vários arquivos. No entanto, a soma total das linhas de todos os arquivos enviados em um dia não deve exceder um milhão para cada cliente.
* Não há restrição quanto ao número de atributos que você pode fazer upload. No entanto, o tamanho total dos dados do perfil externo, que incluem Atributos do cliente, API do perfil, parâmetros de perfil na mbox e saída do script de perfil, não deve exceder 64 KB.
* Os parâmetros e valores diferenciam maiúsculas de minúsculas.

## solicitação POST do HTTP

Faça uma solicitação POST HTTP para [!DNL Target] servidores de borda para processar o arquivo. Este é um exemplo de solicitação HTTP POST para o arquivo batch.txt usando o comando curl:

``` ```
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``` ```

Em que:

BATCH.TXT é o nome do arquivo. CLIENTCODE é o código de cliente [!DNL Target].

Se você não souber seu código de cliente, na interface de usuário do [!DNL Target], clique em **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. O código de cliente é mostrado na seção [!UICONTROL Account Details].

### Inspecionar a resposta

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

Uma resposta padrão bem-sucedida quando o link da URL `batchStatus` acima é clicado é semelhante à seguinte:

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

Os valores esperados para os campos de status são:

| Status | Detalhes |
| --- | --- |
| [!UICONTROL complete] | A solicitação de atualização do lote de perfis foi concluída com êxito. |
| [!UICONTROL incomplete] | A solicitação de atualização do lote de perfis ainda está sendo processada e não foi concluída. |
| [!UICONTROL stuck] | A solicitação de atualização do lote de perfis está paralisada e não pôde ser concluída. |

### Resposta detalhada do URL de status do lote

Uma resposta mais detalhada pode ser obtida ao passar um parâmetro `showDetails=true` para a url `batchStatus` acima.

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
