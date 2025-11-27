---
title: Komma igång med Agent Orchestrator
description: Komma igång med Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: 121cbb5ea8f8b713c6ebae008f7f0d9b3a79e476
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 0%

---

# 1.1.1 Komma igång med Agent Orchestrator

## Video

I den här videon får du en förklaring och demonstration av alla steg som ingår i övningen.

>[!VIDEO](https://video.tv.adobe.com/v/3477257?quality=12&learn=on)

## 1.1.1.1 Ange kontext i Agent Orchestrator

Gå till [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Du borde se det här då. Kontrollera att du är i organisationen **Experience Platform International**.

![Agent Orchestrator](./images/ao1.png)

Klicka på fönstret **context**.

![Agent Orchestrator](./images/ao2.png)

Ställ in kontexten på:

- **Dokumentation för Source**: **Journey Optimizer**

Inställningen Documentation Source hjälper dig att ge preferenser till vilka upplevelselektionsdokument som ska söka efter frågor som rör produktkunskap/Experience League.

- **Sandbox**: **Prod - Accelerate (VA7)**

Inställningen Sandlåda hjälper dig att identifiera vilken AI-assistent för sandlådan som ska titta på när du ställer frågor.

- **Datavy**: **Accelerate 2026 B2C**

Inställningen Datavy hjälper dig att identifiera vilken AI-assistent för datavyer som ska titta på när du ställer frågor.

Klicka på **Ange kontext**.

![Agent Orchestrator](./images/ao3.png)

## 1.1.1.2 Börja med allmänna köptrender för att förankra kontext och zooma in på fiber

**Återgivning**

Få en puls på högsta nivå vid behov - Mobile, Landline, Internet, TV, Fibre - särskilt de senaste 60 dagarna. Här anges baslinjer för säsongsbundenhet, kampanjeffekter och regionala variationer efter lanseringen av New York.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

Du bör då se det här:

![Agent Orchestrator](./images/ao5.png)

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/ao6.png)

Du borde se det här, som fördjupar dig i fiberspecifika trender.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Korrelera order med innehållsinställningar

**Återgivning**

Testa hypotesen om att en inställning för en viss genre (t.ex. SciFi, Sport, Drama) förutsäger hur bredbandsuppgraderingen fungerar - särskilt för behov med hög bandbredd.

Först måste du ta reda på vilket fält som används för att lagra genre-inställningen.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Which field is used to store the preferred genre?
```

![Agent Orchestrator](./images/ao7a.png)

Du bör då se det här, som visar att fältet som används för genren är **_experiencePlatform.individualCharacpropertics.preferences.preferredGenre**.

![Agent Orchestrator](./images/ao7b.png)

Med den informationen kan du börja detaljgranska köpdata.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Du borde se det här då. Klicka på ikonen i blocket **Reasoning klar** för att förstå vad som händer i Agent Orchestrator bakom kulisserna.

![Agent Orchestrator](./images/ao9.png)

Du bör då se en liknande förklaring.

![Agent Orchestrator](./images/ao10.png)

## 1.1.1.4 Identifiera befintliga Fibre Journeys

**Återgivning**

Upptäck vilka aktiva eller nyligen avslutade resor som innehåller&quot;Fiber&quot; i titeln, t.ex.&quot;Fibre Upgrade NYC - Sept&quot;,&quot;Fibre Trial - Streaming Bundle&quot;.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Du borde se det här då. Klicka på **Visa mer**.

![Agent Orchestrator](./images/ao13.png)

Du bör då se en större lista över aktiva eller tidigare resor. Klicka på ikonen **download** om du vill hämta en lista över de här resorna.

![Agent Orchestrator](./images/ao13a.png)

Då skapas en CSV-fil som innehåller alla utdata från AI-assistenten.

![Agent Orchestrator](./images/ao13b.png)

Klicka för att stänga den högra rutan. Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Du borde se det här då. Klicka på länken på en av resorna och välj **Reseinformation**.

![Agent Orchestrator](./images/ao15.png)

Ett nytt fönster öppnas och du kommer direkt till översikten över reseinformation.

![Agent Orchestrator](./images/ao15a.png)

## 1.1.1.5 Kontrollera vilken målgrupp som används

**Återgivning**:

Förstå startvärdesdefinitionen för resan&quot;CitiSignal - Fiber Max Launch Promotion&quot; - vilka egenskaper som driver målsättningen (t.ex.&quot;SciFi Genre Preference&quot;,&quot;4+ enheter&quot;,&quot;ström ≥ 300 GB/månad&quot;).

Ange följande **Fråga**:

```javascript
What was the initial audience in the journey named 
```

Ange sedan manuellt i `+CitiSignal fib` för att aktivera automatisk komplettering. Välj resan **CitiSignal - maximal startkampanj för Fibre**.

![Agent Orchestrator](./images/ao16.png)

Du borde se det här då. Klicka på knappen **Skicka**.

![Agent Orchestrator](./images/ao17.png)

Du borde se det här då.

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 Validera reseprestanda via utfallsanalys

**Återgivning**

Du vill förstå hur väl resan fungerar och veta om det finns några noder eller villkor under resan som har en stor andel profiler som tas bort. Detta är till hjälp när det gäller att förstå om ytterligare justeringar behövs under resan.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

Du borde se det här då.

![Agent Orchestrator](./images/ao20.png)

Rulla ner lite. Du kan nu granska tabellen genom att granska varje nod och dess respektive nummer, bortfallsnummer och utfallsfrekvens.

AI Assistant ger dig observationer och rekommendationer.

Klicka på meningen **Så här fick jag resultaten**.

![Agent Orchestrator](./images/ao21.png)

Du kan sedan se de steg som AI Assistant följer för att nå resultaten.

![Agent Orchestrator](./images/ao22.png)

## 1.1.1.7 Skapa en ny publik

**Återgivning**

Baserat på ovanstående resultat och undersökningar finns det en korrelation mellan kunder som konsumerar mycket data och som har en föredragen genre av sci-fi eller fantasi. Du kommer nu att kombinera dessa attribut i en målgrupp.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Create an audience that combines people with an average download usage per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

Granska planen. Ange `yes` och klicka på **send**.

>[!NOTE]
>
>Planen genereras baserat på en referenshandbok i systemet. Kunderna kommer till slut att kunna anpassa planer och lägga till egna planer, men för tillfället är de statiska.

![Agent Orchestrator](./images/ao33.png)

Granska segmentfrågeuttrycket. Ange `yes` och klicka på knappen **Skicka**.

![Agent Orchestrator](./images/ao34.png)

Granska uppskattningen av segmentstorleken. Ange `yes` och klicka på knappen **Skicka**.

![Agent Orchestrator](./images/ao35.png)

Klicka på **Granska**.

![Agent Orchestrator](./images/ao36.png)

Granska segmentdefinitionen. Klicka på **Skapa**.

![Agent Orchestrator](./images/ao37.png)

Din målgrupp har nu skapats.

![Agent Orchestrator](./images/ao38.png)

>[!NOTE]
>
>När du skapar en ny målgrupp tar det 24 timmar innan målgruppen är tillgänglig för AI Assistant för ytterligare användning.

## 1.1.1.8 Hitta befintliga målgrupper som är anpassade till hög användning och kontrollera om de används

**Återgivning**:

Hitta en målgrupp som heter&quot;tung nedladdning&quot;, som definieras av tröskelvärden för användning av månadsdata.

>[!NOTE]
>
>I det föregående steget skapade du en ny målgrupp, kom ihåg att det kommer att ta 24 timmar innan målgruppen är tillgänglig för AI Assistant för ytterligare användning. Nu bör ni använda en annan befintlig målgrupp istället.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Du borde se det här då. Nu vill ni se alla era målgrupper och hur mycket de har förändrats de senaste dagarna.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
List how much these audiences changed over the last few days.
```

![Agent Orchestrator](./images/ao31.png)

Du borde se det här då. Klicka på **Visa mer**.

![Agent Orchestrator](./images/ao31a.png)

Du borde se det här då. Klicka för att stänga den högra rutan.

![Agent Orchestrator](./images/ao31b.png)

Bläddra nedåt lite för att se hur AI Assistant fungerar.

![Agent Orchestrator](./images/ao31c.png)

Det finns redan en del befintliga målgrupper för&quot;tunga nedladdare&quot;. Låt oss se om de redan används.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao50.png)

Du borde se något liknande.

![Agent Orchestrator](./images/ao51.png)

Nu bör du verifiera om resan är aktiv. Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Are these journeys active? 
```

![Agent Orchestrator](./images/ao52.png)

Du borde se något liknande. Ingen av dessa resor är igång just nu.

![Agent Orchestrator](./images/ao53.png)

För den kommande lanseringen av Fiber Max bör du nu skapa en ny resa.

## 1.1.1.9 Skapa ny resa för Fibre Max-start

**Återgivning**:

Bygg en ny resa för den sammansatta målgruppen:

Stora hämtare ∩ SciFi-inställningar.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Du borde se det här då. Ange `yes` och klicka på generera.

![Agent Orchestrator](./images/aocj2.png)

Du borde se det här då. Ange `yes` och klicka på generera.

![Agent Orchestrator](./images/aocj3.png)

Du borde se det här då. Ange `The first one` och klicka på Skicka.

![Agent Orchestrator](./images/aocj4.png)

Du borde se det här då. Ange `yes` och klicka på Skicka.

![Agent Orchestrator](./images/aocj5.png)

Granska svaret. Ange `yes` och klicka på Skicka.

![Agent Orchestrator](./images/aocj6.png)

Klicka på **Granska**.

![Agent Orchestrator](./images/aocj7.png)

Uppdatera resenamnet med din LDAP för att göra det unikt. Klicka på **Spara**.

![Agent Orchestrator](./images/aocj8.png)

Din resa har nu skapats i utkastläge.

![Agent Orchestrator](./images/aocj9.png)

## Hantering av 1.1.1.10-resekonflikter

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
How can I manage journey conflicts?
```

![Agent Orchestrator](./images/aocj80.png)

Granska informationen.

![Agent Orchestrator](./images/aocj81.png)

Bläddra nedåt och välj **Källor** för att hitta informationen som kommer från Experience League.

![Agent Orchestrator](./images/aocj82.png)

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
List any conflicts for the journey +CitiSignal Fiber Max
```

Välj sedan manuellt resan **CitiSignal - maximal startkampanj för Fibre** i listan.

![Agent Orchestrator](./images/aocj70.png)

Du borde se det här då. Klicka på **skicka**.

![Agent Orchestrator](./images/aocj70a.png)

Granska information om resekonflikter.

![Agent Orchestrator](./images/aocj71.png)

Bläddra nedåt för att hitta fler detaljer om resekonflikter.

![Agent Orchestrator](./images/aocj72.png)

## 1.1.1.11 experiment

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Du bör då se det här:

![Agent Orchestrator](./images/aoea1.png)

Bläddra nedåt och klicka på något av förslagen. Klicka på **skicka**.

>[!NOTE]
>
>Förslagen är dynamiska så att du kan förvänta dig olika förslag varje gång ett svar genereras. Dina förslag kommer troligtvis att skilja sig från de förslag som visas i den här skärmbilden.

![Agent Orchestrator](./images/aoea2.png)

Du bör då se ett detaljerat svar om det förslag som valdes.

![Agent Orchestrator](./images/aoea4.png)

Du har nu slutfört det här labbet.

Gå tillbaka till [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}