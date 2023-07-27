---
keywords: registerExtension, registerextension, extensão de registro, at.js, funções, função, clientCode, serverDomain, globalMboxName, globalMboxAutoCreate, tempo limite, registerExtension2
description: Use o [!UICONTROL registerExtension()] para a [!DNL Adobe Target] Biblioteca JavaScript at.js para registrar uma extensão específica. (at.js 1.x)
title: Como usar o [!UICONTROL registerExtension()] Função?
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 76%

---

# [!UICONTROL registerExtension()] - at.js 1.x

Fornece uma forma padrão de registrar uma extensão específica.

>[!NOTE]
>
>Essa função está disponível para a at.js versão 1.somente *x*. Essa função foi substituída pelo lançamento da at.js 2.*x*. Essa função retorna o conteúdo padrão se for usada com a at.js 2.x.

O parâmetro de opções é obrigatório e tem a seguinte estrutura:

| Chave | Tipo | Obrigatório | Descrição |
|--- |--- |--- |--- |
| name | String | Sim | Nome da extensão. |
| módulos | Array[String] | Sim | Uma matriz de sequências de caracteres representando nomes de módulo solicitados. |
| registrar | Função | Sim | Uma função usada para inicializar e criar a extensão. Esta função recebe argumentos com base na matriz de módulos. |

Notas:

* Se um dos parâmetros não for fornecido, uma exceção será lançada.
* Se a matriz de módulos estiver vazia, uma exceção será lançada.

Para mais informações e exemplos de como usar `[!UICONTROL registerExtension]`, consulte a página [Adobe Experience Cloud Target atjs Extensions](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions) no GitHub.

## Métodos de módulo de configurações

| Chave | Tipo | Descrição |
|--- |--- |--- |
| clientCode | String | Código de cliente |
| serverDomain | String | Domínio do servidor Edge |
| globalMboxName | String | [!DNL Target] nome da mbox global |
| globalMboxAutoCreate | Booleano | Indica se a criação automática está ativada ou não |
| timeout | Número | Tempo limite da solicitação |

## Métodos de módulo do agente de log 

| Chave | Tipo | Descrição |
|--- |--- |--- |
| log | Função | Registra a lista variável de argumentos no console do navegador, se houver um. Ela é ativada somente quando `mboxDebug=true` é transmitido à URL. |
| error | Função | Registra a lista variável de argumentos no console do navegador. Ela só é ativada quando há erros graves, como tempo limite de rede, nó HTML não encontrado, etc. |
