---
keywords: registerExtension, registerextension, extensão de registro, at.js, funções, função, clientCode, serverDomain, globalMboxName, globalMboxAutoCreate, tempo limite, registerExtension2
description: Use a função [!UICONTROL registerExtension()] da biblioteca JavaScript do  [!DNL Adobe Target] at.js para registrar uma extensão específica. (at.js 1.x)
title: Como usar a função [!UICONTROL registerExtension()]?
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
TQID: https://experienceleague.adobe.com/qTWubp0dNesN-8vsooz8pdbjfSw1W1ktm-0bG6YRzJw
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 62%

---

# [!UICONTROL registerExtension()] - at.js 1.x

Fornece uma forma padrão de registrar uma extensão específica.

>[!NOTE]
>
>Esta função está disponível somente para a at.js versão 1.*x*. Esta função foi substituída pelo lançamento da at.js 2.*x*. Essa função retorna o conteúdo padrão se for usada com a at.js 2.x.

O parâmetro de opções é obrigatório e tem a seguinte estrutura:

| Chave | Tipo | Obrigatório | Descrição |
|--- |--- |--- |--- |
| name | String | Sim | Nome da extensão. |
| módulos | [String]Matriz | Sim | Uma matriz de sequências de caracteres representando nomes de módulo solicitados. |
| registrar | Função | Sim | Uma função usada para inicializar e criar a extensão. Esta função recebe argumentos com base na matriz de módulos. |

Notas:

* Se um dos parâmetros não for fornecido, uma exceção será lançada.
* Se a matriz de módulos estiver vazia, uma exceção será lançada.

Para obter mais informações e exemplos de como usar o `[!UICONTROL registerExtension]`, consulte a página [Adobe Experience Cloud Target atjs Extensions](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions) no GitHub.

## Métodos de módulo de configurações

| Chave | Tipo | Descrição |
|--- |--- |--- |
| clientCode | String | Código de cliente |
| serverDomain | String | Domínio do servidor Edge |
| globalMboxName | String | [!DNL Target] nome da mbox global |
| globalMboxAutoCreate | Booleano | Indica se a criação automática está ativada ou não |
| timeout | Número | Tempo-limite da solicitação |

## Métodos de módulo do agente de log

| Chave | Tipo | Descrição |
|--- |--- |--- |
| log | Função | Registra a lista variável de argumentos no console do navegador, se houver um. Ela é ativada somente quando `mboxDebug=true` é transmitido à URL. |
| error | Função | Registra a lista variável de argumentos no console do navegador. Ela só é ativada quando há erros graves, como tempo limite de rede, nó HTML não encontrado, etc. |

