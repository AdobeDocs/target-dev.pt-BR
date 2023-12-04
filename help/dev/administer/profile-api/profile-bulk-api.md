---
title: API de atualização de perfil em massa do Adobe Target
description: Saiba como usar o [!DNL Adobe Target] [!UICONTROL API de atualização de perfil em massa] para enviar os dados de perfil de vários visitantes para [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 8bc819823462fae71335ac3b6c871140158638fe
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 8%

---

# [!DNL Adobe Target Bulk Profile Update API]

A variável [!DNL Adobe Target] [!UICONTROL API de atualização de perfil em massa] permite atualizar perfis de usuário para vários visitantes de um site em massa usando um arquivo em lote.

Usar o [!UICONTROL API de atualização de perfil em massa], você pode enviar dados detalhados do perfil do visitante na forma de parâmetros do perfil para muitos usuários para o [!DNL Target] de qualquer fonte externa. Fontes externas podem incluir os sistemas de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) ou POS (Point of Sale, ponto de venda), que normalmente não estão disponíveis em uma página da Web.

| Versão  | Exemplo de URL | Recursos |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/profile/batchUpdate` | Suporte somente para atualização de perfil em massa. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Caso não seja encontrado, criar perfil.</li><li>Atualização de status por linha.</li></ul> |

>[!NOTE]
>
>A versão 2 (v2) do [!UICONTROL API de atualização de perfil em massa] é a versão atual. No entanto, [!DNL Target] ainda suporta a versão 1 (v1).

## Benefícios da API de atualização do perfil em massa

* Nenhum limite sobre o número de atributos de perfil.
* Os atributos de perfil enviados pelo site podem ser atualizados por meio da API e do oposto.

## Avisos

* O tamanho do arquivo em lote deve ser menor que 50 MB. Além disso, o número total de linhas não deve ultrapassar 500.000 por carregamento.
* Não há limite para o número ou as linhas que você pode fazer upload por um período de 24 horas em lotes subsequentes. No entanto, o processo de ingestão pode ter o fluxo controlado em horário comercial, para garantir que outros processos sejam executados com eficiência.
* As chamadas de atualização em lote v2 consecutivas sem chamadas da mbox entre as mesmas thirdPartyIds substituindo as propriedades atualizadas na primeira chamada de atualização em lote.

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

v2 retorna um status perfil por perfil e v1 retorna somente o status geral. A resposta inclui um link para um URL diferente que tem a mensagem de sucesso perfil por perfil.

### Exemplo de resposta

```
true http://mboxedge19.tt.omtrdc.net/m2/demo/v2/profile/batchStatus?batchId=demo-1845664501&m2Node=00 Batch submitted for processing
```

Se houver um erro, a resposta conterá `success=false` e uma mensagem detalhada para o erro.

Uma resposta bem-sucedida se parece com o seguinte:

``````
demo-1845664501 1436187396849-250353.03_03 success 2403081156529-351655.03_03 success 2403081156529-351656.03_03 success 1436187396849-250351.01_00 success 
``````

Os valores esperados para os campos de status são:

**success**: O perfil foi atualizado. Se o perfil não foi encontrado, um foi criado com os valores do lote.
**erro**: o perfil não foi atualizado ou criado devido a uma falha, exceção ou perda de mensagem.
**pendente**: o perfil ainda não foi atualizado ou criado.



