---
keywords: at.js, 2.0, 1.x, cookies
description: Detalhes sobre como a at.js 2.x e a at.js 1.x lidam com cookies. [!DNL Adobe Target]
title: Cookies do at.js
feature: at.js
exl-id: 154a844a-6855-4af7-8aed-0719b4c389f5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 72%

---

# Cookies do at.js

Informações sobre a at.js 2.x e a at.js 1.*x* comportamento de cookie.

## Comportamento de cookie da at.js 2.x

Para a versão 2.x da at.js (até, mas não incluindo, a versão 2.10.0), *somente os cookies primários são suportados*. Exatamente como no at.js 1.*x*, o cookie próprio, &quot;mbox&quot; está armazenado em `clientdomain.com`, onde `clientdomain` é seu domínio.

O at.js gera uma ID da sessão e a armazena no cookie. A primeira resposta contém informações de atividade, bem como a `TNT` ou`PC ID` gerada pelos [!DNL Target] servidores. O at.js grava o `TNT/PC ID` para o cookie.

O cookie próprio `AMCV_###@AdobeOrg` sempre é definido pelo Serviço de ID de Experience Cloud, embora o `ECID` seja passado em [!DNL Target] solicitações.

>[!NOTE]
>
>Para as versões 2.10.0 e posteriores da at.js, os cookies primários e entre domínios são compatíveis.

### Suporte para cookies de terceiros e rastreamento entre domínios

O rastreamento entre domínios possibilita visualizar sessões em dois sites relacionados, mas com domínios diferentes, como uma única sessão. Você poderia criar [!DNL Target] uma atividade que se expande `siteA.com` e `siteB.com` o visitante permaneceria na mesma experiência ao atravessar domínios. Essa funcionalidade se vincula ao at.js 1.*x* comportamento do cookie próprio e de terceiros.

>[!NOTE]
>
>Para as versões 2.10.0 e posteriores da at.js, há suporte para cookies de terceiros e rastreamento entre domínios.


## at.js 1.Comportamento de cookie *x*

Para versões do at.js 1.*x*, o comportamento de cookie depende de se é um cookie próprio, um cookie de terceiros com um cookie próprio ou um cookie de terceiros.

### Quando utilizar cookies próprios ou de terceiros

A configuração do site determina quais cookies você deseja utilizar. É útil entender como o [!DNL Target] funciona ao tentar entender cookies próprios e de terceiros. Consulte [Como [!DNL Adobe Target] funciona](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) para obter mais informações.

Há três casos de uso principais de cookies:

1. Um domínio.

   Todos os seus testes serão feitos no domínio de primeiro nível (`www.domain.com`, `store.domain.com`, `anysub.domain.com`, etc.).

   Utilize somente cookies próprios. Esse é o padrão.

1. Os usuários navegam entre domínios e você deseja rastrear e testar seu comportamento nesses domínios.

   Exemplo: Um usuário acessa o seu site para efetuar uma compra, mas faz o pagamento utilizando a loja do Yahoo. Três abordagens (consulte seu representante de contas para determinar a melhor abordagem):

   * Habilitar cookies próprios e de terceiros.
   * Habilitar somente cookies de terceiros (muito raro, mas tem a vantagem de manter o cookie do at.js fora de seu domínio).
   * Permitir apenas cookies próprios e enviar o parâmetro `mboxSession` ao atravessar domínios.

     O parâmetro `mboxSession` deve ser enviado para uma página inicial com uma referência ao at.js. Uma página intermediária de redirecionador não pode ser utilizada.

1. Você está utilizando apenas adboxes ou Flashboxes em um site de terceiros.

   Duas abordagens (consulte seu gerente de serviços ao cliente para determinar a melhor abordagem):

   * Habilitar cookies próprios e de terceiros.

     Cookies próprios e de terceiros são necessários para Flashbox e anúncios dinâmicos.

   * Habilitar somente cookies de terceiros.

     Essa abordagem é apenas para casos raros em que as implementações AdBox são usadas sem definição de metas no site.

### Comportamento do cookie próprio

O cookie próprio é armazenado em `clientdomain.com`, onde `clientdomain` é o seu domínio.

O at.js gera um `mboxSession ID` e o armazena no cookie. A primeira resposta contém a oferta, assim como o JavaScript, para armazenar o `mboxPC ID` gerado pelo aplicativo, no cookie.

>[!NOTE]
>
>O cookie próprio `AMCV_###@AdobeOrg` sempre é definido com a ID do visitante do Experience Cloud.

### Comportamento de cookie de terceiros

O cookie de terceiros é armazenado em `clientcode.tt.omtrdc.net` e o cookie próprio é armazenado em `clientdomain.com`, onde `clientdomain` é o seu domínio.

O at.js gera um `mboxSession ID`. A primeira solicitação de local retorna cabeçalhos HTTP de resposta que tentam instalar cookies de terceiros chamados `mboxSession` e `mboxPC`. Uma solicitação de redirecionamento é enviada de volta com um parâmetro extra (`mboxXDomainCheck=true`).

Se o navegador aceitar cookies de terceiros, a solicitação de redirecionamento vai inclui-los, e a oferta será retornada.

Se o navegador rejeita cookies de terceiros, a solicitação de redirecionamento não vai inclui-los, e o conteúdo padrão será exibido em todos os locais da página. Como não existem cookies definidos, o mesmo processo descrito acima é repetido em cada solicitação de página.

### Comportamento do cookie próprio e de terceiros

O cookie de terceiros é armazenado em `clientcode.tt.omtrdc.net` e o cookie próprio é armazenado em `clientdomain.com`, onde `clientdomain` é o seu domínio.

O at.js gera um `mboxSession ID`. A primeira solicitação de local retorna cabeçalhos HTTP de resposta que tentam instalar cookies de terceiros chamados `mboxSession` e `mboxPC`. Uma solicitação de redirecionamento é enviada de volta com um parâmetro extra (`mboxXDomainCheck=true`).

Se o navegador aceitar cookies de terceiros, a solicitação de redirecionamento vai inclui-los, e a oferta será retornada.

Alguns navegadores rejeitam cookies de terceiros. Se o cookie de terceiros for bloqueado, o cookie próprio ainda funcionará. [!DNL Target]O tenta instalar o cookie de terceiros e, caso não seja possível, [!DNL Target] poderá somente rastrear o domínio específico do cliente. O rastreamento de domínio cruzado não funciona se o terceiro estiver bloqueado, a menos que o `mboxSession` esteja anexado no link que cruza domínios. Nesse caso, outro cookie próprio é instalado e sincronizado com o cookie próprio do domínio anterior.

## Configurações de cookie

O cookie possui várias configurações padrão. Você pode alterar essas configurações, se necessário, exceto a duração do cookie. Entre em contato com seu representante de contas ao modificar as configurações de cookie.

| Configuração | Informações |
|--- |--- |
| Nome do cookie | mbox. |
| Domínio do cookie | Domínio de primeiro e segundo nível a partir de onde o conteúdo será disponibilizado. O cookie é sempre um cookie próprio porque é disponibilizado pelo domínio de sua companhia. Exemplo: `mycompany.com`. |
| Domínio do servidor | `clientcode.tt.omtrdc.net`, utilizando o código de cliente de sua conta. |
| Duração do cookie | O cookie permanece no navegador do visitante por dois anos a partir de seu último logon.<P>A configuração `deviceIdLifetime` pode ser substituída na [at.js versão 2.3.1 ou posterior](../atjs/target-atjs-versions.md). Para obter mais informações, consulte [targetGlobalSettings()](../../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md). |
| Política P3P | O cookie é publicado com a política P3P, conforme requerido pela configuração padrão na maioria dos navegadores. Uma política P3P indica ao navegador quem está disponibilizando o cookie e como as informações serão utilizadas. |

O cookie mantém uma série de valores para gerenciar a experiência de seus visitantes nas campanhas:

| Valor | Definição |
|--- |--- |
| session ID | ID único para a sessão do usuário. A duração padrão é de 30 minutos. |
| pc ID | Um ID temporário para o navegador do visitante. Dura 14 dias. |
| check | Um simples valor de teste utilizado para determinar se o navegador do visitante tem suporte a cookies. Definido sempre que o usuário solicita uma página. |
| disable | Configurado se o tempo de carga do visitante exceder o tempo limite configurado no SDK da Web da Adobe Experience Platform ou no arquivo at.js. A duração padrão é de uma hora. |

## Impacto em [!DNL Target] para visitantes do Safari devido a alterações no rastreamento do Apple WebKit

Lembre-se do seguinte:

### Como funciona o Rastreamento do [!DNL Adobe Target]?

| Cookies | Detalhes |
|--- |--- |
| Domínios próprios | Esta é a implementação padrão para [!DNL Target] clientes.  Os cookies &quot;mbox&quot; são definidos no domínio do cliente. |
| Rastreamento de terceiros | O rastreamento de terceiros é importante para anunciar e segmentar casos de uso em [!DNL Target] e em [!DNL Adobe Audience Manager] (AAM).  O rastreamento de terceiros requer técnicas de script entre sites.  [!DNL Target] usa dois cookies, &quot;mboxSession&quot; e &quot;mboxPC&quot; configurados no domínio `clientcode.tt.omtrd.net`. |

### Qual é a abordagem da Apple?

Da Apple:

&quot;A Intelligent Tracking Prevention é um novo recurso do WebKit que reduz o rastreamento entre sites, limitando ainda mais os cookies e outros dados do site&quot;.

&quot;Isso é chamado de rastreamento entre sites e o cookie usado por `example-tracker.com` é chamado de cookie de terceiros. Em nossos testes, encontramos sites populares com mais de 70 desses rastreadores, todos coletando dados em silêncio sobre os usuários&quot;.

| Abordagem | Detalhes |
|--- |--- |
| Intelligent tracking prevention (Prevenção inteligente de rastreamento) | Para obter mais informações, consulte [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) no site WebKit Open Source Web Browser Engine. |
| Cookies | Como o Safari gerencia cookies:<ul><li>Cookies de terceiros que não estão em um domínio que o usuário acessa diretamente nunca são salvos. Esse comportamento não é novo. Cookies de terceiros já não são suportados no Safari.</li><li>Cookies de terceiros definidos em um domínio que o usuário acessa diretamente são removidos após 24 horas.</li><li>Os cookies próprios são removidos após 30 dias se o domínio próprio for classificado como rastreamento de usuários em todos os sites. Esse problema pode se aplicar a grandes empresas que enviam usuários para domínios diferentes online. A Apple não deixou claro como exatamente esses domínios serão classificados, ou como um domínio pode determinar se eles foram classificados como usuários de rastreamento entre sites.</li></ul> |
| Aprendizagem de máquina para identificar domínios que estão em todos os sites | Da Apple:<P>Classificador de aprendizagem de máquina: um modelo de aprendizagem de máquina é usado para classificar os principais domínios controlados de forma privada que podem controlar o usuário em todos os sites, com base nas estatísticas coletadas. Das várias estatísticas coletadas, três vetores mostraram forte sinal de classificação com base nas práticas de rastreamento atuais: sub-origem em número de domínios únicos, subestrutura em número de domínios únicos e número de domínios únicos redirecionados. Toda a coleta e classificação de dados acontece no dispositivo.<P>No entanto, se o usuário interagir com example.com como o domínio principal, geralmente chamado de domínio próprio, a Intelligent Tracking Prevention considera um sinal de que o usuário está interessado no site e ajusta temporariamente seu comportamento, conforme demonstrado na linha do tempo:<P>Se o usuário interagiu com example.com nas últimas 24 horas, seus cookies estarão disponíveis quando `example.com` for um terceiro. Isso permite cenários de login &quot;Fazer login com minha conta X em Y&quot;.<ul><li>Os domínios visitados como domínio de nível superior não serão afetados. Sites como o OKTA, por exemplo</li><li>Identifica domínios que são subdomínios ou subquadros da página atual em vários domínios exclusivos.</li></ul> |

### Como a Adobe será afetada?

| Funcionalidade afetada | Detalhes |
|--- |--- |
| Suporte para cancelamento | As alterações de rastreamento do WebKit da Apple interrompem o suporte ao cancelamento.<P>A opção de não participação de [!DNL Target] usa um cookie no domínio `clientcode.tt.omtrdc.net`. Para obter mais detalhes, consulte [Privacidade](/help/dev/before-implement/privacy/privacy.md).<P>[!DNL Target] aceita dois cancelamentos:<ul><li>Um por cliente (o cliente gerencia o link para opção de não participação).</li><li>Um via Adobe que exclui o usuário de todas as funcionalidades do [!DNL Target] para todos os clientes.</li></ul>Ambos os métodos usam o cookie de terceiros. |
| [!DNL Target] atividades | Os clientes podem escolher sua [duração do perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) para suas contas do [!DNL Target]: até 90 dias. A preocupação é que, se a duração do perfil da conta for superior a 30 dias, e o cookie próprio for limpo porque o domínio do cliente foi marcado como usuários de rastreamento entre sites, o comportamento dos visitantes do Safari será afetado nas seguintes áreas em [!DNL Target]:<P>**[!DNL Target]Relatórios**: se um usuário do Safari entrar em uma atividade, retornar após 30 dias e depois se converter, esse usuário contará como dois visitantes e uma conversão.<P>Esse comportamento é o mesmo para atividades que usam [!DNL Analytics] como fonte de relatórios (A4T).<P>**Associação de Perfil e Atividade**:<ul><li>Dados do perfil são apagados quando o cookie próprio expira.</li><li>Associação de atividade é apagada quando o cookie próprio expira.</li><li> [!DNL Target] não funciona no Safari para contas que usam uma implementação de cookies de terceiros ou uma implementação de cookies próprios e de terceiros. Observe que esse comportamento não é novo. O Safari não permite cookies de terceiros por algum tempo.</li></ul><P>**Sugestões**: se houver uma preocupação de que o domínio do cliente possa ser marcado como uma sessão cruzada de visitantes de rastreamento, é mais seguro definir a duração do perfil para 30 dias ou menos em [!DNL Target]. Isso garante que os usuários sejam rastreados de forma semelhante no Safari e em todos os outros navegadores. |
