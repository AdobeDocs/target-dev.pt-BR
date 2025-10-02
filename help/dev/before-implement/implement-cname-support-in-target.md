---
keywords: atendimento ao cliente;cname;programa de certificado;nome canônico;cookies;certificado;amc;certificado gerenciado pela adobe;digicert;validação de controle de domínio;dcv
description: Trabalhe com o  [!DNL Adobe] Client Care para implementar o suporte CNAME (Canonical Name) no  [!DNL Adobe Target] para lidar com problemas de bloqueio de anúncios.
title: Como usar CNAME no Target?
feature: Privacy & Security
role: Developer
exl-id: bf533771-6d46-48ba-964c-3ad9ce9f7352
source-git-commit: 0f00e3d781500ebdf2ad176bf074acca852256b7
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 1%

---

# CNAME e [!DNL Target]

Instruções para trabalhar com o Atendimento ao Cliente do [!DNL Adobe] para implementar o suporte CNAME (Canonical Name) no [!DNL Adobe Target]. Use o CNAME para lidar com problemas de bloqueio de anúncios ou com políticas de cookies relacionadas a ITP (Intelligent Tracking Prevention). Com o CNAME, as chamadas são feitas para um domínio pertencente ao cliente, em vez de para um domínio pertencente a [!DNL Adobe].

## Solicitar suporte para CNAME em [!DNL Target]

1. Determine a lista de nomes de host necessários para seu certificado SSL (consulte as perguntas frequentes abaixo).
1. [Preencha este formulário](/help/dev/implement/assets/FPC_Request_Form.xlsx) e inclua-o ao [abrir um [!DNL Adobe] tíquete de Atendimento ao Cliente solicitando suporte para CNAME](https://experienceleague.adobe.com/en/docs/target/using/cmp-resources-and-contact-information#reference_ACA3391A00EF467B87930A450050077C):

   * Código de cliente [!DNL Adobe Target]:
   * Nomes de host do certificado SSL (exemplo: `target.example.com target.example.org`):
   * Comprador de certificado SSL ([!DNL Adobe] é altamente recomendado, consulte Perguntas frequentes): Adobe/customer
   * Se o cliente estiver adquirindo o certificado, também conhecido como &quot;Traga seu próprio certificado&quot; (BYOC), preencha estes detalhes adicionais:

      * Organização do certificado (exemplo: Example Company Inc):
      * Unidade organizacional do certificado (opcional, por exemplo: Marketing):
      * País do certificado (exemplo: EUA):
      * Estado/região do certificado (exemplo: Califórnia):
      * Cidade do certificado (exemplo: San Jose):

1. Para cada solicitação de nome de host, o Adobe criará a implementação e voltará com um nome de registro CNAME para você criar, que conterá uma sequência aleatória com o sufixo `tt.omtrdc.net`

   Por exemplo, se você fez uma solicitação para `target.example.com`, enviaremos de volta um CNAME no formato de `abcdefgh.tt.omtrdc.net`. Seu registro CNAME DNS deve ser semelhante a:

   ```
   target.example.com.  IN  CNAME  abcdefgh.tt.omtrdc.net.
   ```

   >[!IMPORTANT]
   >
   >A autoridade de certificação de [!DNL Adobe], DigiCert, não pode emitir um certificado até que esta etapa seja concluída. Portanto, o [!DNL Adobe] não pode atender à sua solicitação para uma implementação CNAME até que esta etapa seja concluída.

1. Se [!DNL Adobe] estiver comprando o certificado, [!DNL Adobe] trabalhará com a DigiCert para comprar e implantar seu certificado nos servidores de produção do [!DNL Adobe].

   Se o cliente estiver comprando o certificado (BYOC), o Atendimento ao Cliente do [!DNL Adobe] enviará a você a CSR (solicitação de assinatura de certificado). Use a CSR ao adquirir o certificado por meio da autoridade de certificação de sua escolha. Depois que o certificado for emitido, envie uma cópia dele e de todos os certificados intermediários para o Atendimento ao Cliente do [!DNL Adobe] para implantação.

   O Atendimento ao cliente do [!DNL Adobe] notifica quando a implementação está pronta.

1. Atualize a `serverDomain` ([documentação](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverDomain)) para o novo nome de host CNAME e defina `overrideMboxEdgeServer` como `false` ([documentação](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver)) na sua configuração at.js.

## Perguntas frequentes

As informações a seguir respondem perguntas frequentes sobre a solicitação e a implementação do suporte CNAME no [!DNL Target]:

### Posso fornecer meu próprio certificado (Traga seu próprio certificado ou BYOC)?

Você pode fornecer seu próprio certificado. No entanto, [!DNL Adobe] recomenda esta prática. O gerenciamento do ciclo de vida do certificado SSL é mais fácil para [!DNL Adobe] e para você, se [!DNL Adobe] comprar e controlar o certificado. O tempo de vida dos certificados SSL só será reduzido (consulte a próxima seção sobre o tempo de vida do certificado). Portanto, o Atendimento ao Cliente do [!DNL Adobe] deve contatá-lo todas as vezes para obter um novo certificado em tempo hábil. Isso se tornará um desafio quando o tempo de vida do certificado for reduzido para apenas 47 dias. A implementação do [!DNL Target] fica comprometida quando o certificado expira porque os navegadores recusam conexões.

>[!IMPORTANT]
>
>Se você solicitar uma implementação CNAME de [!DNL Target] traga seu próprio certificado, será responsável por fornecer certificados renovados ao Atendimento ao Cliente do [!DNL Adobe] toda vez que ele expirar. Permitir que seu certificado CNAME expire antes que o [!DNL Adobe] possa implantar um certificado renovado resulta em uma interrupção para sua implementação específica do [!DNL Target].

### Quanto tempo até meu novo certificado SSL expirar?

O tempo de vida de todos os certificados diminuirá como parte de uma iniciativa importante das autoridades de certificação. Para DigiCert, o provedor de certificados de [!DNL Adobe], a seguinte agenda será aplicada:

Até 15 de março de 2026, o tempo de vida máximo de um certificado TLS é de 398 dias.
A partir de 15 de março de 2026, o tempo de vida máximo de um certificado TLS será de 200 dias.
A partir de 15 de março de 2027, o tempo de vida máximo de um certificado TLS será de 100 dias.
A partir de 15 de março de 2029, o tempo de vida máximo de um certificado TLS será de 47 dias.
Para obter mais informações, consulte o artigo da [DigiCert sobre como reduzir a duração do certificado](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days)

### Quais nomes de host devo escolher? Quantos nomes de host por domínio devo escolher?

As implementações CNAME do [!DNL Target] exigem apenas um nome de host por domínio no certificado SSL e no DNS do cliente. [!DNL Adobe] recomenda um nome de host por domínio. Alguns clientes exigem mais nomes de host por domínio para suas próprias finalidades (teste em preparo, por exemplo), que são compatíveis.

A maioria dos clientes escolhe um nome de host como `target.example.com`. [!DNL Adobe] recomenda seguir esta prática, mas a escolha é sua. Não solicitar um nome de host de um registro DNS existente. Isso causa um conflito e atrasa a resolução da solicitação CNAME [!DNL Target].

### Já tenho uma implementação CNAME para [!DNL Adobe Analytics]. Posso usar o mesmo certificado ou nome de host?

Não, [!DNL Target] requer um nome de host e um certificado separados.

### Minha implementação atual do [!DNL Target] é afetada pela ITP 2.x?

A Apple Intelligent Tracking Prevention (ITP) versão 2.3 apresentou o recurso de Mitigação de Camuflagem CNAME, que pode detectar [!DNL Adobe Target] implementações CNAME e reduz a expiração do cookie para sete dias. No momento, [!DNL Target] não tem uma solução alternativa para a Mitigação de Camuflagem CNAME da ITP. Para obter mais informações sobre a ITP, consulte [Apple Intelligent Tracking Prevention (ITP) 2.x](/help/dev/before-implement/privacy/apple-itp-2x.md).

### Que tipo de interrupção de serviço posso esperar quando minha implementação CNAME é implantada?

Não há interrupção do serviço quando o certificado é implantado (incluindo renovações de certificado).

No entanto, depois de alterar o nome do host no código de implementação [!DNL Target] (`serverDomain` na at.js) para o novo nome de host CNAME (`target.example.com`), os navegadores da Web tratam os visitantes recorrentes como novos visitantes. Os dados de perfil dos visitantes retornados são perdidos porque o cookie anterior está inacessível sob o nome de host antigo (`clientcode.tt.omtrdc.net`). O cookie anterior está inacessível devido aos modelos de segurança do navegador. Essa interrupção ocorre somente na transição inicial para o novo CNAME. As renovações de certificado não têm o mesmo efeito, pois o nome do host não é alterado.

### Qual tipo de chave e algoritmo de assinatura de certificado é usado para minha implementação CNAME?

Todos os certificados são RSA SHA-256 e as chaves são RSA 2048-bit, por padrão. Atualmente, não há suporte para tamanhos de chave maiores que 2048 bits.

### Como posso validar se minha implementação CNAME está pronta para o tráfego?

Use o seguinte conjunto de comandos (no terminal de linha de comando macOS ou Linux, usando bash e curl >=7.49):

1. Copie e cole esta função bash no terminal ou cole a função no arquivo de script de inicialização bash (geralmente `~/.bash_profile` ou `~/.bashrc`) para que a função esteja disponível nas sessões de terminal:

   ```
   function adobeTargetCnameValidation {
     local hostname="$1"
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi
   
     local service="Adobe Target CNAME implementation"
     local edges="31 32 34 35 36 37 38"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local shardFormat="-alb%02d"
     local shards=5
     local shardsFoundCount=0
     local shardsFound
     local shardsFoundOutput
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslLabsUrl="https://ssllabs.com/ssltest/analyze.html?hideResults=on&latest&d=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2 )"
     local curlVersionRequired=">=7.49"
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local edge
     local shard
     local currEdgeShard
     local dnsOutput
     local cnameExists
     local endToEndTestSucceeded
     local curlResult
   
     for shard in $(seq $shards); do
       if [ "$shardsFoundCount" -eq 0 ]; then
         for edge in $edges; do
           if [ "$shard" -eq 1 ]; then
             currEdgeShard="$(printf "$edgeFormat" "$edge" "")"
           else
             currEdgeShard="$(
               printf "$edgeFormat" "$edge" "$(
                 printf -- "$shardFormat" "$shard"
               )"
             )"
           fi
           curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currEdgeShard:443" "$url" 2>&1)"
           if grep -q "$curlValidation" <<< "$curlResult"; then
             shardsFound+=" $currEdgeShard"
             if grep -q "$curlResponseValidation" <<< "$curlResult"; then
               shardsFoundCount=$((shardsFoundCount+1))
               shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currEdgeShard] $miniRule\n"
             else
               shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currEdgeShard] $miniRule\n"
             fi
             shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
             if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
               shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
             fi
           fi
         done
       fi
     done
   
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
     dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
     if grep -qFi ".$edgeDomain" <<< "$dnsOutput"; then
       echo "$success $hostname passes DNS CNAME validation"
       cnameExists=true
     else
       echo -n "$failure $hostname FAILED DNS CNAME validation -- "
       if [ -n "$dnsOutput" ]; then
         echo -e "$dnsOutput is not in the subdomain $edgeDomain"
       else
         echo "required DNS CNAME record pointing to <random-string>.$edgeDomain not found"
       fi
     fi
   
     curlResult="$(curl -vsm20 "$url" 2>&1)"
     if grep -q "$curlValidation" <<< "$curlResult"; then
       if grep -q "$curlResponseValidation" <<< "$curlResult"; then
         echo -en "$success $hostname passes TLS and HTTP response validation"
         if [ -n "$cnameExists" ]; then
           echo
         else
           echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
             "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
         fi
         endToEndTestSucceeded=true
       else
         echo -n "$failure $hostname FAILED HTTP response validation --" \
           "unexpected response from $url -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     else
   
       echo -n "$failure $hostname FAILED TLS validation -- "
       if [ -n "$cnameExists" ]; then
         echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
           "protocols, see curl output below and optionally SSL Labs ($sslLabsUrl):"
         echo ""
         echo "$horizontalRule"
         echo "$curlResult" | sed 's/^/    /g'
         echo "$horizontalRule"
         echo ""
       else
         echo "the required DNS CNAME record is missing, see above"
       fi
     fi
   
     if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo
   
       if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, including detailed browser/client support,"
         echo "  see SSL Labs (click the first IP address if prompted):"
         echo ""
         echo "    $info  $sslLabsUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       if bc -l <<< "$(cut -d. -f1,2 <<< "$curlVersion") $curlVersionRequired" 2>/dev/null | grep -q 0; then
         echo -n " -- insufficient curl version installed: $curlVersion, but this script requires curl version" \
           "$curlVersionRequired because it uses the curl --connect-to flag to bypass DNS and directly test" \
           "each Adobe Target edge shards' SNI confirguation for $hostname"
       fi
       if [ -n "$shardsFoundOutput" ]; then
         echo -e ":\n$shardsFoundOutput"
       fi
       echo
     fi
     echo
     echo "$horizontalRule"
     echo
   }
   ```

1. Cole este comando (substituindo `target.example.com` pelo seu nome de host):

   ```
   adobeTargetCnameValidation target.example.com
   ```

   Se a implementação estiver pronta, você verá a saída como abaixo. A parte importante é que todas as linhas de status de validação mostram `✅` em vez de `🚫`. Cada fragmento CNAME de borda [!DNL Target] deve mostrar `CN=target.example.com`, que corresponde ao nome de host principal no certificado solicitado (nomes de host SAN adicionais no certificado não são impressos nesta saída).

   ```
   $ adobeTargetCnameValidation target.example.com
   
   ==========================================================
   
   Adobe Target CNAME implementation validation for hostname target.example.com:
   ✅ target.example.com passes DNS CNAME validation
   ✅ target.example.com passes TLS and HTTP response validation
   ✅ target.example.com passes shard validation for the following 7 edge shards:
   
   ===== ✅ target.example.com [edge shard: mboxedge31-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge32-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge34-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge35-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge36-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge37-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ===== ✅ target.example.com [edge shard: mboxedge38-alb02.tt.omtrdc.net] =====
   *  expire date: Jul 22 23:59:59 2022 GMT
   *  issuer: C=US; O=DigiCert Inc; CN=DigiCert TLS RSA SHA256 2020 CA1
   *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com
   
   ==========================================================
   
     For additional TLS/SSL validation, including detailed browser/client support,
     see SSL Labs (click the first IP address if prompted):
   
       🔎  https://ssllabs.com/ssltest/analyze.html?hideResults=on&latest&d=target.example.com
   
     To check DNS propagation around the world, see whatsmydns.net:
   
       🔎  DNS A records:     https://whatsmydns.net/#A/target.example.com
       🔎  DNS CNAME record:  https://whatsmydns.net/#CNAME/target.example.com
   
   ==========================================================
   ```

   >[!NOTE]
   >
   >Se esse comando de validação falhar na validação de DNS, mas você já tiver feito as alterações necessárias no DNS, talvez seja necessário aguardar a propagação completa das atualizações de DNS. Os registros DNS têm um [TTL (time-to-live)](https://en.wikipedia.org/wiki/Time_to_live#DNS_records) associado que determina o tempo de expiração do cache para as respostas DNS desses registros. Como resultado, talvez seja necessário aguardar pelo menos tanto tempo quanto seus TTLs. Você pode usar o comando `dig target.example.com` ou [a Caixa de Ferramentas do G Suite](https://toolbox.googleapps.com/apps/dig/#CNAME) para pesquisar seus TTLs específicos. Para verificar a propagação DNS pelo mundo, consulte [whatsmydns.net](https://whatsmydns.net/#CNAME).

### Como usar um link para opção de não participação com CNAME

Se você estiver usando CNAME, o link para opção de não participação deverá conter o parâmetro &quot;client=`clientcode`&quot;, por exemplo:
`https://my.cname.domain/optout?client=clientcode`.

Substitua `clientcode` com seu código de cliente e adicione o texto ou imagem a ser vinculado à [URL de não participação](/help/dev/before-implement/privacy/privacy.md).

## Limitações conhecidas

* O modo de controle de qualidade não é aderente quando você tem CNAME e at.js 1.x porque ele se baseia em um cookie de terceiros. A solução alternativa é adicionar os parâmetros de pré-visualização a cada URL para o qual você navega. O modo de controle de qualidade é aderente quando você tem CNAME e at.js 2.x.
* Ao usar CNAME, fica mais provável que o tamanho do cabeçalho do cookie para chamadas [!DNL Target] aumente. O [!DNL Adobe] recomenda manter o tamanho do cookie abaixo de 8 KB.
