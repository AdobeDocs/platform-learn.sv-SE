---
title: Komma igång med Agent Orchestrator
description: Komma igång med Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: e90dee164dfe098c9fc56a04c481a733c0843858
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# 1.1.1 Komma igång med Agent Orchestrator

## 1.3.1 Ange kontext i Agent Orchestrator

Navigera till AI-assistenten och placera i en stor vy.

Bekräfta att du befinner dig i CJA-kontext för analysuppgifter.

>[!NOTE]
>
>Använd kontextväxling när du går mellan analys (CJA) och orkestration (JO).

## 1.3.2 Börja med allmänna köptrender för att förankra kontexten och zooma in på fiber

**Fråga**:

```javascript
Show me purchases by mainCategory over the last 2 month
```

**Återgivning**: Få en puls på högsta nivå vid behov - Mobile, Landline, Internet, TV, Fibre - särskilt under de senaste 60 dagarna. Här anges baslinjer för säsongsbundenhet, kampanjeffekter och regionala variationer efter NY-utrullningen.

Funderar:

&quot;Fungerar Fibre på att få marknadsandelar efter NY? Ser vi kannibalisering av koppar-/DSL-internet? Vad är det för skillnad mot TV-paket?&quot;

&quot;Det kommer att hjälpa mig att anpassa den adresserbara publiken till Wien och sätta upp realistiska mål.&quot;

Användbara värden som marknadsföraren förväntar sig:

En staplad liggande stapel-/linjediagram över inköp per huvudkategori (kornighet per dag/vecka).

Procent av köp per kategori kontra föregående period.

Kända toppar som korrelerar med kampanjdatum.

>[!NOTE]
>
>Håll ett öga på eftersläpande attribuering - Fiberorder kan tas under &quot;Internet&quot; i vissa äldre scheman. Om så är fallet, stämma av taxonomin före beslut.

 

**Fråga**:

```javascript
Show me purchases by mainCategory over the last 2 monthzoom into fiber performance
```

**Nästa fråga**

`Show me purchases by mainCategory = Fiber over the last 2 months`

Gå ned på Fiberspecifika trender.

**Åtgärd** Observera tillväxtkurva och regionala toppar.

## 1.3.3 Korrelera order med innehållsinställningar

**Fråga**:

```javascript
Show me ordersYTD by preferred genre for the last 2 months
```

**Återgivning** Testa hypotesen att innehållsinställningen (t.ex. SciFi, Sport, Drama) förutsäger hur bredbandsuppgraderingen fungerar - särskilt för behov med hög bandbredd.

**Funderar**

&quot;SciFi-fans tittar ofta på 4K och strömmar från flera enheter, vilket troligen värdesätter låg latens.&quot;

&quot;Låt oss kvantifiera om SciFi (och kanske Sport) korrelerar med de senaste beställningarna.&quot;

**Förväntade utdata**

En pivot med beställningar (YYT-filter används) uppdelad efter föredragen genre, begränsad till de senaste två månaderna.

Rangordna genrer efter orderkonverteringsgrad och AOV (genomsnittligt ordervärde).

Beslut: Om SciFi visar en stark signal blir detta en primär kreativ pelare för Wiens lansering av Fiber Max (t.ex.&quot;aldrig buffra igen&quot;-meddelanden, premiumpaket).

**Fråga**

`Show me ordersYTD by preferred genre for the last 2 months`

**Avsikt**

Analysera konverteringen utifrån genre (t.ex. Sci-Fi, Sport).

**Mål** Verifiera om Sci-Fi fans over-index för Fibre-uppgraderingar.

## 1.3.4 Identifiera befintliga fiberresor

**Fråga**:

```javascript
What journey was running and had Fiber in the name
```

**Återgivning** Identifiera vilka aktiva eller nyligen avslutade resor som innehåller &quot;Fiber&quot; i titeln, t.ex. &quot;Fiber Upgrade NYC - Sept&quot;, &quot;Fiber Trial - Streaming Bundle&quot;.

**Funderar**

&quot;Vilken av dessa resor gick bra och vad utlöste de?&quot;

&quot;Kan jag återanvända den vinnande orkestrationslogiken för Wien?&quot;

**Förväntade utdata**

Lista över resor med status (aktiv, pausad, avslutad), datumintervall, målsegment, nyckeltal (öppen hastighet, aktuell tid, konvertering).

Nästa steg: Kortlista en eller två lyckade fiberresor för kloning/anpassning.

**Fråga**

`What journey was running and had Fiber in the name?`

Visa aktiva eller tidigare resor med Fibre Messaging.

Åtgärd: Kortlista högpresterande resor för kloning.

## 1.3.5 Se om det finns en relevant historisk kampanj

**Fråga**:

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey
```

**Återgivning** Förstå startdefinitionen för resan &quot;SciFi Promo 2024 - jl&quot; - vilken egenskap som driver målsättningen (t.ex. &quot;SciFi Genre Preference&quot;, &quot;4+ devices&quot;, &quot;stream ≥ 300 GB/månad&quot;).

**Funderar**

&quot;Jag vill kombinera beprövad SciFi-kreativitet med Fibre Max-prestandameddelanden.&quot;

&quot;Om publiken överlappar många nedladdare kan vi stapla alla möjligheter.&quot;

**Förväntade utdata**

Målgruppskriterier (inkludering/uteslutning), målgruppsstorlek, regionfilter, senaste besök, tröskelvärden för frekvens.

>[!NOTE]
>
>Ändra sammanhang till CJA

Från och med nu växlar marknadsföraren till analysläge för att säkerställa korrekt rapportering.

**Fråga**:

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey?
```

Granska målgruppskriterier (strömningsvanor, antal enheter).

Mål: Förstå egenskaper för behov med hög bandbredd.

## 1.3.6 Validera resans prestanda via bortfallsanalys

**Fråga**:

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey
```

>[!NOTE]
>
>Ändra sammanhang till CJA)

**Återgivning** Skapa en stegvis funnel i Customer Journey Analytics

Levererad → Öppen → Klickad → Lanserad → Produktvy → Lägg till i kundvagn → Kassa → Beställning slutförd

Inkludera fiberrelaterade SKU-vyer som en gren.

Funderar:

&quot;Var tappar vi bort människor - öppna e-postmeddelanden, läsa in landningssidor, PDP:er, utcheckningsfriktion?&quot;

&quot;studsar SciFi-användare mer eller mindre än genomsnittet på Fibre PDP?&quot;

Förväntade utdata:

En utfallsvisualisering med utfallsfrekvenser vid varje steg.

Segmentövertäckningar (SciFi kontra Sport kontra Övrigt).

Nedbrytning av enhet/webbläsare för teknisk friktion.

Beslut:

Om utcheckningen är hög ska du koordinera med product/UX för att korrigera betalningsflödet.

Om PDP-avslutningen är hög kan du göra anspråk på klarheten (hastigheter, installationstider, paketvärde) på nytt.

>[!NOTE]
>
>Ändra kontext till JO

Nu flyttar marknadsföraren in i Adobe Journey Optimizer för att få ordning och målgrupper att stanna.

**Fråga**:

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey 
```

Bygg funnel-visualisering: Levererat → Öppnad → Klickad → Checka ut → Beställning.

Åtgärd: Identifiera bortfallspunkter och optimera meddelanden eller användarupplevelse.


## 1.3.7 Hitta befintliga målgrupper som är anpassade till hög användning

**Fråga**:

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>Ändra sammanhang till Adobe Journey Optimizer

Återgivning: Hitta alla JO-målgrupper som heter&quot;tung nedladdning&quot; - troligtvis definierade med månatliga tröskelvärden för dataanvändning, timmars direktuppspelning eller enhetskontinuitet.

Funderar:

&quot;Om det finns en publik som Heavy Downloaders är det perfekt för Fibre Max-positionering: hastighet, tillförlitlighet, obegränsat antal nivåer.&quot;

Förväntade utdata:

Målgruppsmetadata: definitionskriterier, storlek, senaste uppdatering, styrningstaggar, regionens tillgänglighet.

**Fråga**:

```javascript
Is there an audience that has " heavy downloaders" in the title 
```

Hitta målgrupper med hög dataanvändning.

Mål: Kombinera med Sci-Fi-inställningar för Fibre Max-mål.

## 1.3.8 Bestäm om dessa målgrupper redan används

**Fråga**:

```javascript
Which of the above are used in a journey? 
```

Återgivning: Kontrollera länkningen mellan målgrupper och resor - se till att vi inte tvivlar på eller kolliderar med aktuella program.

Funderar:

&quot;Om stora nedladdare redan är på en kvarhållningsresa behöver vi undertryckningslogik eller frekvensbegränsning för att undvika utmattning.&quot;

Förväntade utdata:

Mappningar: målgrupp → resenamn, status, kontaktprincip, senaste sändning, prestanda.

Beslut:

Om den används kan du skapa undantag eller delad nedtryckning för att starta Wien.

Grönt ljus för ny resa om det inte används.

Fråga:

Vilket av ovanstående används i en resa?

Säkerställ att kampanjer inte överlappar varandra.

Åtgärd: Använd undertryckning om det behövs.

## 1.3.9 Skapa ny resa för Fibre Max Launch

**Fråga**:

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

Återgivning: Bygg en ny JO-resa för den sammansatta målgruppen:

Stora hämtare ∩ SciFi-inställningar (kbaa_5207bf målgruppsnyckel).

Funderar:

&quot;Det här är den ljuva fläcken för Fiber Max: hög benägenhet + kreativ relevans.&quot;

&quot;Vi kommer att skapa en multitouch-upplevelse som är knuten till Wiens tillgänglighet.&quot;

Resedesign (JO):

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

Måttplan (CJA):

Spåra: Leverans, öppna, klicka, PDP-vy, utcheckningsstart, orderslutförande.

KPI:er: Konverteringsgrad till Fiber Max, uplift vs control, timetoinstall.

Diagnostik: Utfallsrapport per enhet/genre-segment.

Form

Hur allt passar ihop (marknadsförarens mentala modell)

Diagnostisera efterfrågan (övergripande kategorier → Fiber specifikt).

Bevisa innehåll för konverteringssignal (order efter genre).

Mina framgångsrika resor (hitta Fibernamed-resor och SciFi-kampanjens målgrupp).

Validera friktionspunkter (CJA-utfall på SciFi-resa).

Aktivera mot högprioritetssegment (stora hämtningsprogram ∩ SciFi).


Gå tillbaka till [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}