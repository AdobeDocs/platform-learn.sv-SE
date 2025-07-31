---
title: GenStudio for Performance Marketing Campaign Activation to Meta
description: GenStudio for Performance Marketing Campaign Activation to Meta
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 2c7ef715-b8af-4a5b-8873-5409b43d7cb0
source-git-commit: 10f1f6a1f77c41e3c912b3d03b73da7b6c68670c
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# 1.3.3 Kampanjaktivering till Meta

>[!IMPORTANT]
>
>För att slutföra den här övningen måste du ha tillgång till en fungerande AEM Assets CS-redigeringsmiljö där AEM Content Hub är aktiverat. Om du följer övning [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"} har du tillgång till en sådan miljö.

>[!IMPORTANT]
>
>För att kunna utföra alla steg i den här övningen måste du ha tillgång till en befintlig Adobe Workfront-miljö, och i den miljön måste du ha skapat ett projekt och ett arbetsflöde för godkännande. Om du följer övningen [Arbetsflödeshantering med Adobe Workfront](./../../../modules/workflow-planning/module1.2/workfront.md){target="_blank"} har du tillgång till de nödvändiga inställningarna.

>[!IMPORTANT]
>
>Om du tidigare har konfigurerat ett AEM Assets CS-program med en författare- och AEM Assets-miljö kan det bero på att din AEM CS-sandlåda har tagits i viloläge. Eftersom det tar 10-15 minuter att dölja en sådan sandlåda, är det en bra idé att starta separationsprocessen nu så att du inte behöver vänta på den vid ett senare tillfälle.

## 1.3.3.1 Skapa kampanj

Gå till **Kampanjer** i den vänstra menyn i **GenStudio for Performance Marketing**. Klicka på **+ Lägg till kampanj**.

![SGPeM](./images/gscampaign1.png)

Du bör då se en tom kampanjöversikt.

![SGPeM](./images/gscampaign2.png)

Använd `--aepUserLdap-- - CitiSignal Fiber Launch Campaign` som fältnamn.

Använd texten nedan för fältet **Beskrivning**.

```
The CitiSignal Fiber Launch campaign introduces CitiSignal’s flagship fiber internet service—CitiSignal Fiber Max—to key residential markets. This campaign is designed to build awareness, drive sign-ups, and establish CitiSignal as the go-to provider for ultra-fast, reliable, and future-ready internet. The campaign will highlight the product’s benefits for remote professionals, online gamers, and smart home families, using persona-driven messaging across digital and physical channels.
```

Använd texten nedan för fältet **Mål**.

```
Generate brand awareness in target regions
Drive early sign-ups and pre-orders for CitiSignal Fiber Max
Position CitiSignal as a premium, customer-first fiber internet provider
Educate consumers on the benefits of fiber over cable or DSL
```

Använd texten nedan för fältet **Nyckelmeddelanden**.

```
Supporting Points:
Symmetrical speeds up to 2 Gbps
Whole-home Wi-Fi 6E coverage
99.99% uptime guarantee
24/7 concierge support
No data caps or throttling
 Channels:
Digital Advertising: Google Display, YouTube pre-roll, Meta (Facebook/Instagram), TikTok (for gamers)
Email Marketing: Persona-segmented drip campaigns
Social Media: Organic and paid posts with testimonials, speed demos, and influencer partnerships
Out-of-Home (OOH): Billboards, transit ads in suburban commuter corridors
Local Events: Pop-up booths at tech expos, family festivals, and gaming tournaments
Direct Mail: Personalized flyers with QR codes for early sign-up discounts
 
Target Regions:
Primary Launch Markets:
Denver Metro Area, CO
Austin, TX
Raleigh-Durham, NC
Salt Lake City, UT
Demographic Focus:
Suburban neighborhoods with high remote work density
Areas with high smart home adoption
Zip codes with underserved or dissatisfied cable customers
```

Du bör då ha den här:

![SGPeM](./images/gscampaign3.png)

Bläddra nedåt om du vill se fler fält:

![SGPeM](./images/gscampaign4.png)

Ange dagens datum för fältet **Start**.

För fältet **Slut** anger du det till ett datum på en månad från och med nu.

För fältet **Status** anger du det till **Aktiv**.

För fältet **Kanaler** ställer du in det på **Meta**, **Email**, **Paid**, **Display**.

Välj ett valfritt område för fältet **Områden**.

För fältet För fältet **Referenser** > **Produkter**: välj produkten `--aepUserLdap-- - CitiSignal Fiber Max`.

**Referenser** > **Personas**: välj persona `--aepUserLdap-- - Remote Professionals`, `--aepUserLdap-- - Online Gamers`, `--aepUserLdap-- - Smart Home Families`

Du bör då se det här:

![SGPeM](./images/gscampaign5.png)

Din kampanj är nu färdig. Klicka på **pilen** för att gå tillbaka.

![SGPeM](./images/gscampaign6.png)

Då visas kampanjen i listan. Klicka på kalendervyikonen om du vill ändra vyn till kampanjkalendern.

![SGPeM](./images/gscampaign7.png)

Du bör då se en kampanjkalender som ger en mer visuell uppfattning om vilka kampanjer som är aktiva vid den tidpunkten.

![SGPeM](./images/gscampaign8.png)

## 1.3.3.2 Konfigurera anslutning till Meta

>[!IMPORTANT]
>
>Om du vill konfigurera anslutningen till Meta måste du ha ett Meta-användarkonto tillgängligt och det användarkontot måste läggas till i ett Meta Business-konto.

Om du vill konfigurera anslutningen till Meta klickar du på de 3 punkterna **..** och väljer **Inställningar**.

![SGPeM](./images/gsconnection1.png)

Klicka på **Anslut** för **Meta Ads**.

![SGPeM](./images/gsconnection2.png)

Logga in med ditt Meta-konto. Klicka på **Fortsätt**.

![SGPeM](./images/gsconnection3.png)

Om ditt konto är kopplat till ett Meta Business-konto kan du välja den företagsportfölj som har konfigurerats i Meta.

![SGPeM](./images/gsconnection5.png)

När anslutningen har upprättats klickar du på raden **X anslutna konton**.

![SGPeM](./images/gsconnection4.png)

Du bör sedan se information om det Meta Business Account som är anslutet till GenStudio for Performance Marketing.

![SGPeM](./images/gsconnection6.png)

## 1.3.3.3 Skapa ny resurs

Gå till [https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}. Skriv uppmaningen `a neon rabbit running very fast through space` och klicka på **Generera**.

![SGPeM](./images/gsasset1.png)

Sedan visas flera bilder som genereras. Välj den bild du gillar mest, klicka på ikonen **Dela** på bilden och välj sedan **Öppna i Adobe Express**.

![SGPeM](./images/gsasset2.png)

Du ser då att den bild du just har skapat blir tillgänglig i Adobe Express för redigering. Nu måste du lägga till CitiSignal-logotypen på bilden. Gå till **Varumärken** om du vill göra det.

![SGPeM](./images/gsasset3.png)

Du bör då se varumärkesmallen för CitiSignal som du skapade i GenStudio for Performance Marketing visas i Adobe Express. Klicka för att välja din varumärkesmall med namnet `--aepUserLdap-- - CitiSignal`.

![SGPeM](./images/gsasset4.png)

Gå till **Logos** och klicka på den **vita** Citisign-logotypen för att släppa den på bilden.

![SGPeM](./images/gsasset5.png)

Placera CitiSignal-logotypen högst upp i bilden, inte långt från mitten.

![SGPeM](./images/gsasset6.png)

Klicka sedan på **Dela**.

![SGPeM](./images/gsasset7.png)

Välj **AEM Assets**.

![SGPeM](./images/gsasset8.png)

Klicka på **Välj mapp**.

![SGPeM](./images/gsasset9.png)

Välj din AEM Assets CS-databas som ska ha namnet `--aepUserLdap-- - CitiSignal` och markera sedan mappen `--aepUserLdap-- - CitiSignal Fiber Campaign`. Klicka på **Markera**.

![SGPeM](./images/gsasset11.png)

Du borde se det här då. Klicka på **Överför 1 resurs**. Bilden överförs nu till AEM Assets CS.

![SGPeM](./images/gsasset12.png)

Gå till [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Öppna **Experience Manager Assets**.

![SGPeM](./images/gsasset13.png)

Välj din AEM Assets CS-miljö, som ska få namnet `--aepUserLdap-- - CitiSignal dev`.

![SGPeM](./images/gsasset14.png)

Gå till **Assets** och dubbelklicka sedan på mappen `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![SGPeM](./images/gsasset15.png)

Du borde se något liknande. Dubbelklicka på bilden `--aepUserLdap-- - neon rabbit`.

![SGPeM](./images/gsasset16.png)

Bilden `--aepUserLdap-- - neon rabbit` visas sedan. Ändra **status** till **Godkänd** och klicka sedan på **Spara**

>[!IMPORTANT]
>
>Om status för en bild inte är inställd på **Godkänd** visas inte bilden i GenStudio for Performance Marketing. Endast godkända mediefiler är tillgängliga i GenStudio for Performance Marketing.

![SGPeM](./images/gsasset17.png)

Byt tillbaka till GenStudio for Performance Marketing. På den vänstra menyn går du till **Assets** och väljer din AEM Assets CS-databas, som bör ha namnet `--aepUserLdap-- - CitiSignal`. Du kommer då att se bilden som du just har skapat och godkänt bli tillgänglig i GenStudio for Performance Marketing.

![SGPeM](./images/gsasset18.png)

## 1.3.3.4 Skapa och godkänn metaannons

Gå till **Skapa** på den vänstra menyn. Välj **Meta**.

![SGPeM](./images/gsad1.png)

Välj mallen **Meta ad** som du importerade tidigare, med namnet `--aepUserLdap---citisignal-meta-ad`. Klicka på **Använd**.

![SGPeM](./images/gsad2.png)

Du borde se det här då. Ändra namnet på din annons till `--aepUserLdap-- - Meta Ad Fiber Max`.

Välj följande alternativ under **Parametrar**:

- **Varumärke**: `--aepUserLdap-- - CitiSignal`
- **Språk**: `English (US)`
- **Persona**: `--aepUserLdap-- - Smart Home Families`
- **Produkt**: `--aepUserLdap-- - CitiSignal Fiber Max`

Klicka på **Välj från innehåll**.

![SGPeM](./images/gsad3.png)

Välj resursen `--aepUserLdap-- - neon rabbit.png`. Klicka på **Använd**.

![SGPeM](./images/gsad4.png)

Skriv uppmaningen `focus on lightning fast internet for big families` och klicka på **Generera**.

![SGPeM](./images/gsad5.png)

Då borde du se något sådant här. Dina annonser är nu klara att granskas och godkännas. Det gör du genom att klicka på **Begär godkännande** som ansluter till Adobe Workfront.

![SGPeM](./images/gsad6.png)

Välj ditt Adobe Workfront-projekt, som ska få namnet `--aepUserLdap-- - CitiSignal Fiber Launch`. Ange din egen e-postadress under **Bjud in personer** och kontrollera att din roll är inställd på **Godkännare**.

![SGPeM](./images/gsad7.png)

Du kan också använda ett befintligt arbetsflöde för godkännande i Adobe Workfront. Det gör du genom att klicka på **Använd mall** och välja mallen `--aepuserLdap-- - Approval Workflow`. Klicka på **Skicka**.

![SGPeM](./images/gsad8.png)

Klicka på **Visa kommentarer i Workfront** så skickas du nu till Adobe Workfront korrekturrundgränssnitt.

![SGPeM](./images/gsad9.png)

Klicka på **Fatta beslut** i Adobe Workfront Proof UI.

![SGPeM](./images/gsad10.png)

Välj **Godkänd** och klicka på **Fatta beslut**.

![SGPeM](./images/gsad11.png)

Klicka på **Publicera**.

![SGPeM](./images/gsad12.png)

Välj din kampanj `--aepUserLdap-- - CitiSignal Fiber Launch Campaign` och klicka på **Publicera**.

![SGPeM](./images/gsad13.png)

Klicka på **Öppna i innehåll**.

![SGPeM](./images/gsad14.png)

De fyra Meta-annonserna är nu tillgängliga under **Innehåll** > **Erfarenheter**.

![SGPeM](./images/gsad15.png)

## 1.3.3.5 Publicera annonser på metadata

Välj en av annonserna och klicka sedan på **Aktivera**.

![SGPeM](./images/gsmetaad1.png)

Välj en **Call to action** i listan och ange en exempel-URL. Klicka på **Nästa**.

![SGPeM](./images/gsmetaad3.png)

Välj Meta-kontot, den länkade Facebook-sidan, Meta Campaign och Meta Ad Set.

Ge din add ett namn, använd `--aepUserLdap-- Fiber Max Ad`.

Klicka på **Nästa**.

![SGPeM](./images/gsmetaad4.png)

Klicka på **Publicera**.

![SGPeM](./images/gsmetaad5.png)

Klicka på **OK**.

![SGPeM](./images/gsmetaad6.png)

Din annons status är nu inställd på **Publicering**, vilket kan ta några minuter.

![SGPeM](./images/gsmetaad7.png)

Efter några minuter ändras annonsens status till **Publicerad**. Det innebär att annonsen har skickats från GenStudio for Performance Marketing till Meta. Det betyder inte att annonsen redan är publicerad i Meta! Det finns fortfarande ett antal steg att ta i Meta Business Account för att ta annonsen och publicera den så att den kan ses av användare på olika Meta-plattformar.

Klicka på **Visa information**.

![SGPeM](./images/gsmetaad8.png)

Klicka på **Öppna**, som tar dig till ditt Meta Business-konto.

>[!IMPORTANT]
>
>Om du inte har tillgång till det Meta Business-konto som är anslutet till din miljö kan du inte visualisera annonsen i Meta.

![SGPeM](./images/gsmetaad9.png)

Här är en översikt över den annons du just skapade, men nu i Meta.

![SGPeM](./images/gsmetaad10.png)

Du har nu avslutat den här övningen.

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [GenStudio for Performance Marketing](./genstudio.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
