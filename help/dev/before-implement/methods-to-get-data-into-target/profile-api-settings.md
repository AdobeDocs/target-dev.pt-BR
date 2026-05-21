---
keywords: implementação, api, perfil, configurações da api de perfil, token de autenticação
description: Saiba como configurar a autenticação para atualizações em lote por meio de  [!DNL Adobe Target] APIs e gerar um token de autenticação de perfil.
title: Como usar as configurações da API de perfil para ativar ou desativar atualizações em lote?
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
TQID: https://experienceleague.adobe.com/-KYSphaCrm0ICK7g92v9x-uK--nwirs4-DWBR3G5rTM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 347
ht-degree: 33%

---

# Configurações da API de perfil

Habilite ou desabilite a autenticação para atualizações em lote via APIs do [!DNL Adobe Target] e gere um token de autenticação de perfil.

[!DNL Adobe Target] cria e mantém um perfil para cada usuário individual. Este perfil está armazenado no cluster de borda [!DNL Target] e é atualizado em tempo real após cada visita. Também é possível atualizar um perfil individualmente ou em massa por meio da API.

Para maior segurança, você pode fazer com que uma chamada de API de atualização em massa solicite um token de acesso válido a ser enviado no cabeçalho da solicitação.

**Para exigir autenticação e gerar um token de acesso usando a interface de usuário [!DNL Target]:**

1. Clique em **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. Em **[!UICONTROL Profile API]**, deslize o botão **[!UICONTROL Require Authentication]** para a posição habilitada ou desabilitada.

   ![alt imagem](assets/profile_api_settings.png)

1. (Condicional) Se você habilitou o requisito de autenticação, clique em **[!UICONTROL Generate New Profile Authentication Token]**.

   ![alt imagem](assets/profile_api_settings_2.png)

   O token expira de acordo com o tempo listado na caixa Expira em.

   Você deve ter uma das seguintes permissões de usuário para gerar um token de autenticação:

   * Função de administrador ou ter pelo menos direitos de Aprovador

     Para obter mais informações para clientes do Target Standard, consulte [Especificar funções e permissões](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions) em *Usuários*. Para obter mais informações para clientes do [!DNL Target Premium], consulte [Configurar permissões corporativas](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Função de administrador no nível de espaço de trabalho/perfil de produto

     Os espaços de trabalho estão disponíveis somente para clientes do [!DNL Target Premium]. Para obter mais informações, consulte [Configurar permissões corporativas](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Direitos de administrador (permissão de Sysadmin) no nível do produto [!DNL Adobe Target]

Também é possível gerar um token de autenticação de perfil por meio da API. Para obter mais informações, consulte &quot;Perfis&quot; no [Guia da API de perfil e administração do Adobe Target](../../administer/admin-api/admin-api-overview-new.md).

1. Copie o token e inclua-o no cabeçalho da solicitação no formato: &quot;Autorização&quot; : &quot;Portador&quot;.

1. Clique em **[!UICONTROL Generate New Profile Authentication Token]** para regenerar o token conforme necessário.

>[!WARNING]
>
>Redefinir esse token resulta em falha das chamadas de API usando o token atual. Isso necessitará da atualização de qualquer script ou aplicativo que use esse token.
