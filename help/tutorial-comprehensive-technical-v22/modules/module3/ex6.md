---
title: Se hur kundprofilen i realtid fungerar i Call Center
description: Se hur kundprofilen i realtid fungerar i Call Center
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 457347ca-1ce5-4699-bd30-735abdc7b450
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 1%

---

# 3.6 Se hur kundprofilen i realtid fungerar i Call Center

I den här övningen är målet att få er att gå igenom kundresan och agera som en riktig kund.

På denna webbplats har vi implementerat Adobe Experience Platform. Varje åtgärd betraktas som en upplevelsehändelse och skickas till Adobe Experience Platform i realtid, vilket innebär att kundprofilen i realtid hydreras.

I en tidigare övning började du som anonym kund som surfade på webbplatsen, och efter ett par steg blev du en känd kund.

När samma kund så småningom får tag i telefonen och ringer ert callcenter är det avgörande att informationen från andra kanaler blir tillgänglig omedelbart, så att samtalscentrets upplevelse kan vara relevant och personaliserad.

## 3.6.1 Använda din CX-app

Som en del av vårt demosystem har vi skapat en CX App-mall som kan användas för att simulera en callcentermiljö. Följ de här stegen för att skapa ett sådant CX App-projekt.

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Klicka **Nytt projekt**.

Sedan visas ditt CX App-projekt. Klicka på projektet för att öppna det.

![Demo](./images/cxapp3.png)

I CX App-projektet går du till **Integreringar**. Markera Adobe Experience Platform Data Collection-egenskapen som skapades i modul 0. Du måste välja den egenskap som har **(aktivering)** i namnet. Klicka sedan på **Kör**.

![Demo](./images/cxapp4.png)

Du kommer då att se det här.

![Demo](./images/cxapp5.png)

På panelen Profilvisningsprogram kan du se följande kombinationer av ID:n och namnutrymmen:

![Kundprofil](./images/identities.png)

| Identitet | Namnutrymme |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 12507560687324495704459439363261812234 |
| E-post-ID | woutervangeluwe+06022022-01@gmail.com |
| Mobilnummer-ID | +32473622044+06022022-01 |

När kunden ringer till er kundtjänst kan telefonnumret användas för att identifiera kunden. I den här övningen använder du telefonnumret för att hämta kundens profil i appen för kundupplevelser.

Välj **Telefonnummer** i listrutan och ange telefonnumret som du använde på webbplatsen. Träff **Retur**.

![Demo](./images/19.png)

Nu kommer du att se den information som helst skulle visas i Samtalscentret, så att de anställda på Samtalscentret får all relevant information direkt tillgänglig när de talar till en kund.

![Demo](./images/20.png)

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 3](./real-time-customer-profile.md)

[Gå tillbaka till Alla moduler](../../overview.md)
