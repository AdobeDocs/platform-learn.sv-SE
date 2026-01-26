---
title: CJA & ChatGPT med MCP-server
description: CJA & ChatGPT med MCP-server
kt: 5342
doc-type: tutorial
source-git-commit: ca2812e14a22b80b7f00066f9cc482e708b4ac6a
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# 1.5.1 CJA &amp; ChatGPT med MCP-server

>[!IMPORTANT]
>
>Det här labbet använder en funktion som inte har släppts än. Funktionen är fortfarande under utveckling så den är inte allmänt tillgänglig än.


>[!NOTE]
>
>Den här övningen när du konfigurerar och använder en MCP-server med ChatGPT för att ansluta till CJA är relaterad till den här övningen [1.1 Customer Journey Analytics: Bygg en kontrollpanel med Analysis Workspace ovanpå Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md). CJA datavy och anslutning som används i övningen nedan är den datavy och anslutning som skapades i övningen. Om du vill upprepa resultaten nedan bör du följa dessa anvisningar först.

## Video

I den här videon får du en förklaring och demonstration av alla steg som ingår i övningen.

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1 Skapa en anpassad app i ChatGPT för CJA

>[!NOTE]
>
>För att använda CJA i ChatGPT krävs följande:
>- en betald version av OpenAI&#39;s ChatGPT
>- med ChatGPT-webbklienten

Gå till [https://chatgpt.com/](https://chatgpt.com/){target="_blank"} och logga in med din kontoinformation. När du är inloggad bör du se det här. Klicka på ditt användarnamn.

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

- **Namn**: `CJA`
- **URL för MCP-server**: kontakta din Adobe-representant
- **Autentisering**: `OAuth`

Markera kryssrutan för **Jag förstår och vill fortsätta**.

Klicka på **Skapa**.

![ChatGPT](./images/chatgpt6.png)

När du har loggat in bör du se att din CJA-app nu är ansluten.

![ChatGPT](./images/chatgpt8.png)

## 1.5.1.2 Ange kontext i CJA

Stäng fönstret.

![ChatGPT och CJA](./images/chatgpt9.png)

Du borde se det här då. Klicka på ikonen **+**, gå till **Mer** och välj sedan **CJA**.

![ChatGPT och CJA](./images/chatgpt10.png)

Innan du kan interagera ytterligare med CJA via ChatGPT måste kontexten anges.

För den här övningen måste kontexten ställas in så att den används:

- **Datavy**: **—aepUserLdap— - Datavy för flera kanaler**

Inställningen Datavy hjälper dig att identifiera vilka dataView ChatGPT ska titta på när du ställer frågor.

Ange följande **Fråga** och klicka på knappen **Skicka**.

```javascript
list dataviews
```

![ChatGPT och CJA](./images/chatgpt11.png)

Du bör då se en liknande lista över tillgängliga datavyer.

![ChatGPT och CJA](./images/chatgpt11a.png)

Om du vill ändra det till den datavy som ska användas anger du följande **Fråga** och klickar på knappen **Skicka**.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![ChatGPT och CJA](./images/chatgpt12.png)

Du borde se det här då.

![ChatGPT och CJA](./images/chatgpt16.png)

Din kontext är nu korrekt inställd, så du kan börja skicka särskilda uppmaningar härnäst.

## 1.5.1.3 Utforska datavyn

>[!NOTE]
>
>Datavyn som används här har konfigurerats som en del av övningen [Skapa en datavy](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

Ange följande **Fråga** och klicka på knappen **skicka** för att utforska vilka mätvärden och dimensioner som är tillgängliga för dig.

```javascript
list the available metrics and dimensions
```

![ChatGPT och CJA](./images/chatgpt101.png)

Du bör sedan se det här svaret, som innehåller mått och dimensioner som har ställts in som en del av övningen [Skapa en datavy](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

![ChatGPT och CJA](./images/chatgpt102.png)

## 1.5.1.4 friformstabell - produktvyer

Nu kan du börja utforska data. Börja med att ange uppmaningen nedan och klicka på **send** för att skicka din rapportförfrågan.

```javascript
how many product views happened on January 21?
```

![ChatGPT och CJA](./images/chatgpt103.png)

Välj **RunReport**.

![ChatGPT och CJA](./images/chatgpt104.png)

Du borde då se ett liknande svar.

![ChatGPT och CJA](./images/chatgpt105.png)

Nu kan du bryta ned svaret genom att lägga till en dimension. Ange följande **uppmaning** och klicka på knappen **skicka**.

```javascript
break down product views by product name
```

![ChatGPT och CJA](./images/chatgpt106.png)

Du borde då se ett liknande svar.

![ChatGPT och CJA](./images/chatgpt107.png)

Nu kan du även skapa en visualisering. Ange följande **uppmaning** och klicka på knappen **skicka**.

```javascript
create a line visualization by hour for product views on January 21
```

![ChatGPT och CJA](./images/chatgpt108.png)

Välj **UpsertProject**.

![ChatGPT och CJA](./images/chatgpt109.png)

Välj **RunReport**.

![ChatGPT och CJA](./images/chatgpt110.png)

Du borde se det här då.

![ChatGPT och CJA](./images/chatgpt111.png)

Rulla ned.

![ChatGPT och CJA](./images/chatgpt112.png)

Du kan nu även hämta det här linjediagrammet. Ange följande **uppmaning** och klicka på knappen **skicka**.

```javascript
export this chart to PNG
```

![ChatGPT och CJA](./images/chatgpt113.png)

Du borde se det här då. Klicka på **Hämta PNG**.

![ChatGPT och CJA](./images/chatgpt114.png)

Ange följande **uppmaning** och klicka på knappen **skicka**.

```javascript
can you breakdown product views by user agent?
```

![ChatGPT och CJA](./images/chatgpt115.png)

Välj **RunReport**.

![ChatGPT och CJA](./images/chatgpt116.png)

Du borde se det här då.

![ChatGPT och CJA](./images/chatgpt117.png)

## 1.5.1.5 Utfallsvisualisering

Ange följande **uppmaning** och klicka på knappen **skicka**.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![ChatGPT och CJA](./images/chatgpt118.png)

Välj **UpsertProject**.

![ChatGPT och CJA](./images/chatgpt119.png)

Välj **RunReport**.

![ChatGPT och CJA](./images/chatgpt120.png)

Då borde du se något sådant här. Ange följande **uppmaning** och klicka på knappen **skicka**.

```javascript
can you show me a visualization of the above fallout analysis?
```

![ChatGPT och CJA](./images/chatgpt120a.png)

Klicka på **Hämta PNG**.

![ChatGPT och CJA](./images/chatgpt121.png)

Nu ser du visualiseringen av bortfallsanalysen.

![ChatGPT och CJA](./images/chatgpt122.png)

Ange följande **uppmaning** och klicka på knappen **skicka**.

```javascript
break down the fallout analysis at the touchpoint of the add to carts
```

![ChatGPT och CJA](./images/chatgpt123.png)

Välj **RunReport**.

![ChatGPT och CJA](./images/chatgpt124.png)

Gå tillbaka till [Analyser och agenter](./analyticsagents.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}