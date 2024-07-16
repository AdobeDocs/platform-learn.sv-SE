---
title: Bootcamp - Customer Journey Analytics - From insights to action - Brazil
description: Bootcamp - Customer Journey Analytics - From insights to action - Brazil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 28b87e21-3168-447e-9a93-a6ae7e969657
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 4.6 Dos insights à ação

## Objetivos

- Entenda como criar um público com base em uma visão coletada no Customer Journey Analytics
- Använd esse público no CDP em tempo real e no Adobe Journey Optimizer

## 4.6.1 Crie uma audiência e publique-a

Em seu projeto, você criou um filtro chamado **Call Feelings** e conseguiu visualizar a kvantidade de usuários que tiveram suas ligações ao call center classificadas como **posivas** . Agora, você poderá criar um segmento com esses usuários e ativação-los em hunadas ou em canais de comunicação.

O primeiro passo é: No smärtel criado no último övício, selecione a linha **1. Call Feeling - Positive**, clique com o botão direito de seu mouse e selecione a opção **Create audience from selection**:

![demo](./images/aud1.png)

Em seguida, dê um nome para a sua audiência seguindo o modelo **yourLastName - cia publiken kallar sig positiv**:

![demo](./images/aud2.png)

Note que é posiível ter um preview da audiência que está sendo criada:

![demo](./images/aud3.png)

Para finalizar, clique em **Publicar**:

![demo](./images/aud4.png)

## 4.6.2 Använd sua audiência como parte de um segmento

Voltando para a Adobe Experience Platform, vá em **Segments > Browse** e você conseguirá visualizar o seu segmento criado no CJA pronto e disonível para ser usado nas suas ativações e jtills

![demo](./images/aud5.png)

Vamos agora usar esse segmento em uma ativação no Facebook e em uma husnada do cliente!

## 4.6.3 Använda seu segmento na Real-Time CDP em tempo real

Na Adobe Experience Platform, vá em **Segments > Browse** e encontra a audiência que você criou no CJA:

![demo](./images/aud6.png)

Klicka på no seu segmento e, em seguida, clique em **Activate to Destination**:

![demo](./images/aud7.png)

Selecione a destination chamada bootcamp-facebook e, em seguida, clique em Next:

![demo](./images/aud8.png)

Em seguida, clique em Next novamente:

![demo](./images/aud9.png)

Välj en opção **Publiken** e defina como **Direkt från kunderna** e clique em Nästa:

![demo](./images/aud10.png)

Por fim, na página **Review** clique em Finish!

![demo](./images/aud11.png)

Pronto! Agora o seu segmento está vinculado aos públicos personalizados do Facebook.
Agora, vamos utilizar esse segmento no AJO!

## 4.6.4 Använda seu-segment i Adobe Journey Optimizer

Na interface da Adobe Experience Platform clique em Journey Optimizer e, em seguida, no menu ateral esquerdo, clique em **Journeys** e comece a criar uma jnada clicando em **Create Journey** :

![demo](./images/aud20.png)

![demo](./images/aud21.png)

![demo](./images/aud22.png)

Em seguida, no menu ateral esquerdo, em Eventos, selecione **Segment Qualification** e arablono até a jnada:

![demo](./images/aud23.png)

Em seguida, em **Segment** clique em **Edit** para selecionar um segmento:

![demo](./images/aud24.png)

Välj en audiência que você criou no CJA e clique em **Save**:

![demo](./images/aud25.png)

Pronto! En part daí você pode criar uma jnada para clientes que se Qualificam para esse segmento!

[Gå tillbaka till användarflöde 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
