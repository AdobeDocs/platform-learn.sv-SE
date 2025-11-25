---
title: Komma igång med Agent Orchestrator
description: Komma igång med Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: ffdc6b34a82c945c142f433f65a4f2f8d5cdcd18
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 0%

---

# 1.1.1 Komma igång med Agent Orchestrator

## 1.1.1.1 Ange kontext i Agent Orchestrator

Gå till [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Du borde se det här då. Kontrollera att du är i organisationen **Experience Platform International**.

![Agent Orchestrator](./images/ao1.png)

Klicka på fönstret **context**.

![Agent Orchestrator](./images/ao2.png)

Ställ in kontexten på:

- **Dokumentation för Source**: **Customer Journey Analytics**
- **Sandbox**: **Accelerate**
- **Datavy**: **Accelerate 2026 B2C**

Klicka på **Ange kontext**.

![Agent Orchestrator](./images/ao3.png)

>[!NOTE]
>
>I det här labbet kommer du att byta kontext när du går mellan analys och samordning.

## 1.1.1.2 Börja med allmänna köptrender för att förankra kontext och zooma in på fiber

**Återgivning**: Få en puls på högsta nivå vid behov - Mobile, Landline, Internet, TV, Fibre - särskilt under de senaste 60 dagarna. Här anges baslinjer för säsongsbundenhet, kampanjeffekter och regionala variationer efter NY-utrullningen.

**Funderar**:

&quot;Fungerar Fibre på att få marknadsandelar efter NY? Ser vi kannibalisering av koppar-/DSL-internet? Vad är det för skillnad mot TV-paket?&quot;

&quot;Det kommer att hjälpa mig att anpassa den adresserbara publiken till Wien och sätta upp realistiska mål.&quot;

**Körbara avläsningar som marknadsföraren förväntar sig**:

En staplad liggande stapel-/linjediagram över inköp per huvudkategori (kornighet per dag/vecka).

Procent av köp per kategori kontra föregående period.

Kända toppar som korrelerar med kampanjdatum.

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

Du bör då se det här:

>[!NOTE]
>
>Håll ett öga på eftersläpande attribuering - Fiberorder kan tas under &quot;Internet&quot; i vissa äldre scheman. Om så är fallet, stämma av taxonomin före beslut.

![Agent Orchestrator](./images/ao5.png)

Ange följande **Fråga** och klicka på knappen **generera**.

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

Du borde se det här, som fördjupar dig i fiberspecifika trender.

**Åtgärd**: Observera tillväxtkurvan och regionala toppar.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Korrelera order med innehållsinställningar

**Återgivning**: Testa hypotesen att innehållsinställningen (t.ex. SciFi, Sport, Drama) förutser bredbandsuppgraderingsbeteenden, särskilt för behov med hög bandbredd.

**Funderar**

&quot;SciFi-fans tittar ofta på 4K och strömmar från flera enheter, vilket troligen värdesätter låg latens.&quot;

&quot;Låt oss kvantifiera om SciFi (och kanske Sport) korrelerar med de senaste beställningarna.&quot;

**Förväntade utdata**

En pivot med beställningar (YYT-filter används) uppdelad efter föredragen genre, begränsad till de senaste två månaderna.

Rangordna genrer efter orderkonverteringsgrad och AOV (genomsnittligt ordervärde).

Beslut: Om SciFi visar en stark signal blir detta en primär kreativ pelare för Wiens lansering av Fiber Max (t.ex.&quot;aldrig buffra igen&quot;-meddelanden, premiumpaket).

**Avsikt**

Analysera konverteringen utifrån genre (t.ex. Sci-Fi, Sport).

**Mål** Verifiera om Sci-Fi fans over-index för Fibre-uppgraderingar.

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Du bör då se det här:

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 Identifiera befintliga Fibre Journeys

Klicka på fönstret **context**.

![Agent Orchestrator](./images/ao10.png)

Ställ in kontexten på:

- **Dokumentation för Source**: **Adobe Journey Optimizer**
- **Sandbox**: **Accelerate**
- **Datavy**: **Accelerate 2026 B2C**

![Agent Orchestrator](./images/ao11.png)

**Återgivning** Identifiera vilka aktiva eller nyligen avslutade resor som innehåller &quot;Fiber&quot; i titeln, t.ex. &quot;Fiber Upgrade NYC - Sept&quot;, &quot;Fiber Trial - Streaming Bundle&quot;.

**Funderar**

&quot;Vilken av dessa resor gick bra och vad utlöste de?&quot;

&quot;Kan jag återanvända den vinnande orkestrationslogiken för Wien?&quot;

**Förväntade utdata**

Lista över resor med status (aktiv, pausad, avslutad), datumintervall, målsegment, nyckeltal (öppen hastighet, aktuell tid, konvertering).

Nästa steg: Kortlista en eller två lyckade fiberresor för kloning/anpassning.

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Du bör då se det här:

![Agent Orchestrator](./images/ao13.png)

Visa aktiva eller tidigare resor med Fibre Messaging.

Åtgärd: Kortlista högpresterande resor för kloning.

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Du bör då se det här:

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 Kontrollera startvärdet

**Återgivning**:

Förstå startvärdesdefinitionen för resan&quot;CitiSignal - Fiber Max Launch Promotion&quot; - vilka egenskaper som driver målsättningen (t.ex.&quot;SciFi Genre Preference&quot;,&quot;4+ enheter&quot;,&quot;ström ≥ 300 GB/månad&quot;).

**Funderar**

&quot;Jag vill kombinera beprövad SciFi-kreativitet med Fibre Max-prestandameddelanden.&quot;

&quot;Om publiken överlappar många nedladdare kan vi stapla alla möjligheter.&quot;

**Förväntade utdata**

Målgruppskriterier (inkludering/uteslutning), målgruppsstorlek, regionfilter, senaste besök, tröskelvärden för frekvens.

>[!NOTE]
>
>Ändra sammanhang till CJA

Från och med nu växlar marknadsföraren till analysläge för att säkerställa korrekt rapportering.

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
What was the initial audience in the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/ao16.png)
Granska målgruppskriterier (strömningsvanor, antal enheter).

**Mål**: Förstå egenskaper för behov med hög bandbredd.

## 1.1.1.6 Validera reseprestanda via utfallsanalys

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

>[!NOTE]
>
>Ändra sammanhang till CJA)

**Återgivning**:

Bygg en stegvis funnel i Customer Journey Analytics

Levererad → Öppen → Klickad → Lanserad → Produktvy → Lägg till i kundvagn → Kassa → Beställning slutförd

Inkludera fiberrelaterade SKU-vyer som en gren.

**Funderar**:

&quot;Var tappar vi bort människor - öppna e-postmeddelanden, läsa in landningssidor, PDP:er, utcheckningsfriktion?&quot;

&quot;studsar SciFi-användare mer eller mindre än genomsnittet på Fibre PDP?&quot;

**Förväntade utdata**:

En utfallsvisualisering med utfallsfrekvenser vid varje steg.

Segmentövertäckningar (SciFi kontra Sport kontra Övrigt).

Nedbrytning av enhet/webbläsare för teknisk friktion.

**Beslut**:

Om utcheckningen är hög ska du koordinera med product/UX för att korrigera betalningsflödet.

Om PDP-avslutningen är hög kan du göra anspråk på klarheten (hastigheter, installationstider, paketvärde) på nytt.

>[!NOTE]
>
>Ändra kontext till JO

Nu flyttar marknadsföraren in i Adobe Journey Optimizer för att få ordning och målgrupper att stanna.

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey 
```

Bygg funnel-visualisering: Levererat → Öppnad → Klickad → Checka ut → Beställning.

**Åtgärd**: Identifiera bortfallspunkter och optimera meddelanden eller användargränssnitt.

## 1.1.1.7 Hitta befintliga målgrupper som är anpassade efter hög användning

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>Ändra sammanhang till Adobe Journey Optimizer

**Återgivning**:

Hitta en JO-målgrupp som heter&quot;tung nedladdning&quot; - troligtvis definierad av tröskelvärden för användning av data per månad, timmars direktuppspelning eller enhetskontinuitet.

**Funderar**:

&quot;Om det finns en publik som Heavy Downloaders är det perfekt för Fibre Max-positionering: hastighet, tillförlitlighet, obegränsat antal nivåer.&quot;

**Förväntade utdata**:

Målgruppsmetadata: definitionskriterier, storlek, senaste uppdatering, styrningstaggar, regionens tillgänglighet.

Hitta målgrupper med hög dataanvändning.

**Mål**: Kombinera med Sci-Fi-inställningar för målinriktning med Fiber Max.

## 1.1.1.8 Avgör om dessa målgrupper redan används

**Återgivning**:

Kontrollera länkningen mellan olika målgrupper - försäkra oss om att vi inte tvivlar på eller kolliderar med aktuella program.

**Funderar**:

&quot;Om stora nedladdare redan är på en kvarhållningsresa behöver vi undertryckningslogik eller frekvensbegränsning för att undvika utmattning.&quot;

**Förväntade utdata**:

Mappningar: målgrupp → resenamn, status, kontaktprincip, senaste sändning, prestanda.

**Beslut**:

Om den används kan du skapa undantag eller delad nedtryckning för att starta Wien.

Grönt ljus för ny resa om det inte används.

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
Which of the above are used in a journey? 
```

Säkerställ att kampanjer inte överlappar varandra.

**Åtgärd**: Använd undertryckning om det behövs.

## 1.1.1.9 Skapa ny resa för Fibre Max-start

**Återgivning**:

Bygg en ny resa för den sammansatta målgruppen:

Stora hämtare ∩ SciFi-inställningar (kbaa_5207bf målgruppsnyckel).

**Funderar**:

&quot;Det här är den ljuva fläcken för Fiber Max: hög benägenhet + kreativ relevans.&quot;

&quot;Vi kommer att skapa en multitouch-upplevelse som är knuten till Wiens tillgänglighet.&quot;

**Resedesign (JO)**:

Villkor:

Målgrupp: stora nedladdare - Sci-Fi Preference_kbaa_5207bf

Geografi: Tunnelbana i Wien (postnummerlista eller geopolygon)

Berättigande: Inte i aktiv&quot;Fibre Upgrade NYC - Sept&quot;-kampanj; inte en aktuell Fibre-prenumerant.

Utlösare och tidsinställning:

T14 dagar före Wien-lanseringen (jan 2026): Förhandsgranska e-post -&quot;Fiber Max kommer.&quot;

Startvecka: Primär e-post + banner för appar + betald mediesynkronisering (via CDP-mål).

T+3 dagar: Uppträdandet delas - om du inte klickar, knuffas SMS; om du klickar på det men inte beställt, kan du rikta om med ett installationsprogram som är tillgängligt i CTA.

T+10 dagar: Erbjudandetest - kostnadsfri installation jämfört med första månadsrabatt (A/B).

Personalization:

Dynamisk kopia för SciFi-lovers (latens/4K-direktuppspelningskrokar).

Påståenden om hastighet/fördröjning är anpassade för enhetsblandning (spelkonsoler, strömningsrutor).

Rekommendation: Fiber Max + premium-TV scifi content pack.

Styrning:

Frekvenslock: max 3 beröringar per 10 dagar.

Undertryck om det finns en Fibre-prenumerant eller en biljett för installation.

Uppfyll inställningarna för alternativ.

**Måttplan (CJA)**:

Spåra: Leverans, öppna, klicka, PDP-vy, utcheckningsstart, orderslutförande.

KPI:er: Konverteringsgrad till Fiber Max, uplift vs control, timetoinstall.

Diagnostik: Utfallsrapport per enhet/genre-segment.

Hur allt passar ihop (marknadsförarens mentala modell)

Diagnostisera efterfrågan (övergripande kategorier → Fiber specifikt).

Bevisa innehåll för konverteringssignal (order per genre).

Mina framgångsrika resor (hitta Fibernamed-resor och SciFi-kampanjens målgrupp).

Validera friktionspunkter (CJA-utfall på SciFi-resa).

Aktivera mot högprioritetssegment (stora hämtningsprogram ∩ SciFi).

Gå till [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Du borde se det här då. Kontrollera att du är i organisationen **Experience Platform International**.

Klicka på fönstret **context**.

![Agent Orchestrator](./images/ao2.png)

Ställ in kontexten på:

- **Dokumentation för Source**: **Journey Optimizer**
- **Sandbox**: **Accelerate**
- **Datavy**: **Accelerate 2026 B2C**

Klicka på **Ange kontext**.

![Agent Orchestrator](./images/aoea3.png)

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Du borde se det här då. Ange `yes` och klicka på generera.

![Agent Orchestrator](./images/aocj2.png)

Du borde se det här då. Ange `yes` och klicka på generera.

![Agent Orchestrator](./images/aocj3.png)

Du borde se det här då. Ange `The first one` och klicka på generera.

![Agent Orchestrator](./images/aocj4.png)

Du borde se det här då. Ange `yes` och klicka på generera.

![Agent Orchestrator](./images/aocj5.png)

Granska svaret. Ange `yes` och klicka på generera.

![Agent Orchestrator](./images/aocj6.png)

Klicka på **Granska**.

![Agent Orchestrator](./images/aocj7.png)

Uppdatera resenamnet med din LDAP för att göra det unikt. Klicka på **Spara**.

![Agent Orchestrator](./images/aocj8.png)

Din resa har nu skapats i utkastläge.

![Agent Orchestrator](./images/aocj9.png)

## 1.1.1.10 experiment

Gå till [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Du borde se det här då. Kontrollera att du är i organisationen **Experience Platform International**.

Klicka på fönstret **context**.

![Agent Orchestrator](./images/ao2.png)

Ställ in kontexten på:

- **Dokumentation för Source**: **Journey Optimizer**
- **Sandbox**: **Accelerate**
- **Datavy**: **Accelerate 2026 B2C**

Klicka på **Ange kontext**.

![Agent Orchestrator](./images/aoea3.png)

Ange följande **Fråga** och klicka på knappen **generera**.

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Du bör då se det här:

![Agent Orchestrator](./images/aoea1.png)

Klicka på förslaget för att jämföra konverteringsgraden för varje behandling och klicka sedan på **generera**.

![Agent Orchestrator](./images/aoea2.png)

Du bör då se en detaljerad jämförelse som den här:

![Agent Orchestrator](./images/aoea4.png)

Gå tillbaka till [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}