---
keywords: email, adbox, adbox de imagem de email
description: Saiba como usar o [!DNL Adobe Target] para testar dinamicamente imagens em emails e até mesmo alterar essas imagens em tempo real quando alguém abre o email.
title: Como testar uma Adbox de imagem de email?
feature: Implement Email
exl-id: 4512741a-567f-41bb-9721-3e1c4f5302e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 79%

---

# Testar uma Adbox de imagem de email

Teste dinamicamente imagens em emails, e até mesmo mude essas imagens em tempo real quando alguém abre o email.

Redirecionadores podem ser utilizados em emails para rastrear cliques e controlar dinamicamente qual página de aterrissagem é acessada.

O teste de imagens de email é feito por meio de versões modificadas das adboxes. Como os clientes de email não permitem cookies, um identificador exclusivo deve ser gerado para cada email. Esse número é anexado ao URL da adbox e em qualquer redirecionador utilizado no email para rastrear cliques do email.

>[!NOTE]
>
>Embora o [!DNL Target] possa oferecer tecnicamente a otimização de imagens no tempo de abertura, cada cliente de email trata o armazenamento em cache de forma diferente, sendo assim, o sucesso será variado. Independentemente do provedor de serviço de email utilizado, o cliente de email que o usuário final usa para abrir o email (aplicativo do Gmail, Outlook, Hotmail e assim por diante) determina se a imagem é realmente obtida no tempo de abertura. Por exemplo, o Gmail armazena quase tudo em cache, assim, a imagem que o usuário final vê depende de quando o Gmail escolhe chamar e armazenar em cache a imagem.

**Código de amostra de uma adbox de imagem de email:**

```
<img src="https://{clientcode}.tt.omtrdc.net/m2/​{clientcode}/ubox/​image?
mbox={email_header}&
mboxDefault=​{http%3A%2F%2Fwww.domain.com%2Fheader.jpg}&
mboxXDomain=disabled&
mboxSession={123456}&
mboxPC={123456}" border=:"0"/>
```

Onde os valores abaixo são específicos para você:

| Valor | Descrição |
|--- |--- |
| clientcode | O código de cliente de sua empresa. Encontre isso em seu at.js listado como `clientCode='yourclientcode'`. Todos os caracteres em minúsculas e sem caracteres especiais. |
| image | O tipo de oferta. É sempre &quot;image&quot; para anúncios gráficos e &quot;page&quot; para redirecionadores. |
| email_header | O nome da adbox. |
| `mboxDefault=http%3A%2F%2Fwww.domain.com%2Fheader.jpg` | Obrigatório. Substitua o URL pelo conteúdo padrão apropriado para sua adbox. Esta deve ser uma referência absoluta e deve ser codificada no URL. |
| `mboxXDomain=disabled` | Instrui [!DNL Target] a não tentar definir um cookie. |
| `mboxSession=123456` e `mboxPC=123456` | Dois valores são exigidos por [!DNL Target] para mesclar o perfil deste usuário com o perfil existente para o seu site. 123456 é o identificador exclusivo gerado por email. Insira esse valor dinamicamente em cada adbox e URL de redirecionador. Esse número deve ser único para cada email enviado. Se um email semanal é enviado para 1.000 destinatários, 1.000 IDs únicas devem ser geradas.<br />O identificador único por email deve ser atribuído ao mboxSession e mboxPC em cada adbox e URL de redirecionador. O formato recomendado para esse identificador é timestamp-NNNNN, onde NNNNN é um número aleatório de 5 dígitos, mas qualquer formato alfanumérico funcionará. Alguns serviços de envio de emails em grandes quantidades e qualquer linguagem de programação podem gerar esse identificador único. |
