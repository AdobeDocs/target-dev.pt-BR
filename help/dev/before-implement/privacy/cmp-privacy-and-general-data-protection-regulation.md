---
keywords: gdpr, eu, união europeia, privacidade, perguntas frequentes, perguntas frequentes, california consumer privacy act, ccpa, privacidade, proteção de dados, opt-out, opt-out, governo, regulation, gdpr5, gdpr6, gdpr7, gdpr9, eu0, eu1, eu2, eu3, eu4, eu5
description: Saiba mais sobre o Target e o Regulamento Geral sobre a Proteção de Dados da União Europeia (GDPR), a Lei de Privacidade do Consumidor da Califórnia (CCPA) e outros requisitos de privacidade.
title: Como o Target lida com privacidade e regulamentos de proteção de dados?
feature: Privacy & Security
exl-id: 40bac3c5-8e6f-4a90-ac0c-eddce1dbe6c0
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '2329'
ht-degree: 62%

---

# Privacidade e regulamentos sobre proteção de dados

Informações sobre o Regulamento Geral de Proteção de Dados da União Europeia (RGPD), a Lei de Privacidade do Consumidor da Califórnia (CCPA) e outros requisitos internacionais de privacidade. Saiba como esses regulamentos afetam sua organização e a Adobe Target.

## Visão geral de Privacidade e Regulamento Geral sobre a Proteção de Dados (RGPD) 

O RGPD da União Europeia entra em vigor em 25 de maio de 2018. Para obter mais informações sobre o que este regulamento significa para você, consulte [RGPD e seus negócios](https://business.adobe.com/pt/privacy/general-data-protection-regulation.html).

Quando a Adobe oferece software e serviços para uma empresa, ela age como um Processador de dados de quaisquer dados pessoais que processa e armazena como parte do oferecimento desses serviços. Como Processador de dados, a Adobe processa dados pessoais de acordo com a permissão e as instruções de sua empresa (por exemplo, como definido em seu contrato com a Adobe).

Como o Controlador de dados, você determinará os dados pessoais que a Adobe processa e armazena em seu nome. Se você usa as soluções da Adobe Experience Cloud, a Adobe pode hospedar dados pessoais, dependendo das soluções usadas e das informações que você escolher enviar para a sua conta da Adobe Experience Cloud. Para obter uma lista detalhada de exemplos, consulte [Privacidade na Adobe Experience Cloud](https://www.adobe.com/pt/privacy/experience-cloud.html#collect).

O Adobe Experience Cloud fornece APIs prontas para o GDPR para controladores de dados que permitem que eles concluam as seguintes tarefas:

* Acessar informações do titular de dados armazenadas no Target
* Excluir informações do titular de dados armazenadas no Target

Para obter mais informações, consulte:

* [visão geral do Adobe Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=pt-BR)
* [Guia de API do Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/api/overview.html?lang=pt-BR)
* [Visão geral da interface do Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=pt-BR)

## Visão geral da California Consumer Privacy Act (CCPA)

A lei California Consumer Privacy Act (CCPA) concede aos consumidores da Califórnia novos direitos sobre suas informações pessoais e impõe responsabilidades de proteção de dados em determinadas entidades que fazem negócios na Califórnia. A CCPA entrou em vigor em 1º de janeiro de 2020.

Em um nível superior, a lei concede aos cidadãos da Califórnia vários direitos cruciais, incluindo o seguinte:

* Solicitar informações (acesso a dados)
* Recusar a venda de informações pessoais (um direito definido amplamente para recusar o compartilhamento de informações com terceiros)
* Excluir informações pessoais
* Ser informado que as informações pessoais estão sendo divulgadas ou vendidas

Se você estava ocupado se preparando para a lei de privacidade da Europa (GDPR) no ano passado, alguns desses direitos podem ser familiares e muito do trabalho que você fez pode ser reaproveitado.

>[!NOTE]
>
>O acesso e a exclusão de dados conforme se aplicam à CCPA seguem o mesmo processo para o RGPD.

## Aceitação do Adobe Target e do Adobe Experience Platform

O Target oferece suporte à funcionalidade de aceitação por meio de tags na Adobe Experience Platform, para ajudar a apoiar a estratégia de gerenciamento de consentimento. A funcionalidade de inclusão permite que os clientes controlem como e quando a tag do Target é acionada. Também há uma opção por meio do Adobe Experience Platform para pré-aprovar a tag do Target. Para habilitar a capacidade de usar a aceitação na biblioteca at.js do Target, você deve usar `targetGlobalSettings` e adicionar a configuração `optinEnabled=true`. No Adobe Experience Platform, selecione &quot;ativar&quot; na lista suspensa Aceitação de GDPR, na exibição de instalação da extensão. Consulte [Implementar o Target usando o Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) para obter mais detalhes.

O trecho de código a seguir mostra como habilitar a configuração `optinEnabled=true`:

```
window.targetGlobalSettings = {
  optinEnabled: true
};
```

>[!NOTE]
>
>A funcionalidade de Opt-in é compatível com o at.js versão 1.7.0 e o at.js 2.1.0 ou posterior. O Opt-in não é compatível com o at.js versões 2.0.0 e 2.0.1.

O uso do Adobe Experience Platform para gerenciar o opt-in é a abordagem recomendada. Existe ainda mais controle granular no Adobe Experience Platform para ocultar elementos selecionados da sua página, antes do acionamento do Target, que pode ser útil como parte de sua estratégia de consentimento.

Há três cenários a serem considerados ao usar a inclusão:

1. **A marca do Destino é pré-aprovada por meio da Adobe Experience Platform (ou pelo titular dos dados que aprovou o Destino anteriormente):** A marca do Destino não é mantida para consentimento e funciona conforme esperado.
1. **A tag do Target NÃO é pré-aprovada e `bodyHidingEnabled` é FALSE:** A tag do Target é acionada somente após o consentimento ser coletado do cliente. Antes de o consentimento ser coletado, apenas o conteúdo padrão está disponível. Após o recebimento do consentimento, o Target é chamado e o conteúdo personalizado fica disponível para o titular dos dados (visitante). Como apenas o conteúdo padrão está disponível antes do consentimento, é importante utilizar uma estratégia apropriada, como uma página inicial que cubra qualquer parte da página ou conteúdo que possa ser personalizado. Esse processo garante que a experiência permaneça consistente para o titular dos dados (visitante).
1. **A tag do Target NÃO é pré-aprovada e `bodyHidingEnabled` é TRUE:** A tag do Target é acionada somente após o consentimento ser coletado do cliente. Antes de o consentimento ser coletado, apenas o conteúdo padrão está disponível. No entanto, como `bodyHidingEnabled` é definido para verdadeiro, `bodyHiddenStyle` determina qual conteúdo na página fica oculto até que a tag do Target seja acionada (ou o titular dos dados recuse a inclusão, sendo que nesse caso o conteúdo padrão é exibido). Por padrão, o `bodyHiddenStyle` está configurado como `body { opacity:0;}`, o que oculta a tag do corpo HTML. A configuração de página recomendada da Adobe é apresentada abaixo para que todo o corpo da página, além da caixa de diálogo do gerenciador de consentimento, fique oculto, colocando o conteúdo da página em um contêiner e o diálogo do gerenciador de consentimento em um contêiner separado. Essa configuração define o Target para que ele apenas oculte o contêiner de conteúdo da página. Consulte a [Visão geral do Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?).

   A configuração de página recomendada para o cenário 3 é:

   ```
   <html> 
   <head> 
   //visitor, at.js 
   </head> 
   
   <body> 
   <div id = "consentManagerDialog"> 
   
   //consent manager html dialog goes here 
   </div> 
   
   <div id="pageContent"> 
   // page content goes here 
   </div> 
   
   </body> 
   </html> 
   ```

   Considerando o `bodyHiddenStyle` de:

   ```
   #pageContent { opacity:0;}
   ```

## Perguntas frequentes sobre privacidade e regulamentos sobre proteção de dados FAQ

Perguntas frequentes sobre o Regulamento Geral sobre a Proteção de Dados (RGPD) da União Europeia, a California Consumer Privacy Act (CCPA) e outros requisitos de privacidade internacionais específicos para o Target.

### Qual é a política da Adobe para esses regulamentos?

A Adobe já atende às obrigações como um Processador de dados ou está fazendo implementações de acordo. A Adobe tem uma base sólida de controles de segurança e privacidade certificados por design e fez melhorias no produto antes do prazo final de maio de 2018. Clientes empresariais têm a responsabilidade de implementar essas melhorias, além de atualizar quaisquer políticas e procedimentos necessários.

### Minha empresa, o Controlador de dados, precisará enviar uma solicitação do GDPR ou da CCPA para cada solução da Adobe Experience Cloud usada?

Não, a Adobe oferece uma maneira central para ajudar Controladores de dados a atender aos requisitos do GDPR e da CCPA. Os Controladores de dados não precisam acessar diretamente cada solução.

Todas as solicitações do GDPR e da CCPA nas soluções da Experience Cloud, incluindo o Target, são feitas por meio de uma API central da Adobe, atualmente denominada API do GDPR. A API conclui a solicitação no conjunto de soluções da Experience Cloud do Controlador de dados.

### Quais informações a Adobe permite que os clientes excluam em resposta a uma solicitação do usuário/titular dos dados?

As informações relacionadas a um visitante individual dentro do Target são contidas no Perfil de visitante do Target. O Target permite que os clientes excluam todos os dados associados a uma ID em seus respectivos Perfis do visitante. Para obter exemplos dos dados de perfil armazenados pelo Target, consulte [Perfil do Visitante](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html).

Dados agregados ou anônimos (por exemplo, dados de relatórios) não usados para identificar uma certa pessoa, ou dados não relevantes a um pessoa específico (por exemplo, dados de conteúdo), não estão no escopo de uma solicitação de exclusão de usuário.

Por padrão, os perfis do visitante do Target que ficaram inativos por 90 dias são excluídos, sem nenhuma ação necessária.

### Quais IDs são compatíveis para ajudar os clientes a concluírem uma solicitação de acesso e exclusão do GDPR ou da CCPA para o Target?

O Target é compatível com os seguintes tipos de ID para localizar um perfil de cliente:

| ID de usuário | Tipo de ID de namespace | ID de namespace | Definição |
|--- |--- |--- |--- |
| Experience Cloud ID (ECID) | Padrão | 4 | Adobe Experience Cloud ID, anteriormente conhecida como ID de visitante ou Experience Cloud ID. É possível usar a API do JavaScript para localizar esta ID (veja os detalhes abaixo). |
| ID TnT / ID de cookie(TNTID) | Padrão | 9 | Identificador de direcionamento definido como cookie no navegador do visitante. É possível usar a API do JavaScript para localizar esta ID (veja os detalhes abaixo). |
| ID de terceiros / ID de CRM (THIRDPARTYID) | Específico do Target | N/A | Se você fornecer seu CRM ao Target ou qualquer outra informação de identificador exclusivo referente a seus clientes. |

>[!NOTE]
>
>Embora o Target seja compatível com cookies próprios e de terceiros entre domínios, apenas cookies próprios do Target são recomendados para o GDPR e para a CCPA.

### Como o Target aborda a administração de consentimento?

O RGPD e a CCPA não alteram quando é necessário obter consentimento, mas como obtê-lo. A estratégia de consentimento de cada cliente depende de sua coleta de dados e práticas de uso, bem como da política de privacidade. O gerenciamento do consentimento não é compatível com o Target e não deve ser obtido por meio dele para GDPR e CCPA.

No momento, a Adobe não oferece uma solução de Administração de consentimento, mas há várias ferramentas em desenvolvimento no mercado para atender a alguns dos novos requisitos. Para obter mais informações sobre as ferramentas de privacidade em geral, incluindo gerenciadores de consentimento, consulte o [Relatório de fornecedores de tecnologia de privacidade de 2017](https://iapp.org/media/pdf/resource_center/Tech-Vendor-Directory-1.4.1-electronic.pdf) no site da *International Association of Privacy Professionals (iapp)*.

O Target oferece suporte a funcionalidade de aceitação por meio do Adobe Experience Platform, para apoiar a sua estratégia de gerenciamento de consentimento. A funcionalidade de inclusão permite que os clientes controlem como e quando a tag do Target é acionada. Também há uma opção por meio do Adobe Experience Platform para pré-aprovar a tag do Target. O uso do Adobe Experience Platform para gerenciar o opt-in é a abordagem recomendada. Existe ainda mais controle granular no Adobe Experience Platform para ocultar elementos selecionados da sua página, antes do acionamento do Target, que pode ser útil como parte de sua estratégia de consentimento.

Para obter mais informações sobre GDPR, CCPA e Adobe Experience Platform, consulte [A Biblioteca JavaScript de Privacidade da Adobe e GDPR](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?). Além disso, consulte a seção *Aceitação do Adobe Target e da Adobe Experience Platform* acima.

### O `AdobePrivacy.js` envia informações para a API do RGPD?

O AdobePrivacy.js *não* envia essas informações para a API. Isso deve ser feito pelo cliente. Esta biblioteca fornece apenas as IDs armazenadas no navegador para esse visitante específico.

### O que é removido por `removeIdentities`?

`removeIdentities`O *remove somente* essas identidades do navegador, e depende apenas se a solução da Adobe implementou isso.

Por exemplo, o Target exclui os cookies que armazenam suas IDs, mas o Adobe Audience Manager (AAM) não exclui a ID do demdex armazenada em um cookie de terceiros.

### Quais informações precisam ser incluídas em uma solicitação do GDPR e da CCPA do Target?

Além dos requisitos do Privacy Service central, uma mensagem válida do GDPR ou da CCPA para o Target contém:

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            "namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            "namespace":"TNTID", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"THIRDPARTYID", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
}
```

### Que tipos de respostas posso esperar do Target por meio da API do RGPD? 

| Status da solicitação | Mensagem de resposta do Target | Cenário |
|--- |--- |--- |
| Processamento | Processamento | O Target recebeu a solicitação do RGPD ou da CCPA e está processando. |
| Concluído | Não aplicável - o contexto da empresa não é aplicável | A ID de IMS na solicitação do RGPD ou da CCPA não está mapeada para nenhum cliente do Target.<br />Algumas empresas têm várias IDs de IMS. Envie a ID de IMS onde o Target é provisionado. |
| Concluído | Não aplicável - contexto do usuário não encontrado | A ID fornecida na solicitação do RGPD ou da CCPA para o visitante específico ou titular dos dados não está presente no armazenamento de perfil do Target.<br />Esse resultado também será retornado se você tentar enviar um tipo de ID de namespace que não seja suportado pelo Target (veja acima as IDs suportadas). |
| Erro | Mensagem de erro (os detalhes dependem do tipo de erro) | Erro ao buscar ou excluir o perfil do titular de dados solicitado.<br />Erro ao fazer upload no Azure para a solicitação de acesso. |

### Que resposta é enviada pelo Target à API do GDPR para uma solicitação de acesso?

Respostas a solicitações de acesso a dados contêm um resumo do perfil do Target referente ao visitante em questão. Esse retorno é enviado para a API do GDPR da Experience Cloud que, por sua vez, envia uma resposta aos Controladores de dados.

Este é um exemplo de resposta da API de acesso do Target:

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            ~"namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            ~"namespace":"tntId", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"thirdPartyId", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
} 
```

| Campo | Descrição |
|--- |--- |
| jobId | Indica a ID de trabalho do RGPD ou da CCPA da API central do RGPD. |
| imsOrgID | Oferece um identificador exclusivo para sua empresa. |
| namespace | Também conhecido como fonte de dados. Consulte “Quais IDs são compatíveis para ajudar os clientes a concluírem uma solicitação de acesso e exclusão do RGPD ou da CCPA para o Target?” neste tópico. |
| type | O tipo de ID para a qual você solicitou o acesso de dados do RGPD ou da CCPA. O Target aceita diversos tipos de ID, alguns são padrão e outros são específicos ao Target. Consulte “Quais IDs são compatíveis para ajudar os clientes a concluírem uma solicitação de acesso e exclusão do RGPD ou da CCPA para o Target?” neste tópico. |
| value | A ID do namespace/fonte de dados. Consulte “Quais IDs são compatíveis para ajudar os clientes a concluírem uma solicitação de acesso e exclusão do RGPD ou da CCPA para o Target?” para saber mais sobre os valores aceitos. |
| código de integração | Códigos de integração são nomes amigáveis para suas fontes de dados e ajudam a monitorar suas fontes de dados de maneira mais fácil do que seria com IDs de fontes de dados. |

Quando diversos valores são fornecidos para identificar os perfis, cada identificador válido terá um arquivo de perfil. Um ou mais arquivos de perfil são enviados ao GDPR Azure Blob central por meio da API central do GDPR, no formato de resposta JSON do perfil do Target.

Uma amostra JSON de perfil do Target pode ser semelhante ao seguinte exemplo:

```
{"profileAttributes": 
 
"Sample_Parameter":{"value":"Gold Loyalty Status","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"user.ReturnTimeOfDay":{"value":"44.0","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"firstSessionStart":{"value":"1523497450602","modifiedAt":"2018-04-11T21:44:10.000-04:00"}, 
 
"user.sessionCountScript":{"value":"1","modifiedAt":"2018-04-11T21:44:14.000-04:00"} 
   } 
} 
```

A seguinte tabela apresenta descrições dos campos ilustrativos de JSON de perfil:

| Campo | Descrição |
|--- |--- |
| Sample_Parameter | Várias informações no perfil do Target são enviadas por upload ou fornecidas diretamente pelo Controlador de dados. Neste exemplo, um parâmetro foi enviado por upload para o perfil do Target usando a API de atualização de perfil. Para obter mais informações, consulte [Métodos para obter dados no Target](/help/dev/before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md). |
| user.ReturnTimeOfDay | Este campo padrão inclui o horário da visita de retorno mais recente de um usuário. |
| firstSessionStart | Este campo padrão inclui o horário de início da primeira sessão do usuário. |
| user.sessionCountScript | Várias informações no perfil do Target são enviadas por upload ou fornecidas diretamente pelo Controlador de dados. Neste exemplo, um script de perfil está incrementando o número de sessões que esse visitante fez no site do Controlador de dados. Para obter mais informações, consulte [Atributos de scripts de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html). |

>[!NOTE]
>
>Esta amostra de código é uma versão reduzida de um JSON de perfil do Target para ilustração. Vários campos do perfil do Target não são padrão. O que é retornado depende de quais informações estão nesse perfil do visitante específico.

### O Target suporta ofuscação de IP? 

O Target suporta ofuscação de IP se você optar por usá-lo como parte de sua estratégia de implementação do GDPR ou da CCPA. Para obter mais informações, consulte [Privacidade](privacy.md#replacement-of-last-octet-of-ip-addresses).

### Devo fazer algo para impedir que meus dados sejam compartilhados ou vendidos a terceiros?

O Target não permite que os clientes compartilhem ou vendam dados diretamente do Target para terceiros, portanto, não há recusa de venda para o Target.
