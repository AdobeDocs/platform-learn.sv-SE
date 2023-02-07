---
title: Bootcamp - Mixing physical and digital - Journey Optimizer Create your travel and push - Brazilnotification
description: Bootcamp - Mixing physical and digital - Journey Optimizer Create your travel and push - Brazilnotification
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 1%

---

# 3.3 Krim sua jnada e notificação push

Neste övício, você irá configurar a jnada e a mensagem que preca ser acionada quando alguém inserir uma sinalização (beacon) usando o aplicativo móvel.

Faça-inloggning på Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **Startsida** ingen Journey Optimizer. Primeiro, verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** Vi väljer sandlådelista. Neste exemplo, nome do sandbox é **Bootläger**. Você estará na visualização da **Startsida**  do seu, sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Brott mot en sua jnada

Ingen meny à esquerda, clique em **Resor**. Em seguida, clique em **Skapa resa** para criar uma nova journnada.

![ACOP](./images/createjourney.png)

Você verá uma tela de husnada vazia.

![ACOP](./images/journeyempty.png)

Ingen övício anterior, você criou um novo **Händelse**. Você nomeo o even to `yourLastNameBeaconEntryEvent` e substituiu `yourLastName` bl.a. sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve Consiar este even to como o o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu even to na lista de eventos.

![ACOP](./images/eventlist.png)

Markera en seu even to, arablone solte o even to na tela de jnada. Sua janda agora deve ser semelhante ao seguinte. Clique em **OK** para salvar suas alternações.

![ACOP](./images/journeyevent.png)

Como segunda etapa da husnada, você deve adicionar uma ação **Push**. Vá para o lado esquerdo da tela para **Åtgärder**, selecione a ação **Push** e arablone solte a ação no segundo nó da sua jnada.

![ACOP](./images/journeyactions.png)

Ingen lado direito da tela, agora você deve criar sua notificação push.

Definiera en **Kategori** como **Marknadsföring** e selecione um push surface que allow ite enviar notificações push. Nesse caso, a superfície push a ser selecionada é **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Krim a sua mensagem

Clique em **Redigera innehåll**.

![ACOP](./images/emptymsg.png)

Em seguida, a tela abaixo será exibida:

![ACOP](./images/emailmsglist.png)

Vamos definition o conteúdo da notificação push.

Clique no campo de texto **Titel**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece **Olá**. Clique no ícone de personalização.

![Journey Optimizer](./images/msg6.png)

Agora você preca trazer o token de personalização para o campo **Förnamn** que está armazenado em `profile.person.name.firstName`. Ingen meny à esquerda, selecione **Profilattribut**, role para baixo/navegue para encontrar o elemento **Person** e clique na seta para avançar um nível até chegar ao campo `profile.person.name.firstName`. Clique no ícone **+** para adicionar o campo à tela. Clique em **Spara**.

![Journey Optimizer](./images/msg7.png)

Então, você irá retornar para esta tela. Clique no ícone de personalização ao lado do campo **Brödtext**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escreva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em seguida, clique em  **Sammanhangsberoende attribut** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique em **Händelser**.

![ACOP](./images/jomsg4.png)

Clique no nome do seu even to, que deve ser semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **Montera kontext**.

![ACOP](./images/jomsg6.png)

Clique em **POI-interaktion**.

![ACOP](./images/jomsg7.png)

Clique em **POI-detalj**.

![ACOP](./images/jomsg8.png)

Klick nej **+** icon no **POI-namn**.
Em seguida, o seguinte será exibido. Clique em **Spara**.

![ACOP](./images/jomsg9.png)

Sua mensagem agora está prta. Clique na seta no canto superior esquerdo para retornar à sua husnada.

![ACOP](./images/jomsg11.png)

Clique em **OK**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da husnada, você deve adicionar uma ação  **sendMessageToScreen**. Vá para o lado esquerdo da tela para **Åtgärder**, selecione a ação **sendMessageToScreen** e arablone solte a ação no terceiro nó da sua jnada. Em seguida, você verá a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar uma mensagem no **Slutpunkt** usado pela exibição na loja. A ação **sendMessageToScreen** espera que múltiplas variáveis sejam definidas. Você pode visualizar essas variáveis rolando para baixo até ver **Åtgärdsparametrar**.

![ACOP](./images/jomsg16.png)

Agora você preca definr os valores para cada parâmetro de ação. Siga esta tabela para entender quais valores são necessary ários e onde.

| Parameter | value |
|:-------------:| :---------------:|
| LEVERANS | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| FÖRNAMN | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDLÅDA | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

Para definition esses valores, clique no ícone **Redigera**.

![ACOP](./images/jomsg17.png)

Fyrkant, selecone **Avancerat läge**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. Clique em **OK**.

![ACOP](./images/jomsg19.png)

Repita esse processo para adicionar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao even to`yourLastNameBeaconEntryEvent`. Lembre-se de substituir  `yourLastName` bl.a. sobrenome.

O resulado final deve ser semelhante ao seguinte:

![ACOP](./images/jomsg20.png)

Role para cima e clique em **OK**.

![ACOP](./images/jomsg21.png)

Du måste fortfarande ge din resa ett namn. Du kan göra det genom att klicka på **Egenskaper** i skärmens övre högra hörn.

![ACOP](./images/journeyname.png)

Você pode inserir o nome da jnada aqui. Använd `yourLastName - Beacon Entry Journey`. Clique em **OK** para salvar suas alternações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jnada clicando em **Publicera**.

![ACOP](./images/publishjourney.png)

Clique em **Publicera** novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de bekräftmação verde informando que sua jnada agora está Publicada.

![ACOP](./images/published.png)

Sua janda agora está ativa e pode ser acionada.

Você terminou este övício.

Próxima etapa: [3.4 Testa sua janda](./ex4.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
