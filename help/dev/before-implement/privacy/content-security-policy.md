---
keywords: política de segurança de conteúdo, csp, at.js, lista de permissões, incluir na lista de permissões, cintilação, pré-ocultar, pré-ocultação, pré-ocultação, política de segurança de conteúdo, iFrame, iframe
description: Saiba mais sobre as diretivas de Política de Segurança de Conteúdo (CSP) que devem ser adicionadas ao usar o  [!DNL Adobe Target].
title: Como o  [!DNL Target]  lida com as Políticas de segurança de conteúdo (CSP)?
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
source-git-commit: c43c79b29768694eac534e22047b5ee6a3d0ccd5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 28%

---

# Diretivas da Política de segurança de conteúdo (CSP)

Se você estiver usando a [Política de Segurança de Conteúdo](https://en.wikipedia.org/wiki/Content_Security_Policy) (CSP) para a implementação do [!DNL Adobe Target], deverá adicionar as seguintes diretivas da CSP ao usar o [at.js 2.1 ou posterior](../../implement/client-side/atjs/target-atjs-versions.md):

* `connect-src` com o `*.tt.omtrdc.net` na lista de permissões. Necessário para permitir a solicitação de rede para a borda do [!DNL Target].
* `style-src unsafe-inline`. Necessário para controle de pré-ocultação e cintilação.
* `script-src unsafe-inline`. Necessário para permitir a execução do JavaScript que pode fazer parte de uma oferta do HTML.

## Perguntas frequentes

Consulte as seguintes perguntas frequentes sobre políticas de segurança:

### O CORS (Compartilhamento de recursos entre origens) e as políticas entre domínios do Flash apresentam problemas de segurança?

A maneira recomendada de implementar a política CORS é permitir o acesso apenas a origens confiáveis que o exijam por meio de uma lista de permissões de domínios confiáveis. O mesmo pode ser dito para a política entre domínios do Flash. Alguns clientes do [!DNL Target] estão preocupados com o uso de caracteres curingas para domínios no Target. A preocupação é que, se um usuário estiver conectado a um aplicativo e visitar um domínio permitido pela política, qualquer conteúdo mal-intencionado em execução nesse domínio poderá recuperar conteúdo confidencial do aplicativo e realizar ações dentro do contexto de segurança do usuário conectado. Essa situação é comumente chamada de CSRF (Falsificação de solicitação entre sites).

No entanto, em uma implementação [!DNL Target], essas políticas não devem representar um problema de segurança.

“adobe.tt.omtrdc.net” é um domínio de propriedade da Adobe. O [!DNL Adobe Target] é uma ferramenta de teste e personalização e espera-se que o [!DNL Target] possa receber e processar solicitações de qualquer lugar sem exigir autenticação. Essas solicitações contêm pares de chave/valor usados para testes A/B, recomendações ou personalização de conteúdo.

O Adobe não armazena informações pessoais identificáveis (PII) ou outras informações confidenciais nos servidores de borda do [!DNL Adobe Target], para os quais &quot;adobe.tt.omtrdc.net&quot; aponta.

Espera-se que o [!DNL Target] possa ser acessado de qualquer domínio por meio de chamadas JavaScript. A única maneira de permitir esse acesso é aplicando &quot;Access-Control-Allow-Origin&quot; com um curinga.

### Como permitir ou impedir que meu site seja incorporado como um iFrame em domínios estrangeiros?

Para permitir que o [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=pt-BR){target=_blank} (VEC) incorpore seu site em um iFrame, o CSP (se definido) deve ser alterado na configuração do servidor Web. [!DNL Adobe] domínios devem estar na lista de permissões e configurados.

Por motivos de segurança, talvez você queira impedir que seu site seja incorporado como um iFrame em domínios estrangeiros.

As seções a seguir explicam como permitir ou impedir que o VEC incorpore seu site em um iFrame.

#### Permitir que o VEC incorpore o site em um iFrame

A solução mais fácil para habilitar o VEC para incorporar o site em um iFrame é permitir `*.adobe.com`, que é o curinga mais amplo.

Por exemplo:

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

Como na ilustração a seguir (clique para ampliar):


![CSP com curinga mais amplo](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

Talvez você queira permitir somente o serviço [!DNL Adobe] real. Este cenário pode ser alcançado usando `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com`.

Por exemplo:

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

Como na ilustração a seguir (clique para ampliar):

![CSP com escopo de ExperienceCloud](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

O acesso mais restritivo à conta de uma empresa pode ser obtido usando o `https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com`, em que `<Client Code>` representa seu código de cliente específico.

Por exemplo:

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

Como na ilustração a seguir (clique para ampliar):

![CSP com escopo de clientcode](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Se você tiver o [Launch/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) implementado, ele também deverá ser desbloqueado.
>
>Por exemplo:
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### Impedir que o VEC incorpore seu site em um iFrame

Para impedir que o VEC incorpore seu site em um iFrame, é possível restringir somente a &quot;self&quot;.

Por exemplo:

`Content-Security-Policy: frame-ancestors 'self'`

Como mostrado na ilustração a seguir (clique para ampliar):

![Erro de CSP](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

A seguinte mensagem de erro é exibida:

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

