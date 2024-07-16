---
title: Bootcamp - Mixing physical and digital - Journey Optimizer Create your travel and push notification
description: Bootcamp - Mixing physical and digital - Journey Optimizer Create your travel and push notification
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: be8c23ec-c5f8-4abc-849f-994446072a84
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 3.3 Skapa din resa och skicka push-meddelanden

I den här övningen ska du konfigurera den resa och det meddelande som ska utlösas när någon går in i en sändare med mobilappen.

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `Bootcamp`. Om du vill ändra från en sandlåda till en annan klickar du på **Prod** och väljer sandlådan i listan. I det här exemplet heter sandlådan **Bootcamp**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Skapa din resa

Klicka på **Resor** på den vänstra menyn. Klicka sedan på **Skapa resa** för att skapa en ny resa.

![ACOP](./images/createjourney.png)

Då ser du en tom skärm för resan.

![ACOP](./images/journeyempty.png)

I föregående övning skapade du en ny **Event**. Du gav den ett namn som `yourLastNameBeaconEntryEvent` och ersatte `yourLastName` med ditt efternamn. Detta var resultatet av händelseskapandet:

![ACOP](./images/eventdone.png)

Du måste nu ta det här evenemanget som början på den här resan. Du kan göra detta genom att gå till vänster på skärmen och söka efter händelsen i listan med händelser.

![ACOP](./images/eventlist.png)

Markera händelsen, dra och släpp den på arbetsytan för resan. Din resa ser nu ut så här. Klicka på **OK** om du vill spara ändringarna.

![ACOP](./images/journeyevent.png)

Som det andra steget i resan måste du lägga till en **push**-åtgärd. Gå till vänster på skärmen till **Åtgärder**, välj åtgärden **Skjut** och dra och släpp den på den andra noden på resan.

![ACOP](./images/journeyactions.png)

Till höger på skärmen måste du nu skapa ett push-meddelande.

Ange **kategorin** till **Marknadsföring** och välj en push-yta som gör att du kan skicka push-meddelanden. I det här fallet är den push-yta som ska väljas **mmeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Skapa ett meddelande

Klicka på **Redigera innehåll**.

![ACOP](./images/emptymsg.png)

Då ser du det här:

![ACOP](./images/emailmsglist.png)

Låt oss definiera innehållet i push-meddelandet.

Klicka på textfältet **Titel**.

![Journey Optimizer](./images/msg5.png)

Börja skriva **Hi** i textområdet. Klicka på personaliseringsikonen.

![Journey Optimizer](./images/msg6.png)

Du måste nu hämta en personaliseringstoken för fältet **Förnamn** som lagras under `profile.person.name.firstName`. Välj **Profilattribut** på den vänstra menyn, rulla nedåt/navigera för att hitta elementet **Person** och klicka på pilen för att gå en nivå längre tills du når fältet `profile.person.name.firstName`. Klicka på ikonen **+** för att lägga till fältet på arbetsytan. Klicka på **Spara**.

![Journey Optimizer](./images/msg7.png)

Du kommer då tillbaka hit. Klicka på personaliseringsikonen bredvid fältet **Brödtext**.

![Journey Optimizer](./images/msg11.png)

Skriv `Welcome at the ` i textområdet.

![Journey Optimizer](./images/msg12.png)

Klicka sedan på **Sammanhangsberoende attribut** och **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Klicka på **Händelser**.

![ACOP](./images/jomsg4.png)

Klicka på namnet på händelsen som ska se ut så här: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Klicka på **Montera kontext**.

![ACOP](./images/jomsg6.png)

Klicka på **POI Interaction**.

![ACOP](./images/jomsg7.png)

Klicka på **POI-detalj**.

![ACOP](./images/jomsg8.png)

Klicka på ikonen **+** på **POI-namn**.
Då ser du det här. Klicka på **Spara**.

![ACOP](./images/jomsg9.png)

Meddelandet är nu klart. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![ACOP](./images/jomsg11.png)

Klicka på **OK**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Skicka ett meddelande till en skärm

Som det tredje steget i resan måste du lägga till en **sendMessageToScreen**-åtgärd. Gå till vänster på skärmen till **Åtgärder**, markera åtgärden **sendMessageToScreen** och dra och släpp den på den tredje noden på resan. Då ser du det här.

![ACOP](./images/jomsg15.png)

Åtgärden **sendMessageToScreen** är en anpassad åtgärd som publicerar ett meddelande till slutpunkten som används av butiksskärmen. Åtgärden **sendMessageToScreen** förväntar sig ett antal variabler som ska definieras. Du kan se dessa variabler genom att rulla nedåt tills du ser **åtgärdsparametrar**.

![ACOP](./images/jomsg16.png)

Du måste nu ange värden för varje åtgärdsparameter. Följ den här tabellen för att förstå vilka värden som krävs var.

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

{style="table-layout:auto"}

Klicka på ikonen **Redigera** om du vill ange dessa värden.

![ACOP](./images/jomsg17.png)

Välj sedan **Avancerat läge**.

![ACOP](./images/jomsg18.png)

Klistra sedan in värdet baserat på tabellen ovan. Klicka på **OK**.

![ACOP](./images/jomsg19.png)

Upprepa den här processen om du vill lägga till värden för varje fält.

>[!IMPORTANT]
>
>Det finns en referens till händelsen `yourLastNameBeaconEntryEvent` för fältet-ECID. Ersätt `yourLastName` med ditt efternamn.

Slutresultatet ska se ut så här:

![ACOP](./images/jomsg20.png)

Bläddra uppåt och klicka på **OK**.

![ACOP](./images/jomsg21.png)

Du måste fortfarande ge din resa ett namn. Du kan göra det genom att klicka på ikonen **Penna** längst upp till vänster på skärmen.

![ACOP](./images/journeyname.png)

Du kan sedan ange resans namn här. Använd `yourLastName - Beacon Entry Journey`. Klicka på **OK** om du vill spara ändringarna.

![ACOP](./images/journeyname1.png)

Nu kan du publicera din resa genom att klicka på **Publish**.

![ACOP](./images/publishjourney.png)

Klicka på **Publish** igen.

![ACOP](./images/publish1.png)

Då visas ett grönt bekräftelsefält som anger att din resa nu är publicerad.

![ACOP](./images/published.png)

Din resa är nu live och kan utlösas.

Du har nu avslutat den här övningen.

Nästa steg: [3.4 Testa din resa](./ex4.md)

[Gå tillbaka till användarflöde 3](./uc3.md)

[Gå tillbaka till Alla moduler](../../overview.md)
