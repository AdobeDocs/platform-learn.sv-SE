---
title: Skapa ett XDM-schema
description: Lär dig hur du skapar ett XDM-schema för mobilappshändelser.
exl-id: c6b0d030-437a-4afe-b7d5-5a7831877983
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 0%

---

# Skapa ett XDM-schema

Lär dig hur du skapar ett XDM-schema för mobilappshändelser.

Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

## Vad är XDM-scheman?

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner som gör att alla program kan kommunicera med plattformstjänster. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som kan ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och uttrycka kundattribut i personaliseringssyfte.

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Innan data kan hämtas in till Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera schemafältgrupper.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [grunderna för schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en) eller kursen [Modellera era kundupplevelsedata med XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm).

>[!TIP]
>
>Om du känner till SDR (Analytics Solution Design Reference) kan du se ett schema som en mer robust SDR.

## Förutsättningar

Du måste ha behörighet att skapa ett Experience Platform-schema för att kunna slutföra lektionen.

## Utbildningsmål

I den här lektionen kommer du att:

* Skapa ett schema i datainsamlingsgränssnittet
* Lägg till en standardfältgrupp i schemat
* Skapa och lägg till en anpassad fältgrupp i schemat

## Navigera till scheman

1. Logga in på Adobe Experience Cloud.

1. Öppna appväljaren och välj **[!UICONTROL Datainsamling]**

   ![3x3-listruta](assets/mobile-schema-navigate1.png)

1. Se till att du är i sandlådan Experience Platform som du använder för den här självstudiekursen.

   >[!NOTE]
   >
   > Kunder som använder plattformsbaserade program som CDP i realtid bör använda en utvecklingssandlåda för den här kursen. Andra kunder använder standardproduktionssandlådan.


1. Välj **[!UICONTROL Scheman]** under **[!UICONTROL Datahantering]**.

   ![taggar, startskärm](assets/mobile-schema-navigate3.png)

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

I utbildningssyfte kommer du att använda färdiga och anpassade fältgrupper.

* **Consumer Experience Event**: Fördefinierad fältgrupp som har många vanliga fält.
* **Appinformation**: Anpassad fältgrupp som utformats för att efterlikna koncept i TrackState/TrackAction Analytics.

<!--Later in the tutorial, you can [update the schema](lifecycle-data.md) to include the **[!UICONTROL AEP Mobile Lifecycle Details]** field group.-->

## Skapa ett schema

1. Välj **[!UICONTROL Skapa schema]** för att visa alternativmenyn väljer du **[!UICONTROL XDM ExperienceEvent]**.

   ![Välja ExperienceEvent i listrutan](assets/mobile-schema-create.png)

1. Sök efter `Consumer Experience Event`.

1. Du kan förhandsgranska fälten och/eller läsa beskrivningen för mer information innan du väljer.

1. Markera kryssrutan och sedan **[!UICONTROL Lägg till fältgrupper]**.

   ![Markerar fältgrupp](assets/mobile-schema-select-field-groups.png)

   Du kommer tillbaka till huvudfönstret för schemakomposition där du kan se alla tillgängliga fält.

1. Ge schemat ett namn genom att välja **[!UICONTROL Namnlöst schema]** överst till vänster och sedan en **[!UICONTROL Visningsnamn]** &amp; **[!UICONTROL Beskrivning]**, till exempel `Luma Tutorial Mobile` och `"Luma App" schema for Adobe Tutorial`

1. Välj **[!UICONTROL Spara]**.

   ![Markering används](assets/mobile-schema-name-save.png)

>[!NOTE]
>
>Tänk på att du inte behöver använda alla fält i en grupp. Om det är till hjälp kan du tänka dig ett schema som ett tomt datalager. I appen fyller du i relevanta värden vid rätt tidpunkt.
>
>The `Consumer Experience Event` har en datatyp som kallas `Web information`som beskriver händelser som sidvisning och länkklick. Just nu finns det ingen paritet för mobilappar med den här funktionen, så du kommer att skapa en egen.

## Skapa en anpassad datatyp

Börja med att skapa en anpassad datatyp som beskriver de två händelserna:

* Skärmvy
* Appinteraktion

1. Välj **[!UICONTROL Datatyper]** tabbtangenten och sedan **[!UICONTROL Skapa datatyp]**.

   ![Välja datatypmeny](assets/mobile-schema-datatype-create.png)

1. Ge den en **[!UICONTROL Visningsnamn]** och **[!UICONTROL Beskrivning]**, till exempel `App Information` och `Custom data type describing "Screen Views" & "App Actions"`

   ![Ange namn och beskrivning](assets/mobile-schema-datatype-name.png)

   >[!TIP]
   >
   > Använd alltid läsbar, beskrivande [!UICONTROL visningsnamn] för era anpassade fält, eftersom detta gör dem mer tillgängliga för marknadsförarna när fälten visas i tjänster som segmentbyggaren.


1. Om du vill lägga till ett fält väljer du knappen (+).

   Det här fältet är ett behållarobjekt för programinteraktion. Ge den en kamelväska **[!UICONTROL Fältnamn]** `appInteraction`, **[!UICONTROL visningsnamn]** `App Interaction`och **[!UICONTROL type]** `Object`.

1. Välj **[!UICONTROL Använd]**.

   ![Lägga till en ny programåtgärdshändelse](assets/mobile-schema-datatype-app-action.png)

1. Om du vill mäta hur ofta en åtgärd har inträffat lägger du till ett fält genom att markera knappen (+) bredvid `appInteraction` objekt som du skapade.

1. Ge den en kamelväska **[!UICONTROL Fältnamn]** `appAction`, **[!UICONTROL visningsnamn]** av `App Action` och **[!UICONTROL type]** `Measure`.

   Det här steget motsvarar ett lyckat evenemang i Adobe Analytics.

1. Välj **[!UICONTROL Använd]**.

   ![Lägger till namnfält för åtgärd](assets/mobile-schema-datatype-action-name.png)

1. Lägg till ett fält som beskriver interaktionstypen genom att markera knappen (+) bredvid `appInteraction` -objekt.

1. Ge den en **[!UICONTROL Fältnamn]** `name`, **[!UICONTROL visningsnamn]** av `Name` och **[!UICONTROL type]** `String`.

   Det här steget motsvarar en dimension i Adobe Analytics.

   ![Markering används](assets/mobile-schema-datatype-apply.png)

1. Rulla längst ned på den högra listen och välj **[!UICONTROL Använd]**.

1. Följ samma mönster för att skapa en `appStateDetails` objekt som innehåller ett mätfält som kallas `screenView` och två strängar som kallas `screenName` och `screenType`.

1. Välj **[!UICONTROL Spara]**.

   ![Slutligt tillstånd för datatyp](assets/mobile-schema-datatype-final.png)

## Lägg till en anpassad fältgrupp

Lägg nu till en anpassad fältgrupp med din anpassade datatyp:

1. Öppna schemat som du skapade tidigare i den här lektionen.

1. Välj **[!UICONTROL Lägg till]** nästa **[!UICONTROL Fältgrupper]**.

   ![Lägger till ny fältgrupp](assets/mobile-schema-fieldgroup-add.png)

1. Den här gången skapar du en anpassad fältgrupp genom att välja **[!UICONTROL Skapa ny fältgrupp]** alternativknapp intill överkanten och sedan ange ett namn och en beskrivning, till exempel `App Interactions` och `Fields for app interactions`.

   ![Ange namn och beskrivning](assets/mobile-schema-fieldgroup-name.png)

1. Lägg till ett fält i schemats rot från huvuddispositionsskärmen.

1. Markera (+) bredvid schemats namn.

1. Ange en **[!UICONTROL Fältnamn]** av `appInformation`, ett visningsnamn för `App Information`.

1. Välj `App Information` från **[!UICONTROL Typ]** den datatyp du skapade i föregående övning.

1. Välj **[!UICONTROL Använd]**.

   ![Markering används](assets/mobile-schema-fieldgroup-apply.png)

>[!NOTE]
>
>Anpassade fältgrupper placeras alltid under din Experience Cloud-organisationsidentifierare.
>
>`_techmarketingdemos` ersätts med din organisations unika värde.

Nu har du ett schema att använda för resten av självstudiekursen.

Nästa: **[Skapa en [!UICONTROL datastream]](create-datastream.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)