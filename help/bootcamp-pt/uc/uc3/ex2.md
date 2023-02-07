---
title: Bootcamp - Blending physical and digital - Journey Optimizer Create your event - Brazil
description: Bootcamp - Blending physical and digital - Journey Optimizer Create your event - Brazil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 3.2 Kriminalvårdsöar till och med

Faça-inloggning på Adobe Journey Optimizer acessando a [Adobe Experience Cloud]. Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a **Startsida** ingen Journey Optimizer. Primeiro, verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** Vi väljer sandlådelista. Neste exemplo, nome do sandbox é **Bootläger**. Você estará na visualização da **Startsida** do seu, sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Ingen meny à esquerda, role para baixo e clique em **Konfigurationer**. Em seguida, clique no botão **Hantera** em Eventos.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos DISoníveis. Clique em **Skapa händelse** para começar a criar seu próprio even to.

![ACOP](./images/emptyevent.png)

Uma nova janela de even to vazia irá aparecer.

Em primeiro lugar, dê um nome ao seu even to como, por example: `yourLastNameBeaconEntryEvent` e adicione uma descrição como, por example: `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certifique-se de que **Typ** está defindo como **Unitary** e, para a seleção de **Typ av händelse-ID**, selecione **Systemgenererat**.

![ACOP](./images/eventidtype.png)

Ett etapa seguinte é a seleção do schema. UM schema foi preparado para este övício. Använd till schema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Fält**. Agora você deve passar o mouse sobre a seção **Fält** e três ícones pop-up serão exibidos. Clique no ícone de **Redigera**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Fält**, ond você deve selecionar algun dos campos que precamos para personalizar a jnada. Escolheremos outros atributos de perfil posteriormente, utilizando os dados já existentes na Adobe Experience Platform

![ACOP](./images/eventfields.png)

Role para baixo até ver o objeto `Place context` e marque a caixa de seleção. Com isso, todo o contexto da localização do cliente será disonibilizado para a servernada. Clique em **OK** para salvar suas alternações.

![ACOP](./images/eventpayloadbr.png)

Em seguida, você deverá ver a tela abaixo. Clique em **Spara** mais uma vez para salvar suas alternações.

![ACOP](./images/eventsave.png)

Till och med agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu even to novamente para abrir a tela **Redigera händelse** mais uma vez. Passera till musobjekt **Fält** para ver os 3 ícones. Clique no ícone **Visa**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo do payload esperado.
Seu even to tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil até visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jnada que você construirá em um dos próximos övícios. Lembre-se deste eventID, você pode precise dele posteriormente.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Clique em **OK** e, em seguida, clique em **Avbryt**.

Você terminou este övício.

Próxima etapa: [3.3 Krim sua jnada e notificação push](./ex3.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
