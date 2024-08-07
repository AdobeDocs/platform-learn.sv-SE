---
title: Bootcamp - Blending physical and digital - Journey Optimizer Create your event - Brazil
description: Bootcamp - Blending physical and digital - Journey Optimizer Create your event - Brazil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 2133b560-09d8-419d-bb99-05d0f3df52cc
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 3.2 Kriminalvårdsdagen

Faça-inloggning på Adobe Journey Optimizer acessando a [Adobe Experience Cloud]. Klicka på **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redireccionado para a **Home** no Journey Optimizer. Primeiro, verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selecone or sandbox na list. Neste exemplo, nome do sandbox é **Bootcamp**. Você estará na visualização da **Home** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Ingen meny à esquerda, role para baixo e clique em **Configurations**. Fem seguida, clique no botão **Manage** em Eventos.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos DISoníveis. Klicka på em **Skapa händelse** para começar a criar seu próprio even to.

![ACOP](./images/emptyevent.png)

Uma nova janela de even to vazia irá aparecer.

Em primeiro lugar, dê um nome ao seu even to como, por example: `yourLastNameBeaconEntryEvent` e adicione uma descrição como, por example: `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certifique-se de que **Type** está defindo como **Unitary** e, para a seleção de **Event ID Type**, selecione **System Generated** .

![ACOP](./images/eventidtype.png)

Ett etapa seguinte é a seleção do schema. UM schema foi preparado para este övício. Använd schemat `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Fields**. Agora você deve passar o mouse sobre a seção **Fields** e três ícones pop-up serão exibidos. Klicka på ingen ícone de **Edit**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Fields**, ond você deve selecionar algun dos campos que precamos para personalizar a jenada. Escolheremos outros atributos de perfil posteriormente, utilizando os dados já existentes na Adobe Experience Platform

![ACOP](./images/eventfields.png)

Role para baixo até ver o object `Place context` e marque a caixa de seleção. Com isso, todo o contexto da localização do cliente será disonibilizado para a servernada. Clique em **OK** para salvar suas alternativ ações.

![ACOP](./images/eventpayloadbr.png)

Em seguida, você deverá ver a tela abaixo. Clique em **Save** mais uma vez para salvar suas alternações.

![ACOP](./images/eventsave.png)

Till och med agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Klicka på no seu even to novamente para abrir a tela **Edit Event** mais uma vez. Passe o mouse sobre **Fields** para ver os 3 ícones. Klicka på ingen ícone **View**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo do payload esperado.
Seu even to tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil até visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jnada que você construirá em um dos próximos övícios. Lembre-se deste eventID, você pode precise dele posteriormente.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Klicka på em **OK** e, em seguida, clique em **Cancelar**.

Você terminou este övício.

Próxima etapa: [3.3 Crie sua jnada e notificação push](./ex3.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
