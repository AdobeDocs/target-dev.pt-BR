---
keywords: implementar, implementar, configurar, configurar, parâmetro de página
description: Obter dados no  [!DNL Target] usando atributos de perfil na página.
title: Como Obter Dados No  [!DNL Target] Usando Atributos De Perfil Na Página?
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 43%

---

# Atributos de perfil na página

Os atributos de perfil na página em [!DNL Adobe Target] (também chamados &quot;atributos de perfil in-mbox&quot;) são pares de nome/valor transmitidos diretamente pelo código da página e armazenados no perfil do visitante para uso futuro.

Os atributos de perfil na página permitem que os dados específicos do usuário sejam armazenados no perfil do Target para direcionamento e segmentação posteriores.

## Formato

Os atributos de perfil na página são passados para [!DNL Target] por meio de uma chamada de servidor como um par nome/valor da cadeia de caracteres com o prefixo &quot;perfil&quot;. antes do nome do Atributo.

Os nomes e valores do atributo são personalizáveis (embora alguns sejam &quot;nomes reservados&quot; para usos específicos).

Estes são alguns exemplos de atributos de perfil na página:

* `profile.membershipLevel=silver`
* `profile.visitCount=3`

## Exemplo de casos de uso

* **Informações de logon**: compartilha dados que não são PII (Informações de Identificação Pessoal) com [!DNL Target] com base no logon do usuário. Esses dados podem ser status de associação, histórico de pedido ou mais.
* **Armazenar informações**: rastreia qual loja é a localização preferencial deste usuário.
* **Interações anteriores**: rastreia o que o usuário fez no site antes para informar sobre personalizações futuras.

## Benefícios do método

Os dados são enviados para [!DNL Target] em tempo real e podem ser usados na mesma chamada de servidor em que os dados entram.

## Avisos

Precisa de atualizações do código da página (diretamente ou por meio de um sistema de gerenciamento de tags).

Os atributos e valores estão visíveis nas chamadas do servidor, para que um visitante possa ver os valores. Se você compartilhar informações como intervalos de crédito ou outras informações potencialmente privadas, esse método pode não ser a melhor abordagem.

## Exemplos de código

targetPageParamsAll (anexa os atributos a todas as chamadas de mbox na página):

`function targetPageParamsAll() { return "profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

targetPageParams (anexa os atributos ao mbox global na página):

`function targetPageParams() { return profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

Atributos no código mboxCreate:

`<div class="mboxDefault"> default content to replace by offer </div> <script> mboxCreate('mboxName','profile.param1=value1','profile.param2=value2'); </script>`

## Links para informações relevantes

[Atributos do perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=pt-BR)

[Perfil do visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=pt-BR)
