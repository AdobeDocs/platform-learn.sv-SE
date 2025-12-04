---
title: Komma igång med Brand Concierge
description: Komma igång med Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: ea5fa4694205a94f63d277fdcf2018951fa31fbc
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# 1.4.1 Komma igång med Brand Concierge

## Video

I den här videon får du en förklaring och demonstration av alla steg som ingår i övningen.

## 1.4.1.1 Brand Concierge - översikt

När du konfigurerar Brand Concierge är de två viktigaste elementen:

- **Agentdisposition (konfigurationslager)**

  Syfte: Den primära användargränssnittsplattformen som används för att skapa och konfigurera konversationsbaserade AI-upplevelser.

  Viktiga ansvarsområden:

   - Definiera och hantera datakällor och kunskapsbanker
   - Ange varumärkesuttryck (ton, stil, skyddsritningar)
   - Ställ in mötesbokningsagenten

- **Agent Orchestrator (körningsmotor)**

  Syfte: Motiverings- och organiseringsmotorn som tolkar användarförfrågningar och utför lämpliga agentåtgärder.

  Viktiga ansvarsområden:

   - Tolka användningsmetoder för naturligt språk
   - Generera och genomföra flerstegsplaner
   - Välj och anropa lämpliga operatorer/verktyg
   - Stärk varumärkessammanhang, regelefterlevnad och skyddsprofiler
   - Koordinera arbetsflöden med flera agenter
   - Sammanställa och sammanställa svar från flera datakällor

- **Brand Concierge-konversationsmiljö (tjänstlager)**

  Syfte: Det kundcentrerade konversationstjänstskiktet som hanterar chattsessioner, kontext och kundinteraktioner.

  Nyckelkomponenter:

   - Web Agent (klient): Användargränssnitt för webbläsare eller mobilchatt som är integrerat med SDK
   - Konversationstjänst (backend): Hanterar sessionstillstånd och fungerar som orchestration-gateway

  Viktiga ansvarsområden:

   - Hantera användarsessioner och konversationstryckningar
   - Hantera användarautentisering och profiler
   - Skicka meddelanden mellan klienten och Agent Orchestrator
   - Kontext för beständig konversation
   - Logga beteendehändelser och drifthändelser till AEP för analys
   - Använd ytspecifika konfigurationer

## 1.4.1.2 Brand Concierge-instanskonfiguration

Följ stegen nedan för att börja skapa en egen Brand Concierge-instans.

Gå till [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Öppna **Brand Concierge**.

![Brand Concierge](./images/bc1.png)

Du borde se det här då. Klicka på menyn **markering av sandlåda**.

![Brand Concierge](./images/bc2.png)

Välj den sandlåda som du har tilldelats. Den sandlådan ska ha namnet `--aepUserLdap-- - bc`.

![Brand Concierge](./images/bc3.png)

Klicka på **Kom igång**.

![Brand Concierge](./images/bc4.png)

Använd `--aepUserLdap-- - CitiSignal Brand Concierge` som namn på din Brand Concierge-instans.

Ange följande text under **Vad vill du att concierge ska göra?**.

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

Klicka på **Skapa**.

![Brand Concierge](./images/bc5.png)

Du borde se det här då. Klicka på **Kom igång** för att lägga till en kunskapskälla.

![Brand Concierge](./images/bc6.png)

Välj **Webbplatslänkar** och klicka på **Fortsätt**.

![Brand Concierge](./images/bc7.png)

Du borde se det här då. Ange `CitiSignal website` som namn för din kunskapskälla.

Nu måste du överföra en CSV-fil som innehåller länkarna till din webbplats. Hämta [CitiSignal-webbplatslänkar till CSV-filen](./assets/citisignal-website-links.csv) till skrivbordet.

Klicka på **Bläddra bland filer**.

![Brand Concierge](./images/bc8.png)

Öppna filen **citisign-website-links.csv** och uppdatera länkarna så att de pekar på din egen CitiSignal-webbplats.

![Brand Concierge](./images/bc8a.png)

Markera filen **citisign-website-links.csv** som du just laddat ned och redigerat. Klicka på **Öppna**.

![Brand Concierge](./images/bc9.png)

Filen läggs nu till i den här kunskapskällan. Klicka på **Lägg till**.

![Brand Concierge](./images/bc10.png)

Du borde se det här då. Klicka på **Ta mig hem**.

![Brand Concierge](./images/bc11.png)

Du borde se det här då. Klicka på **Kom igång** på **produktrådgivningen för konsumenter**-kortet.

![Brand Concierge](./images/bc12.png)

Du borde se det här då. Fyll i följande fält med texten nedan.

**Vad bör koncierge känna till om produkten eller publiken innan de ger rekommendationer?**

```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

**Finns det några affärsregler eller begränsningar som koncierge ska följa när den gör rekommendationer?**

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

**Finns det några specifika nyckelord eller fraser som koncierge ska följa eller undvika?**

```
Competitor pricing, competitor products
```

Dina uppdateringar sparas automatiskt. Klicka på **pilen** för att gå tillbaka till föregående skärm.

![Brand Concierge](./images/bc13.png)

Du borde se det här då. Klicka på **Kom igång** för att anpassa ditt varumärkesuttryck.

![Brand Concierge](./images/bc14.png)

Du kan göra egna val på sidan **Varumärkesuttryck** och se till att ett alternativ är valt för varje fråga.

![Brand Concierge](./images/bc15.png)

Bläddra nedåt och välj en inställning för fältet **Svarslängd**.

Dina uppdateringar sparas automatiskt.

![Brand Concierge](./images/bc16.png)

Rulla uppåt och klicka på **pilen** för att gå tillbaka till föregående skärm.

![Brand Concierge](./images/bc17.png)

Du kommer då tillbaka hit. Klicka på **Kunskapskällor**.

![Brand Concierge](./images/bc18.png)

Klicka på **Skapa dina kunskapskällor**.

![Brand Concierge](./images/bc19.png)

Välj **Produktkatalog** och klicka på **Fortsätt**.

![Brand Concierge](./images/bc20.png)

Du borde se det här då. Ange `CitiSignal Products` som namn för din kunskapskälla.

![Brand Concierge](./images/bc21.png)

Nu måste du överföra en CSV-fil som innehåller länkarna till din webbplats. Hämta [CitiSignal-produktkatalog](./assets/CitiSignal-catalog.json.zip) till skrivbordet och zippa upp den.

![Brand Concierge](./images/bc26.png)

Klicka på **Bläddra bland filer** och välj sedan **Bläddra på enheten**.

![Brand Concierge](./images/bc22.png)

Markera filen **CitiSignal-catalog.json** och klicka på **Öppna**.

![Brand Concierge](./images/bc23.png)

Du borde se det här då. Klicka på **Lägg till**.

![Brand Concierge](./images/bc24.png)

Du kommer då tillbaka hit.

![Brand Concierge](./images/bc25.png)

Efter 10-20 minuter ska **Status** för båda kunskapskällorna vara **Slutförd**. Klicka på **Hem**.

![Brand Concierge](./images/bc27.png)

Du borde se det här då. Klicka på **+ Connect** på kortet för **webbplatslänkar**.

![Brand Concierge](./images/bc28.png)

Välj kunskapskällan **CitiSignal-webbplats** och klicka på **Spara**.

![Brand Concierge](./images/bc29.png)

Du borde se det här då. Klicka på **+ Connect** på kortet för **produktkatalog**.

![Brand Concierge](./images/bc30.png)

Välj kunskapskällan **CitiSignal-produkter** och klicka på **Spara**.

![Brand Concierge](./images/bc31.png)

Du borde se det här då. Klicka på **Förhandsgranska** för att börja interagera med din Brand Concierge.

![Brand Concierge](./images/bc32.png)

Nu kan du börja ställa frågor som är relaterade till de angivna kunskapskällorna.

![Brand Concierge](./images/bc33.png)

## 1.4.1.3 steg för AEP-introduktion

Brand Concierge använder Adobe Experience Platform för att lagra interaktionsdata från konversationer. Anslutningen mellan Brand Concierge och Experience Platform kräver att ett datastream konfigureras och används av Brand Concierge.

### Datastream

Gå till [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Öppna **Experience Platform**.

![Brand Concierge](./images/aep1.png)

Kontrollera att du har markerat rätt sandlåda, som ska heta `--aepUserLdap-- - bc`. Bläddra nedåt i den vänstra menyn och välj **Datastreams**.

![Brand Concierge](./images/aep2.png)

Klicka på **Ny dataström**.

![Brand Concierge](./images/aep3.png)

Ange **Datastream-namnet** `--aepUserLdap-- - Brand Concierge` och välj sedan **Mappningsschema** `cja-brand-concierge-sb-XXX`.

Klicka på **Spara**.

![Brand Concierge](./images/aep4.png)

Din datastream är nu konfigurerad. Kopiera datastream-namnet och datastream-ID:t och skriv ned dem i en textfil på datorn.

![Brand Concierge](./images/aep5.png)

### Brand Concierge Configuration Management API

Nästa steg är att aktivera API:t för konfigurationshantering i Brand Concierge för att konfigurera datastream som du nyss skapade. Detta krävs för att lösa saker som IMS Org ID och sandlådedetaljer under bearbetningen av begäran.

Detta är för närvarande ett internt Adobe-steg som måste utföras. I annat fall måste du utföra det här steget eftersom datastream inte är korrekt konfigurerat för Brand Concierge.

Nästa steg: [Implementera Brand Concierge på din webbplats](./ex2.md){target="_blank"}

Gå tillbaka till [Brand Concierge](./brandconcierge.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}