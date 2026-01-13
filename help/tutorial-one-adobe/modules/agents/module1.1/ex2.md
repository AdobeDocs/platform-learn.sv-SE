---
title: Adobe Marketing Agent med ChatGPT
description: Adobe Marketing Agent med ChatGPT
kt: 5342
doc-type: tutorial
source-git-commit: 9663ef2838024e293acc72c203b1e3578911d57f
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# 1.1.2 Adobe Marketing Agent med ChatGPT

>[!IMPORTANT]
>
>Det här labbet använder en funktion som inte har släppts än. Funktionen är fortfarande under utveckling så den är inte allmänt tillgänglig än.

## Video

I den här videon får du en förklaring och demonstration av alla steg som ingår i övningen.

>[!VIDEO](https://video.tv.adobe.com/v/3478410?quality=12&learn=on)

## 1.1.2.1 Skapa en anpassad app i ChatGPT för Adobe Marketing Agent

>[!NOTE]
>
>För att använda Adobe Marketing Agent i ChatGPT krävs följande:
>- en betald version av OpenAI&#39;s ChatGPT
>- med ChatGPT-webbklienten

Gå till https://chatgpt.com/ och logga in med din kontoinformation. När du är inloggad bör du se det här. Klicka på ditt användarnamn.

![ChatGPT](./images/chatgpt1.png)

Välj **Inställningar**.

![ChatGPT](./images/chatgpt2.png)

Gå till **Appar** och välj sedan **Avancerade inställningar**.

![ChatGPT](./images/chatgpt3.png)

Aktivera **utvecklarläget** och klicka sedan på **Bakåt**.

![ChatGPT](./images/chatgpt4.png)

Klicka på **Skapa app**.

![ChatGPT](./images/chatgpt5.png)

Fyll i fälten så här:

- **Namn**: `Adobe Marketing Agent`
- **URL för MCP-server**: kontakta din Adobe-representant
- **Autentisering**: `OAuth`

Markera kryssrutan för **Jag förstår och vill fortsätta**.

Klicka på **Skapa**.

![ChatGPT](./images/chatgpt6.png)

ChatGPT kommer nu att försöka ansluta till ditt Adobe-konto. Välj **Tillåt åtkomst** och sedan måste du logga in med ditt Adobe-konto.

![ChatGPT](./images/chatgpt7.png)

När du har loggat in bör du se att din Adobe Marketing Agent är ansluten.

![ChatGPT](./images/chatgpt8.png)

## 1.1.2.2 Ange kontext i Adobe Marketing Agent

Stäng fönstret.

![Agent Orchestrator](./images/chatgpt9.png)

Du borde se det här då. Klicka på ikonen **+**, gå till **Mer** och välj sedan **Adobe Marketing Agent**.

![Agent Orchestrator](./images/chatgpt10.png)

Innan du kan interagera ytterligare med Adobe Marketing Agent via ChatGPT måste kontexten anges.

För den här övningen måste kontexten ställas in så att den används:

- **Sandbox**: **Prod - Accelerate (VA7)**

Inställningen Sandlåda hjälper dig att identifiera vilken AI-assistent för sandlådan som ska titta på när du ställer frågor.

- **Datavy**: **Accelerate 2026 B2C**

Inställningen Datavy hjälper dig att identifiera vilken AI-assistent för datavyer som ska titta på när du ställer frågor.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
list sandboxes
```

![Agent Orchestrator](./images/chatgpt11.png)

Du bör då se en liknande lista över tillgängliga sandlådor. Den aktuella sandlådan i det här exemplet är inställd på **prod**.

Om du vill ändra det till den sandlåda som ska användas anger du följande **Fråga** och klickar på knappen **Skicka** .

```javascript
switch to sandbox accelerate
```

![Agent Orchestrator](./images/chatgpt12.png)

Du borde se det här då. Klicka på **Ange kontext**.

![Agent Orchestrator](./images/chatgpt13.png)

Du borde se det här då. Ange följande **Fråga** och klicka på knappen **skicka** för att ange att datavyn ska användas.

```javascript
list dataviews
```

![Agent Orchestrator](./images/chatgpt14.png)

Du bör då se en liknande lista över tillgängliga sandlådor. Den aktuella sandlådan i det här exemplet är inställd på **prod**.

Om du vill ändra det till den sandlåda som ska användas anger du följande **Fråga** och klickar på knappen **Skicka** .

```javascript
switch to Accelerate 2026 B2C
```

![Agent Orchestrator](./images/chatgpt15.png)

Du borde se det här då. Klicka på **Ange kontext**.

![Agent Orchestrator](./images/chatgpt16.png)

Du borde se det här då.

![Agent Orchestrator](./images/chatgpt17.png)

Din kontext är nu en egenskapsuppsättning, så du kan börja skicka särskilda uppmaningar härnäst.

## 1.1.2.3 Börja med allmänna köptrender för att förankra kontext och zooma in på fiber

**Återgivning**

Få en puls på högsta nivå vid behov - Mobile, Landline, Internet, TV, Fibre - särskilt de senaste 60 dagarna. Här anges baslinjer för säsongsbundenhet, kampanjeffekter och regionala variationer efter lanseringen av New York.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/chatgpt18.png)

Du bör då se det här:

![Agent Orchestrator](./images/chatgpt19.png)

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/chatgpt20.png)

Du borde se det här, som fördjupar dig i fiberspecifika trender.

![Agent Orchestrator](./images/chatgpt21.png)

## 1.1.2.4 Korrelera order med innehållsinställningar

**Återgivning**

Testa hypotesen om att en inställning för en viss genre (t.ex. SciFi, Sport, Drama) förutsäger hur bredbandsuppgraderingen fungerar - särskilt för behov med hög bandbredd.

Först måste du ta reda på vilket fält som används för att lagra genre-inställningen.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Which field is used to store the preferred genre in the sandbox accelerate?
```

![Agent Orchestrator](./images/chatgpt22.png)

Du bör då se det här, som visar att fältet som används för genren är **_experiencePlatform.individualCharacpropertics.preferences.preferredGenre**.

![Agent Orchestrator](./images/chatgpt23.png)

Med den informationen kan du börja detaljgranska köpdata.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/chatgpt24.png)

Du borde se det här då. Klicka på **Referensinformation**.

![Agent Orchestrator](./images/chatgpt25.png)

Du borde se det här då.

![Agent Orchestrator](./images/chatgpt26.png)

Bläddra nedåt om du vill se mer information.

![Agent Orchestrator](./images/chatgpt27.png)

## 1.1.2.5 Identifiera befintliga Fibre Journeys

**Återgivning**

Upptäck vilka aktiva eller nyligen avslutade resor som innehåller&quot;Fiber&quot; i titeln, t.ex.&quot;Fibre Upgrade NYC - Sept&quot;,&quot;Fibre Trial - Streaming Bundle&quot;.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/chatgpt28.png)

Du borde se det här då. Klicka på **Referensinformation**.

![Agent Orchestrator](./images/chatgpt29.png)

Då borde ni se en lista över resor.

![Agent Orchestrator](./images/chatgpt30.png)

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/chatgpt31.png)

Du borde se det här då. Klicka på **Referensinformation**.

![Agent Orchestrator](./images/chatgpt32.png)

Du borde se det här då.

![Agent Orchestrator](./images/chatgpt33.png)

Bläddra nedåt om du vill se mer information.

![Agent Orchestrator](./images/chatgpt34.png)

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/chatgpt35.png)

Du borde se det här då.

![Agent Orchestrator](./images/chatgpt36.png)

## 1.1.2.6 Validera reseprestanda via utfallsanalys

**Återgivning**

Du vill förstå hur väl resan fungerar och veta om det finns några noder eller villkor under resan som har en stor andel profiler som tas bort. Detta är till hjälp när det gäller att förstå om ytterligare justeringar behövs under resan.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/chatgpt37.png)

Du borde se det här då.

![Agent Orchestrator](./images/chatgpt38.png)

Rulla ner lite. Du kan nu granska tabellen genom att granska varje nod och dess respektive nummer, bortfallsnummer och utfallsfrekvens.

![Agent Orchestrator](./images/chatgpt39.png)

Rulla ned lite till för att se observationer och rekommendationer.

![Agent Orchestrator](./images/chatgpt40.png)

Du har nu slutfört det här labbet.

Gå tillbaka till [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}