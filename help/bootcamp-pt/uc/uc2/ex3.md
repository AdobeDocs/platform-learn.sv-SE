---
title: Bootcamp - Journey Optimizer Create your travel and email message - Brazil
description: Bootcamp - Journey Optimizer Create your travel and email message - Brazil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: d486d1aa-7b8e-4301-91e6-4c84fba0c72a
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# 2.3 Krim sua janda e mensagem de e-mail

Neste övício, você irá configurar a jnada que preca ser acionada quando alguém criar uma conta no site de demonstração.

Faça-inloggning på Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **Home** no Journey Optimizer. Primeiro, verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selecone or sandbox na list. Neste exemplo, nome do sandbox é **Bootcamp**. Você estará na visualização da **Home** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Brott mot en sua jnada

Ingen meny à esquerda, klique em **Journeys**. Em seguida, clique em **Create Journey** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de husnada vazia.

![ACOP](./images/journeyempty.png)

Ingen träningcio-främre, você criou um novo **Event**. Você nomeou o even to `seuSobrenomeAccountCreationEvent` e substituiu `seuSobrenome` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve Consiar este even to como o o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu even to na lista de eventos.

![ACOP](./images/eventlist.png)

Markera en seu even to, arablone solte o even to na tela de Jornada. Sua Jornada agora deve ser semelhante ao seguinte:

![ACOP](./images/journeyevent.png)

Como segunda etapa da husnada, você deve adicionar uma etapa curta de **Wait**. Vá para o lado esquerdo da tela até a seção **Orchestration** para encontrar isso. Você usará atributos de perfil e precará garantir que eles sejam preenchidos no Perfil do Cliente em tempo real.

![ACOP](./images/journeywait.png)

Sua janda agora deve ser semelhante ao seguinte. Ingen lado direito da tela você preca configurar o tempo de espera. Definiera en gemensam minuto. Isso dará bastante tempo para que os atributos do perfil estejam disoníveis após o skilo do even to.

![ACOP](./images/journeywait1.png)

Clique em **OK** para salvar suas alternativ ações.

Como terceira etapa da husnada, você deve adicionar uma ação **Email**. Vá para o lado esquerdo da tela para **Actions**, selecione a ação **Email** e arablone solte a ação no segundo nó da sua hunada. Agora o seguinte será exibido.

![ACOP](./images/journeyactions.png)

Definiera en **kategori** gemensam **marknadsföring** e-postmarkering **e-postyta** som kan återanvändas i e-postmeddelanden. Nesse caso, en **e-postyta** a ser selecionada é E-mail. Certifique-se de que as caixas de seleção **Click on email** e **email opens** estejam marcadas.

![ACOP](./images/journeyactions1.png)

En próximo etapa é criar sua mensagem. Para isso, klicka på em **Redigera innehåll**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Krim a sua mensagem

Para criar sua mensagem, clique em **Edit content**.

![ACOP](./images/journeyactions2.png)

O seguinte será exibido.

![ACOP](./images/journeyactions3.png)

Klicka på ingen campo de texto **Subject line**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece **Olá**

![Journey Optimizer](./images/msg6.png)

En linha de assunto ainda não está prta. Em seguida, você preca trazer o token de personalização para o **Förnamn** que está armazenado em `profile.person.name.firstName` . Ingen meny à esquerda, role para baixo para encontrar o elemento **Person** e clique na seta para visualizar mais campos

![Journey Optimizer](./images/msg7.png)

Agora encontre o elemento **Fullständigt namn** e clique na seta para visualizar mais campos.

![Journey Optimizer](./images/msg8.png)

Por fim, localize or campo **First name** e clique no símbolo **+** ao lado dele. Você verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida, adicione o texto, **agraDecember os a sua inscrição!**. Klicka på **Spara**.

![Journey Optimizer](./images/msg10.png)

Então, você irá retornar para esta tela. Klicka på e-post **Skicka Designer** para criar eller conteúdo e-post.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, será solyckado que você forneça o conteúdo do e-mail através de 3 métodos diferentes:

- **Designa från grunden**: Comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar a estrutura e os components de conteúdo para criar visualmente o conteúdo e-mail.
- **Koda din egen**: Crie seu próprio modelo de e-mail kodificando usando HTML
- **Importera HTML**: Importera modelo HTML existente, que você poderá editar.

Klicka på **Importera HTML**.

![Journey Optimizer](./images/msg12.png)

Arrappe solte o arquivo **mailtemplatebootcamp.html**, que você pode baixa [aqui](../../assets/html/mailtemplatebootcamp.html.zip). Clique em Importar.

![Journey Optimizer](./images/msg13.png)

Você verá este modelo de e-mail padrão:

![Journey Optimizer](./images/msg14.png)

Vamos personalizar o e-mail. Clique ao lado do texto **Olá** e, em seguida, clique no ícone **Add Personalization**.

![Journey Optimizer](./images/msg35.png)

Em seguida, você preca trazer o token de personalização **Förnamn** que está armazenado em `profile.person.name.firstName` . Ingen meny, lokalisera till element **Person**, faça uma busca detail ada no elemento **Fullständigt namn** e clique no ícone **+** para adicionar o campo **Förnamn** ao-redigerare.

Klicka på **Spara**.

![Journey Optimizer](./images/msg36.png)

Agora você verá como o campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

Klicka på em **Save** para salvar sua mensagem.

![Journey Optimizer](./images/msg55.png)

Retorne para o smärtel de mensagens clicando na seta ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você final a criação do seu email de cadastro. Clique na seta no canto superior esquerdo para retornar à sua husnada.

![Journey Optimizer](./images/msg57.png)

Klicka på dem **OK**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publicera en sua jnada

Você ainda preca dar um Nome à sua jnada. Você pode fazer isso clicando no ícone **Properties** no canto superior direito da tela.

![ACOP](./images/journeyname.png)

Você pode fazer isso clicando no item clicar no item &quot;Name&quot; e inserindo o seguinte nome `yourLastName - Account Creation Journey`. Klicka på em **OK** para salvar som mudanças.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jnada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de bekräftmação verde informando que sua jnada agora está Publicada.

![ACOP](./images/published.png)

Você terminou este övício.

Próxima etapa: [2.4 Teste sua janda](./ex4.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
