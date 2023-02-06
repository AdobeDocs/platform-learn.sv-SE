---
title: Bootcamp - Journey Optimizer Create your travel and email message - Brazil
description: Bootcamp - Journey Optimizer Create your travel and email message - Brazil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 3%

---

# 2.3 Krim sua janda e mensagem de e-mail

Neste övício, você irá configurar a jnada que preca ser acionada quando alguém criar uma conta no site de demonstração.

Faça-inloggning på Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **Startsida**  ingen Journey Optimizer. Primeiro, verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** Vi väljer sandlådelista. Neste exemplo, nome do sandbox é **Bootläger**. Você estará na visualização da **Startsida** do seu, sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Brott mot en sua jnada

Ingen meny à esquerda, clique em **Resor**. Em seguida, clique em **Skapa resa** para criar uma nova journnada.

![ACOP](./images/createjourney.png)

Você verá uma tela de husnada vazia.

![ACOP](./images/journeyempty.png)

Ingen övício anterior, você criou um novo **Händelse**. Você nomeo o even to `yourLastNameAccountCreationEvent` e substituiu `yourLastName` bl.a. sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve Consiar este even to como o o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu even to na lista de eventos.

![ACOP](./images/eventlist.png)

Markera en seu even to, arablone solte o even to na tela de Jornada. Sua Jornada agora deve ser semelhante ao seguinte:

![ACOP](./images/journeyevent.png)

Como segunda etapa da hunada, você deve adicionar uma etapa curta de **Vänta**. Vá para o lado esquerdo da tela até a seção **Orchestration** para encontrar isso. Você usará atributos de perfil e precará garantir que eles sejam preenchidos no Perfil do Cliente em tempo real.

![ACOP](./images/journeywait.png)

Sua janda agora deve ser semelhante ao seguinte. Ingen lado direito da tela você preca configurar o tempo de espera. Definiera en gemensam minuto. Isso dará bastante tempo para que os atributos do perfil estejam disoníveis após o skilo do even to.

![ACOP](./images/journeywait1.png)

Clique em **OK** para salvar suas alternações.

Como terceira etapa da husnada, você deve adicionar uma ação **E-post**. Vá para o lado esquerdo da tela para **Åtgärder**, selecione a ação **E-post** e arablone solte a ação no segundo nó da sua jnada. Agora o seguinte será exibido.

![ACOP](./images/journeyactions.png)

Ange **Kategori** till **Marknadsföring** och välj en e-postyta som gör att du kan skicka e-post. I det här fallet är e-postytan som ska väljas **E-post**. Se till att kryssrutorna för **Klicka på e-post** och **e-post öppnas** båda är aktiverade.

Definiera en **Kategori** como **Marknadsföring** e selecione uma superfície de e-mail que behörighetita o envio de e-mail. Nesse caso, a superfície e-mail a ser selecionada é E-mail. Certifique-se de que as caixas de seleção **Klicka på e-post** e **e-post öppnas** estejam marcadas.

![ACOP](./images/journeyactions1.png)

En próximo etapa é criar sua mensagem. Para isso, clique em **Redigera innehåll**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Krim a sua mensagem

Para criar sua mensagem, clique em **Redigera innehåll**.

![ACOP](./images/journeyactions2.png)

O seguinte será exibido.

![ACOP](./images/journeyactions3.png)

Clique no campo de texto **Subject line**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece **Olá**

![Journey Optimizer](./images/msg6.png)

En linha de assunto ainda não está prta. Em seguida, você preca trazer o token de personalização para o **Förnamn** que está armazenado em `profile.person.name.firstName`. Ingen meny à esquerda, role para baixo para encontrar o elemento **Person** e clique na seta para ir um nível mais profundamento.

![Journey Optimizer](./images/msg7.png)

Agora encontre o elemento **Fullständigt namn** e clique na seta para ir um nível mais profundamento.

![Journey Optimizer](./images/msg8.png)

Por fim, localize o campo **Förnamn** e clique no símbolo **+**  aao lado dele. Você verá o token de personalização aparecer no campo de texto.

![Journey Optimizer](./images/msg9.png)

Em seguida, adicione o texto, **agraDecember a sua inscrição!** Clique em Salvar. . Clique em **Spara**.

![Journey Optimizer](./images/msg10.png)

Então, você irá retornar para esta tela. Clique em **E-postdesigner**  para criar o conteúdo do e-mail.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, será solyckado que você forneça o conteúdo do e-mail através de 3 métodos diferentes:

- **Designa från grunden**: Comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar a estrutura e os components de conteúdo para criar visualmente o conteúdo e mail.
- **Koda din egen**: Crie seu próprio modelo de e-mail kodificando usando HTML
- **Importera HTML**: Importe um modelo HTML existente, que você poderá editar.

Clique em **Importera HTML**.

![Journey Optimizer](./images/msg12.png)

Arablonsolte o arquivo **mailmallebootcamp.html**, que você pode baixa [här](../../assets/html/mailtemplatebootcamp.html.zip). Clique em Importar.

![Journey Optimizer](./images/msg13.png)

Você verá este modelo de e-mail padrão:

![Journey Optimizer](./images/msg14.png)

Vamos personalizar o e-mail. Clique ao lado do texto **Olá** e, em seguida, clique no ícone **Lägg till personalisering**.

![Journey Optimizer](./images/msg35.png)

Em seguida, você preca trazer o token de personalização **Förnamn** que está armazenado em `profile.person.name.firstName`. Ingen meny, lokalisera eller element **Person**, faça uma busca detail hada no elemento **Fullständigt namn** e clique no ícone **+** para adicionar o campo **Förnamn** ao editor de expressão.

Clique em **Spara**.

![Journey Optimizer](./images/msg36.png)

Agora você verá como o campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

Clique em **Spara** para salvar sua mensagem.

![Journey Optimizer](./images/msg55.png)

Retorne para o smärtel de mensagens clicando na seta ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você final a criação do seu e-mail de cadastro. Clique na seta no canto superior esquerdo para retornar à sua husnada.

![Journey Optimizer](./images/msg57.png)

Clique em **OK**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publicera en sua jnada

Você ainda preca dar um Nome à sua jnada. Você pode fazer isso clicando no ícone **Egenskaper** ingen canto superior direito da tela.

![ACOP](./images/journeyname.png)

Você ainda preca dar um Nome à sua jnada. Você pode fazer isso clicando no ícone `yourLastName - Account Creation Journey`. Clique em **OK** para salvar as mudanças.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jnada clicando em **Publicera**.

![ACOP](./images/publishjourney.png)

Clique em **Publicera**  novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de bekräftmação verde informando que sua jnada agora está Publicada.

![ACOP](./images/published.png)

Você terminou este övício.

Próxima etapa: [2.4 Testa sua janda](./ex4.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)