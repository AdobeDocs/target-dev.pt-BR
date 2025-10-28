---
keywords: implementar, implementação, lista de permissões, lista branca, incluo na lista de permissões, lista de permissões, borda, bordas, $9
description: Exiba uma lista de hosts para ajudá-lo a incluir na lista de permissões [!DNL Adobe Target] bordas (nós de fornecimento distribuídos geograficamente que garantem tempos de resposta ideais para os usuários finais).
title: Como Incluir na lista de permissões  [!DNL Target] Nós do Edge?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 662d415bc3c216bcd038f07dcaa0fd83f6518690
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Incluir na lista de permissões [!DNL Target] nós de borda

Informações e uma lista atualizada de hosts para ajudá-lo a incluir na lista de permissões [!DNL Adobe Target] bordas.

Uma borda é uma arquitetura de fornecimento distribuída geograficamente que garante tempos de resposta ideais para usuários finais que solicitem o conteúdo, independentemente de sua localização. Cada nó de borda tem todas as informações necessárias para responder à solicitação de conteúdo do usuário e rastrear os dados de análise dessa solicitação. As solicitações do usuário são roteadas para o nó de borda mais próximo. Para obter mais informações, consulte [A rede de borda](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Você pode incluir na lista de permissões [!DNL Target] nós de borda, se desejar.

>[!IMPORTANT]
>
>Incluir na lista de permissões Além de converter os endereços IP NAT (Network Address Translation, tradução de endereço de rede) de [!DNL Target] bordas e [!DNL Target] endereços IP de borda discutidos no artigo, você também deve incluir na lista de permissões todos os [!DNL Adobe Analytics] blocos de endereço IP.
>
>Para obter mais informações, consulte [Todos os blocos de endereço IP do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} na documentação das *notas técnicas do Adobe Analytics*.
>
>A infraestrutura do [!DNL Adobe Target] está sendo atualizada e os clientes que desejam incluir na lista de permissões endereços devem usar ambos os conjuntos de IPs. Se isso não for feito, os clientes que usam implementações do lado do servidor ou híbridas nas quais as chamadas da API do Target para busca de experiências são originadas de uma rede atrás de um firewall configurado para usar um incluo na lista de permissões.

Para garantir acesso ininterrupto ao [!DNL Target] por meio do [!DNL Experience Edge Connector], os clientes podem atualizar suas configurações de rede para permitir tráfego para o serviço proxy.

## Visão geral do serviço de proxy

* **Ponto de Extremidade de Serviço**: `https://tnt-web-proxy.adobe.io`.
* **Infraestrutura**: hospedada na plataforma [!DNL Adobe] do Ethos.
* **Observação**: este serviço usa roteamento DNS baseado em latência e não depende de endereços IP estáticos.

## Alvos CNAME

O serviço de proxy roteia o tráfego dinamicamente entre várias regiões usando registros CNAME. Estes são os destinos atuais:

| Localização do Edge | Endereços IP de saída |
| --- | --- |
| Região | Destino CNAME |
| Europa (eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| Leste dos EUA (us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| Leste dos EUA (us-east-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

## Entradas de incluo na lista de permissões recomendadas

Para garantir uma conectividade confiável, inclua na lista de permissões os seguintes nomes de host:

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

## Opcional: descoberta de IP

Se suas políticas de rede exigirem o incluir na lista de permissões baseado em IP, você poderá visualizar os endereços IP públicos atuais associados ao serviço proxy usando esta ferramenta:

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`