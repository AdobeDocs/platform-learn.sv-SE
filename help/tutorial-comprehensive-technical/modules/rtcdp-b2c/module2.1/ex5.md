---
title: Se hur kundprofilen i realtid fungerar i Call Center
description: Se hur kundprofilen i realtid fungerar i Call Center
kt: 5342
doc-type: tutorial
exl-id: 47c96696-644a-43b9-8deb-846bd2587af0
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 2.1.5 Se hur kundprofilen i realtid fungerar i Call Center

I den här övningen är målet att få er att gå igenom kundresan och agera som en riktig kund.

På denna webbplats har vi implementerat Adobe Experience Platform. Varje åtgärd betraktas som en upplevelsehändelse och skickas till Adobe Experience Platform i realtid, vilket innebär att kundprofilen i realtid hydreras.

I en tidigare övning började du som anonym kund som surfade på webbplatsen, och efter ett par steg blev du en känd kund.

När samma kund så småningom får tag i telefonen och ringer ert callcenter är det avgörande att informationen från andra kanaler blir tillgänglig omedelbart, så att samtalscentrets upplevelse kan vara relevant och personaliserad.

## Använd din CX-app

Gå till [https://dsn.adobe.com](https://dsn.adobe.com). När du har loggat in med din Adobe ID ser du det här. Klicka på de tre punkterna **..** i ditt CX App-projekt och klicka sedan på **Redigera** för att öppna det.

![Demo](./images/cxapp3.png)

Gå till **Integreringar** i ditt CX-appprojekt. Klicka på **Välj miljö**.

![Demo](./images/cxapp3a.png)

Markera den Adobe Experience Platform Data Collection-egenskap som skapades i Getting Started. Du måste markera egenskapen som har **(cx-app)** i namnet.

![Demo](./images/cxapp4.png)

Då ser du det här. Klicka på **Kör**.

![Demo](./images/cxapp4a.png)

Sedan måste du välja en av dina identiteter och enligt namnutrymmet och klicka på **sökikonen**.

![Kundprofil](./images/identities.png)

| Identitet | Namnutrymme |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 79943948563923140522865572770524243489 |
| Experience Cloud ID (ECID) | 70559351147248820114888181867542007989 |
| E-post-ID | woutervangeluwe+18112024-01@gmail.com |
| Mobilnummer-ID | +32473622044+18112024-01 |

När kunden ringer till er kundtjänst kan telefonnumret användas för att identifiera kunden. I den här övningen använder du telefonnumret för att hämta kundens profil i appen för kundupplevelser.

![Demo](./images/19.png)

Nu kommer du att se den information som helst skulle visas i Samtalscentret, så att de anställda på Samtalscentret får all relevant information direkt tillgänglig när de talar till en kund.

![Demo](./images/20.png)

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 2.1](./real-time-customer-profile.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
