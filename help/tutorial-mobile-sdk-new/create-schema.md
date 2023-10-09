---
title: Skapa ett XDM-schema
description: Lär dig hur du skapar ett XDM-schema för mobilappshändelser.
feature: Mobile SDK,Schemas
hide: true
exl-id: 66a3c062-93e5-4183-8fb4-1f72cacb6552
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '1506'
ht-degree: 0%

---

# Skapa ett XDM-schema

Lär dig hur du skapar ett XDM-schema för mobilappshändelser.

Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

## Vad är XDM-scheman?

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner som gör att alla program kan kommunicera med plattformstjänster. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som kan ge insikter på ett snabbare och mer integrerat sätt. Ni får värdefulla insikter från kundåtgärder, kan definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Innan data kan hämtas in till Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera schemafältgrupper.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [grunderna för schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en) eller kursen [Modellera era kundupplevelsedata med XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm).

>[!TIP]
>
>Om du känner till SDR (Analytics Solution Design Reference) kan du se ett schema som en mer robust SDR. Se [Skapa och underhåll ett SDR-dokument (Solution Design Reference)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html?lang=en) för mer information.

## Förutsättningar

Du måste ha behörighet att skapa ett Experience Platform-schema för att kunna slutföra lektionen.

## Utbildningsmål

I den här lektionen kommer du att:

* Skapa ett schema i datainsamlingsgränssnittet
* Lägg till en standardfältgrupp i schemat
* Skapa och lägg till en anpassad fältgrupp i schemat

## Navigera till scheman

1. Logga in på Adobe Experience Cloud.

1. Se till att du är i sandlådan Experience Platform som du använder för den här självstudiekursen.

1. Öppna appväljaren ![Appväxlare](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg)  (längst upp till höger),

1. Välj **[!UICONTROL Datainsamling]** på menyn.

   ![Logga in i Experience Cloud](assets/experiencecloud-login.png)

   >[!NOTE]
   >
   > Kunder som använder plattformsbaserade program som Real-Time CDP bör använda en utvecklingssandlåda för den här självstudiekursen. Andra kunder använder standardproduktionssandlådan.


1. Välj **[!UICONTROL Scheman]** under **[!UICONTROL Datahantering]** till vänster.

   ![taggar, startskärm](assets/mobile-schema-navigate.png)

Du finns nu på huvudschemasidan och visas med en lista över befintliga scheman. Du kan även se flikar som motsvarar grundstenarna i ett schema:

* **Fältgrupper** är återanvändbara komponenter som definierar ett eller flera fält för att samla in specifika data, t.ex. personuppgifter, hotellinställningar eller adress.
* **Klasser** Definiera beteendeaspekterna för de data som schemat innehåller. Till exempel: `XDM ExperienceEvent` hämtar tidsserie, händelsedata och `XDM Individual Profile` hämtar attributdata om en individ.
* **Datatyper** används som referensfälttyper i klasser eller fältgrupper på samma sätt som grundläggande litteralfält.

Ovanstående beskrivningar är en översikt på hög nivå. Mer information finns i [Byggstenar för schema](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schema-building-blocks.html) video eller läs [Grunderna för schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en) i produktdokumentationen.

I den här självstudiekursen använder du fältgruppen Consumer Experience Event och skapar en anpassad som demonstrerar processen.

>[!NOTE]
>
>Adobe fortsätter att lägga till fler standardfältgrupper och de bör användas när det är möjligt, eftersom dessa fält är underförstådda av Experience Platform tjänster och ger större enhetlighet när de används i olika plattformskomponenter. Att använda standardfältgrupper ger påtagliga fördelar som automatisk mappning i Analytics och AI-funktioner i Platform.

## Luma app schema architecture

I ett verkligt scenario kan schemats designprocess se ut så här:

* Samla verksamhetskrav.
* Hitta färdiga fältgrupper som täcker så många krav som möjligt.
* Skapa anpassade fältgrupper för eventuella luckor.

I utbildningssyfte använder du fördefinierade och anpassade fältgrupper.

* **Consumer Experience Event**: Fördefinierad fältgrupp med många vanliga fält.
* **Appinformation**: Anpassad fältgrupp som utformats för att efterlikna koncept i TrackState/TrackAction Analytics.

<!--Later in the tutorial, you can [update the schema](lifecycle-data.md) to include the **[!UICONTROL AEP Mobile Lifecycle Details]** field group.-->

## Skapa ett schema

1. Välj **[!UICONTROL Skapa schema]**.

1. I **[!UICONTROL Välj en klass]** steg i **[!UICONTROL Skapa schema]** guide, välj **[!UICONTROL Experience Event]** under **[!UICONTROL Välj en basklass för schemat]**.

1. Välj **[!UICONTROL Nästa]**.

   ![Basklass för schemaguiden](assets/schema-wizard-base-class.png)

1. I **[!UICONTROL Namn och granskning]** steg i **[!UICONTROL Skapa schema]** guide, ange **[!UICONTROL Visningsnamn för schema]**, till exempel `Luma Mobile Event Schema` och [!UICONTROL Beskrivning], till exempel `Schema for Luma mobile app experience events`.

   >[!NOTE]
   >
   >Om du går igenom den här självstudiekursen med flera personer i en och samma sandlåda, eller om du använder ett delat konto, bör du överväga att lägga till eller föregå en identifiering som en del av namnkonventionen. Använd till exempel `Luma Mobile App Event Schema - Joe Smith` istället för `Luma Mobile App Event Schema`. Se även anteckningen i [Ökning](overview.md).

1. Välj **[!UICONTROL Slutför]** för att avsluta guiden.

   ![Schemanamn och granskning](assets/schema-wizard-name-and-review.png)


1. Välj ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **Lägg till** nästa **[!UICONTROL Fältgrupper]**.

   ![Lägg till fältgrupp](assets/add-field-group.png)

1. Sök efter `Consumer Experience Event`.

1. Välj ![Förhandsgranska](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Preview_18_N.svg) om du vill förhandsgranska fälten och/eller läsa beskrivningen för mer information innan du väljer en fältgrupp.

1. Välj **Consumer Experience Event**.

1. Välj **[!UICONTROL Lägg till fältgrupper]**.

   ![Markerar fältgrupp](assets/schema-select-field-groups.png)

   Du kommer tillbaka till huvudfönstret för schemakomposition där du kan se alla tillgängliga fält.

1. Välj **[!UICONTROL Spara]**.

>[!NOTE]
>
>Tänk på att du inte behöver använda alla fält i en grupp. Du kan även ta bort fält om det gör att schemat blir kortfattat och begripligt. Om det är till hjälp kan du tänka dig ett schema som ett tomt datalager. I appen fyller du i relevanta värden vid rätt tidpunkt.

The [!UICONTROL Consumer Experience Event] fältgruppen har en datatyp som heter [!UICONTROL Webbinformation]som beskriver händelser som sidvisning och länkklick. Just nu finns det ingen paritet för mobilappar med den här funktionen, så du kommer att skapa en egen.

## Skapa en anpassad datatyp

Börja med att skapa en anpassad datatyp som beskriver de två händelserna:

* Skärmvy
* Appinteraktion

1. Välj **[!UICONTROL Datatyper]** -fliken.

1. Välj **[!UICONTROL Skapa datatyp]**.

   ![Välja datatypmeny](assets/schema-datatype-create.png)

1. Ange en **[!UICONTROL Visningsnamn]** och **[!UICONTROL Beskrivning]**, till exempel `App Information` och `Custom data type describing "Screen Views" & "App Actions"`

   ![Ange namn och beskrivning](assets/schema-datatype-name.png)

   >[!TIP]
   >
   > Använd alltid läsbar, beskrivande [!UICONTROL visningsnamn] för era anpassade fält, eftersom detta gör dem mer tillgängliga för marknadsförarna när fälten visas i tjänster som segmentbyggaren.


1. Om du vill lägga till ett fält väljer du ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) -knappen.


1. Det här fältet är ett behållarobjekt för programinteraktion. Ange därför ett fodral **[!UICONTROL Fältnamn]** `appInteraction`, **[!UICONTROL Visningsnamn]** `App Interaction`och markera `Object` från **[!UICONTROL Typ]** lista.

1. Välj **[!UICONTROL Använd]**.

   ![Lägga till en ny programåtgärdshändelse](assets/schema-datatype-app-action.png)

1. Om du vill mäta hur ofta en åtgärd har inträffat lägger du till ett fält genom att markera ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) knappen bredvid **[!UICONTROL appInteraction]** objekt som du skapade.

1. Ge den en kamelväska **[!UICONTROL Fältnamn]** `appAction`, **[!UICONTROL Visningsnamn]** av `App Action` och **[!UICONTROL Typ]** `Measure`.

   Det här steget motsvarar ett lyckat evenemang i Adobe Analytics.

1. Välj **[!UICONTROL Använd]**.

   ![Lägger till namnfält för åtgärd](assets/schema-datatype-action-name.png)

1. Lägg till ett fält som beskriver typen av interaktion genom att markera ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) knappen bredvid **[!UICONTROL appInteraction]** -objekt.

1. Ge den en **[!UICONTROL Fältnamn]** `name`, **[!UICONTROL Visningsnamn]** av `Name` och **[!UICONTROL Typ]** `String`.

   Det här steget motsvarar en dimension i Adobe Analytics.

   ![Markering används](assets/schema-datatype-apply.png)

1. Rulla längst ned på den högra listen och välj **[!UICONTROL Använd]**.

1. Skapa en `appStateDetails` objekt som innehåller **[!UICONTROL Mät]** fältet anropades `screenView` och två **[!UICONTROL Sträng]** fält anropade `screenName` och `screenType`följer du samma steg som när du skapade **[!UICONTROL appInteraction]** -objekt.

1. Välj **[!UICONTROL Spara]**.

   ![Slutligt tillstånd för datatyp](assets/schema-datatype-final.png)

## Lägga till en anpassad fältgrupp

Lägg nu till en anpassad fältgrupp med din anpassade datatyp:

1. Öppna schemat som du skapade tidigare i den här lektionen.

1. Välj ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Lägg till]** nästa **[!UICONTROL Fältgrupper]**.

   ![Lägger till ny fältgrupp](assets/schema-fieldgroup-add.png)

1. Välj **[!UICONTROL Skapa ny fältgrupp]**.

1. Ange en **[!UICONTROL Visningsnamn]** och **[!UICONTROL Beskrivning]**, till exempel `App Interactions` och `Fields for app interactions`.

1. Välj **Lägg till fältgrupper**.

   ![Ange namn och beskrivning](assets/schema-fieldgroup-name.png)

1. Välj **[!UICONTROL Appinteraktioner**].

1. Lägg till ett fält i schemats rot genom att markera ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) intill schemanamnet.

1. Ange en **[!UICONTROL Fältnamn]** av `appInformation`, a **[!UICONTROL Visningsnamn]** av `App Information`och en **[!UICONTROL Typ]** av `App Information`.

1. Välj **[!UICONTROL Appinteraktioner]** från **[!UICONTROL Fältgrupp]** för att tilldela fälten till den nya fältgruppen.

1. Välj **[!UICONTROL Använd]**.

1. Välj **[!UICONTROL Spara]**.

   ![Markering används](assets/schema-fieldgroup-apply.png)

>[!NOTE]
>
>Anpassade fältgrupper placeras alltid under din Experience Cloud-organisationsidentifierare.


>[!SUCCESS]
>
>Nu har du ett schema att använda för resten av självstudiekursen.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Skapa en [!UICONTROL datastream]](create-datastream.md)**
