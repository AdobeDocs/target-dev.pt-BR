---
keywords: privacidade, endereço ip, geosegmentação, recusar, recusar, recusar, privacidade de dados, regulamentos governamentais, regulamentos, gdpr, ccpa, privacidade, informações de identificação pessoal, PII
description: Saiba como [!DNL Adobe Target] está em conformidade com as leis de privacidade de dados aplicáveis, incluindo a coleta e o tratamento de endereços IP, PII e instruções de recusa.
title: Como o Target lida com problemas de privacidade, incluindo PII?
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 58%

---

# Privacidade

O [!DNL Adobe Target] possibilitou processos e definições que permitem seu uso [!DNL Target] em conformidade com as leis de privacidade de dados aplicáveis.

## Coleta de endereços IP e informações pessoais identificáveis (PII)

O endereço IP de um visitante do seu site é transmitido para um Centro de processamento de dados da Adobe (DPC). Dependendo da configuração de rede do visitante, o endereço IP não representa necessariamente o endereço IP do computador dele. Por exemplo, o endereço IP pode ser o endereço IP externo de um firewall NAT (Network Address Translation, tradução de endereço de rede), proxy HTTP ou gateway de Internet.

>[!IMPORTANT]
>
>[!DNL Target] O não armazena endereços IP do usuário ou informações pessoais identificáveis (PII). Os endereços IP são usados somente pelo [!DNL Target] durante a sessão (na memória, nunca persistiu).

## Substituição do último octeto de endereços IP

o Adobe desenvolveu uma configuração de &quot;privacidade por design&quot; que os usuários podem ativar para o Adobe [!DNL Target]. Quando ativado, Adobe [!DNL Target] ofusca imediatamente o último octeto (a última parte) do endereço IP no momento em que o endereço IP é coletado. Essa anonimização é realizada antes de qualquer processamento do endereço IP, inclusive antes de uma consulta geográfica opcional do endereço IP.

Quando esse recurso é ativado, o endereço IP fica anônimo de forma que não seja mais identificado como informações pessoais. Como resultado, [!DNL Target] O pode ser usado em conformidade com as leis de privacidade de dados em países que não permitem a coleta de informações pessoais. A obtenção de informações do nível da cidade provavelmente será muito afeta pela ofuscação do endereço IP. A obtenção de informações do nível da região e do país será pouco afetada.

As seguintes configurações estão disponíveis no [!DNL Target] Navegando até **[!UICONTROL Administração]** > **[!UICONTROL Implementação]**:

* [!UICONTROL Ofuscação do último octeto]: [!DNL Target] Oculta o último octeto do endereço IP.
* [!UICONTROL Ofuscação de IP inteiro]: [!DNL Target] Oculta todo o endereço IP.
* [!UICONTROL Nenhum]: [!DNL Target] não oculta nenhuma parte do endereço IP.

  ![obfuscate-ip-options](assets/obfuscate-ip.png)

[!DNL Target] recebe o endereço IP completo e o ofusca (se estiver definido como Último octeto ou IP inteiro) conforme especificado. [!DNL Target] em seguida, mantém o endereço IP ofuscado na memória somente durante a sessão atual.

## GeoSegmentation 

Se você ativar a substituição do último octeto do endereço IP, os valores restantes do endereço IP poderão ser analisados por meio de relatórios no [!DNL Target]. Se o último octeto do endereço IP não for ofuscado, o endereço IP inteiro poderá ser analisado no [!DNL Target]. Você pode usar o recurso GeoSegmentation para mapear o local do visitante por área geográfica. Os dados de GeoSegmentation são granulares somente no nível da cidade ou no nível de código postal, e não no nível individual.

Se os endereços IP forem completamente ofuscados, a GeoSegmentation e a geolocalização não estarão disponíveis.

## Link para opção de não participação

Você pode adicionar um link para opção de não participação a seus sites para permitir que os visitantes optem por não participar de todas as contagens e entregas de conteúdo.

1. Adicione o seguinte link a seu site:

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. (Condicional) Se você estiver usando CNAME, o link deverá conter a tag &quot;client=`clientcode` parâmetro, por exemplo:
   `https://my.cname.domain/optout?client=clientcode`.

1. Substitua o `clientcode` com seu código de cliente e adicione o texto ou imagem a ser conectado ao URL de não participação.

Qualquer visitante que clicar neste link não será incluído em qualquer solicitação de mbox chamadas de suas sessões de navegação até que excluam seus cookies, ou por dois anos, o que acontecer primeiro. Isto funciona através da configuração um cookie chamado `disableClient` para o visitante no domínio `clientcode.tt.omtrdc.net`.

Mesmo se estiver usando uma implementação de cookie primário, a opção de não participação fornecida é definida por meio de um cookie de terceiros. Se o cliente estiver usando somente um cookie próprio, [!DNL Target] verifica se um cookie de opção de não participação está definido.

## Privacidade e regulamentos sobre proteção de dados

Consulte [Regulamentos de privacidade e proteção de dados](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) para obter informações sobre o Regulamento Geral de Proteção de Dados da União Europeia (GDPR), a Lei de Privacidade do Consumidor da Califórnia (CCPA) e outros requisitos internacionais de privacidade e como esses regulamentos afetam sua organização e o [!DNL Target].

## Coleta de dados de uso de recursos

Os dados de uso de recursos individuais são coletados para fins de Adobe interno para identificar se [!DNL Target] Os recursos do estão funcionando como pretendido ou para identificar os recursos que estão sendo subutilizados. Várias medidas de latência são coletadas para ajudar a resolver problemas de desempenho. Os dados pessoais não são coletados.

Você pode recusar o relatório de dados de uso em nossos SDKs definindo `telemetryEnabled` como falso nas opções de inicialização do cliente. Para mais informações, consulte [telemetryEnabled em targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).
