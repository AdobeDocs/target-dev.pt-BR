---
keywords: implementação, api, perfil, configurações da api de perfil, token de autenticação
description: Saiba como configurar autenticação para atualizações em lote via [!DNL Adobe Target] e gerar um token de autenticação de perfil.
title: Como usar as configurações da API de perfil para ativar ou desativar atualizações em lote?
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 42%

---

# Configurações da API de perfil

Ative ou desative a autenticação para atualizações em lote via [!DNL Adobe Target] e gerar um token de autenticação de perfil.

[!DNL Adobe Target]O cria e mantém um perfil para cada usuário individual. Esse perfil é armazenado no [!DNL Target] cluster de borda e é atualizado em tempo real após cada visita. Também é possível atualizar um perfil individualmente ou em massa por meio da API.

Para maior segurança, você pode fazer com que uma chamada de API de atualização em massa solicite um token de acesso válido a ser enviado no cabeçalho da solicitação.

**[!DNL Target]Para solicitar a autenticação e gerar um token de acesso usando a interface de usuário do :**

1. Clique em **[!UICONTROL Administração]** > **[!UICONTROL Implementação]**.
1. Em **[!UICONTROL API de perfil]** deslize o **[!UICONTROL Exigir autenticação]** alterne para a posição ativado ou desativado.

   ![imagem alt](assets/profile_api_settings.png)

1. (Condicional) Se você ativou o requisito de autenticação, clique em **[!UICONTROL Gerar novo token de autenticação de perfil]**.

   ![imagem alt](assets/profile_api_settings_2.png)

   O token expira de acordo com o tempo listado na caixa Expira em.

   Você deve ter uma das seguintes permissões de usuário para gerar um token de autenticação:

   * Função de administrador ou ter pelo menos direitos de Aprovador

     Para obter mais informações para clientes do Target Standard, consulte [Especificar funções e permissões](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions) in *Usuários*. Para obter mais informações para clientes do [!DNL Target Premium], consulte [Configurar permissões corporativas](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Função de administrador no nível de espaço de trabalho/perfil de produto

     Os espaços de trabalho estão disponíveis somente para clientes do [!DNL Target Premium]. Para obter mais informações, consulte [Configurar permissões corporativas](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Direitos de administrador (permissão de Sysadmin) no nível do produto [!DNL Adobe Target]

Também é possível gerar um token de autenticação de perfil por meio da API. Para obter mais informações, consulte &quot;Perfis&quot; no [Guia da API de administração e perfil do Adobe Target](../../administer/admin-api/admin-api-overview-new.md).

1. Copie o token e inclua-o no cabeçalho da solicitação no formato: &quot;Autorização&quot; : &quot;Portador&quot;.

1. Clique em **[!UICONTROL Gerar novo token de autenticação de perfil]** para regenerar o token conforme necessário.

>[!WARNING]
>
>Redefinir esse token resulta em falha das chamadas de API usando o token atual. Isso necessitará da atualização de qualquer script ou aplicativo que use esse token.
