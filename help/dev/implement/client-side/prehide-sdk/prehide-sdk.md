---
keywords: pré-ocultar SDK, cintilação, anti-cintilação, pré-ocultação, pré-ocultação, liga, at.js, implementação, consentimento, CMP, posicionamento de script, em linha, externo, seleção de SDK
description: Saiba como integrar o  [!DNL Adobe Target] Pré-ocultar SDK para eliminar o flash de conteúdo não personalizado (cintilação) durante o carregamento da página. O SDK funciona com o Adobe Alloy (Web SDK) e a at.js.
title: Pré-ocultar Guia de integração do SDK
feature: Implementation
hide: true
source-git-commit: 81818370d32ee8c3f3538e5d8d942f66c13e6a13
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 0%

---


# Pré-ocultar guia de integração do SDK

Uma pequena biblioteca síncrona de JavaScript que impede a cintilação visual causada pela personalização de [!DNL Adobe Target] que reescreve um mid-render de página. Adicione uma tag `<script>` embutida na parte superior de `<head>` e a página será revelada somente depois que o conteúdo personalizado estiver pronto, ou quando o temporizador de segurança for acionado.

## Etapas de integração {#integration-steps}

1. Baixe o pacote.

   Use a interface do usuário do Gerenciador de Cintilação para baixar `prehide.min.js`. O arquivo é pré-configurado com o código de cliente e o tempo limite do protetor, portanto, nenhum bloco `PrehideConfig` é necessário.

1. Incorpore-o em linha na parte superior de `<head>`.

   Cole o conteúdo de `prehide.min.js` diretamente dentro de uma marca `<script>` embutida como o primeiro filho de `<head>`. Consulte [Em linha vs. externo](#inline-vs-external) para saber por que em linha é preferível.

   ```html
   <!-- 1. Prehide SDK: must be FIRST in <head> and BEFORE any Adobe SDK -->
   <script>
     // paste the contents of prehide.min.js here
   </script>
   
   <!-- 2. Then load Alloy.js OR at.js -->
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Opcional) Adicione um bloco de configuração de tempo de execução.

   Necessário somente se você hospeda o pacote automaticamente sem baixá-lo por meio da interface do usuário ou se precisar substituir a opção do SDK. Coloque o bloco de configuração antes do script prehide:

   ```html
   <script>
     window.PrehideConfig = {
       org: "your-client-code",
       sdk: "alloy"            // or "atjs" (defaults to "alloy")
     };
   </script>
   <script> /* prehide.min.js inline contents */ </script>
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Opcional) Autorizar.

   Se sua implementação usar uma Plataforma de gerenciamento de consentimento (CMP), chame `window.Prehide.setConsent(...)` assim que o estado de consentimento for conhecido. Consulte [Gerenciamento de consentimento](#consent-management).

1. Verificar.

   Abra DevTools e confirme se o `<style id="alloy-prehiding">` (ou o `at-body-style` para at.js) aparece no `<head>` na primeira pintura e é removido após a conclusão do SDK. Execute `window.Prehide.getState()` no console para inspecionar o estado do tempo de execução.

## Onde colocar o script {#script-placement}

>[!IMPORTANT]
>
>O SDK Prehide deve ser executado antes de Alloy/at.js. Se o Alloy for carregado primeiro, a página renderiza o conteúdo não personalizado e, em seguida, renderiza novamente. Essa é a cintilação exata que esse SDK foi projetado para evitar.
></br>>Não adicione `async` ou `defer` à tag de script Prehide do SDK. A execução síncrona é necessária para que a regra de ocultação seja inserida antes que o navegador comece a dispor a página.

O SDK Pré-oculto deve aparecer anteriormente no documento em relação ao SDK [!DNL Adobe Target] que faz a limpeza depois dele. A ordem de carga é não negociável:

```html
<!doctype html>
<html>
<head>
  <!-- ① Prehide SDK FIRST. Inline. Synchronous. No async/defer. -->
  <script> /* prehide.min.js inline contents */ </script>

  <!-- ② Alloy or at.js loads next -->
  <script src="https://cdn.alloy.adobe.com/alloy.min.js"></script>

  <!-- ③ Then everything else: meta, css, third-party tags, ... -->
  <link rel="stylesheet" href="main.css">
</head>
<body> ... your page ... </body>
</html>
```

## Em linha vs. externo {#inline-vs-external}

Há duas maneiras de incluir `prehide.min.js`:

| Método | Exemplo | Notas |
| --- | --- | --- |
| Em linha (preferencial) | `<script>/* full contents of prehide.min.js pasted directly into the page */</script>` | Sem resposta de rede. O SDK é executado antes que qualquer outra coisa seja renderizada. |
| Externo (somente se o inliner for impossível) | `<script src="/static/prehide.min.js"></script>` | Introduz uma solicitação de rede de bloqueio antes da primeira renderização. Mesmo com HTTP/2 e armazenamento em cache de borda, geralmente custa de 30 a 80 ms. |

### Por que o incorporado é preferível

>[!TIP]
>
>Embutir o pacote diretamente dentro de `<script>...</script>` no seu modelo do HTML. Trate-o como um bloco CSS crítico: pequeno, em linha e sempre no topo.

* Nenhuma busca de bloqueio de renderização. A finalidade do Prehide SDK é inserir as regras de ocultação *antes* da primeira renderização. Um `<script src>` externo adiciona uma rede completa exatamente nessa janela crítica.
* Nenhum novo modo de falha. Um arquivo externo pode ser 404, atingir o tempo limite ou ser bloqueado por um bloqueador de anúncios. Uma cópia integrada não pode ser adicionada.
* O pacote é pequeno (~6 KB). Os custos internos são menores que um favicon comum, e nenhum benefício de armazenamento em cache é grande o suficiente para superar a ida e volta extra na primeira renderização.
* Compatível com cache. Quando incorporado na resposta do HTML, o SDK é armazenado em cache junto com o restante do documento pela camada de armazenamento em cache existente (CDN ou cache HTTP do navegador).
* Pacote específico do cliente. O arquivo baixado tem o código de cliente devolvido no momento do download. A inserção em linha garante que cada visitante receba o pacote personalizado correto sem uma solicitação adicional.

## Configuração {#configuration}

O SDK aceita a configuração de duas fontes, em ordem de prioridade. Lê o que estiver disponível primeiro.

### A: Espaços reservados para tempo de download (sem configuração de tempo de execução)

Ao baixar `prehide.min.js` da interface do usuário do Gerenciador de cintilação, o servidor substitui três espaços reservados dentro do pacote:

| Espaço reservado | Substituído por | Fallback se não substituído |
| --- | --- | --- |
| `__FM_CLIENT_CODE__` | Seu código de cliente (por exemplo, `"acmecorp"`) | Lê `window.PrehideConfig.org` |
| `__FM_TIMEOUT__` | Duração do timer de proteção em ms (por exemplo, `"3000"`) | `5000` ms |
| `__FM_VERSION__` | Versão do SDK (por exemplo, `"1.0.0"`) | `"0.0.0-dev"` |

Se você usar o pacote baixado pela interface do usuário, nenhum bloco `PrehideConfig` será necessário. Simplesmente embutir o script.

### B: Tempo de execução `window.PrehideConfig` (integração manual)

Para pacotes auto-hospedados ou não modificados, declare um objeto de configuração antes da execução do script prehide:

```html
<script>
  window.PrehideConfig = {
    org: "acmecorp",        // required (or rely on baked-in __FM_CLIENT_CODE__)
    sdk: "alloy"             // optional: "alloy" (default) or "atjs"
  };
</script>
```

| Campo | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `org` | string | Sim (a menos que cozido) | O código de cliente do cliente. Usado como o segmento da organização do URL CDN do qual as regras de pré-ocultação são buscadas. |
| `sdk` | `"alloy"` \| `"atjs"` | Não | O Adobe SDK foi carregado na página. Consulte [seleção de SDK](#sdk-selection). |

## Seleção do SDK {#sdk-selection}

O [!DNL Adobe Target] oferece dois SDKs de entrega: Alloy (o moderno Web SDK) e o at.js (a biblioteca clássica). Cada um procura por um *elemento `<style>`* diferente `id` quando a personalização é concluída e o remove para revelar a página. O SDK Prehide deve inserir o `id` correspondente; caso contrário, a página permanecerá oculta até o temporizador de segurança ser acionado.

| Valor `sdk` | ID da tag de estilo inserida | Removido por | Quando usar |
| --- | --- | --- | --- |
| `"alloy"` *(padrão)* | `<style id="alloy-prehiding">` | Ligar o SDK na personalização concluída | Você está carregando o Alloy / Adobe Web SDK nesta página. |
| `"atjs"` | `<style id="at-body-style">` | at.js no modo de personalização concluído | Você está carregando a biblioteca clássica de at.js nesta página. |

### Como definir

```html
<!-- For at.js -->
<script>
  window.PrehideConfig = { org: "acmecorp", sdk: "atjs" };
</script>
<script> /* prehide.min.js inline */ </script>
<script src="https://cdn.adobe.com/.../at.js"></script>
```

>[!WARNING]
>
>Aviso de incompatibilidade. A configuração `sdk: "alloy"` ao carregar a at.js (ou vice-versa) significa que a SDK não encontrará o elemento pré-ocultar a ser removido. O temporizador de guarda acabará revelando a página, mas os visitantes experimentarão uma janela oculta mais longa. Sempre defina `sdk` para corresponder à biblioteca que você está carregando.

Valores desconhecidos ou ausentes retornam para `"alloy"`, portanto, as integrações existentes do Alloy continuam a funcionar sem qualquer alteração de configuração.

## Gerenciamento de consentimento {#consent-management}

>[!NOTE]
>
>* O valor de consentimento nunca é armazenado em `window`. Somente a função é exposta; o estado interno permanece privado para a SDK.
>* As transições de `"out"` para `"in"` não ocultam novamente a página, pois ocultar novamente o conteúdo totalmente renderizado causaria interrupções visuais.
>* `setConsent` pode ser chamado várias vezes em uma única exibição de página. Cada chamada substitui o estado anterior.

O Prehide SDK inclui uma API com reconhecimento de consentimento para coordenar com seu CMP. Usá-lo é opcional. Se `setConsent` nunca for chamado, o SDK se comportará como uma integração padrão sem consentimento.

### Superfície da API

```js
// Single function call. Pass a status string.
window.Prehide.setConsent("pending");  // banner shown, awaiting decision
window.Prehide.setConsent("in");       // user accepted personalization
window.Prehide.setConsent("out");      // user declined personalization

// Read-only debug snapshot.
window.Prehide.getState();
// → { sdk, version, consentStatus, consentApiUsed,
//      rulesResolved, hasSelectorsToGuard, guardTimeout }
```

### O que cada status faz

| Chama | Efeito no temporizador de guarda | Efeito no conteúdo oculto |
| --- | --- | --- |
| `setConsent("pending")` | O temporizador ativo é limpo. Nenhuma ação de segurança é executada até que o consentimento seja resolvido. | Os seletores permanecem ocultos indefinidamente. |
| `setConsent("in")` | Limpo e, em seguida, reiniciado com o tempo limite configurado. Aguarda as regras resolverem se ainda não tiverem feito isso. | O conteúdo permanece oculto até que o SDK personalize ou o temporizador de proteção seja acionado. |
| `setConsent("out")` | Limpo. A página é reexibida imediatamente. | A página é exibida imediatamente. As regras que resolverem depois *não* ocultam novamente o conteúdo. |
| *(nunca chamado)* | O timer padrão é executado de `init()` pela duração configurada. | O conteúdo permanece oculto até que o SDK personalize ou o temporizador de proteção seja acionado. (Modo herdado compatível com versões anteriores.) |

### Padrão recomendado: fase pendente explícita

1. Assim que o CMP exibir a interface de consentimento, ligue para `setConsent("pending")`. Isso limpa o temporizador de segurança para que a página permaneça oculta enquanto o visitante decide, evitando um flash de conteúdo não personalizado atrás do banner.

   ```js
   window.Prehide.setConsent("pending");
   ```

1. Quando o visitante aceitar a personalização, ligue para `setConsent("in")`. O temporizador de proteção é reiniciado e o Alloy/at.js assume o controle, revelando a página quando a personalização é aplicada.

   ```js
   window.Prehide.setConsent("in");
   ```

1. Quando o visitante recusar a personalização, chame `setConsent("out")`. A página é exibida imediatamente e permanece visível. As regras CDN que forem resolvidas posteriormente não as ocultarão novamente.

   ```js
   window.Prehide.setConsent("out");
   ```

### Exemplo: integração do estilo OneTrust

```js
// Called once OneTrust has rendered its banner.
function onOneTrustReady() {
  // Pause the guard timer while the banner is visible.
  window.Prehide.setConsent("pending");

  OneTrust.OnConsentChanged(function (event) {
    if (event.consentedToTargeting) {
      window.Prehide.setConsent("in");
    } else {
      window.Prehide.setConsent("out");
    }
  });
}
```

### Exemplo: estilo TCF/IAB

```js
// Optional: pause the guard while UI is up.
window.Prehide.setConsent("pending");

// Your CMP eventually emits the final TC string.
function onTcData(tcData) {
  const hasTargetConsent = /* derive from tcData */;
  window.Prehide.setConsent(hasTargetConsent ? "in" : "out");
}
```

