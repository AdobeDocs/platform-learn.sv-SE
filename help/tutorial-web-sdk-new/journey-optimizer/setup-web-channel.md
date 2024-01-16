---
title: Konfigurera webbkanal med Platform Web SDK
description: Lär dig implementera webbkanal med Platform Web SDK. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Web Channel,Web SDK
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '2463'
ht-degree: 0%

---


# Konfigurera webbkanal med Platform Web SDK

Lär dig implementera webbkanal med Platform Web SDK. Den här guiden innehåller grundläggande krav för webbkanalen, detaljerade konfigurationssteg och en djupdykning i ett användningsexempel som fokuserar på lojalitetsstatus.

Genom att följa den här guiden kan Journey Optimizer-användare effektivt använda webbkanalen för avancerad onlineanpassning med Journey Optimizer Web Designer.

## Utbildningsmål

När lektionen är slut kan du:

* Förstå funktionen och betydelsen av Web SDK när det gäller att leverera webbkanalsupplevelsen.
* Förstå processen med att skapa en webbkanalskampanj från början till slut med exempelexemplet Luma Loyalty Rewards.
* Konfigurera kampanjegenskaper, åtgärder och scheman i gränssnittet.
* Förstå funktionaliteten och fördelarna med tillägget Adobe Experience Cloud Visual Editing Helper.
* Lär dig redigera webbsidesinnehåll, inklusive bilder, sidhuvuden och andra element, med Web Designer.
* Lär dig hur du infogar erbjudanden på en webbsida med beslutsdelen för erbjudandet.
* Bekanta dig med bästa praxis för att säkerställa kvaliteten och framgången för en webbkanalskampanj.

## Förutsättningar

För att slutföra lektionerna i det här avsnittet måste du först:

* Se till att din AEP Web SDK-version är 2.16 eller senare.
* Om du använder Journey Optimizer webbdesigner för att skapa din webbkanalsupplevelse måste du kontrollera att du använder webbläsarna Google Chrome eller Microsoft® Edge.
* Kontrollera också att du har laddat ned webbläsartillägget Adobe Experience Cloud Visual Editing Helper. Aktivera tillägget för hjälpwebbläsaren för visuell redigering i webbläsarens verktygsfält innan du skapar webbkanalsupplevelsen.
   * I Journey Optimizer webbdesigner är det inte säkert att vissa webbplatser öppnas på grund av någon av följande orsaker:
      1. Webbplatsen har strikta säkerhetsregler.
      1. Webbplatsen är inbäddad i en iframe.
      1. Kundens QA- eller stage-sajt är inte externt tillgänglig (det är en intern sajt).
* Kontrollera att cookies från tredje part tillåts i webbläsaren. Det kan vara nödvändigt att inaktivera alla annonsblockerare i webbläsaren.
* När du skapar webbupplevelser och inkluderar innehåll från Adobe Experience Manager Assets Essentials-biblioteket måste du konfigurera underdomänen för publicering av det här innehållet. [Läs mer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/web-delegated-subdomains.html?lang=en).
* Om du använder funktionen för innehållsexperimenterande ska du se till att din webbdatauppsättning också ingår i rapportkonfigurationen.
* För närvarande finns det två typer av implementeringar som gör det möjligt att skapa och leverera webbkanalskampanjer på dina webbegenskaper:
   * Endast på klientsidan: Om du vill ändra webbplatsen måste du implementera Adobe Experience Platform Web SDK.
   * Hybridläge: Du kan använda API:t för AEP Edge Network Server för att begära anpassning på serversidan. Svaret från API:t skickas sedan till Adobe Experience Platform Web SDK för återgivningsändringar på klientsidan. Mer information finns i API-dokumentationen för Adobe Experience Platform Edge Network Server. Ytterligare information och implementeringsexempel för hybridläget finns i det här blogginlägget.

>[!NOTE]
>
>Implementering på serversidan stöds för närvarande inte.

## Terminologi

Först och främst bör ni förstå den terminologi som används i webbkanalskampanjer.

* **Webbkanal**: Ett medium för kommunikation eller leverans av innehåll via webben. I den här guiden hänvisar den till den mekanism genom vilken personaliserat innehåll levereras till webbplatsbesökare som använder Platform Web SDK, inom Adobe Journey Optimizer.
* **Webbyta**: Avser en webbegenskap som identifieras av en URL där innehållet levereras. Det kan omfatta en eller flera webbsidor.
* **Journey Optimizer Web Designer**: Ett specifikt verktyg eller gränssnitt i Journey Optimizer där användare kan designa sina webbkanalsupplevelser.
* **Adobe Experience Cloud Visual Editing Helper**: Ett webbläsartillägg som gör det lättare att redigera och utforma webbkanalsupplevelser visuellt.
* **Datastream**: En konfiguration i Adobe Experience Platform-tjänsten som säkerställer att webbkanalsupplevelserna kan levereras.
* **Kopplingsprincip**: En konfiguration som säkerställer korrekt aktivering och publicering av inkommande kampanjer.
* **Målgrupp**: Ett specifikt segment med användare eller besökare som uppfyller vissa kriterier.
* **Webbdesigner**: Ett gränssnitt eller verktyg som gör det enklare att redigera och designa webbupplevelser visuellt utan att djupdyka i koden.
* **Uttrycksredigeraren**: Ett verktyg i Web Designer som gör att användare kan lägga till personalisering i webbinnehåll, eventuellt baserat på dataattribut eller andra kriterier.
* **Beslutskomponent för erbjudande**: En komponent i Web Designer som hjälper till att avgöra vilket erbjudande som är bäst lämpat att visas för en viss besökare baserat på beslutshantering.
* **Content Experiment**: En metod för att testa olika innehållsvariationer för att ta reda på vilken som fungerar bäst när det gäller det önskade måttet, till exempel inkommande klick.
* **Behandling**: I samband med innehållsexperiment avser en behandling en specifik variation av innehåll som testas mot en annan.
* **Simulering**: En förhandsvisningsmekanism som visualiserar webbkanalsupplevelsen innan den aktiveras för aktiva målgrupper.

## Konfigurera datastream

Kontrollera att ett datastream har definierats i Adobe Experience Platform och att alternativet Adobe Journey Optimizer är aktiverat. Detta måste konfigureras innan webbkanalsupplevelsen kan levereras av Platform Web SDK.

Så här konfigurerar du Adobe Journey Optimizer i datastream:

1. Gå till gränssnittet Datainsamling.
1. Välj **Datastreams**.
1. Markera tidigare skapade Luma Web SDK-dataström.

   ![Välj datastream](../assets/web-channel-select-datastream.png)

1. Välj **Redigera** i Adobe Experience Platform Service.

   ![Redigera datastream](../assets/web-channel-edit-datastream.png)

1. Kontrollera **Adobe Journey Optimizer** box.

   ![Kryssruta för AJO](../assets/web-channel-check-ajo-box.png)

1. Välj **Spara**.

Detta säkerställer att inkommande händelser för Journey Optimizer hanteras korrekt av Adobe Experience Platform Edge.

## Konfigurera sammanfogningsprincipen

Kontrollera att en sammanfogningsprincip har definierats med **Princip för aktiv-direktkoppling** aktiverat alternativ. Det här alternativet används av Journey Optimizer inkommande kanaler för att säkerställa korrekt aktivering och publicering av inkommande kampanjer.

Så här konfigurerar du alternativet i sammanfogningsprincipen:

1. Gå till **Kund > Profiler** gränssnitt.
1. Välj **Sammanfoga principer**.
1. Välj din profil och växla **Princip för aktiv-direktkoppling** i **Konfigurera** steg.

   ![Växla sammanfogningsprincip](..//assets/web-channel-active-on-edge-merge-policy.png)

## Konfigurera webbdatauppsättningen för innehållsexperiment

Om du vill använda innehållsexperiment i webbkanalskampanjer måste du se till att den webbdatauppsättning som används också ingår i rapportkonfigurationen. Journey Optimizer rapporteringssystem använder datauppsättningen i skrivskyddat läge för att fylla i OTB-innehållsundersökningsrapporter.

[I det här avsnittet beskrivs hur du lägger till datauppsättningar för rapportering av innehållsexperiment](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/content-experiment/reporting-configuration.html?lang=en#add-datasets).

## Use Case Overview - Loyalty Rewards

I den här lektionen används ett exempel på Loyalty Rewards-användningsexempel för att beskriva implementeringen av en webbkanalsupplevelse med hjälp av Web SDK.

Med detta exempel får ni en bättre förståelse för hur Journey Optimizer kan hjälpa er att leverera de bästa inkommande upplevelserna till era kunder med hjälp av Journey Optimizer kampanjer och Web Designer.

>[!NOTE]
>
>Eftersom den här självstudiekursen riktar sig till implementerare är det värt att notera att den här lektionen handlar om omfattande gränssnittsarbete i AJO. Sådana användargränssnittsuppgifter hanteras vanligtvis av marknadsförare, men det kan vara bra för implementerare att få insikt i processen, även om de till slut inte är ansvariga för att skapa webbkanalskampanjer.

### Skapa lojalitetskampanj

Låt oss börja med att skapa webbkanalskampanjen Loyalty Rewards i Adobe Journey Optimizer.

Så här skapar du exempelkampanjen:

1. Navigera till Resehantering > Kampanjer i den vänstra navigeringen
1. Klicka **Skapa kampanj** i det övre högra hörnet.
1. I **Egenskaper** anger du hur kampanjen ska köras. För användningsfallet Loyalty Rewards väljer du **Schemalagd**.

   ![Schemalagd kampanj](../assets/web-channel-campaign-properties-scheduled.png)

1. I **Åtgärder** väljer du **Webbkanal**. I det här skedet väljer du även webbyta.

>[!NOTE]
>
>En webbyta refererar till en webbegenskap som identifieras av en URL där innehållet levereras. Den kan motsvara en enda sidas URL eller innehålla flera sidor, vilket gör att du kan använda ändringarna på en eller flera webbsidor.

Välj **Sidans URL** webbsidesalternativ för att distribuera upplevelsen på en sida för kampanjen. Ange Luma-sidans URL.

1. När webbytan är definierad väljer du **Skapa**.

   ![Markera webbyta](../assets/web-channel-web-surface.png)

1. Nu kan du lägga till ytterligare information i den nya webbkanalskampanjen. Ge först namnet på kampanjen. Anropa det *Luma Loyalty Rewards - Gold Status - oktober 2023*&#39;. Du kan också lägga till en beskrivning till kampanjen. Lägg även till **Taggar** för att förbättra den övergripande kampanjtaxonomin.

   ![Namnge kampanjen](../assets/web-channel-campaign-name.png)

1. Som standard är kampanjen aktiv för alla webbplatsbesökare. I det här fallet bör endast guldstatuspoängare se upplevelsen. Aktivera detta genom att klicka på **Välj målgrupp** och väljer *Luma Loyalty Rewards - Guldstatus* målgrupp.

1. I **Namnutrymme för identitet** markerar du namnutrymmet för att identifiera individer inom det valda segmentet. Eftersom du distribuerar kampanjen på Luma-webbplatsen kan du välja ECID-namnutrymmet. Profiler i &#39;*Luma Loyalty Rewards - Guldstatus* målgruppen som saknar ECID-namnutrymmet bland sina olika identiteter omfattas inte av webbkanalskampanjen.

   ![Välj identitetstyp](../assets/web-channel-indentity-type.png)

1. Schemalägg kampanjen till början den 1 december med **Kampanjstart** och upphör den 31 december med **Kampanjslut** alternativ.

   ![Kampanjschema](../assets/web-channel-campaign-schedule.png)

>[!NOTE]
>
>Tänk på att webbupplevelsen visas när besökaren öppnar sidan för webbkanalskampanjer. Till skillnad från andra typer av kampanjer i Adobe Journey Optimizer **Åtgärdsutlösare** -avsnittet kan inte konfigureras.

### Experimentera med lojalitetsmaterial

I **Åtgärd** kan du skapa ett experiment för att testa vilket innehåll som fungerar bäst för *Luma Loyalty Rewards - Guldstatus* målgrupp. Låt oss skapa och testa två behandlingar som en del av kampanjkonfigurationen.

Så här skapar du innehållsexperimentet:

1. Klicka **Skapa experiment**.

   ![Skapa experiment](../assets/web-channel-create-content-experiment.png)

1. Välj först **Resultatmått**. Detta är måttet för att avgöra innehållets effektivitet. Välj **Unika inkommande klick**, för att se vilken innehållsbehandling som genererar fler klick på webbupplevelsen CTA.

   ![Välj framgångsmått](../assets/web-channel-content-experiment-metric.png)

1. När du skapar ett experiment med webbkanalen och väljer **Inkommande klick**, **Unika inkommande klick**, **Sidvyer**, eller **Unika sidvyer** mätvärden, **Klicka på Åtgärd** I den här listrutan kan du hålla reda på och övervaka klick och vyer på specifika sidor.

1. Du kan också ange en **Spärra** som inte får någon av de två behandlingarna. Låt det vara omarkerat för tillfället.

1. Du kan också välja att **Fördela jämnt**. Markera det här alternativet för att se till att uppdelningarna alltid är jämnt fördelade.

[Läs mer om experiment med innehåll i Adobe Journey Optimizer Web Channel](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/content-experiment/get-started-experiment.html?lang=en).

### Redigera innehåll med hjälp av den visuella hjälpen

Låt oss nu skapa webbkanalsupplevelsen. Använd Adobe Experience Cloud **Visual Helper**. Det här verktyget är ett webbläsartillägg som är kompatibelt med Google Chrome och Microsoft® Edge. Kontrollera att du har hämtat tillägget innan du försöker skapa dina upplevelser. Se även till att webbsidan innehåller Web SDK.

1. I **Åtgärd** fliken för kampanjen, klicka på **Redigera innehåll**. Eftersom du angav en enda sidadress som yta bör du vara redo att börja arbeta i dispositionen.

   ![Redigera innehåll](../assets/web-channel-edit-content.png)

1. Klicka nu **Redigera webbsida** för att börja skapa.

   ![Redigera webbsida](../assets/web-channel-edit-web-page.png)

1. Börja med att redigera vissa element med hjälp av webbdispositionen. Använd snabbmenyn för att redigera Luma-hjältebildhuvudet. Justera formatet för den sammanhangsberoende rutan till höger.

   ![Lägga till sammanhangsberoende redigeringar](../assets/web-channel-some-contextual-edit.png)

1. Lägg även till personalisering i behållaren med **Uttrycksredigerare**.

   ![Lägg till personalisering](../assets/web-channel-add-basic-personalization.png)

1. Se till att materialet spåras korrekt för klickningar. Välj **Klicka på spårningselement** på snabbmenyn.

   ![Klicka på spår](../assets/web-channel-click-tracking.png)

1. Använd **Beslutskomponent för erbjudande** för att infoga erbjudanden på webbsidan. Den här komponenten använder **Beslutshantering** för att välja det bästa erbjudandet att leverera till Luma-besökare.


### Designändringar för HTML

Det finns några tillgängliga metoder om du vill göra mer avancerade eller anpassade ändringar av webbplatsen som en del av kampanjen Loyalty Rewards.

Använd **Komponenter** för att lägga till HTML eller annat innehåll direkt på Luma-webbplatsen.

![Utforska komponentfönstret](../assets/web-channel-components-pane.png)

Lägg till en ny HTML-komponent högst upp på sidan. Redigera HTML i komponenten från designgränssnittet eller **Sammanhangsberoende** fönster.

![Lägg till anpassad HTML](../assets/web-channel-add-html-component.png)

Du kan också lägga till HTML-redigeringar från **Ändringar** fönster. I den här rutan kan du markera en komponent på sidan och redigera den i designergränssnittet.

Lägg till HTML i redigeraren för *Luma Loyalty Rewards - Guldstatus* målgrupp. Klicka **Validera**.

![Validera HTML](../assets/web-channel-add-custom-html-validate.png)

Granska nu den nya anpassade HTML-komponenten så att den passar och känns.

![Granska anpassad HTML](../assets/web-channel-review-custom-html.png)

Redigera en viss komponent med **CSS-väljartyp** modifiering.

![Ändra CSS](../assets/web-channel-css-selector.png)

Lägg till anpassad kod med **Sida `<head>` type** modifiering.

![Ändra huvud](../assets/web-channel-page-head-modification.png)

Möjligheterna är oändliga med **Visual Helper**.

### Simulera innehåll för Loyalty Rewards

Titta på en förhandsgranskning av den ändrade webbsidan innan du aktiverar kampanjen. Tänk på att du måste ha testprofiler konfigurerade för att simulera webbkanalsupplevelser.

Så här simulerar du upplevelsen:

1. Välj **Simulera innehåll** inom kampanjen.

   ![Simulera innehåll](../assets/web-channel-simulate-content.png)

1. Välj en testprofil för att ta emot simuleringen. Tänk på att testprofilen ska finnas i *Luma Loyalty Rewards - Guldstatus* målgruppen för att få rätt behandling.

1. Förhandsgranskningen visas för testprofilen.

### Aktivera kampanjen Loyalty Rewards

Aktivera slutligen webbkanalskampanjen.

1. Välj **Granska för aktivering**.

1. Du uppmanas att bekräfta kampanjinformationen en sista gång. Välj **Aktivera**. Det kan ta upp till 15 minuter innan kampanjen publiceras på webbplatsen.

### Lojalitetsprogram - QA

Det bästa är att följa **Webb** i kampanjens livs- och globala rapporter för kampanjspecifika nyckeltal. För den här kampanjen ska du övervaka upplevelseintrycken och klicka på en frekvens.

![Visa webbrapport](../assets/web-channel-web-report.png)

### Validering av webbkanal med Adobe Experience Platform Debugger

Tillägget Adobe Experience Platform Debugger, som finns för både Chrome och Firefox, analyserar dina webbsidor för att identifiera problem med implementeringen av Adobe Experience Cloud lösningar.

Du kan använda felsökaren på Luma-webbplatsen för att validera webbkanalsupplevelsen i produktionen. Detta är en bra metod när Loyalty Rewards-användningsexemplet är öppet och körs för att säkerställa att allt är korrekt konfigurerat.

[Lär dig hur du konfigurerar felsökaren i webbläsaren med hjälp av guiden här](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html?lang=en).

Så här börjar du valideringen med felsökaren:

1. Navigera till webbsidan Luma med webbkanalsupplevelsen.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Öppna **Adobe Experience Platform debugger**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Navigera till **Sammanfattning**. Verifiera att **Dataström-ID** matchar **datastream** in **Adobe datainsamling** som du har aktiverat Adobe Journey Optimizer för.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Du kan sedan logga in på webbplatsen med olika Luma-förmånskonton och använda felsökaren för att validera begäranden som skickas till Adobe Experience Platform Edge-nätverket.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Under **Lösningar** navigera till **Experience Platform Web SDK**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. I **Konfiguration** flik, växla på **Aktivera felsökning**. Detta aktiverar loggning för sessionen i en **Adobe Experience Platform Assurance** session.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Logga in på webbplatsen med olika Luma-förmånskonton och använd felsökaren för att validera förfrågningar som skickas till **Adobe Experience Platform Edge-nätverk**. Alla dessa förfrågningar ska registreras i **Säkerhet** för loggspårning.
<!--
   ![ADD SCREENSHOT](#)
-->