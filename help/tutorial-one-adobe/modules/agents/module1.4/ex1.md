---
title: Komma igång med Brand Concierge
description: Komma igång med Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: 6642acb3fdce2c9d3a9b919d5c9457191e4780a6
workflow-type: tm+mt
source-wordcount: '536'
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

Välj den sandlåda som du har tilldelats. Den sandlådan ska ha namnet `--aepUserLdap--`.

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



```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

```
Competitor pricing, competitor products
```

Dina uppdateringar sparas automatiskt. Klicka på **pilen** för att gå tillbaka till föregående skärm.

![Brand Concierge](./images/bc13.png)

Du borde se det här då. Klicka på **Kom igång** för att anpassa ditt varumärkesuttryck.

![Brand Concierge](./images/bc14.png)

Du kan göra egna val på sidan **Varumärkesuttryck**.

![Brand Concierge](./images/bc15.png)

Bläddra nedåt och välj en inställning för fältet **Svarslängd**.

Dina uppdateringar sparas automatiskt.

![Brand Concierge](./images/bc16.png)

Rulla uppåt och klicka på **pilen** för att gå tillbaka till föregående skärm.

![Brand Concierge](./images/bc17.png)


Gå tillbaka till [Brand Concierge](./brandconcierge.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}