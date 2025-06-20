---
title: GenStudio for Performance Marketing Campaign Activation to Meta
description: GenStudio for Performance Marketing Campaign Activation to Meta
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 2c7ef715-b8af-4a5b-8873-5409b43d7cb0
source-git-commit: b8f7b370a5aba82a0dcd6e7f4f0222fe209976f7
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 1.3.3 Kampanjaktivering till Meta

>[!IMPORTANT]
>
>För att slutföra den här övningen måste du ha tillgång till en fungerande AEM Assets CS-redigeringsmiljö där AEM Content Hub är aktiverat. Om du följer övning [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"} har du tillgång till en sådan miljö.

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

Placera CitiSignal-logotypen i det övre vänstra hörnet.

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

## 1.3.3.5 Publicera annonser på metadata

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [GenStudio for Performance Marketing](./genstudio.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
