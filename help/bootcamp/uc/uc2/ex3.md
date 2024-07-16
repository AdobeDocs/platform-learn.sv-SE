---
title: Bootcamp - Journey Optimizer Skapa din resa och ditt e-postmeddelande
description: Bootcamp - Journey Optimizer Skapa din resa och ditt e-postmeddelande
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: 138a70fa-fe50-4585-b47f-150db4770c3d
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 2.3 Skapa din resa och ditt e-postmeddelande

I den här övningen konfigurerar du den resa som behöver utlösas när någon skapar ett konto på demowebbplatsen.

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `Bootcamp`. Om du vill ändra från en sandlåda till en annan klickar du på **Prod** och väljer sandlådan i listan. I det här exemplet heter sandlådan **Bootcamp**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Skapa din resa

Klicka på **Resor** på den vänstra menyn. Klicka sedan på **Skapa resa** för att skapa en ny resa.

![ACOP](./images/createjourney.png)

Då ser du en tom skärm för resan.

![ACOP](./images/journeyempty.png)

I föregående övning skapade du en ny **Event**. Du gav den ett namn som `yourLastNameAccountCreationEvent` och ersatte `yourLastName` med ditt efternamn. Detta var resultatet av händelseskapandet:

![ACOP](./images/eventdone.png)

Du måste nu ta det här evenemanget som början på den här resan. Du kan göra detta genom att gå till vänster på skärmen och söka efter händelsen i listan med händelser.

![ACOP](./images/eventlist.png)

Markera händelsen, dra och släpp den på arbetsytan på resan. Din resa ser nu ut så här:

![ACOP](./images/journeyevent.png)

Som det andra steget i resan måste du lägga till ett kort **Vänta**-steg. Gå till vänster på skärmen till avsnittet **Orchestration** om du vill hitta det här. Du kommer att använda profilattribut och måste se till att de är ifyllda i kundprofilen i realtid.

![ACOP](./images/journeywait.png)

Din resa ser nu ut så här. Till höger på skärmen måste du konfigurera väntetiden. Ställ in den på 1 minut. Detta ger mycket tid för profilattributen att vara tillgängliga när händelsen har utlösts.

![ACOP](./images/journeywait1.png)

Klicka på **OK** om du vill spara ändringarna.

Som det tredje steget på resan måste du lägga till en **e-poståtgärd**. Gå till vänster på skärmen till **Åtgärder**, välj åtgärden **E-post** och dra och släpp den på den andra noden på resan. Nu ser du det här.

![ACOP](./images/journeyactions.png)

Ange **kategorin** till **Marknadsföring** och välj en e-postyta som gör att du kan skicka e-post. I det här fallet är e-postytan som ska väljas **E-post**. Kontrollera att kryssrutorna för **klick på e-post** och **e-post** är aktiverade.

![ACOP](./images/journeyactions1.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka på **Redigera innehåll**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Skapa ett meddelande

Klicka på **Redigera innehåll** om du vill skapa ditt meddelande.

![ACOP](./images/journeyactions2.png)

Nu ser du det här.

![ACOP](./images/journeyactions3.png)

Klicka på textfältet **Ämnesrad**.

![Journey Optimizer](./images/msg5.png)

Börja skriva **Hi** i textområdet

![Journey Optimizer](./images/msg6.png)

Ämnesraden är inte färdig än. Därefter måste du hämta en personaliseringstoken för fältet **Förnamn** som lagras under `profile.person.name.firstName`. Bläddra nedåt i den vänstra menyn för att hitta elementet **Person** och klicka på pilen för att gå en nivå längre ned.

![Journey Optimizer](./images/msg7.png)

Leta reda på elementet **Fullständigt namn** och klicka på pilen för att gå en högre nivå.

![Journey Optimizer](./images/msg8.png)

Leta reda på fältet **Förnamn** och klicka på **+** bredvid det. Sedan visas personaliseringstoken i textfältet.

![Journey Optimizer](./images/msg9.png)

Lägg sedan till texten **, tack för att du registrerar dig!**. Klicka på **Spara**.

![Journey Optimizer](./images/msg10.png)

Du kommer då tillbaka hit. Klicka på **E-posta Designer** för att skapa e-postens innehåll.

![Journey Optimizer](./images/msg11.png)

På nästa skärm får du tre olika metoder för att ange e-postens innehåll:

- **Designa från grunden**: Börja med en tom arbetsyta och använd WYSIWYG-redigeraren för att dra och släppa struktur och innehållskomponenter för att visuellt bygga upp e-postens innehåll.
- **Koda din egen**: Skapa en egen e-postmall genom att koda den med HTML
- **Importera HTML**: Importera en befintlig HTML-mall som du kan redigera.

Klicka på **Importera HTML**. Du kan också klicka på **Sparade mallar** och välja mallen **Bootcamp - e-postmall**.

![Journey Optimizer](./images/msg12.png)

Om du har valt **Importera HTML** kan du nu dra och släppa filen **mailtemplateBootcamp.html** som du kan hämta [här](../../assets/html/mailtemplatebootcamp.html.zip). Klicka på Importera.

![Journey Optimizer](./images/msg13.png)

Du kommer då att se den här standardmallen för e-post:

![Journey Optimizer](./images/msg14.png)

Låt oss personalisera e-postmeddelandet. Klicka bredvid texten **Hej** och klicka sedan på ikonen **Lägg till Personalization** .

![Journey Optimizer](./images/msg35.png)

Därefter måste du hämta en **förnamn**-personaliseringstoken som lagras under `profile.person.name.firstName`. Leta reda på elementet **Person** på menyn, gå ned till elementet **Fullständigt namn** och klicka sedan på ikonen **+** för att lägga till fältet Förnamn i uttrycksredigeraren.

Klicka på **Spara**.

![Journey Optimizer](./images/msg36.png)

Nu kommer du att märka hur personaliseringsfältet har lagts till i texten.

![Journey Optimizer](./images/msg37.png)

Klicka på **Spara** för att spara meddelandet.

![Journey Optimizer](./images/msg55.png)

Gå tillbaka till meddelandekontrollpanelen genom att klicka på **pilen** intill ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/msg56.png)

Du har nu skapat e-postmeddelandet med din registrering. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/msg57.png)

Klicka på **OK**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publish din resa

Du måste fortfarande ge din resa ett namn. Du kan göra det genom att klicka på ikonen **Penna** längst upp till vänster på skärmen.

![ACOP](./images/journeyname.png)

Du kan sedan ange resans namn här. Använd `yourLastName - Account Creation Journey`. Klicka på **OK** om du vill spara ändringarna.

![ACOP](./images/journeyname1.png)

Nu kan du publicera din resa genom att klicka på **Publish**.

![ACOP](./images/publishjourney.png)

Klicka på **Publish** igen.

![ACOP](./images/publish1.png)

Då visas ett grönt bekräftelsefält som anger att din resa nu är publicerad.

![ACOP](./images/published.png)

Du har nu avslutat den här övningen.

Nästa steg: [2.4 Testa din resa](./ex4.md)

[Gå tillbaka till användarflöde 2](./uc2.md)

[Gå tillbaka till Alla moduler](../../overview.md)