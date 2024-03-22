---
keywords: implementar, implementação, lista de permissões, lista branca, lista de permissões, lista de permissões, borda, bordas, $9
description: Incluir na lista de permissões Exibir uma lista de hosts para ajudá-lo a migrar [!DNL Adobe Target] bordas (nós de fornecimento distribuídos geograficamente que garantem tempos de resposta ideais para os usuários finais).
title: Como Incluir na lista de permissões? [!DNL Target] Nós de borda?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 49b6572c0d414ab304712691c97794bb0b1e3781
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# ➡ Incluir na lista de permissões [!DNL Target] nós de borda

Informações e uma lista atualizada de hosts para ajudá-lo a realizar a inclui na lista de permissões [!DNL Adobe Target] bordas.

Uma borda é uma arquitetura de fornecimento distribuída geograficamente que garante tempos de resposta ideais para usuários finais que solicitem o conteúdo, independentemente de sua localização. Cada nó de borda tem todas as informações necessárias para responder à solicitação de conteúdo do usuário e rastrear os dados de análise dessa solicitação. As solicitações do usuário são roteadas para o nó de borda mais próximo. Para obter mais informações, consulte [A rede de borda](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Incluir na lista de permissões Você pode mudar a imagem [!DNL Target] nós de borda, se desejado.

>[!IMPORTANT]
>
>Incluir na lista de permissões Além do recurso de tradução de endereço de rede (NAT) de endereços IP de [!DNL Target] bordas e [!DNL Target] endereços IP de borda discutidos no artigo, você também deve incluir na lista de permissões todos [!DNL Adobe Analytics] Blocos de endereço IP.
>
>Para obter mais informações, consulte [Todos os blocos de endereço IP do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} no *Notas técnicas do Adobe Analytics* documentação.
>
>[!DNL Adobe Target] A infraestrutura do está sendo atualizada e os clientes que desejam atualizar endereços de inclui na lista de permissões do devem usar ambos os conjuntos de IPs. Se isso não for feito, os clientes que usam implementações do lado do servidor ou híbridas nas quais as chamadas da API do Target para busca de experiências são originadas de uma rede atrás de um firewall configurado para usar um incluo na lista de permissões.
>
>Todas as Bordas4 *x* os endereços listados nas duas tabelas abaixo estão programados para serem atualizados em 9 de agosto de 2023.

## NAT (Network Address Translation, tradução de endereço de rede) de endereços IP [!DNL Target] bordas

Lista de endereços IP de saída de [!DNL Target] bordas. ➡ Incluir na lista de permissões esses IPs se você planeja ter [!DNL Target] entre em contato com os serviços.

| Local da borda | Endereços IP de saída |
| --- | --- |
| Edge41 (Mumbai) | 3.6.2.221<br />13.235.112.4 <br />52.66.66.192 |
| Edge42 (Tóquio) | 52.69.55.232<br />43.206.61.43 <br />13.113.73.214 |
| Edge44 (Costa Leste dos EUA) | 54 164 192 223<br />52.86.86.203 <br />54.88.167.98 |
| Edge45 (Costa Oeste dos EUA) | 52.40.124.129<br />54 148 219 69 <br />54.189.208.212 |
| Edge46 (Sydney) | 54.253.144.4<br />54.66.198.142 <br />13.211.218.51 |
| Edge47 (Irlanda) | 52.208.136.136<br />54.170.28.19 <br />99.80.111.82 |
| Edge48 (Cingapura) | 3.1.141.36<br />18 143 112 116 <br />52.76.61.44 |

## [!DNL Target] endereços IP de borda

Lista de endereços IP de [!DNL Target] bordas. ➡ Inclua na lista de permissões esses IPs se quiser fazer chamadas de API para o [!DNL Target] bordas.

Essa lista será alterada com frequência, à medida que os balanceadores de carga aumentarem e diminuírem com base nos perfis de tráfego.

| Local da borda | Domínio | Endereço IP |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(onde CLIENTCODE é o seu [!DNL Target] client ID) |  |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 15.206.104.6<br />3.109.14.178 <br />13 234 139 131 |
| Edge42 (Tóquio) | `mboxedge42.tt.omtrdc.net` | 52.194.84.34<br />3.115.158.39 <br />18 180 123 21 |
| Edge44 (Costa Leste dos EUA) | `mboxedge44.tt.omtrdc.net` | 54.205.210.54<br />23.20.189.8 <br />35 169 173 155 |
| Edge45 (Costa Oeste dos EUA) | `mboxedge45.tt.omtrdc.net` | 35 161 163 45<br />44 230 114 101 <br />35 161 120 22 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 3 104 142 61<br />52.62.4.152 <br />54 253 105 140 |
| Edge47 (Irlanda) | `mboxedge47.tt.omtrdc.net` | 18.203.168.186<br />54 228 83 91 <br />54 217 181 83 |
| Edge48 (Cingapura) | `mboxedge48.tt.omtrdc.net` | 54.179.6.70<br />13.215.150.94 <br />18.136.47.70 |

À medida que os balanceadores de carga detectam alterações no perfil de tráfego, ele é dimensionado para cima ou para baixo. O tempo necessário para o Balanceamento de Carga Elástica ser dimensionado pode variar de 1 a 7 minutos, dependendo das alterações detectadas. Quando os balanceadores de carga são dimensionados, eles atualizam o registro DNS com a nova lista de endereços IP. Para garantir que você esteja aproveitando a capacidade aumentada, o Elastic Load Balancing usa uma configuração TTL no registro DNS de 60 segundos.
