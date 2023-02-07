---
title: Bootcamp - Customer Journey Analytics - From insights to action - Brazil
description: Bootcamp - Customer Journey Analytics - From insights to action - Brazil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: febeba3596d3f98b2352c5ef8688ee011d25c9fe
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 4.6 Dos insights à ação

## Objetivos

- Entenda como criar um público com base em uma visão coletada no Customer Journey Analytics
- Använd esse público no CDP em tempo real e no Adobe Journey Optimizer

## 4.6.1 Crie uma audiência e publique-a

Em seu projeto, você criou um filtro chamado **Utlysningar** e conseguiu visualizar a kvantidade de usuários que tiveram suas ligações ao call center classificadas como **posivas**. Agora, você poderá criar um segmento com esses usuários e ativação-los em hunadas ou em canais de comunicação.

O primeiro passo é: Ingen smärtsam criado no último övício, selecione a linha **1. Samtalskunskap - positiv**, clique com o botão direito de seu mouse e selecione a opção **Skapa målgrupp från urval**:

![demo](./images/aud1.png)

Em seguida, dê um nome para a sua audiência seguindo o modelo **yourLastName - publiken i USA känner sig positiv**:

![demo](./images/aud2.png)

Note que é posiível ter um preview da audiência que está sendo criada:

![demo](./images/aud3.png)

Para finalizar, clique em **Publikat**:

![demo](./images/aud4.png)

## 4.6.2 Använd sua audiência como parte de um segmento

Voltando para a Adobe Experience Platform, vá em **Segment > Bläddra** e você conseguirá visualizar o seu segmento criado no CJA pronto e disonível para ser usado nas suas ativações e tills vidare!

![demo](./images/aud5.png)

Vamos agora usar esse segmento em uma ativação no Facebook e em uma husnada do cliente!

## 4.6.3 Använda seu segmento na Real-Time CDP em tempo real

Na Adobe Experience Platform, vá em **Segment > Bläddra** e encontra audiência que você criou no CJA:

![demo](./images/aud6.png)

Clique no seu segmento e, em seguida, clique em **Aktivera till mål**:

![demo](./images/aud7.png)

Selecione a destination chamada bootcamp-facebook e, em seguida, clique em Next:

![demo](./images/aud8.png)

Em seguida, clique em Next novamente:

![demo](./images/aud9.png)

Selecione a opção **Målgruppens ursprung** e defina como **Direkt från kunderna** e clique em Next:

![demo](./images/aud10.png)

Por fim, na página **Granska** clique em Finish!

![demo](./images/aud11.png)

Pronto! Agora o seu segmento está vinculado aos públicos personalizados do Facebook.
Agora, vamos utilizar esse segmento no AJO!

## 4.6.4 Använda seu-segment i Adobe Journey Optimizer

Na interface da Adobe Experience Platform clique em Journey Optimizer e, em seguida, no menu ateral esquerdo, clique em **Resor** Han kommer med en kriar uma jnada clicando em **Skapa resa**:

![demo](./images/aud20.png)

![demo](./images/aud21.png)

![demo](./images/aud22.png)

Em seguida, no menu ateral esquerdo, em Eventos, selecione **Segmentkvalificering** e arablono até a jodnada:

![demo](./images/aud23.png)

Em seguida, em **Segment** klippa **Redigera** para selecionar um segmento:

![demo](./images/aud24.png)

Selecone a audiência que você criou no CJA e clique em **Spara**:

![demo](./images/aud25.png)

Pronto! En part daí você pode criar uma jnada para clientes que se Qualificam para esse segmento!

[Gå tillbaka till användarflöde 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
