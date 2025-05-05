---
title: Como configurar a autenticação de  [!DNL Adobe Target] APIs
description: Como faço para gerar os tokens de autenticação necessários para interagir com êxito com as  [!DNL Adobe Target] APIs?
feature: APIs/SDKs, Administration & Configuration
exl-id: fc67363c-6527-40aa-aff1-350b5af884ab
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---

# Configurar autenticação para [!DNL Adobe Target] APIs

As APIs de Administrador [!DNL Adobe Target], incluindo as APIs [!DNL Recommendations Admin], são protegidas por autenticação para garantir que somente usuários autorizados as usem para acessar [!DNL Adobe Target]. Use o [Adobe Developer Console](https://developer.adobe.com/console/home) para gerenciar esta autenticação para todos os [!DNL Adobe Experience Cloud solutions], incluindo o [!DNL Adobe Target].

>[!IMPORTANT]
>
>As credenciais da Conta de serviço (JWT) descritas neste artigo serão substituídas em favor das novas credenciais de servidor para servidor do OAuth.
>
>As credenciais da Conta de serviço (JWT) continuarão a funcionar até 1º de janeiro de 2025. Você deve migrar seu aplicativo ou integração para usar a nova credencial OAuth de servidor para servidor antes de 1º de janeiro de 2025.
>
>Para obter mais informações e instruções passo a passo para migrar sua integração, consulte [Migrando da credencial de Conta de Serviço (JWT) para a credencial de servidor para servidor OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/){target=_blank} na documentação do *Developer Console*.
>
>Para obter informações sobre como configurar novas credenciais do OAuth, consulte a [implementação de credenciais de servidor para servidor do OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/){target=_blank} na documentação do *Developer Console*.

Estas são as etapas preliminares necessárias para gerar os tokens de autenticação JWT herdados necessários para interagir com êxito com as APIs do [!DNL Adobe Target]:

1. Crie um projeto (anteriormente chamado de integração) no [!DNL Adobe Developer Console].
1. Exportar detalhes do projeto para o Postman.
1. Gerar um token de acesso do portador.
1. Teste o token de acesso do portador.

## Pré-requisitos

| Recurso | Detalhes |
| --- | --- |
| Postman | Para concluir essas etapas com êxito, obtenha o [aplicativo Postman](https://www.postman.com/downloads/) para seu sistema operacional. O Postman Basic é gratuito com a criação da conta. Embora não seja necessário para usar APIs do [!DNL Adobe Target] em geral, o Postman facilita os fluxos de trabalho da API e o [!DNL Adobe Target] fornece várias coleções do Postman para ajudar a executar suas APIs e aprender como elas operam. O restante deste guia pressupõe conhecimento prático do Postman. Para obter ajuda, consulte a [documentação do Postman](https://learning.getpostman.com/). |
| Referências | Familiaridade com os seguintes recursos é presumida no restante deste guia:<ul><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentação da API de perfil e de administrador do Target](../administer/admin-api/admin-api-overview-new.md)</li><li>[Documentação da API do Recommendations](https://developer.adobe.com/target/administer/recommendations-api/)</li></ul> |

## Criar um projeto Adobe I/O

Nesta seção, você acessará [!DNL Adobe Developer Console] e criará um projeto para [!DNL Adobe Target]. Para obter mais informações, consulte a [documentação sobre projetos](https://developer.adobe.com/developer-console/docs/guides/projects/).

&lt;!—(1) Gere sua chave privada e certificado público, de acordo com a [documentação sobre autenticação](https://developer.adobe.com/developer-console/docs/guides/authentication/). // [//]: # (conforme descrito na **Etapa 1** de [Como configurar o Adobe IO: Autenticação - Passo a Passo](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). Depois de concluir a Etapa 1, retorne a este guia e retome com a Etapa 2 abaixo. // O resultado desta etapa deve ser a criação de um arquivo `private.key` e um arquivo `certificate_pub.crt`. Retorne a este guia após gerar os dois arquivos.)—>

1. No [Adobe Admin Console](https://adminconsole.adobe.com/), verifique se a sua conta de usuário [!DNL Adobe] recebeu acesso de nível de [Administrador de Produto](https://helpx.adobe.com/br/enterprise/using/admin-roles.html) e [Desenvolvedor](https://helpx.adobe.com/br/enterprise/using/manage-developers.html) ao [!DNL Target].

1. No [Adobe Developer Console](https://developer.adobe.com/console/home), selecione o [!UICONTROL Experience Cloud Organization] para o qual deseja criar essa integração. (Observe que é provável que você só tenha acesso a um único [!UICONTROL Experience Cloud Organization].)

   ![configure-io-target-createproject2.png](assets/configure-io-target-createproject2.png)

1. Clique em **[!UICONTROL Create new project]**.

   ![configure-io-target-createproject3.png](assets/configure-io-target-createproject3.png)

1. Clique em **[!UICONTROL Add API]** para adicionar uma REST API ao seu projeto para acessar serviços e produtos do [!DNL Adobe].

   ![Adicionar API](assets/configure-io-target-createproject4.png)

1. Selecione **[!DNL Adobe Target]** como o serviço [!DNL Adobe] ao qual você deseja integrar. Clique no botão **[!UICONTROL Next]** que aparece.

   ![configure-io-target-createproject5](assets/configure-io-target-createproject5.png)

1. Selecione uma opção para associar chaves públicas e privadas à integração de conta de serviço que você está criando para [!DNL Target]. Para este exemplo, selecione **[!UICONTROL Option 1: Generate a key pair]** e clique em **[!UICONTROL Generate keypair]**.

   ![configure-io-target-createproject6](assets/configure-io-target-createproject6.png)

1. Conforme instruído, anote o arquivo de configuração baixado automaticamente (`config`), que contém sua chave privada. Clique em **[!UICONTROL Next]**.

   ![configure-io-target-createproject7](assets/configure-io-target-createproject7.png)

1. Em seu sistema de arquivos, verifique o local de `config`, que é o arquivo de configuração compactado criado na etapa anterior. Novamente, esse arquivo `config` contém sua chave privada, que será necessária posteriormente. O local exato em seu sistema de arquivos pode ser diferente do mostrado aqui.

   ![configure-io-target-createproject8](assets/configure-io-target-createproject8.png)

1. De volta à Adobe Developer Console, selecione o(s) [perfil(is) de produto](https://helpx.adobe.com/pt/enterprise/using/manage-products-and-profiles.html) correspondente(s) às propriedades nas quais você está usando o Adobe Recommendations. (Se você não estiver usando propriedades do, selecione a opção Workspace padrão.) Clique em **[!UICONTROL Save configured API]**.

   ![configure-io-target-createproject9](assets/configure-io-target-createproject9.png)

1. Clique em **[!UICONTROL Create Integration]**. Você deve receber uma mensagem temporária indicando que sua API foi configurada com êxito.
1. Como etapa final, renomeie seu projeto com um nome mais significativo que o `Project 1` original. Para fazer isso, navegue até o projeto usando o caminho de navegação como mostrar, clique em **[!UICONTROL Edit project]** para acessar o modal **[!UICONTROL Edit Project]** e renomeie o projeto.

   ![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
>
>Neste exemplo, nomeamos nosso projeto como Integração &quot;[!DNL Target]&quot;. Se você prevê usar seu projeto para mais do que apenas [!DNL Adobe Target], talvez queira nomeá-lo adequadamente. Por exemplo, você pode optar por nomeá-lo como &quot;APIs de Adobe&quot; ou &quot;APIs de Experience Cloud&quot;, pois ele pode ser usado com outras soluções na Adobe Experience Cloud.

## Exportar detalhes do projeto

Agora que você tem um projeto Adobe que pode ser usado para acessar o [!DNL Target], é necessário enviar os detalhes desse projeto junto com as solicitações da API Adobe. Esses detalhes são necessários para interagir com várias APIs Adobe, incluindo várias APIs [!DNL Target]. Por exemplo, os detalhes da integração incluem informações de autorização e autenticação exigidas pelas [!DNL Target] APIs de administrador. Portanto, para usar as APIs com o Postman, é necessário obter esses detalhes no Postman.

Há várias maneiras de especificar os detalhes do seu projeto no Postman, mas nesta seção, aproveitamos alguns recursos e coleções pré-criados. Primeiro (nesta seção), você exportará os detalhes da sua integração em um ambiente do Postman. Em seguida (na seção a seguir), você gerará um token de acesso do portador para conceder acesso aos recursos de Adobe necessários.

>[!NOTE]
>
>Para obter instruções de vídeo aplicáveis a qualquer solução de Experience Cloud, incluindo [!DNL Target], consulte [Usar o Postman com APIs de Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=pt-BR). As seguintes seções são relevantes para as APIs do [!DNL Target]: 1. Crie e exporte a API de Experience Platform para o Postman 2. Gerar um token de acesso com o Postman. Essas etapas também são fornecidas abaixo.

1. Ainda no [Adobe Developer Console](https://developer.adobe.com/console/home), navegue para exibir as credenciais **[!UICONTROL Service Account (JWT)]** do novo projeto. Use a navegação à esquerda ou a seção **[!UICONTROL Credentials]**, como mostrado.

   ![JWT1](assets/configure-io-target-jwt1.png)

   Em **[!UICONTROL Credential details]**, observe que você pode visualizar **[!UICONTROL Public key(s)]**, **[!UICONTROL Client ID]** e outras informações relacionadas à sua conta de serviço.

   ![JWT1a](assets/configure-io-target-jwt1a.png)

1. Clique para acessar as informações sobre a API **[!DNL Adobe Target]**. Use a navegação à esquerda ou a seção **Produtos e serviços conectados** como mostrado.

   ![JWT2](assets/configure-io-target-jwt2.png)

1. Clique em **[!UICONTROL Download for Postman]** > **[!UICONTROL Service Account (JWT)]** para criar um arquivo JSON capturando suas informações de autenticação para um ambiente Postman.

   ![JWT3](assets/configure-io-target-jwt3.png)

   Observe o arquivo JSON no seu sistema de arquivos.

   ![JWT3a](assets/configure-io-target-jwt3a.png)

1. No Postman, clique no ícone de engrenagem para gerenciar seus ambientes, em seguida, clique em **[!UICONTROL Import]** para importar o arquivo JSON (ambiente).

   ![JWT4](assets/configure-io-target-jwt4.png)

1. Escolha seu arquivo e clique em **[!UICONTROL Open]**.

   ![JWT5](assets/configure-io-target-jwt5.png)

1. No modal **Gerenciar ambientes** do Postman, clique no nome do ambiente recém-importado para inspecioná-lo. (O nome do ambiente pode ser diferente do mostrado aqui. Edite o nome conforme desejado. Ele não precisa necessariamente corresponder ao nome do projeto [!DNL Adobe].)

   ![JWT6](assets/configure-io-target-jwt6.png)

1. Os valores de `CLIENT_SECRET` e `API_KEY` (juntamente com outras variáveis) foram preenchidos previamente a partir da sua integração, conforme definido na Adobe Developer Console. (A variável `CLIENT_SECRET` do Postman deve corresponder à credencial de Adobe `CLIENT SECRET` conforme exibida no Developer Console, e `API_KEY` no Postman também deve corresponder a `CLIENT ID` no Developer Console.) Por outro lado, a observação `PRIVATE_KEY`, `JWT_TOKEN` e `ACCESS_TOKEN` estão em branco. Vamos começar fornecendo o valor `PRIVATE_KEY`.

   ![JWT7](assets/configure-io-target-jwt7.png)

1. Em seu sistema de arquivos, abra o arquivo `config` e abra o arquivo de chave `private`.

   ![JWT8](assets/configure-io-target-jwt8.png)

1. Selecione e copie todo o conteúdo do arquivo de chave `private`.

   ![JWT9](assets/configure-io-target-jwt9.png)

1. No Postman, cole seu valor de chave privada nos campos **[!UICONTROL INITIAL VALUE]** e **[!UICONTROL CURRENT VALUE]**.

   ![JWT10](assets/configure-io-target-jwt10.png)

1. Clique em **[!UICONTROL Update]** e feche o modal Ambientes.

## Gerar o token de acesso do portador

Nesta seção, você gera o token de acesso do portador, que é necessário para autenticar sua interação com APIs [!DNL Adobe Target]. Para gerar o token de acesso do portador, é necessário enviar os detalhes da integração (estabelecidos nas seções anteriores) ao [Adobe Identity Management Service (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Há algumas maneiras diferentes de fazer isso, mas neste guia aproveitamos uma coleção do Postman que contém uma chamada IMS pré-criada que torna o processo direto e fácil. Depois de importar a coleção, você pode reutilizá-la sempre que necessário, para gerar novos tokens não apenas para [!DNL Adobe Target], mas também para outras APIs de Adobe.

1. Navegue até o [Adobe Chamadas de amostra da API de serviço do Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).

   ![token1](assets/configure-io-target-generatetoken1.png)

1. Clique no **[!UICONTROL Adobe I/O Access Token Generation Postman collection]**.

   ![token2](assets/configure-io-target-generatetoken2.png)

1. Obtenha o JSON bruto para esta coleção clicando em **[!UICONTROL Raw]** e copiando o JSON resultante para a área de transferência. (Como alternativa, você pode salvar o JSON bruto como um arquivo .json.)

   ![token3](assets/configure-io-target-generatetoken3.png)

1. No Postman, importe a coleção colando e enviando o JSON bruto da área de transferência. (Como alternativa, você pode fazer upload do arquivo .json salvo.) Clique em **[!UICONTROL Continue]**.

   ![token4](assets/configure-io-target-generatetoken4.png)

1. Selecione a solicitação **[!UICONTROL IMS: JWT Generate + Auth via User Token]** na coleção Adobe I/O Access Token Generation Postman, verifique se o ambiente está selecionado e clique em **[!UICONTROL Send]** para gerar o token.

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Esse token de acesso do portador será válido por 24 horas. Envie a solicitação novamente sempre que precisar gerar um novo token.

1. Abra o modal Gerenciar ambientes novamente e selecione seu ambiente.

   ![token6](assets/configure-io-target-jwt11.png)

1. Observe que os valores `ACCESS_TOKEN` e `JWT_TOKEN` agora estão preenchidos.

   ![token7](assets/configure-io-target-generatetoken7.png)

Pergunta: Preciso usar a coleção Adobe I/O Access Token Generation Postman para gerar o JSON Web Token (JWT) e o token de acesso do portador?

Resposta: Não. A coleção Adobe I/O Access Token Generation Postman está disponível para conveniência a fim de gerar mais facilmente o JWT e o token de acesso do portador no Postman. Como alternativa, você pode usar os recursos no Adobe Developer Console para gerar manualmente o token de acesso do portador.

## Testar o token de acesso do portador

Neste exercício, você usará seu novo token de acesso de portador enviando uma solicitação de API que recupera uma lista de atividades da conta [!DNL Target]. Uma resposta bem-sucedida indica que o projeto [!DNL Adobe] e a autenticação estão funcionando como esperado para usar a API.

1. Importe a [[!DNL Adobe Target] Coleção de Postman de APIs de administrador](https://developers.adobetarget.com/api/#admin-postman-collection). Siga todos os prompts até que a coleção seja importada no Postman.

   ![testtoken1](assets/configure-io-target-testtoken0.png)

1. Expanda a coleção e observe a solicitação **[!UICONTROL List activities]**.

   ![testtoken1](assets/configure-io-target-testtoken1.png)

1. Observe que variáveis como `{{access_token}}` não são resolvidas inicialmente. Você poderia resolver isso de várias maneiras diferentes, por exemplo, você poderia definir uma nova variável de coleção chamada `{{access_token}}`, mas neste guia, você alterará a solicitação da API para aproveitar o ambiente do Postman que estava usando anteriormente. Isso permitirá que o ambiente continue a servir como uma consolidação única e consistente de todas as variáveis comuns nas APIs do Adobe.

   ![testtoken2](assets/configure-io-target-testtoken2.png)

1. Digite para substituir `{{access_token}}` por `{{ACCESS_TOKEN}}`.

   ![token de teste3](assets/configure-io-target-testtoken3.png)

1. Digite para substituir `{{api_key}}` por `{{API_KEY}}`.

   ![testtoken4](assets/configure-io-target-testtoken4.png)

1. Digite para substituir `{{tenant}}` por `{{TENANT_ID}}`. A nota `{{TENANT_ID}}` ainda não foi reconhecida.

   ![testtoken4](assets/configure-io-target-testtoken4a.png)

1. Abra o modal Gerenciar ambientes e selecione seu ambiente.

   ![JWT11](assets/configure-io-target-jwt11.png)

1. Digite para adicionar uma nova variável de ambiente `{{TENANT_ID}}`. Copie e cole seu valor de ID de locatário nos campos **[!UICONTROL INITIAL VALUE]** e **[!UICONTROL CURRENT VALUE]** para sua nova variável de ambiente `TENANT_ID`.

   ![token de teste5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >A ID do Locatário é diferente de seu [!DNL Target] `clientcode`. A ID do Locatário existe na URL quando você está conectado a [!DNL Target]. Para obter sua ID de Locatário, faça logon na Adobe Experience Cloud, abra o [!DNL Target] e clique no cartão de Destino. Use o valor da ID do locatário conforme observado no subdomínio do URL. Por exemplo, se a URL ao fazer logon no [!DNL Adobe Target] for `<https://mycompany.experiencecloud.adobe.com/...>`, sua ID de Locatário será &quot;mycompany&quot;.

1. Envie sua solicitação depois de verificar se você selecionou o ambiente correto. Você deve receber uma resposta contendo sua lista de atividades.

   ![testtoken6](assets/configure-io-target-testtoken6.png)

Agora que você verificou a autenticação de Adobe, é possível usá-la para interagir com as APIs do [!DNL Adobe Target] (bem como com outras APIs de Adobe). Por exemplo, você pode [Usar APIs do Recommendations](recs-api/overview.md) para criar ou gerenciar recomendações, ou pode usá-las com a [API de Entrega do Target](/help/dev/implement/delivery-api/overview.md).
