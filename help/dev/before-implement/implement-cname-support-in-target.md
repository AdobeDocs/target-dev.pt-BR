---
keywords: atendimento ao cliente, cname, programa de certificado, nome canônico, cookies, certificado, amc, certificado gerenciado pela adobe, digicert, validação de controle de domínio, dcv, atendimento ao cliente2
description: Trabalhe com [!UICONTROL Adobe Client Care] para implementar o suporte CNAME (Canonical Name) em  [!DNL Adobe Target]  para lidar com problemas de bloqueio de anúncios.
title: Como usar CNAME no Target?
feature: Privacy & Security
exl-id: 5709df5b-6c21-4fea-b413-ca2e4912d6cb
source-git-commit: f894122217529cb40369c003a3b4ed5419fb0505
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 0%

---

# CNAME e Target

Instruções para trabalhar com [!DNL Adobe Client Care] para implementar o suporte CNAME (Canonical Name) em [!DNL Adobe Target]. Use o CNAME para lidar com problemas de bloqueio de anúncios ou com políticas de cookies relacionadas a ITP (Intelligent Tracking Prevention). Com o CNAME, as chamadas são feitas para um domínio pertencente ao cliente, em vez de para um domínio pertencente à Adobe.

## Solicitar suporte para CNAME no Target

1. Determine a lista de nomes de host necessários para seu certificado SSL (consulte as perguntas frequentes abaixo).

1. Para cada nome de host, crie um registro CNAME no DNS apontando para o nome de host [!DNL Target] comum `clientcode.tt.omtrdc.net`.

   Por exemplo, se o código de cliente for &quot;cnamcustomer&quot; e o nome de host proposto for `target.example.com`, o registro CNAME de DNS será semelhante a:

   ```
   target.example.com.  IN  CNAME  cnamecustomer.tt.omtrdc.net.
   ```

   >[!WARNING]
   >
   >A autoridade de certificação da Adobe, DigiCert, não pode emitir um certificado até que esta etapa seja concluída. Portanto, a Adobe não pode atender à sua solicitação para uma implementação CNAME até que essa etapa seja concluída.

1. [Preencha este formulário](assets/FPC_Request_Form.xlsx) e inclua-o ao [abrir um tíquete de Atendimento ao Cliente do Adobe solicitando suporte para CNAME](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?lang=pt-BR&#reference_ACA3391A00EF467B87930A450050077C):

   * Código de cliente [!DNL Adobe Target]:
   * Nomes de host do certificado SSL (exemplo: `target.example.com target.example.org`):
   * Comprador de certificado SSL (o Adobe é altamente recomendado, consulte Perguntas frequentes): Adobe/customer
   * Se o cliente estiver adquirindo o certificado, também conhecido como &quot;Traga seu próprio certificado&quot; (BYOC), preencha estes detalhes adicionais:
      * Organização do certificado (exemplo: Example Company Inc):
      * Unidade organizacional do certificado (opcional, por exemplo: Marketing):
      * País do certificado (exemplo: EUA):
      * Estado/região do certificado (exemplo: Califórnia):
      * Cidade do certificado (exemplo: San Jose):

1. Se a Adobe estiver comprando o certificado, a Adobe trabalhará com a DigiCert para comprar e implantar seu certificado nos servidores de produção da Adobe.

   Se o cliente estiver comprando o certificado (BYOC), o Atendimento ao cliente da Adobe enviará a solicitação de assinatura do certificado (CSR). Use a CSR ao adquirir o certificado por meio da autoridade de certificação de sua escolha. Depois que o certificado for emitido, envie uma cópia do certificado e dos certificados intermediários para o Atendimento ao cliente da Adobe para implantação.

   O Atendimento ao cliente da Adobe notifica quando a implementação está pronta.

1. Atualize a `serverDomain` [documentação](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverdomain) para o novo nome de host CNAME e defina `overrideMboxEdgeServer` como `false` [documentação](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver) na sua configuração at.js.

## Perguntas frequentes

As informações a seguir respondem às perguntas frequentes sobre a solicitação e a implementação do suporte CNAME no Target:

### Posso fornecer meu próprio certificado (Traga seu próprio certificado ou BYOC)?

Você pode fornecer seu próprio certificado. No entanto, a Adobe não recomenda essa prática. O gerenciamento do ciclo de vida do certificado SSL é mais fácil para a Adobe e para você, caso a Adobe compre e controle o certificado. Os certificados SSL devem ser renovados todos os anos. Portanto, o Atendimento ao cliente da Adobe deve entrar em contato com você todos os anos para obter um novo certificado em tempo hábil. Alguns clientes podem ter dificuldade em produzir um certificado renovado em tempo hábil. A implementação do [!DNL Target] fica comprometida quando o certificado expira porque os navegadores recusam conexões.

>[!WARNING]
>
>Se você solicitar uma implementação CNAME com o seu próprio certificado [!DNL Target], será responsável por fornecer certificados renovados ao Atendimento ao cliente da Adobe todos os anos. Permitir que seu certificado CNAME expire antes que a Adobe possa implantar um certificado renovado resulta em uma interrupção para sua implementação específica do [!DNL Target].

### Quanto tempo até meu novo certificado SSL expirar?

Todos os certificados adquiridos pela Adobe são válidos por um ano. Consulte o artigo da [DigiCert sobre certificados de 1 ano](https://www.digicert.com/blog/position-on-1-year-certificates) para obter mais informações.

### Quais nomes de host devo escolher? Quantos nomes de host por domínio devo escolher?

As implementações de CNAME do Target exigem apenas um nome de host por domínio no certificado SSL e no DNS do cliente. A Adobe recomenda um nome de host por domínio. Alguns clientes exigem mais nomes de host por domínio para suas próprias finalidades (teste em preparo, por exemplo), que são compatíveis.

A maioria dos clientes escolhe um nome de host como `target.example.com`. A Adobe recomenda seguir essa prática, mas a escolha é sua. Não solicitar um nome de host de um registro DNS existente. Isso causa um conflito e atrasa a resolução da solicitação CNAME [!DNL Target].

### Já tenho uma implementação CNAME para o Adobe Analytics. Posso usar o mesmo certificado ou nome de host?

Não, [!DNL Target] requer um nome de host e um certificado separados.

### Minha implementação atual do [!DNL Target] é afetada pela ITP 2.x?

A Apple Intelligent Tracking Prevention (ITP) versão 2.3 apresentou o recurso de Mitigação de Camuflagem CNAME, que pode detectar [!DNL Target] implementações CNAME e reduz a expiração do cookie para sete dias. No momento, [!DNL Target] não tem uma solução alternativa para a Mitigação de Camuflagem CNAME da ITP. Para obter mais informações sobre a ITP, consulte [Apple Intelligent Tracking Prevention (ITP) 2.x](../before-implement/privacy/apple-itp-2x.md).

### Que tipo de interrupção de serviço posso esperar quando minha implementação CNAME é implantada?

Não há interrupção do serviço quando o certificado é implantado (incluindo renovações de certificado).

No entanto, depois de alterar o nome do host no código de implementação [!DNL Target] (`serverDomain` na at.js) para o novo nome de host CNAME (`target.example.com`), os navegadores da Web tratam os visitantes recorrentes como novos visitantes. Os dados de perfil dos visitantes retornados são perdidos porque o cookie anterior está inacessível sob o nome de host antigo (`clientcode.tt.omtrdc.net`). O cookie anterior está inacessível devido aos modelos de segurança do navegador. Essa interrupção ocorre somente na transição inicial para o novo CNAME. As renovações de certificado não têm o mesmo efeito, pois o nome do host não é alterado.

### Qual tipo de chave e algoritmo de assinatura de certificado é usado para minha implementação CNAME?

Todos os certificados são RSA SHA-256 e as chaves são RSA 2048-bit, por padrão. Tamanhos de chaves maiores que 2048 bits devem ser solicitados explicitamente através de [!UICONTROL Customer Care].

### Como posso validar se minha implementação CNAME está pronta para o tráfego?

Use o seguinte conjunto de comandos (no terminal de linha de comando macOS ou Linux, usando bash e curl >=7.49):

1. Copie e cole esta função bash no terminal ou cole a função no arquivo de script de inicialização bash (geralmente `~/.bash_profile` ou `~/.bashrc`) para que a função esteja disponível nas sessões de terminal:

   +++ Ver detalhes

   ```bash {line-numbers="true"}
    function adobeTargetCnameValidation {
   
     local hostname="$1"
   
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi
   
     local service="Adobe Target CNAME implementation"
     local edges="41 42 44 45 46 47 48"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local poolDomain="pool.data.adobedc.net"
     local shards=5
     local shardsFoundCount=0
     local shardsFound=""
     local shardsFoundOutput=""
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslShopperUrl="https://www.sslshopper.com/ssl-checker.html#hostname=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2)"
     local curlVersionRequired=7.49
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local cnameExists=""
     local endToEndTestSucceeded=""
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local currShard="${region}-${poolDomain}"
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currShard:443" "$url" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         shardsFound+=" $currShard"
   
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundCount=$((shardsFoundCount+1))
           shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currShard] $miniRule\n"
         else
           shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currShard] $miniRule\n"
         fi
   
         shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
   
         if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
         fi
       fi
     done
   
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
   
     local dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
     if grep -qFi ".$edgeDomain" <<< "$dnsOutput"; then
       echo "$success $hostname passes DNS CNAME validation"
       cnameExists=true
     else
       echo -n "$failure $hostname FAILED DNS CNAME validation -- "
       if [ -n "$dnsOutput" ]; then
         echo -e "$dnsOutput is not in the subdomain $edgeDomain"
       else
         echo "required DNS CNAME record pointing to <target-client-code>.$edgeDomain not found"
       fi
     fi
   
     for region in IRL1 IND1 SIN OR SYD VA TYO; do
       local curlResult="$(curl -vsm20 --connect-to "$hostname:443:${region}-pool.data.adobedc.net:443" "https://$hostname$curlEndpoint" 2>&1)"
   
       if grep -q "$curlValidation" <<< "$curlResult"; then
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           echo -en "$success $hostname passes TLS and HTTP response validation for region $region"
           if [ -n "$cnameExists" ]; then
             echo
           else
             echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
               "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
           fi
           endToEndTestSucceeded=true
         else
           echo -n "$failure $hostname FAILED HTTP response validation for region $region --" \
             "unexpected response from $url -- "
           if [ -n "$cnameExists" ]; then
             echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
           else
             echo "the required DNS CNAME record is missing, see above"
           fi
         fi
       else
         echo -n "$failure $hostname FAILED TLS validation for region $region -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
             "protocols, see curl output below and optionally SSL Shopper ($sslShopperUrl):"
           echo ""
           echo "$horizontalRule"
           echo "$curlResult" | sed 's/^/    /g'
           echo "$horizontalRule"
           echo ""
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     done
   
     if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo
   
       if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, see SSL Shopper:"
         echo ""
         echo "    $info  $sslShopperUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       echo ""
     fi
   
     echo
     echo "$horizontalRule"
     echo
   }
   ```

   +++

1. Cole este comando (substituindo `target.example.com` pelo seu nome de host):

   ```adobeTargetCnameValidation target.example.com```

Se a implementação estiver pronta, você verá a saída como abaixo. A parte importante é que todas as linhas de status de validação mostram `✅` em vez de `🚫`. Cada fragmento CNAME da borda do Target deve mostrar `CN=target.example.com`, que corresponde ao nome de host principal no certificado solicitado (nomes de host SAN adicionais no certificado não são impressos nesta saída).

    +++ Ver detalhes
    
    &quot;bash {line-numbers=&quot;true&quot;}
    $ adobeTargetCnameValidation
    target.example.com===============================================================Validação de implementação CNAME Adobe Target para nome de host target.example.com:
    ✅ target.example.com passa a validação CNAME DNS
    ✅ target.example.com passa a validação de resposta TLS e HTTP para a região IRL1
    ✅ target.example.com passa na validação de resposta TLS e HTTP para região IND1
    ✅ target.example.com passa na validação de resposta TLS e HTTP para região SIN
    ✅ target.example.com passa na validação de resposta TLS e HTTP para região OU
    ✅ target.example.com passa na validação de resposta TLS e HTTP para região SYD
    ✅ target.example.com passa na validação de resposta TLS e HTTP para região VA
    ✅ target.example.com passa na validação de resposta TLS e HTTP para região TYO
    ✅ target.example.com passa na validação de fragmento para os 7 fragmentos de borda a seguir:==== ✅ target.example.com [fragmento de borda: IRL1-pool.data.adobedc.net] =====
    * Data de vencimento: 20 23 de fevereiro:59:59 2026 GMT
    * emissor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    * assunto: C=US; ST=Califórnia; L=San Jose; O=Adobe Systems Incorporated; CN=target.example&rbrace; [edge shard: IND1-pool.data.adobedc.net] =====✅* data de expiração: 20 de fevereiro de 23
    59 de 2026 GMT:59:* emissor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    * assunto: C=US; ST=Califórnia; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== 
     target.example.com [fragmento de borda: SIN-pool.data.adobedc.net] ====✅* data de expiração: 20 23 de fevereiro
    59 2026 GMT:59:* emissor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    * assunto: C=US; ST; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com====== 
     target.example.com [fragmento de borda: OR-pool.data.adobedc.net] =====✅* data de expiração: 20 de fevereiro de 23
    59 de 2026 GMT:59:* emissor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS SHA256 2020 CA1
    * assunto: C=US; ST=Califórnia; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com====== 
     target.example.com [fragmento de borda: SYD-pool.data.adobedc.net] =====✅* data de expiração: 20 de fevereiro de 2023
    59 de 2026 GMT:59:* emissor: C=US; O=DigiCert; CN=DigiCert Global G2 SHA256 2020 CA1
    * assunto: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com====== 
     target.example.com [fragmento de borda: VA-pool.data.adobedc.net] ====✅* data de vencimento: 20 de fevereiro de 2023
    59 de 2026 GMT:59:* emissor: C=US; O=DigiCert CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    * assunto: C=US; ST=Califórnia; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com====== 
     target.example.com target.example.com [fragmento de borda: TYO-pool.data.adobedc.net] ====✅* data de expiração: 20 de fevereiro 23
    59 2026 GMT:59:* emissor: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    * assunto: C=US; ST=Califórnia; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com========================================================= Para obter a validação adicional de TLS/SSL, consulte Comprador SSL:    
     https://www.sslshopper.com/ssl-checker.html#hostname=target.example.com Para verificar a propagação de DNS no mundo, consulte whatsmydns.net:    🔎 registros DNS A:     Registro CNAME DNS https://whatsmydns.net/#A/target.example.com🔎: https://whatsmydns.net/#CNAME/target.example.com
    🔎&quot;
    +++
    
    

>[!NOTE]
>
>Se esse comando de validação falhar na validação de DNS, mas você já tiver feito as alterações necessárias no DNS, talvez seja necessário aguardar a propagação completa das atualizações de DNS. Os registros DNS têm um [TTL (time-to-live)](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) associado que determina o tempo de expiração do cache para as respostas DNS desses registros. Como resultado, talvez seja necessário aguardar pelo menos tanto tempo quanto seus TTLs. Você pode usar o comando `dig target.example.com` ou [a Caixa de Ferramentas do G Suite](https://toolbox.googleapps.com/apps/dig/#CNAME) para pesquisar seus TTLs específicos. Para verificar a propagação DNS pelo mundo, consulte [whatsmydns.net](https://whatsmydns.net/#CNAME).

### Como usar um link para opção de não participação com CNAME

Se você estiver usando CNAME, o link para opção de não participação deverá conter o parâmetro &quot;client=`clientcode`&quot;, por exemplo:
`https://my.cname.domain/optout?client=clientcode`.

Substitua `clientcode` com seu código de cliente e adicione o texto ou imagem a ser vinculado à [URL de não participação](privacy/privacy.md).

## Limitações conhecidas

* O modo de controle de qualidade não é aderente quando você tem CNAME e at.js 1.x porque ele se baseia em um cookie de terceiros. A solução alternativa é adicionar os parâmetros de pré-visualização a cada URL para o qual você navega. O modo de controle de qualidade é aderente quando você tem CNAME e at.js 2.x.
* Ao usar CNAME, fica mais provável que o tamanho do cabeçalho do cookie para chamadas [!DNL Target] aumente. A Adobe recomenda manter o tamanho do cookie abaixo de 8 KB.
