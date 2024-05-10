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

Logga in på Adobe Journey Optimizer genom att [Adobe Experience Cloud](https://experience.adobe.com). Klicka **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till **Startsida**  i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas anropas `Bootcamp`. Om du vill ändra från en sandlåda till en annan klickar du på **Prod** och välj sandlådan i listan. I det här exemplet heter sandlådan **Bootläger**. Då är du i **Startsida** vy över din sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Skapa din resa

Klicka på **Resor**. Klicka på Nästa **Skapa resa** för att skapa en ny resa.

![ACOP](./images/createjourney.png)

Då ser du en tom skärm för resan.

![ACOP](./images/journeyempty.png)

I föregående övning skapade du en ny **Händelse**. Du namngav den så här `yourLastNameBeaconEntryEvent` och ersatt `yourLastName` med ditt efternamn. Detta var resultatet av händelseskapandet:

![ACOP](./images/eventdone.png)

Du måste nu ta det här evenemanget som början på den här resan. Du kan göra detta genom att gå till vänster på skärmen och söka efter händelsen i listan med händelser.

![ACOP](./images/eventlist.png)

Markera händelsen, dra och släpp den på arbetsytan för resan. Din resa ser nu ut så här. Klicka **OK** för att spara ändringarna.

![ACOP](./images/journeyevent.png)

Som det andra steget på resan måste du lägga till en **Push** åtgärd. Gå till skärmens vänstra sida för att **Åtgärder** väljer du **Push** och sedan dra och släppa det på den andra noden på din resa.

![ACOP](./images/journeyactions.png)

Till höger på skärmen måste du nu skapa ett push-meddelande.

Ange **Kategori** till **Marknadsföring** och välj en push-yta som gör att du kan skicka push-meddelanden. I det här fallet är den push-yta som ska markeras **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Skapa ett meddelande

Klicka **Redigera innehåll**.

![ACOP](./images/emptymsg.png)

Då ser du det här:

![ACOP](./images/emailmsglist.png)

Låt oss definiera innehållet i push-meddelandet.

Klicka på **Titel** textfält.

![Journey Optimizer](./images/msg5.png)

Börja skriva i textområdet **Hej**. Klicka på personaliseringsikonen.

![Journey Optimizer](./images/msg6.png)

Du måste nu ta in en token för anpassning för fältet **Förnamn** som lagras under `profile.person.name.firstName`. Välj **Profilattribut**, bläddra nedåt/navigera för att hitta **Person** och klicka på pilen för att gå en nivå längre tills du når fältet `profile.person.name.firstName`. Klicka på **+** om du vill lägga till fältet på arbetsytan. Klicka **Spara**.

![Journey Optimizer](./images/msg7.png)

Du kommer då tillbaka hit. Klicka på ikonen för anpassning bredvid fältet **Brödtext**.

![Journey Optimizer](./images/msg11.png)

Skriv i textområdet `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

Klicka på Nästa **Sammanhangsberoende attribut** och sedan **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Klicka **Händelser**.

![ACOP](./images/jomsg4.png)

Klicka på namnet på din händelse som ska se ut så här: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Klicka **Montera kontext**.

![ACOP](./images/jomsg6.png)

Klicka **POI Interaction**.

![ACOP](./images/jomsg7.png)

Klicka **POI-detalj**.

![ACOP](./images/jomsg8.png)

Klicka på **+** ikon på **POI name**.
Då ser du det här. Klicka **Spara**.

![ACOP](./images/jomsg9.png)

Meddelandet är nu klart. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![ACOP](./images/jomsg11.png)

Klicka **OK**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Skicka ett meddelande till en skärm

Som det tredje steget på resan måste du lägga till en **sendMessageToScreen** åtgärd. Gå till skärmens vänstra sida för att **Åtgärder** väljer du **sendMessageToScreen** och sedan dra och släppa det på den tredje noden på din resa. Då ser du det här.

![ACOP](./images/jomsg15.png)

The **sendMessageToScreen** är en anpassad åtgärd som publicerar ett meddelande till slutpunkten som används av butiksskärmen. The **sendMessageToScreen** för åtgärden förväntas ett antal variabler som ska definieras. Du kan se dessa variabler genom att rulla nedåt tills du ser dem **Åtgärdsparametrar**.

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

Klicka på knappen **Redigera** -ikon.

![ACOP](./images/jomsg17.png)

Nästa, välj **Avancerat läge**.

![ACOP](./images/jomsg18.png)

Klistra sedan in värdet baserat på tabellen ovan. Klicka **OK**.

![ACOP](./images/jomsg19.png)

Upprepa den här processen om du vill lägga till värden för varje fält.

>[!IMPORTANT]
>
>För fältet ECID finns en referens till händelsen `yourLastNameBeaconEntryEvent`. Se till att ersätta `yourLastName` efter ditt efternamn.

Slutresultatet ska se ut så här:

![ACOP](./images/jomsg20.png)

Bläddra uppåt och klicka **OK**.

![ACOP](./images/jomsg21.png)

Du måste fortfarande ge din resa ett namn. Du kan göra det genom att klicka på **Penna** ikonen längst upp till vänster på skärmen.

![ACOP](./images/journeyname.png)

Du kan sedan ange resans namn här. Använd `yourLastName - Beacon Entry Journey`. Klicka **OK** för att spara ändringarna.

![ACOP](./images/journeyname1.png)

Nu kan du publicera din resa genom att klicka **Publicera**.

![ACOP](./images/publishjourney.png)

Klicka **Publicera** igen.

![ACOP](./images/publish1.png)

Då visas ett grönt bekräftelsefält som anger att din resa nu är publicerad.

![ACOP](./images/published.png)

Din resa är nu live och kan utlösas.

Du har nu avslutat den här övningen.

Nästa steg: [3.4 Testa din resa](./ex4.md)

[Gå tillbaka till användarflöde 3](./uc3.md)

[Gå tillbaka till Alla moduler](../../overview.md)
