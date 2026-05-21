---
keywords: implementar, implementar, configurar, configurar, criar script de atributos de perfil
description: Obter dados em  [!DNL Target] usando atributos de perfil de script.
title: Como Obter Dados no  [!DNL Target] Usando Atributos de Perfil de Script?
feature: Implementation
exl-id: ba11f1de-e68b-4505-8e3e-cd4d46ef59a2
TQID: https://experienceleague.adobe.com/bRsl4ipgw0OeuVD0d69wmnHmrVvcGt9o0KmkhrEECZQ
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 292
ht-degree: 71%

---

# Atributos de perfil de script

Os atributos do perfil de script são pares de nome/valor definidos na solução [!DNL Adobe Target]. O valor é determinado na execução de um snippet do JavaScript no servidor Target, a cada chamada do servidor.

Os usuários gravam pequenos snippets de código que são executados de acordo com a chamada de mbox e antes de um visitante ser avaliado para associação de público-alvo e atividade.

## Formato

Os atributos de perfil do script são criados na seção Públicos-alvo do Target. Qualquer nome de atributo é válido, e o valor é o resultado de uma função JavaScript gravada pelo usuário [!DNL Target]. O nome do atributo é automaticamente préfixado pelo &quot;usuário. &quot; em [!DNL Target] para diferenciá-los dos atributos de perfil na página.

O snippet de código é gravado em linguagem Rhino JS e podem fazer referência a tokens e outros valores.

## Exemplo de casos de uso

* **Abandono do carrinho**: quando o visitante chega no carrinho de compras, defina o script de perfil como 1. Quando o visitante faz a conversão, redefina-o para 0. Se o valor =1, então o visitante tem um item no carrinho.
* **Contagem de visitas**: em cada nova visita, incremente a contagem em 1 para rastrear a frequência com que um visitante retorna ao site.

## Benefícios do método

Não requer atualizações de código de página.

Executado antes das decisões de associação de público-alvo e atividade, portanto esses atributos de script de perfil pode afetar a associação em uma única chamada do servidor.

Pode ser bastante robusto. Cerca de 2.000 instruções podem ser executadas por script.

## Avisos

Requer conhecimento de JavaScript.

O pedido de execução dos scripts de perfil não pode ser garantido, então não podem depender uns dos outros.

A depuração pode ser difícil.

## Exemplos de código

Os scripts de perfil são bastante flexíveis:

```
user.purchase_recency: var dayInMillis = 3600 * 24 * 1000; if (mbox.name == 'orderThankyouPage') {  user.setLocal('lastPurchaseTime', new Date().getTime()); } var lastPurchaseTime = user.getLocal('lastPurchaseTime'); if (lastPurchaseTime) {  return ((new Date()).getTime()-lastPurchaseTime)/dayInMillis; }
```

### Links para informações relevantes

[Atributos de script de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=pt-BR#concept_8C07AEAB0A144FECA8B4FEB091AED4D2)
