---
title: Bootcamp - Customer Journey Analytics - Från insikter till handling
description: Bootcamp - Customer Journey Analytics - Från insikter till handling
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 7a38a0a4-46e4-41f2-9a75-316dfde7128f
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 4.6 Från insikter till handling

## Mål

- Förstå hur man bygger en målgrupp baserat på en vy som samlats in i Customer Journey Analytics
- Använd den här målgruppen i Real-Time CDP och Adobe Journey Optimizer

## 4.6.1 Skapa en målgrupp och publicera den

I ditt projekt skapade du ett filter med namnet **Ring samtal** och kunde visa antalet användare som hade sina samtal till callcentret klassificerade som **positivt**. Nu kan du skapa ett segment med de här användarna och aktivera dem på resor eller i kommunikationskanaler.

Det första steget är: Markera rad **1 på panelen som skapades i den senaste övningen. Anropsfunktion - Positiv**, högerklicka och välj alternativet **Skapa målgrupp från urval**:

![demo](./images/aud1.png)

Ge sedan målgruppen ett namn som följer modellen **yourLastName - CJA-målgruppsanropet som känns positivt**:

![demo](./images/aud2.png)

Observera att det går att förhandsgranska den målgrupp som skapas:

![demo](./images/aud3.png)

Klicka slutligen på **Publish**.

![demo](./images/aud4.png)

## 4.6.2 Använda er målgrupp som en del av ett segment

Gå tillbaka till Adobe Experience Platform, gå till **Segment > Bläddra** så ser du att ditt segment som skapats i CJA är klart och tillgängligt att användas i dina aktiveringar och resor!

![demo](./images/aud5.png)

Nu ska vi använda det här segmentet i en aktivering av Facebook och på en kundresa!

## 4.6.3 Använda ditt segment i Real-Time CDP i realtid

I Adobe Experience Platform går du till **Segment > Bläddra** och söker efter den målgrupp du har skapat i CJA:

![demo](./images/aud6.png)

Klicka på ditt segment och sedan på **Aktivera till mål**:

![demo](./images/aud7.png)

Välj målet **bootcamp-facebook** och klicka sedan på **Next**.

![demo](./images/aud8.png)

Klicka på **Nästa** igen.

![demo](./images/aud9.png)

Välj alternativet **Publiken** som har sitt ursprung och ange det som **Direkt från kunderna**. Klicka sedan på **Nästa**.

![demo](./images/aud10.png)

Klicka på **Slutför**.

![demo](./images/aud11.png)

Ditt segment är nu anslutet till Facebook anpassade målgrupper. Nu ska vi använda samma segment i Adobe Journey Optimizer.

## 4.6.4 Använda ditt segment i Adobe Journey Optimizer

I Adobe Experience Platform klickar du på **Journey Optimizer** och sedan på **Resor** på den vänstra menyn. Klicka sedan på **Skapa resa** för att börja skapa en resa.

![demo](./images/aud20.png)

![demo](./images/aud21.png)

![demo](./images/aud22.png)

Välj sedan **Segmentkvalificering** under **Händelser** på den vänstra menyn och dra den till resan:

![demo](./images/aud23.png)

Under Segment klickar du på **Redigera** för att markera ett segment:

![demo](./images/aud24.png)

Markera målgruppen som du skapade tidigare i CJA och klicka på **Spara**.

![demo](./images/aud25.png)

Redo! Härifrån kan ni skapa en resa för kunder som är kvalificerade för detta segment.

[Gå tillbaka till användarflöde 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
