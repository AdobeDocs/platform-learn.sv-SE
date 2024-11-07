---
title: Offer decisioning - Offer decisioning 101
description: Offer decisioning - Offer decisioning 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# 3.3.1 Offer decisioning 101

## 3.3.1.1 Terminologi

För att få en bättre förståelse för Offer decisioning rekommenderar vi att du läser [översikten](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) om hur Offer decisioning Application Service fungerar med Adobe Experience Platform.

När du arbetar med Offer decisioning måste du förstå följande koncept:

| Villkor | Förklaring |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Erbjudande** | Ett erbjudande är ett marknadsföringsmeddelande som kan ha kopplade regler som anger vem som kan se erbjudandet. Ett erbjudande har status: utkast, godkänt eller arkiverat. |
| **Placement** | Den kombination av plats (eller kanaltyp) och kontext (eller innehållstyp) i vilken ett erbjudande visas för en slutanvändare. Det är en kombination av kanalerna Text, HTML, Image, JSON för mobiler, webben, sociala medier, snabbmeddelanden och icke-digitala. |
| **Regel** | Den logik som definierar och styr slutanvändarnas rätt till ett erbjudande. |
| **Personaliserat erbjudande** | Ett anpassningsbart marknadsföringsmeddelande baserat på regler och begränsningar för behörighet. |
| **Reserverbjudande** | Det standarderbjudande som visas när en slutanvändare inte är berättigad till något av erbjudandena i den mängd som används. |
| **Hämtning** | Används i en offertdefinition för att definiera hur många gånger ett erbjudande kan presenteras totalt och för en viss användare. |
| **Prioritet** | Nivå för att fastställa prioritetsrangordningen utifrån en resultatmängd med erbjudanden. |
| **Samling** | Används för att filtrera bort en delmängd av erbjudanden från listan med personaliserade erbjudanden för att snabba upp offera decisioningen. |
| **Beslut** | En kombination av en uppsättning erbjudanden, placering och profil marknadsföraren vill att beslutsmotorn ska erbjuda det bästa erbjudandet. |
| **AEM Assets Essentials** | En universell och centraliserad upplevelse för lagring, sökning och val av mediefiler i Adobe Experience Cloud Solutions och Adobe Experience Platform. |

{style="table-layout:auto"}

## 3.3.1.2 Offer decisioning

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och väljer sandlådan i listan. I det här exemplet heter sandlådan **AEP Enablement FY22**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

Klicka på **Erbjudanden** på den vänstra menyn. Nu visas menyn Erbjudanden, som innehåller saker som Erbjudanden, Samlingar och Beslut.

![Placeringar](./images/homedec.png)

Klicka på **Komponenter**. Nu visas menyn Erbjudanden som innehåller funktioner som Placements, Tags, Rules och Rankings.

![Placeringar](./images/components.png)

## 3.3.1.3 Placeringar

Gå till **Placements**.

![Placeringar](./images/placements.png)

På fliken **Placements** kan du definiera dina placeringar för dina erbjudanden. När du definierar ett beslut definierar placeringen var det resulterande erbjudandet ska visas (kanaltyp) och i vilken form (innehållstyp).

Om du inte ser några placeringar i din Adobe Experience Platform-instans skapar du dem enligt anvisningarna nedan och på skärmbilden.

| Namn | Kanaltyp | Innehållstyp |
| ---------------------- | ------------ | ------------ |
| **Icke-digital - text** | Icke-digital | Text |
| **Webb - JSON** | Webb | JSON |
| **Webb - HTML** | Webb | HTML |
| **Webb - Text** | Webb | Text |
| **Webb - bild** | Webb | Bild |
| **E-post - JSON** | E-post | JSON |
| **E-post - HTML** | E-post | HTML |
| **E-post - text** | E-post | Text |
| **E-post - bild** | E-post | Bild |

{style="table-layout:auto"}

**Obs!** Ändra ingenting till de placeringar som redan är tillgängliga.

Klicka på en placering för att visa dess inställningar.

![Placeringar](./images/placement1.png)

Nu visas alla fält i placeringen:

- **Namn** på placeringen
- **Placement-ID**
- **Kanaltyp** för placeringen
- **Innehållstyp** för placeringen, som kan vara **Text**, **HTML**, **Bild** eller **JSON**
- **Beskrivningsfält** som tillåter att ytterligare beskrivning för placeringen läggs till

## 3.3.1.4 Beslutsregler

En regel (kallas även behörighetskrav) motsvarar ett **segment**. En regel är i själva verket ett segment med den enda skillnaden att en regel kan användas med ett erbjudande för att ge det bästa erbjudandet till en profil i Adobe Experience Platform.

Som du redan vet hur man definierar segment baserat på de tidigare aktiveringsmodulerna kan vi snabbt gå tillbaka till segmenteringsmiljön:

Gå till **Regler**. Klicka på **+ Skapa regel**.

![Beslutsregler](./images/rules.png)

Då visas segmenteringsmiljön i Adobe Experience Platform.

![Beslutsregler](./images/createrule1.png)

Du kan nu komma åt alla fält som ingår i unionens schema för kundprofilen i realtid och kan bygga ut alla regler.

Det är också intressant att veta att du helt enkelt kan återanvända redan definierade segment i Adobe Experience Platform genom att gå till **Publiker** > ``--aepTenantId--``.

![Beslutsregel](./images/decisionruleaud.png)

Då ser du det här:

![Beslutsregel](./images/decisionruleaud1.png)

Om du vill kan du nu konfigurera egna regler. För den här övningen behöver du två regler:

- alla - Manliga kunder
- alla - kvinnliga kunder

Om dessa regler inte finns än, var vänlig och skapa dem. Använd dessa regler om de redan finns och skapa inga nya regler.

Attributet som ska användas för att skapa regeln är **XDM Individual Profile** > **Person** > **Kön**.

Här är till exempel regeldefinitionen för regeln **all - hanterade kunder**:

![Beslutsregel](./images/allmale.png)

Här är till exempel regeldefinitionen för regeln **all - kvinnliga kunder**:

![Beslutsregel](./images/allfemale.png)

## 3.3.1.5 Erbjudanden

Gå till **Erbjudanden** och välj **Erbjudanden**. Klicka på **+ Skapa erbjudande**.

![Beslutsregel](./images/offers1.png)

Du kommer då att se den här popup-rutan.

![Beslutsregel](./images/offers2.png)

Skapa inga erbjudanden nu - det gör du i nästa övning.

Du ser nu att det finns två typer av erbjudanden:

- Personaliserade erbjudanden
- Reserverbjudanden

Ett personaliserat erbjudande är specifikt innehåll som ska visas i en viss situation. Ett personaliserat erbjudande är särskilt utformat för att leverera en personlig och sammanhangsberoende upplevelse om specifika kriterier uppfylls.

Ett reserverbjudande är ett erbjudande som visas om villkoren för personaliserade erbjudanden inte uppfylls.

## 3.3.1.6 Beslut

I ett beslut kombineras placeringar, en samling personaliserade erbjudanden och ett reserverbjudande som i slutändan ska användas av Offera decisioningen för att hitta det bästa erbjudandet för en viss profil, baserat på varje enskild personaliserad erbjudandeegenskap, som prioritet, behörighetsbegränsning och total-/användarbegränsning.

Klicka på **Beslut** om du vill konfigurera ditt **beslut**.

![Beslutsregel](./images/activity.png)

I nästa övning kommer ni att konfigurera era egna erbjudanden och beslut.

Nästa steg: [3.3.2 Konfigurera erbjudanden och beslut](./ex2.md)

[Gå tillbaka till modul 3.3](./offer-decisioning.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
