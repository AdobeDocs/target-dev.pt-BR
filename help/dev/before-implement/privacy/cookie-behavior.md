---
keywords: Visão geral e referência, webkit, cookies, primários, de terceiros, primários, de terceiros,
description: Saiba mais sobre [!DNL Target] comportamento do cookie (cookie próprio, cookie de terceiros com cookie próprio ou cookie de terceiros sozinho).
title: Onde posso encontrar informações sobre [!DNL Target] Cookies?
feature: at.js
exl-id: d44e02ce-8920-4130-bcad-699ca77c0dad
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 57%

---

# [!DNL Target] cookies

O comportamento de cookies depende do tipo do cookie, podendo ser um cookie próprio, um cookie de terceiros com um cookie próprio ou somente um cookie de terceiros.

>[!NOTE]
>
>Para obter informações detalhadas sobre os diferentes cookies usados pelo [!DNL Target], consulte [[!DNL Adobe Target] cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-target.html?lang=pt-BR){target=_blank} no *Guia de componentes da interface central do Experience Cloud*.
>
>Este tópico contém informações sobre `mboxSession` e `mboxPC`. As práticas recomendadas de implementação recomendam que você não vincule nem armazene informações confidenciais com os dados do cookie: `mboxSession` ou `mboxPC`.

Consulte também [Exclua o [!DNL Target] cookie](cookie-deleting.md).

## Quando utilizar cookies próprios ou de terceiros

A configuração do site determina quais cookies você deseja utilizar. É útil compreender como [!DNL Target] O funciona ao tentar entender cookies próprios e de terceiros. Consulte [Como [!DNL Adobe] [!DNL Target] Works](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) para obter mais informações.

Há três casos de uso principais de cookies:

1. Um domínio.

   Todos os seus testes ocorrem em um domínio de nível superior (`www.domain.com`, `store.domain.com`, `anysub.domain.com`e assim por diante).

   Abordagem: usar somente cookies primários (o padrão).

1. Os usuários navegam entre domínios e você deseja rastrear e testar seu comportamento nesses domínios.

   Exemplo: Um usuário acessa o seu site para efetuar uma compra, mas faz o pagamento utilizando a loja do Yahoo. Três abordagens (consulte seu representante de contas para determinar a melhor abordagem):

   * Habilitar cookies próprios e de terceiros.
   * Habilitar somente cookies de terceiros (raro, mas tem a vantagem de manter o cookie da mbox fora do seu domínio).
   * Permitir apenas cookies próprios e enviar o parâmetro `mboxSession` ao atravessar domínios.

     A variável `mboxSession` deve ser enviado para uma página inicial e referenciado da biblioteca do JavaScript (Adobe Experience Platform Web SDK ou at.js). Uma página intermediária de redirecionador não pode ser utilizada.

1. Você somente está utilizando adboxes ou Flashboxes em um site de terceiros.

   Duas abordagens (consulte seu representante de conta para determinar a melhor abordagem):

   * Habilitar cookies próprios e de terceiros.

     Cookies próprios e de terceiros são requeridos pelo Flashbox e anúncios dinâmicos.

   * Habilitar somente cookies de terceiros.

     Essa abordagem é apenas para casos raros em que as implementações AdBox são usadas sem definição de metas no site.

## Comportamento do cookie próprio

O cookie próprio é armazenado em clientdomain.com, onde `clientdomain` é o seu domínio.

A biblioteca do JavaScript gera um `mboxSession ID` e o armazena no [!DNL Target] cookie. A primeira resposta de mbox contém a oferta e o JavaScript armazena a variável `mboxPC ID` gerado pelo aplicativo, no cookie da mbox.

>[!NOTE]
>
>O cookie próprio AMCV_###@AdobeOrg sempre é definido com a ID de visitante do Experience Cloud.

## Comportamento de cookie de terceiros

O cookie de terceiros é armazenado em clientcode.tt.omtrdc.net e o cookie próprio é armazenado em clientdomain.com, onde `clientdomain` é o seu domínio.

A biblioteca do JavaScript gera um `mboxSession ID`. A primeira solicitação de local retorna cabeçalhos HTTP de resposta que tentam instalar cookies de terceiros chamados `mboxSession` e `mboxPC`. Uma solicitação de redirecionamento é enviada de volta com um parâmetro extra (`mboxXDomainCheck=true`).

Se o navegador aceitar cookies de terceiros, a solicitação de redirecionamento vai inclui-los, e a oferta será retornada.

Se o navegador rejeita cookies de terceiros, a solicitação de redirecionamento não vai inclui-los, e o conteúdo padrão será exibido em todos os locais da página. Como não existem cookies definidos, o mesmo processo descrito acima é repetido em cada solicitação de página.

>[!NOTE]
>
>O cookie demdex.net será configurado se os cookies de terceiros não estiverem bloqueados.

## Comportamento do cookie próprio e de terceiros

O cookie de terceiros é armazenado em clientcode.tt.omtrdc.net e o cookie próprio é armazenado em clientdomain.com, onde `clientdomain` é o seu domínio.

A biblioteca do JavaScript gera um `mboxSession ID`. A primeira solicitação de local retorna cabeçalhos HTTP de resposta que tentam instalar cookies de terceiros chamados `mboxSession` e `mboxPC`. Uma solicitação de redirecionamento é enviada de volta com um parâmetro extra (`mboxXDomainCheck=true`).

Se o navegador aceitar cookies de terceiros, a solicitação de redirecionamento vai inclui-los, e a oferta será retornada.

Alguns navegadores rejeitam cookies de terceiros. Se o cookie de terceiros for bloqueado, o cookie próprio ainda funcionará. [!DNL Target]O tenta instalar o cookie de terceiros e, caso não seja possível, [!DNL Target] poderá somente rastrear o domínio específico do cliente. O rastreamento entre domínios não funciona se o cookie de terceiros estiver bloqueado, a menos que a variável `mboxSession` está anexado no link que cruza domínios. Nesse caso, outro cookie próprio é instalado e sincronizado com o cookie próprio do domínio anterior.

## Configurações de cookie

O cookie possui várias configurações padrão. Você pode alterar essas configurações, se necessário, exceto a duração do cookie. Entre em contato com seu representante de contas ao modificar as configurações de cookie.

| Configuração | Informações |
|--- |--- |
| Nome do cookie | mbox. |
| Domínio do cookie | Domínio de primeiro e segundo nível a partir de onde o conteúdo será disponibilizado. Como é disponibilizado pelo domínio de sua empresa, o cookie é um cookie próprio.<br />Exemplo: `mycompany.com`. |
| Domínio do servidor | `clientcode.tt.omtrdc.net`, utilizando o código de cliente de sua conta. |
| Duração do cookie | O cookie permanece no navegador do visitante por duas semanas a partir do último logon. Não é possível alterar a duração do cookie. |
| Política P3P | O cookie é publicado com a política P3P, conforme requerido pela configuração padrão na maioria dos navegadores. Uma política P3P indica a um navegador que está disponibilizando o cookie e como as informações são usadas. |

O cookie mantém vários valores para gerenciar a experiência dos visitantes nas campanhas:

| Valor | Definição |
|--- |--- |
| session ID | ID único para a sessão do usuário. Por padrão, essa ID dura 30 minutos. |
| pc ID | Um ID temporário para o navegador do visitante. Dura 14 dias. |
| check | Um simples valor de teste utilizado para determinar se o navegador do visitante tem suporte a cookies. Definido sempre que o usuário solicita uma página. |
| disable | Configurado se o tempo de carga do visitante ultrapassar o tempo limite configurado no arquivo da biblioteca JavaScript. Por padrão, esse valor dura uma hora. |

## Impacto em [!DNL Target] para visitantes do Safari devido a alterações no rastreamento do Apple WebKit

**Como o [!DNL Target] trabalho de rastreamento?**

| Cookies | Detalhes |
|--- |--- |
| Domínios próprios | A implementação padrão para [!DNL Target] clientes. Os cookies &quot;mbox&quot; são definidos no domínio do cliente. |
| Rastreamento de terceiros | O rastreamento de terceiros é importante para anunciar e segmentar casos de uso no [!DNL Target] e no [!DNL Adobe Audience Manager] (AAM) O rastreamento de terceiros requer técnicas de script entre sites. [!DNL Target]O usa dois cookies, &quot;mboxSession&quot; e &quot;mboxPC&quot; configurados no domínio `clientcode.tt.omtrd.net`. |
**Qual é a abordagem da Apple?**

Da Apple:

&quot;A Intelligent Tracking Prevention é um novo recurso do WebKit que reduz o rastreamento entre sites, limitando ainda mais os cookies e outros dados do site&quot;.

&quot;Isso é chamado de rastreamento entre sites e o cookie usado por `example-tracker.com` é chamado de cookie de terceiros. Em nossos testes, encontramos sites populares com mais de 70 desses rastreadores, todos coletando dados em silêncio sobre os usuários&quot;.

| Abordagem | Detalhes |
|--- |--- |
| Intelligent tracking prevention (Prevenção inteligente de rastreamento) | Para obter mais informações, consulte [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) no site WebKit Open Source Web Browser Engine. |
| Cookies | Como o Safari gerencia cookies:<ul><li>Cookies de terceiros que não estão em um domínio que o usuário acessa diretamente nunca são salvos. Esse comportamento não é novo. Cookies de terceiros já não são suportados no Safari.</li><li>Cookies de terceiros definidos em um domínio que o usuário acessa diretamente são removidos após 24 horas.</li><li>Os cookies próprios são removidos após 30 dias se o domínio próprio for classificado como rastreamento de usuários em todos os sites. Esse problema pode se aplicar a grandes empresas que enviam usuários para domínios diferentes online. A Apple não deixou claro como exatamente esses domínios são classificados ou como um domínio pode determinar se foram classificados como usuários de rastreamento entre sites.</li></ul> |
| Aprendizagem de máquina para identificar domínios que estão em todos os sites | Da Apple:<br />Classificador de aprendizagem de máquina: um modelo de aprendizagem de máquina é usado para classificar os principais domínios controlados de forma privada que podem controlar o usuário em todos os sites, com base nas estatísticas coletadas. Das várias estatísticas coletadas, três vetores mostraram forte sinal de classificação com base nas práticas de rastreamento atuais: sub-origem em número de domínios únicos, subestrutura em número de domínios únicos e número de domínios únicos redirecionados. Toda a coleta e classificação de dados acontece no dispositivo.<br />No entanto, se o usuário interagir com `example.com` como o domínio principal, geralmente chamado de domínio próprio, a Intelligent Tracking Prevention considera um sinal de que o usuário está interessado no site e ajusta temporariamente seu comportamento, conforme demonstrado na linha do tempo:<br />Se o usuário interagiu com `example.com` nas últimas 24 horas, os cookies estarão disponíveis quando `example.com` O é um terceiro. Esta prática permite cenários de login &quot;Fazer login com minha conta X em Y&quot;.<ul><li>Os domínios visitados como domínio de nível superior não são afetados. Sites como o OKTA, por exemplo</li><li>Identifica domínios que são subdomínios ou subestruturas da página atual em vários domínios únicos.</li></ul> |

**Como o [!DNL Adobe] afetado?**

| Funcionalidade afetada | Detalhes |
|--- |--- |
| Suporte para cancelamento | As alterações de rastreamento do WebKit da Apple interrompem o suporte ao cancelamento.<br />O cancelamento do Target usa um cookie no domínio `clientcode.tt.omtrdc.net`. Para obter mais detalhes, consulte [Privacidade](privacy.md).<br />O Target suporta dois cancelamentos:<ul><li>Um por cliente (o cliente gerencia o link para opção de não participação).</li><li>Um via [!DNL Adobe] que recusa o usuário de todos [!DNL Target] funcionalidade para todos os clientes.</li></ul>Ambos os métodos usam o cookie de terceiros. |
| Atividades do Target | Os clientes podem escolher seus  [duração do perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) para seus [!DNL Target] contas (até 90 dias). A preocupação é que, se a duração do perfil da conta for superior a 30 dias, e o cookie próprio for limpo porque o domínio do cliente foi marcado como usuários de rastreamento entre sites, o comportamento dos visitantes do Safari será afetado nas seguintes áreas no Target:<br />**Relatórios do Target**: se um usuário do Safari entrar em uma atividade, retornar após 30 dias e depois se converter, ele será contado como dois visitantes e uma conversão.<br />Esse comportamento é o mesmo para atividades que usam o Analytics como fonte de geração de relatórios (A4T).<br />**Associação de perfil e atividade**:<ul><li>Dados do perfil são apagados quando o cookie próprio expira.</li><li>Associação de atividade é apagada quando o cookie próprio expira.</li><li> [!DNL Target]O não funciona no Safari para contas que usam uma implementação de cookies de terceiros ou uma implementação de cookies próprios e de terceiros. Esse comportamento não é novo. O Safari não permite cookies de terceiros por um tempo.</li></ul><br />**Sugestões**: se houver uma preocupação de que o domínio do cliente possa ser marcado como uma sessão cruzada de visitantes de rastreamento, é mais seguro definir a duração do perfil para 30 dias ou menos no Target. Esse limite garante que os usuários sejam rastreados de forma semelhante no Safari e em todos os outros navegadores. |
