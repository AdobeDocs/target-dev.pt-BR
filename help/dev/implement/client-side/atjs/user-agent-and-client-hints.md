---
keywords: at.js, agente do usuário do navegador, agente do usuário, dicas do cliente, agente do usuário
description: Saiba como o Adobe Target usa o user-agent e as Client Hints (Notas do cliente) para qualificar visitantes para segmentação e personalização.
title: User Agent e Client Hints
feature: at.js
exl-id: e0d87d95-ee95-4ca9-8632-222ae1fb9a91
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 74%

---

# User-agent e Client Hints

O Adobe Target usa o user-agent para qualificar visitantes para segmentação e personalização.

>[!NOTE]
>
>As informações deste artigo se aplicam à [at.js versão 2.9.0](target-atjs-versions.md) (ou posterior).

Cada vez que um navegador faz uma solicitação a um servidor, as informações sobre o navegador e o ambiente em que o navegador é executado são incluídas no cabeçalho da solicitação. Desde os primeiros dias da internet, esses dados vêm sendo agregados numa sequência chamada user-agent (agente do usuário).

O texto a seguir é um exemplo de user-agent de um computador com Mac OS X usando um navegador Safari:

```
Mozilla/5.0 (Linux; Android 12; SM-S908E) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Mobile Safari/537.36 
```

Desse user-agent, o servidor que recebe a solicitação pode discernir as seguintes informações sobre o navegador e o sistema operacional:

| Informações | Detalhes |
| --- | --- |
| Nome do software | Chrome |
| Versão do software | 101 |
| Versão completa do software | 101.0.4951.41 |
| Nome do mecanismo de layout | AppleWebKit |
| Versão do mecanismo de layout | 537.36 |
| Sistema operacional | Android |
| Versão do sistema operacional | Android 12 (Snow Cone) |
| Dispositivo | SM-S908E (Samsung Galaxy S22 Ultra) |

Ao longo dos anos, a quantidade de informações de navegador e dispositivo incluída na sequência user-agent aumentou.

## Casos de uso do user-agent

Os User-agents vêm sendo usados há muito tempo para fornecer às equipes de marketing e desenvolvedores informações importantes sobre como os navegadores, sistemas operacionais e dispositivos exibem o conteúdo do site, bem como sobre como os usuários interagem com os sites. Os User-agents também são usados para bloquear spam e filtrar bots que rastreiam sites para vários fins adicionais.

Entretanto, nos últimos anos, alguns proprietários de sites e fornecedores de marketing têm usado o user-agent junto com outras informações incluídas nos cabeçalhos de solicitação para criar impressões digitais que podem ser usadas como meio de identificar usuários sem o conhecimento deles. Apesar do importante propósito do user-agent para os proprietários do site, os desenvolvedores de navegador decidiram fazer alterações em como os user-agents operam para limitar possíveis problemas de privacidade para os visitantes do site.

Os desenvolvedores de navegador criaram User-Agent Client Hints como uma solução para esse desafio. As Client Hints (Notas do cliente) ainda permitem que os sites coletem as informações necessárias do navegador, do sistema operacional e do dispositivo, além de fornecerem maior proteção contra métodos de rastreamento ocultos, como impressão digital.

## Client Hints

As User-Agent Client Hints fornecem aos proprietários do site a capacidade de acessar muitas das informações disponíveis no user-agent, mas com mais privacidade. Quando navegadores modernos enviam um user-agent para um servidor da web, o user-agent completo é enviado em cada solicitação, independentemente da necessidade. As Client Hints, por outro lado, executam um modelo em que o servidor deve solicitar ao navegador as informações adicionais que ele deseja saber sobre o cliente. Ao receber essa solicitação, o navegador pode aplicar suas próprias políticas ou configurações do usuário para determinar quais dados são retornados. Em vez de expor todo o user-agent por padrão em todas as solicitações, o acesso agora é gerenciado de forma explícita e auditável.

As User-Agent Client Hints estão disponíveis no Chrome desde a versão 89. Versões recentes de navegadores baseados em Chromium, como Microsoft Edge, Opera, Brave, Chrome Android, Opera Android e Samsung Internet, também admitem a API Client Hints.

As Client Hints contidas nos cabeçalhos da primeira solicitação feita pelo navegador a um servidor da web contêm a marca do navegador, a versão principal do navegador e um indicador de se o cliente é um dispositivo móvel. Cada parte dos dados tem seu próprio valor de cabeçalho, em vez de ser agrupada em uma única sequência user-agent.

Por exemplo, estas são algumas Client Hints:

```
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99" 
Sec-CH-UA-Mobile: ?0 
Sec-CH-UA-Platform: "macOS"
```

... considerando que este é o user-agent para o mesmo navegador:

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36 
```

Embora as informações sejam semelhantes, a primeira solicitação para o servidor inclui Client Hints que contêm apenas um subconjunto do que está disponível na sequência user-agent. Faltam na solicitação a arquitetura do sistema operacional, a versão completa do sistema operacional, o nome do mecanismo de layout, a versão do mecanismo de layout e a versão completa do navegador. No entanto, em solicitações subsequentes, a API Client Hints permite que os servidores da web solicitem detalhes adicionais e de alta entropia sobre o dispositivo. Quando esses valores de alta entropia são solicitados, dependendo da política do navegador ou das configurações do usuário, a resposta do navegador pode incluir essas informações.

O exemplo a seguir é um objeto JSON retornado pela API Client Hints quando valores de alta entropia são solicitados:

```
{ 

    "architecture":"x86", 
    "bitness":"64", 
    "brands":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100" 
        } 
    ], 
    "fullVersionList":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99.0.0.0" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100.0.4896.127" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100.0.4896.127" 
        } 
    ], 
    "mobile":false, 
    "model":"", 
    "platformVersion":"12.2.1" 
} 
```

Os valores de alta entropia incluem várias informações adicionais que não estão disponíveis nas informações padrão das Client Hints. A tabela a seguir contém detalhes de quais dados estão disponíveis na solicitação padrão em comparação às informações de alta entropia das User-Agent Client Hints.

| Cabeçalho HTTP | JavaScript | User-agent | Client hint | Client hint de alta entropia |
| --- | --- | --- | --- | --- |
| Sec-CH-UA | brands | Sim | Sim | Não |
| Sec-CH-UA-Platform | platform | Sim | Sim | Não |
| Sec-CH-UA-Mobile | mobile | Sim | Sim | Não |
| Sec-CH-UA-Platform-Version | platformVersion | Sim | Não | Sim |
| Sec-CH-UA-Arch | architecture | Sim | Não | Sim |
| Sec-CH-UA-Model | model | Sim | Não | Sim |
| Sec-CH-UA-Bitness | Bitness | Sim | Não | Sim |
| Sec-CH-UA-Full-Version-List | fullVersionList | Sim | Não | Sim |

## Migração para as Client Hints

Atualmente, os navegadores baseados em Chromium continuam a enviar o user-agent juntamente com Client Hints nos cabeçalhos de solicitações feitas aos servidores da web. No entanto, a partir de abril de 2022 e até fevereiro de 2023, a quantidade de dados contidos na sequência user-agent será reduzida. Outros navegadores, como Safari e Firefox, continuarão a utilizar a sequência user-agent; no entanto, também reduzirão o volume de informação contida na sequência.

## Casos de uso do Target que exigem Client Hints

Os seguintes casos de uso do Target requerem Client Hints:

### Atributos do público

Se você usa públicos do Target e qualquer um dos atributos de público a seguir, o Target exige Client Hints para executar a segmentação correta:

* Navegador
* Sistema operacional
* Dispositivo móvel

### Scripts de perfil

Se você usa scripts de perfil e fizer referência ao atributo `user.browser` (que se refere ao user-agent), talvez seja necessário atualizar o script de perfil para também verificar uma ou mais Client Hints. Você pode acessar qualquer uma das Client Hints usando a função `user.clientHint('sec-ch-ua-xxxxx')`. Todas as letras do nome do cabeçalho da Client Hint devem estar em minúsculas.

O exemplo a seguir mostra como detectar corretamente um sistema operacional Windows em um script de perfil:

```
"return (((user.browser != null) && (user.browser.indexOf(\"Windows\") > -1)) || " + 
      "((user.clientHint('sec-ch-ua-platform') != null) && 
(user.clientHint('sec-ch-ua-platform') === 'Windows')));" 
```

Esta é uma tabela de Client Hints e a semântica de uso do script de perfil correspondente.

| Cabeçalho da Client Hint | Entropia | Atributo de público | Uso do script de perfil |
| --- | --- | --- | --- |
| [Sec-CH-UA](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA) | Baixo | Navegador | `user.clientHint('sec-ch-ua')` |
| [Sec-CH-UA-Arch](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Arch) | Alto | Exposto aos usuários pelos scripts de perfil | `user.clientHint('sec-ch-ua-arch')` |
| [Sec-CH-UA-Bitness](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Bitness) | Alto | Exposto aos usuários pelos scripts de perfil | `user.clientHint('sec-ch-ua-bitness')` |
| [Sec-CH-UA-Full-Version-List](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Full-Version-List) | Alto | Navegador | `user.clientHint('sec-ch-ua-full-version-list')` |
| [Sec-CH-UA-Mobile](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Mobile) | Baixo | Dispositivo móvel | `user.clientHint('sec-ch-ua-mobile')` |
| [Sec-CH-UA-Model](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Model) | Alto | Dispositivo móvel | `user.clientHint('sec-ch-ua-model')` |
| [Sec-CH-UA-Platform](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform) | Baixo | Sistema operacional | `user.clientHint('sec-ch-ua-platform')` |
| [Sec-CH-UA-Platform-Version](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform-Version) | Alto | Exposto aos usuários pelos scripts de perfil | `user.clientHint('sec-ch-ua-platform-version')` |

## Como passar as Client Hints para o Adobe Target

As seções a seguir contêm mais informações sobre como enviar as Client Hints, dependendo da implementação do Target.

### at.js versão 2.9.0 (ou posterior)

A partir da at.js 2.9.0, as User Agent Client Hints serão coletadas automaticamente do navegador e enviadas para o Target quando `getOffer/getOffers()` é chamado. Por padrão, a at.js coleta apenas Client Hints de baixa entropia. Se estiver executando a segmentação de público ou usando scripts de perfil com base em dados da categoria de alta entropia descrita nas seções anteriores, será necessário configurar o at.js para coletar Client Hints de alta entropia do navegador em `targetGlobalSettings`.

```
window.targetGlobalSettings = { allowHighEntropyClientHints: true };
```

### SDKs do lado do servidor

Para obter mais informações sobre como passar Client Hints por meio de SDKs do lado do servidor, consulte [Client Hints](../../server-side/sdk-guides/core-principles/audience-targeting.md#client-hints) em Documentação de implementação do lado do servidor.
