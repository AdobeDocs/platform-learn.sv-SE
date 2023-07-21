---
title: Bootcamp - Journey Optimizer Create your event - Brazil
description: Bootcamp - Journey Optimizer Create your event - Brazil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Kriminalvårdsdagen

Faça-inloggning på Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **Startsida** ingen Journey Optimizer. Primeiro, verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para outro, clique em Prod e selecione o sandbox na list. Neste exemplo, nome do sandbox é **Bootläger**. Você estará na visualização da **Startsida** do seu, sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Ingen meny à esquerda, role para baixo e clique em **Konfigurationer**. Em seguida, clique no botão **Hantera** abaixo de **Händelser**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos DISoníveis. Clique em **Skapa händelse** para começar a criar seu próprio even to.

![ACOP](./images/emptyevent.png)

Uma nova janela de even to vazia irá aparecer.

![ACOP](./images/emptyevent1.png)

Em primeiro lugar, dê um nome ao seu even to como, por example: `seuSobrenomeAccountCreationEvent` e adicione uma descrição como, por example: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certifique-se de que **Typ** está defindo como **Unitary** e, para a seleção de **Typ av händelse-ID**, selecione **Systemgenererat**.

![ACOP](./images/eventidtype.png)

Ett etapa seguinte é a seleção do schema. UM schema foi preparado para este övício. Använd till schema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Fält**. Agora você deve passar o mouse sobre a seção **Fält** e três ícones pop-up serão exibidos. Clique no ícone **Redigera**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Fält**, ond você deve selecionar algun dos campos que precamos para personalizar o e-mail. Escolheremos outros atributos de perfil posteriormente, utilizando os dados já existentes na Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Inget objekt `_experienceplatform.demoEnvironment`, pcertifique-se de selecionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Inget objekt `_experienceplatform.identification.core`, certifique-se de selecionar o campo **e-post**.

![ACOP](./images/eventpayloadbrid.png)

Clique em **OK** till para salvar suas alternações.

![ACOP](./images/saveok.png)

Em seguida, a tela abaixo deve ser exibida. Clique em **Spara**  mais uma vez para salvar suas alternações...

![ACOP](./images/eventsave.png)

Till och med agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu even to novamente para abrir mais uma vez a tela **Redigera händelse**. Passera till musobjekt **Fält** para ver os 3 ícones outra vez. Clique no ícone **Visa nyttolast**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo da carga útil esperada.
Seu even to tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil (nyttload) até visualizar `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jnada que você construirá em um dos próximos övícios. Lembre-se deste eventID, você pode precise dele posteriormente.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Clique em **OK** e, em seguida, clique em **Avbryt**.

Agora você terminou este övício.

Próxima etapa: [ 2.3 Crie sua mensagem de e-mail](./ex3.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
