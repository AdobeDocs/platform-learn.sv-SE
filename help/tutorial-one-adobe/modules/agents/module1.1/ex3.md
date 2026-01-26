---
title: Adobe Marketing Agent med Microsoft Copilot
description: Adobe Marketing Agent med Microsoft Copilot
kt: 5342
doc-type: tutorial
source-git-commit: 1eafbf27de93b45288bec8cb3cd70f04e8cc715e
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# 1.1.3 Adobe Marketing Agent med Microsoft Copilot

[!BADGE Beta]

+++Se detaljer
Genom att använda Adobe Marketing Agent med Microsoft Copilot Beta bekräftar du härmed att Beta tillhandahålls i befintligt skick utan någon garanti av något slag. Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, modifiera eller på annat sätt stödja Beta. Du rekommenderas att vara försiktig och inte på något sätt förlita dig på att sådana Beta och/eller medföljande material fungerar korrekt eller fungerar korrekt. Beta betraktas som Konfidentiell information om Adobe.  All &quot;Feedback&quot; (information om Beta, inklusive men inte begränsad till problem eller defekter som du stöter på när du använder Beta, förslag, förbättringar och rekommendationer) som du ger Adobe tilldelas härmed till Adobe, inklusive alla rättigheter, titlar och intressen i och för sådan feedback.

+++

>[!IMPORTANT]
>
>Det här labbet använder en funktion som inte har släppts än. Funktionen är fortfarande under utveckling så den är inte allmänt tillgänglig än.

## Förhandskrav

För att kunna följa stegen i detta labb enligt nedan krävs följande åtkomst:

- Tillgång till Real-Time CDP, Journey Optimizer och Customer Journey Analytics
- Åtkomst till AI Assistant i Adobe Experience Cloud
- Tillgång till AEP Agent Orchestrator
- Åtkomst till Microsoft Copilot

## Video

I den här videon får du en förklaring och demonstration av alla steg som ingår i övningen.

>[!VIDEO](https://video.tv.adobe.com/v/3479158?quality=12&learn=on)

## 1.1.3.1 Lägg till Adobe Marketing Agent i Microsoft Teams &amp; Copilot

Öppna Microsoft Teams och logga in med din kontoinformation. När du är inloggad bör du se det här.

Klicka på **Appar**.

![ChatGPT](./images/copilot1.png)

Välj **Hantera dina program**.

![ChatGPT](./images/copilot2.png)

Välj **Överför en app**.

![ChatGPT](./images/copilot3.png)

Välj **Överför en anpassad app**.

![ChatGPT](./images/copilot4.png)

Markera den manifestfil som du har fått av din instruktör och klicka på **Öppna**.

![ChatGPT](./images/copilot5.png)

Klicka på **Lägg till**.

![ChatGPT](./images/copilot6.png)

Klicka på **Öppna med Copy**.

![ChatGPT](./images/copilot7.png)

Adobe Marketing Agent har lästs in.

![ChatGPT](./images/copilot8.png)

Skriv uppmaningen `login` och klicka på knappen **Skicka**.

![ChatGPT](./images/copilotlogin1.png)

Klicka på **Logga in på Adobe Marketing Agent**.

![ChatGPT](./images/copilotlogin2.png)

Ett nytt fönster öppnas där du ombeds logga in med dina Adobe-kontouppgifter.

![ChatGPT](./images/copilotlogin3.png)

När autentiseringen är klar kan du behöva markera den specifika instans som du vill använda. Om den här skärmen visas markerar du instansen —aepImsOrgName—.

![ChatGPT](./images/copilotlogin4.png)

Sedan kommer en liknande kod att genereras. Klicka på **Kopiera** för att kopiera koden.

![ChatGPT](./images/copilotlogin5.png)

Klistra in koden i Adobe Marketing Agent-fönstret i Copilot och klicka på knappen **Skicka** .

![ChatGPT](./images/copilotlogin6.png)

Du borde se något liknande. Du är nu inloggad på Adobe Marketing Agent i Microsoft Copilot.

![ChatGPT](./images/copilotlogin7.png)

## 1.1.3.2 Ange kontext i Adobe Marketing Agent

Innan du kan interagera ytterligare med Adobe Marketing Agent via Copilot måste kontexten anges.

För den här övningen måste kontexten ställas in så att den används:

- **Sandbox**: **Prod - Accelerate (VA7)**

  Inställningen för sandlådan hjälper dig att identifiera vilken sandlåda som AI-assistenten ska titta på när du ställer frågor.

- **Datavy**: **Accelerate 2026 B2C**

  Inställningen för datavy hjälper dig att identifiera vilken AI-assistent för datavyer som ska titta på när du ställer frågor.

![Agent Orchestrator](./images/copilotlogin7.png)

Om du vill ändra sandlådan anger du följande kommando och klickar på knappen **Skicka** .

```javascript
change sandbox
```

![Agent Orchestrator](./images/copilot9.png)

Du borde se något liknande. Markera den sandlåda som du behöver använda och klicka på **välj**.

![Agent Orchestrator](./images/copilot10.png)

Du borde se det här då. Om du vill ändra datavyn anger du följande kommando och klickar på knappen **Skicka** .

```javascript
change dataview
```

![Agent Orchestrator](./images/copilot11.png)

Du borde se något liknande. Markera den datavy som du vill använda och klicka på **välj**.

![Agent Orchestrator](./images/copilot12.png)

Du borde se det här då. Kontexten är nu korrekt inställd så att du kan börja skicka särskilda uppmaningar härnäst.

![Agent Orchestrator](./images/copilot13.png)

## 1.1.3.3 Börja med allmänna köptrender för att förankra kontext och zooma in på fiber

**Återgivning**

Få en puls på högsta nivå vid behov - Mobile, Landline, Internet, TV, Fibre - särskilt de senaste 60 dagarna. Här anges baslinjer för säsongsbundenhet, kampanjeffekter och regionala variationer efter lanseringen av New York.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me purchases by mainCategory over the last 4 months.
```

![Agent Orchestrator](./images/copilot18.png)

Du bör då se det här:

![Agent Orchestrator](./images/copilot19.png)

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me purchases by mainCategory = Fiber over the last 4 months broken down by week
```

![Agent Orchestrator](./images/copilot20.png)

Du borde se det här, som fördjupar dig i fiberspecifika trender.

![Agent Orchestrator](./images/copilot21.png)

## 1.1.3.4 Korrelera order med innehållsinställningar

**Återgivning**

Testa hypotesen om att en inställning för en viss genre (t.ex. SciFi, Sport, Drama) förutsäger hur bredbandsuppgraderingen fungerar - särskilt för behov med hög bandbredd.

Först måste du ta reda på vilket fält som används för att lagra genre-inställningen.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Which field is used to store the preferred genre
```

![Agent Orchestrator](./images/copilot22.png)

Du bör då se det här, som visar att fältet som används för genren är **_experiencePlatform.individualCharacpropertics.preferences.preferredGenre**.

![Agent Orchestrator](./images/copilot23.png)

Med den informationen kan du börja detaljgranska köpdata.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me ordersYTD by preferredGenre for the last 4 months
```

![Agent Orchestrator](./images/copilot24.png)

Du borde se det här då. Klicka på **Visa data**.

![Agent Orchestrator](./images/copilot25.png)

Du borde se det här då.

![Agent Orchestrator](./images/copilot26.png)

## 1.1.3.5 Identifiera befintliga Fibre Journeys

**Återgivning**

Upptäck vilka aktiva eller nyligen avslutade resor som innehåller&quot;Fiber&quot; i titeln, t.ex.&quot;Fibre Upgrade NYC - Sept&quot;,&quot;Fibre Trial - Streaming Bundle&quot;.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/copilot28.png)

Då borde ni se en lista över resor.

![Agent Orchestrator](./images/copilot29.png)

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/copilot31.png)

Du borde se det här då.

![Agent Orchestrator](./images/copilot33.png)

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/copilot35.png)

Du borde se det här då.

![Agent Orchestrator](./images/copilot36.png)

## 1.1.3.6 Validera reseprestanda via utfallsanalys

**Återgivning**

Du vill förstå hur väl resan fungerar och veta om det finns några noder eller villkor under resan som har en stor andel profiler som tas bort. Detta är till hjälp när det gäller att förstå om ytterligare justeringar behövs under resan.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/copilot37.png)

Du borde se det här då.

![Agent Orchestrator](./images/copilot38.png)

Rulla ned lite till för att se observationer och rekommendationer. Klicka på de tre punkterna **..** och välj sedan **Reseinformation** för att öppna den specifika resan i Adobe Journey Optimizer.

![Agent Orchestrator](./images/copilot40.png)

Du borde se det här då.

![Agent Orchestrator](./images/copilot41.png)

Du har nu slutfört det här labbet.

Gå tillbaka till [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}