---
keywords: implementar, implementação, lista de permissões, lista branca, lista de permissões, lista de permissões, borda, bordas, $9
description: Incluir na lista de permissões Exiba uma lista de hosts para ajudá-lo a modificar [!DNL Adobe Target] bordas (distribuídas geograficamente para atender aos nós que garantem tempos de resposta ideais para os usuários finais).
title: Como Faço Para Incluir na lista de permissões Nós Do Edge [!DNL Target] ?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 1583cfe8ea1009fd1df5c5a0e5f3f95f72daf2b9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# ➡ Incluir na lista de permissões nós de borda [!DNL Target]

Incluir na lista de permissões Informações e uma lista atualizada de hosts para ajudá-lo a executar a pesquisa de [!DNL Adobe Target] bordas.

Uma borda é uma arquitetura de fornecimento distribuída geograficamente que garante tempos de resposta ideais para usuários finais que solicitem o conteúdo, independentemente de sua localização. Cada nó de borda tem todas as informações necessárias para responder à solicitação de conteúdo do usuário e rastrear os dados de análise dessa solicitação. As solicitações do usuário são roteadas para o nó de borda mais próximo. Para obter mais informações, consulte [A rede de borda](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=pt-BR#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Incluir na lista de permissões Você pode modificar [!DNL Target] nós de borda, se desejar.

>[!IMPORTANT]
>
>Incluir na lista de permissões incluir na lista de permissões Além de converter os endereços IP NAT (Network Address Translation, tradução de endereço de rede) de [!DNL Target] bordas e [!DNL Target] endereços IP de borda discutidos no artigo, você também deve gravar todos os [!DNL Adobe Analytics] blocos de endereço IP.
>
>Para obter mais informações, consulte [Todos os blocos de endereço IP do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=pt-BR#all-adobe-analytics-ip-address-blocks){target=_blank} na documentação das *notas técnicas do Adobe Analytics*.
>
>A infraestrutura do [!DNL Adobe Target] está sendo atualizada, e os clientes que desejam realizar a inclui na lista de permissões de endereços devem usar ambos os conjuntos de IPs. Se isso não for feito, os clientes que usam implementações do lado do servidor ou híbridas nas quais as chamadas da API do Target para busca de experiências são originadas de uma rede atrás de um firewall configurado para usar um incluo na lista de permissões.
>
>Todos os endereços Edge4 *x* listados nas duas tabelas abaixo estão agendados para serem atualizados em 9 de agosto de 2023.

## Endereços IP NAT de [!DNL Target] bordas

Lista de endereços IP de saída de [!DNL Target] bordas. [!DNL Target] Inclua na lista de permissões esses IPs se você planeja que o  entre em contato com seus serviços.

| Localização do Edge | Endereços IP de saída |
| --- | --- |
| Edge41 (Mumbai) | 3.6.2.221<P>13.235.112.4 <P>52.66.66.192 |
| Edge42 (Tóquio) | 52.69.55.232<P>43.206.61.43 <P>13.113.73.214 |
| Edge44 (Costa Leste dos EUA) | 54 164 192 223<P>52.86.86.203 <P>54.88.167.98 |
| Edge45 (Costa Oeste dos EUA) | 52.40.124.129<P>54 148 219 69 <P>54.189.208.212 |
| Edge46 (Sydney) | 54.253.144.4<P>54.66.198.142 <P>13.211.218.51 |
| Edge47 (Irlanda) | 52.208.136.136<P>54.170.28.19 <P>99.80.111.82 |
| Edge48 (Cingapura) | 3.1.141.36<P>18 143 112 116 <P>52.76.61.44 |

## [!DNL Target] endereços IP de borda

Lista de endereços IP de [!DNL Target] bordas. ➡ Inclua na lista de permissões esses IPs se desejar fazer chamadas de API para [!DNL Target] bordas.

Essa lista será alterada com frequência, à medida que os balanceadores de carga aumentarem e diminuírem com base nos perfis de tráfego.

| Localização do Edge | Domínio | Endereço IP |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(onde CLIENTCODE é a sua ID de cliente [!DNL Target]) |  |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 3.6.2.221<P>52.66.66.192<P>13.235.112.4 |
| Edge42 (Tóquio) | `mboxedge42.tt.omtrdc.net` | 43.206.61.43<P>13.113.73.214<P>52.69.55.232 |
| Edge44 (Costa Leste dos EUA) | `mboxedge44.tt.omtrdc.net` | 54.88.167.98<P>54 164 192 223<P>52.86.86.203 |
| Edge45 (Costa Oeste dos EUA) | `mboxedge45.tt.omtrdc.net` | 52.40.124.129<P>54 148 219 69<P>54.189.208.212 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 54.66.198.142<P>54.253.144.4<P>13.211.218.51 |
| Edge47 (Irlanda) | `mboxedge47.tt.omtrdc.net` | 54.170.28.19<P>52.208.136.136<P>99.80.111.82 |
| Edge48 (Cingapura) | `mboxedge48.tt.omtrdc.net` | 52.76.61.44<P>3.1.141.36<P>18 143 112 116 |

À medida que os balanceadores de carga detectam alterações no perfil de tráfego, ele é dimensionado para cima ou para baixo. O tempo necessário para o Balanceamento de Carga Elástica ser dimensionado pode variar de 1 a 7 minutos, dependendo das alterações detectadas. Quando os balanceadores de carga são dimensionados, eles atualizam o registro DNS com a nova lista de endereços IP. Para garantir que você esteja aproveitando a capacidade aumentada, o Elastic Load Balancing usa uma configuração TTL no registro DNS de 60 segundos.
