---
keywords: cookie, cookies, excluir cookie, excluir [!DNL Target] cookie, google chrome, chrome, mozilla firefox, firefox, microsoft edge, safari, cookie1
description: Saiba como excluir os cookies do navegador do  [!DNL Target]  para validar suas experiências.
title: Como excluir o cookie  [!DNL Target] ?
feature: Privacy & Security
exl-id: c975c47f-8d81-4abe-aa89-f65275a73002
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 3%

---

# Excluir o cookie [!DNL Target]

Você pode excluir o cookie do navegador [!DNL Adobe Target] (mbox) para poder validar todas as suas experiências durante os testes.

Se não houver nenhum cookie [!DNL Target] (mbox), você será considerado um novo visitante e verá uma nova experiência. Há várias maneiras de excluir sua mbox sem excluir todos os cookies do navegador.

>[!NOTE]
>
>As instruções a seguir estão corretas para os navegadores e as versões listadas. Pesquise na Internet para obter instruções sobre o navegador ou a versão específica.

## Exclua o cookie [!DNL Target] do Google Chrome

Versão 84.0.4147,105

1. Clique no menu **[!UICONTROL Chrome]** > **[!UICONTROL Preferences]**.
1. Clique na guia **[!UICONTROL Privacy and Security]**.
1. Clique em **[!UICONTROL Cookies and other site data]**.
1. Clique em **[!UICONTROL See all cookies and site data]**.
1. Expanda a seção `adobe.com`, selecione o cookie **mbox** e clique no ícone excluir (X).

## Exclua o cookie [!DNL Target] do Mozilla Firefox

Versão 79.0

### Excluir todos os cookies associados a `adobe.com`

1. Clique no menu **[!UICONTROL Firefox]** > **[!UICONTROL Preferences]**.
1. Clique na guia **[!UICONTROL Privacy and Security]**.
1. Em **Cookies e Dados do Site*, clique em &#x200B;** [!UICONTROL Manage Data]**.
1. Selecione o site `adobe.com` e clique em **[!UICONTROL Remove Selected]**.

>[!WARNING]
>
>Isso exclui todos os cookies associados ao site `adobe.com`. Se quiser excluir um cookie individual de um site, siga as instruções abaixo.

### Excluir um cookie individual (mbox)

1. No Firefo, clique em **[!UICONTROL Tools]** > **[!UICONTROL Web Developer]** > **[!UICONTROL Storage Inspector]**.
1. Clique na guia **[!UICONTROL Advanced]**.
1. Navegue até a página da Web que contém o cookie que deseja excluir.
1. Expanda a seção **[!UICONTROL Cookies]** e clique em `https://experience.adobe.com`.
1. Clique com o botão direito do mouse no cookie **[!UICONTROL mbox]** e depois clique em **[!UICONTROL Delete]**.

## Exclua o cookie [!DNL Target] do Microsoft Edge

Versão 84.0.522.52

1. Clique no menu **[!UICONTROL Microsoft Edge]** > **[!UICONTROL Preferences]**.
1. Clique na guia **[!UICONTROL Site Permissions]**.
1. Clique em **[!UICONTROL Cookies and site data]**.
1. Clique em **[!UICONTROL See all cookies and site data]**.
1. Expanda a seção `adobe.com`, selecione o cookie **mbox** e clique no ícone excluir (X).

## Exclua o cookie [!DNL Target] do Apple Safari

Versão 13.1.2

### Excluir todos os cookies associados a `adobe.com`

1. Clique no menu **[!UICONTROL Safari]** > **[!UICONTROL Preferences]**.
1. Clique na guia **[!UICONTROL Privacy]**.
1. Clique em **[!UICONTROL Manage Website Data]**.
1. Selecione os sites dos cookies que você deseja excluir e clique em **[!UICONTROL Remove]**.

>[!WARNING]
>
>Isso exclui todos os cookies associados ao site `adobe.com`. Se quiser excluir um cookie individual de um site, siga as instruções abaixo.

### Excluir um cookie individual (mbox)

1. Clique no menu **[!UICONTROL Safari]** > **[!UICONTROL Preferences]**.
1. Clique na guia **[!UICONTROL Advanced]**.
1. Selecione a opção **[!UICONTROL Show Develop menu in menu bar]**.
1. Navegue até a página da Web que contém o cookie que deseja excluir.
1. Clique no menu **[!UICONTROL Develop]** > **[!UICONTROL Show Web Inspector]**.
1. Clique na guia **[!UICONTROL Storage]**.
1. Expanda a seção **[!UICONTROL Cookies]** e clique em `www.adobe.com`.
1. Clique com o botão direito do mouse no cookie **mbox** e clique em **[!UICONTROL Delete]**.
