---
title: Komma igång med Agent Orchestrator
description: Komma igång med Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: dee5b0855eeeb455bf22f511d11cd13f7e904889
workflow-type: tm+mt
source-wordcount: '1112'
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

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

Du borde se det här, som fördjupar dig i fiberspecifika trender.

**Åtgärd**: Observera tillväxtkurvan och regionala toppar.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Korrelera order med innehållsinställningar

**Återgivning**

Testa hypotesen om att innehållsinställningen (t.ex. SciFi, Sport, Drama) förutser hur bredbandsuppgraderingen fungerar - särskilt för behov med hög bandbredd.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Du bör då se det här:

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 Identifiera befintliga Fibre Journeys

**Återgivning**

Upptäck vilka aktiva eller nyligen avslutade resor som innehåller&quot;Fiber&quot; i titeln, t.ex.&quot;Fibre Upgrade NYC - Sept&quot;,&quot;Fibre Trial - Streaming Bundle&quot;.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Du bör då se det här:

![Agent Orchestrator](./images/ao13.png)

Visa aktiva eller tidigare resor med Fibre Messaging.

Åtgärd: Kortlista högpresterande resor för kloning.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Du bör då se det här:

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 Kontrollera startvärdet

**Återgivning**:

Förstå startvärdesdefinitionen för resan&quot;CitiSignal - Fiber Max Launch Promotion&quot; - vilka egenskaper som driver målsättningen (t.ex.&quot;SciFi Genre Preference&quot;,&quot;4+ enheter&quot;,&quot;ström ≥ 300 GB/månad&quot;).

Ange följande **Fråga** och ange sedan fib **+CitiSignal** för att aktivera automatisk komplettering. Välj resan **CitiSignal - maximal startkampanj för Fibre**.

```javascript
What was the initial audience in the journey named 
```

![Agent Orchestrator](./images/ao16.png)

Du borde se det här då. Klicka på knappen **Skicka**.

![Agent Orchestrator](./images/ao17.png)

Du borde se det här då.

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 Validera reseprestanda via utfallsanalys

**Återgivning**

Bygg en stegvis funnel i Customer Journey Analytics

Levererad → Öppen → Klickad → Lanserad → Produktvy → Lägg till i kundvagn → Kassa → Beställning slutförd

Inkludera fiberrelaterade SKU-vyer som en gren.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

## 1.1.1.7 Skapa en ny publik

**Återgivning**

Baserat på ovanstående resultat finns det en korrelation mellan kunder som konsumerar mycket data och som har en föredragen genre av sci-fi eller fantasi. Du kommer nu att kombinera dessa attribut i en målgrupp.

Gå till [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Ange följande **Fråga** och klicka på knappen **Skicka**.

>[!NOTE]
>
>Verifiera att assistentens kontext pekar på sandlådan **Accelerate** och datavyn **Accelerate 2026 B2C**

```javascript
Create an audience that combines people with an average download per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

Granska planen. Ange `yes` och klicka på **send**.

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
>När du skapar en ny målgrupp tar det 24 timmar innan målgruppen är tillgänglig för assistenten för vidare användning.

## 1.1.1.8 Hitta befintliga målgrupper som är anpassade till hög användning och kontrollera om de används

**Återgivning**:

Hitta en målgrupp som heter&quot;tung nedladdning&quot;, som definieras av tröskelvärden för användning av månadsdata.

>[!NOTE]
>
>I föregående steg skapade du en ny målgrupp, kom ihåg att det kommer att ta 24 timmar innan målgruppen är tillgänglig för assistenten för ytterligare användning. Nu bör ni använda en annan befintlig målgrupp istället.

Gå till [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Du borde se det här då. Kontrollera att du är i organisationen **Experience Platform International**.

Ange följande **Fråga** och klicka på knappen **Skicka**.

>[!NOTE]
>
>Verifiera att assistentens kontext pekar på sandlådan **Accelerate** och datavyn **Accelerate 2026 B2C**

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Du borde se det här då.

![Agent Orchestrator](./images/ao31.png)

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
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao52.png)

Du borde se något liknande. Den resan går inte just nu.

![Agent Orchestrator](./images/ao53.png)

För den kommande lanseringen av Fiber Max bör du nu skapa en ny resa.

## 1.1.1.9 Skapa ny resa för Fibre Max-start

**Återgivning**:

Bygg en ny resa för den sammansatta målgruppen:

Stora hämtare ∩ SciFi-inställningar (kbaa_5207bf målgruppsnyckel).

Gå till [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Du borde se det här då. Kontrollera att du är i organisationen **Experience Platform International**.

Ange följande **Fråga** och klicka på knappen **Skicka**.

>[!NOTE]
>
>Verifiera att assistentens kontext pekar på sandlådan **Accelerate** och datavyn **Accelerate 2026 B2C**

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

## Hantering av 1.1.1.10-resekonflikter

Gå till [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Du borde se det här då. Kontrollera att du är i organisationen **Experience Platform International**.

Ange följande **Fråga** och klicka på knappen **Skicka**.

>[!NOTE]
>
>Kontrollera att hjälpens sammanhang pekar mot dokumentationskällan **Journey Optimizer**, sandlådan **Accelerate** och datavyn **Accelerate 2026 B2C**

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
List any conflicts for "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aocj70.png)

Granska information om resekonflikter.

![Agent Orchestrator](./images/aocj71.png)

Bläddra nedåt för att hitta fler detaljer om resekonflikter.

![Agent Orchestrator](./images/aocj72.png)

## 1.1.1.11 experiment

Gå till [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Du borde se det här då. Kontrollera att du är i organisationen **Experience Platform International**.

Ange följande **Fråga** och klicka på knappen **Skicka**.

>[!NOTE]
>
>Verifiera att assistentens kontext pekar på sandlådan **Accelerate** och datavyn **Accelerate 2026 B2C**

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Du bör då se det här:

![Agent Orchestrator](./images/aoea1.png)

Klicka på förslaget för att jämföra konverteringsgraden för varje behandling och klicka sedan på **send**.

![Agent Orchestrator](./images/aoea2.png)

Du bör då se en detaljerad jämförelse som den här:

![Agent Orchestrator](./images/aoea4.png)

Gå tillbaka till [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}