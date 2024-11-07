---
title: Journey Optimizer Skapa en resa och ett e-postmeddelande
description: Journey Optimizer Skapa ditt e-postmeddelande
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# 3.1.2 Skapa din resa och ditt e-postmeddelande

I den här övningen ska du konfigurera resan och det meddelande som ska utlösas när någon skapar ett konto på demowebbplatsen.

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och väljer sandlådan i listan. I det här exemplet heter sandlådan **AEP Enablement FY22**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

## 3.1.2.1 Skapa din resa

Klicka på **Resor** på den vänstra menyn. Klicka sedan på **Skapa resa** för att skapa en ny resa.

![ACOP](./images/createjourney.png)

Då ser du en tom skärm för resan.

![ACOP](./images/journeyempty.png)

I föregående övning skapade du en ny **Event**. Du gav den ett namn som detta `ldapAccountCreationEvent` och ersatte `ldap` med din ldap. Detta var resultatet av händelseskapandet:

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

## 3.1.2.2 Skapa ett meddelande

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

Klicka på **Skapa från grunden**.

![Journey Optimizer](./images/msg12.png)

På den vänstra menyn hittar du de strukturkomponenter som du kan använda för att definiera e-postmeddelandets struktur (rader och kolumner).

![Journey Optimizer](./images/msg13.png)

Dra och släpp en **1:2-kolumn till vänster** från menyn på arbetsytan. Detta blir platshållare för logotypbilden.

![Journey Optimizer](./images/msg14.png)

Dra och släpp en **1:1-kolumn** under den föregående komponenten. Det här blir banderollblocket.

![Journey Optimizer](./images/msg15.png)

Dra och släpp en **1:2-kolumn till vänster** under den föregående komponenten. Det här blir det faktiska innehållet med en bild på vänster sida och text på höger sida.

![Journey Optimizer](./images/msg16.png)

Dra och släpp en **1:1-kolumn** under den föregående komponenten. Det här blir e-postsidfoten. Arbetsytan bör nu se ut så här:

![Journey Optimizer](./images/msg17.png)

Sedan använder vi Innehållskomponenter för att lägga till innehåll i dessa block. Klicka på menyalternativet **Innehållskomponenter**

![Journey Optimizer](./images/msg18.png)

Dra och släpp en **bild**-komponent i den första cellen på den första raden. Klicka på **Bläddra**.

![Journey Optimizer](./images/msg19.png)

Då ser du det här. Navigera till mappen **enablement-assets** och markera filen **luma-logo.png**. Klicka på **Markera**.

![Journey Optimizer](./images/msg21.png)

Nu är du tillbaka här:

![Journey Optimizer](./images/msg25.png)

Gå till **Innehållskomponenter** och dra och släpp en **Bild** -komponent i den första cellen på den första raden. Klicka på **Bläddra**.

![Journey Optimizer](./images/msg26.png)

Gå till mappen **enablement-assets** i popup-fönstret **Assets** . I den här mappen hittar du alla resurser som tidigare har förberetts och överförts av det kreativa teamet. Välj **module23-thankyou-new.png** och klicka på **Select**.

![Journey Optimizer](./images/msg28.png)

Då får du den här:

![Journey Optimizer](./images/msg30.png)

Markera bilden och rulla nedåt i den högra menyn tills du ser **Storlek**-breddreglagekomponenten. Använd reglaget för att ändra bredden till f.i. **60%**.

![Journey Optimizer](./images/msg31.png)

Gå sedan till **Innehållskomponenter** och dra och släpp en **Text** -komponent i strukturkomponenten på den fjärde raden.

![Journey Optimizer](./images/msg33.png)

Välj standardtexten **Skriv texten här.** som du skulle göra med en textredigerare. Skriv **Bästa** i stället. Lägg märke till att textverktygsfältet visas när du är i textläge.

![Journey Optimizer](./images/msg34.png)

Klicka på ikonen **Lägg till anpassning** i verktygsfältet.

![Journey Optimizer](./images/msg35.png)

Därefter måste du hämta en **förnamn**-personaliseringstoken som lagras under `profile.person.name.firstName`. Leta reda på elementet **Person** på menyn, gå ned till elementet **Fullständigt namn** och klicka sedan på ikonen **+** för att lägga till fältet Förnamn i uttrycksredigeraren.

Klicka på **Spara**.

![Journey Optimizer](./images/msg36.png)

Nu kommer du att märka hur personaliseringsfältet har lagts till i texten.

![Journey Optimizer](./images/msg37.png)

I samma textfält trycker du på **Enter** två gånger för att lägga till två rader och skriva **Tack för att du har skapat ditt konto med Luma!**.

![Journey Optimizer](./images/msg38.png)

Den sista kontrollen som utförs för att se till att e-postmeddelandet är klart är att förhandsgranska det. Klicka på knappen **Simulera innehåll** .

![Journey Optimizer](./images/msg50.png)

Börja med att identifiera vilken profil du vill använda för förhandsgranskningen. Markera namnutrymmet **email** genom att klicka på ikonen bredvid fältet **Ange ID-namnområde**.

Markera namnutrymmet **E-post** i listan med identitetsnamnutrymmen.

I fältet **Identitetsvärde** anger du e-postadressen för en tidigare demoprofil som redan finns lagrad i kundprofilen i realtid. Till exempel **woutervangeluwe+06022022-01@gmail.com** och klicka på knappen **Sök efter testprofil**

![Journey Optimizer](./images/msg53.png)

När din profil visas i tabellen klickar du på fliken **Förhandsgranska** för att öppna förhandsvisningsskärmen.

När förhandsgranskningen är klar kontrollerar du att personaliseringen är korrekt på ämnesraden, att både brödtexten och avprenumerationslänken är markerade som en hyperlänk.

Klicka på **Stäng** för att stänga förhandsgranskningen.

![Journey Optimizer](./images/msg54.png)

Klicka på **Spara** för att spara meddelandet.

![Journey Optimizer](./images/msg55.png)

Gå tillbaka till meddelandekontrollpanelen genom att klicka på **pilen** intill ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/msg56.png)

Du har nu skapat e-postmeddelandet med din registrering. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/msg57.png)

Klicka på **OK**.

![Journey Optimizer](./images/msg57a.png)

## 3.1.2.3 Publish din resa

Du måste fortfarande ge din resa ett namn. Du kan göra det genom att klicka på ikonen **Egenskaper** längst upp till höger på skärmen.

![ACOP](./images/journeyname.png)

Du kan sedan ange resans namn här. Använd `--aepUserLdap-- - Account Creation Journey`. Klicka på **OK** om du vill spara ändringarna.

![ACOP](./images/journeyname1.png)

Nu kan du publicera din resa genom att klicka på **Publish**.

![ACOP](./images/publishjourney.png)

Klicka på **Publish** igen.

![ACOP](./images/publish1.png)

Då visas ett grönt bekräftelsefält som anger att din resa nu är publicerad.

![ACOP](./images/published.png)

Du har nu avslutat den här övningen.

Nästa steg: [3.1.3 Uppdatera din datainsamlingsegenskap och testa din resa](./ex3.md)

[Gå tillbaka till modul 3.1](./journey-orchestration-create-account.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
