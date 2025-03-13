---
keywords: Navegadores, Pré-requisitos, Requisitos, Internet Explorer, chrome, firefox, safari, android, superfície, Navegadores0
description: Saiba quais navegadores de Internet  [!DNL Adobe Target] oferecem suporte para sua interface e para entrega de conteúdo.
title: Quais Navegadores O [!DNL Target] Suporta?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: 1b6dcb24d677b758ed1daf85dc0a7e9e5b42680d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 20%

---

# Navegadores compatíveis

O aplicativo [!DNL Adobe Target] e a entrega de conteúdo foram testados em uma grande variedade de navegadores e dispositivos.

Para obter informações mais importantes sobre TLS, consulte [Alterações na criptografia do TLS (Transport Layer Security)](tls-transport-layer-security-encryption.md).

## Interface do [!DNL Target] Standard/Premium

A interface [!DNL Target] oferece suporte aos seguintes navegadores e dispositivos:

>[!NOTE]
>
>O Target suporta a versão mais recente de cada navegador listado e a versão mais recente menos 1.


| Tipo de dispositivo | Versão do navegador |
|--- |--- |
| [!DNL Windows] | <ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul> |
| [!DNL Mac] | <ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul> |

## Requisitos de edição visual

Para abrir, criar e visualizar suas páginas da Web de maneira confiável no [!UICONTROL Visual Experience Composer] (VEC), você deve ter a [extensão de navegador da Adobe Experience Cloud Visual Editing Helper](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank} instalada no navegador da Web ou usar o [!UICONTROL Enhanced Experience Composer (EEC)].

>[!NOTE]
>
>[!DNL Google Chrome] e [!DNL Microsoft Edge] são os únicos navegadores atualmente com suporte para edição visual de páginas da Web no [!DNL Adobe Target].


## Entrega de conteúdo

A entrega de conteúdo foi testada nos seguintes navegadores e dispositivos:

| Tipo de dispositivo | Versão do navegador |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 e 10. Testado no modo de emulação. **Observação**: a entrega de conteúdo no IE 9 não é mais compatível com o at.js 1.3.0 (e posterior). A entrega de conteúdo no IE 10, 11 e em todas as versões mais antigas não é mais compatível com o at.js 2.5.0 (e posterior).</li><li>Internet Explorer 11 **Observação**: a entrega de conteúdo no IE 10, 11 e em todas as versões mais antigas não é mais compatível com o at.js 2.5.0 (e posterior).</li><li>Microsoft Edge</li><li>Chrome (mais recente, mais recente menos 1)</li><li>Firefox (mais recente, mais recente menos 1)</li></ul> |
| Mac | <ul><li>Apple Safari (Mais Recente). **Observação**: para obter mais informações sobre como o Safari processa cookies próprios e de terceiros, consulte [Cookie do Target](../implement/client-side/atjs/atjs-cookies.md).</li><li>Firefox (mais recente, mais recente menos 1)</li><li>Chrome (mais recente, mais recente menos 1)</li></ul> |
| Móvel/Tablet | <ul><li>Apple iOS (mais recente)</li><li>Dispositivos e tablets Android (Android 4 e posterior)</li><li>Microsoft Surface (Windows 8.1)</li></ul> |

Observe o seguinte:

* O [!DNL Adobe Experience Platform Web SDK] foi projetado para funcionar de forma ideal nas versões mais recentes do [!DNL Google Chrome], [!DNL Safari], [!DNL Firefox] e [!DNL Microsoft Edge Chromium]. Você pode ter problemas ao usar determinados recursos em versões mais antigas desses navegadores ou navegadores obsoletos, como o [!DNL Internet Explorer].
* Para implementações da at.js, o [!DNL Target] exibe o conteúdo padrão nas versões anteriores do Internet Explorer e possivelmente nas versões anteriores dos navegadores listados.
* O Internet Explorer trata todos os elementos desconhecidos (como elementos personalizados) como o mesmo tipo de elemento. Como resultado, a entrega não funciona com elementos personalizados.
* O [!DNL Target] exibe o conteúdo padrão em navegadores não listados acima e nos navegadores usando o [modo quirks](https://en.wikipedia.org/wiki/Quirks_mode). O at.js requer um tipo de doctype que é renderizado no modo padrão, por exemplo: `<!DOCTYPE html>`.
* A infraestrutura de entrega do [!DNL Adobe] está sendo protegida para NÃO ser compatível com dispositivos e navegadores TLS 1.0 após 12 de setembro de 2018. Consulte [Mudanças de criptografia TLS (Transport Layer Security)](../before-implement/tls-transport-layer-security-encryption.md) para entender o impacto geral dessa mudança.
