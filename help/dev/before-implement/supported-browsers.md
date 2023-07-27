---
keywords: Navegadores, Pré-requisitos, Requisitos, Internet Explorer, chrome, firefox, safari, android, superfície, Navegadores0
description: Saiba quais navegadores de Internet [!DNL Adobe Target] O é compatível com sua interface e para a entrega de conteúdo.
title: O que os navegadores fazem [!DNL Target] Suporte?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 43%

---

# Navegadores compatíveis

O aplicativo [!DNL Adobe Target] e a entrega de conteúdo foram testados em uma grande variedade de navegadores e dispositivos.

Para obter informações mais importantes sobre TLS, consulte [Alterações na criptografia da Segurança da camada de transporte (TLS)](tls-transport-layer-security-encryption.md).

## [!DNL Target]Interface do Standard/Premium

A variável [!DNL Target] A interface do é compatível com os seguintes navegadores e dispositivos:

| Tipo de dispositivo | Versão do navegador |
|--- |--- |
| Windows | <ul><li>Microsoft Edge</li><li>Google Chrome (mais recente, mais recente menos 1)</li><li>Mozilla Firefox (mais recente, mais recente menos 1)</li></ul> |
| Mac | <ul><li>Firefox (mais recente, mais recente menos 1)</li><li>Chrome (mais recente, mais recente menos 1)</li></ul> |

## Entrega de conteúdo

A entrega de conteúdo foi testada nos seguintes navegadores e dispositivos:

| Tipo de dispositivo | Versão do navegador |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 e 10. Testado no modo de emulação. **Nota**: a entrega de conteúdo no IE 9 não é mais compatível com o at.js 1.3.0 (e posterior). A entrega de conteúdo no IE 10, 11 e em todas as versões mais antigas não é mais compatível com o at.js 2.5.0 (e posterior).</li><li>Internet Explorer 11. **Nota**: a entrega de conteúdo no IE 10, 11 e em todas as versões mais antigas não é mais compatível com o at.js 2.5.0 (e posterior).</li><li>Microsoft Edge</li><li>Chrome (mais recente, mais recente menos 1)</li><li>Firefox (mais recente, mais recente menos 1)</li></ul> |
| Mac | <ul><li>Apple Safari (mais recente). **Observação**: para obter mais informações sobre como o Safari processa cookies próprios e de terceiros, consulte [Cookie do Target](../implement/client-side/atjs/atjs-cookies.md).</li><li>Firefox (mais recente, mais recente menos 1)</li><li>Chrome (mais recente, mais recente menos 1)</li></ul> |
| Móvel/Tablet | <ul><li>Apple iOS (mais recente)</li><li>Dispositivos e tablets Android (Android 4 e posterior)</li><li>Microsoft Surface (Windows 8.1)</li></ul> |

Observe o seguinte:

* Para implementações da at.js, [!DNL Target] O exibe o conteúdo padrão nas versões anteriores do Internet Explorer e possivelmente nas versões anteriores dos navegadores listados.
* O Internet Explorer trata todos os elementos desconhecidos (como elementos personalizados) como o mesmo tipo de elemento. Como resultado, a entrega não funciona com elementos personalizados.
* [!DNL Target]O exibe o conteúdo padrão nos navegadores não listados acima e nos navegadores que usam o [modo QUIRKS](https://en.wikipedia.org/wiki/Quirks_mode). O at.js requer um tipo de doctype que é renderizado no modo padrão, por exemplo: `<!DOCTYPE html>`.
* [!DNL Adobe]A infraestrutura do Delivery está sendo protegida para NÃO ser compatível com dispositivos e navegadores que usam o TLS 1.0 após 12 de setembro de 2018. Consulte [Mudanças de criptografia TLS (Transport Layer Security)](../before-implement/tls-transport-layer-security-encryption.md) para entender o impacto geral dessa mudança.
