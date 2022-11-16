---
title: Komma igång - Skapa ditt datastream
description: Komma igång - Skapa ditt datastream
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: c967b01e-9a0b-4a74-b536-706db0cb237f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# 0.3 Skapa ditt datastream

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Efter föregående övning har du nu två datainsamlingsegenskaper: en för webben och en för mobilen.

![DSN](./images/launchprop.png)

Dessa egenskaper är nästan klara att användas, men innan du kan börja samla in data med dessa egenskaper måste du konfigurera en datastream. Du får mer information om vad ett datastream är och vad det betyder i Exercise 1.2.

Följ dessa steg tills vidare.

## 0.3.1 Skapa ditt datastream för webben

Klicka **[!UICONTROL Datastreams]** eller **[!UICONTROL Datastreams (beta)]**.

![Klicka på ikonen Edge Configuration (Kantkonfiguration) i den vänstra navigeringen](./images/edgeconfig1a.png)

I skärmens övre högra hörn väljer du namnet på sandlådan, som bör vara `--aepSandboxId--`.

![Klicka på ikonen Edge Configuration (Kantkonfiguration) i den vänstra navigeringen](./images/edgeconfig1b.png)

Klicka **[!UICONTROL Ny datastream]**.

![Klicka på ikonen Edge Configuration (Kantkonfiguration) i den vänstra navigeringen](./images/edgeconfig1.png)

För **[!UICONTROL Eget namn]** och för den valfria beskrivningen anger du `--demoProfileLdap-- - Demo System Datastream`. För händelseschema väljer du **Demonstrationssystem - händelseschema för webbplats (Global v1.1)**. Klicka **Spara**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig2.png)

Du kommer då att se det här. Klicka **Lägg till tjänst**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig3.png)

Välj tjänsten **[!UICONTROL Adobe Experience Platform]**, som visar ytterligare fält. Du kommer då att se det här.

För händelsedatauppsättning väljer du **Demo System - händelsedatauppsättning för webbplats (Global v1.1)** och för profildatauppsättning väljer du **Demonstrationssystem - profildatauppsättning för webbplats (Global v1.1)**. Klicka **Spara**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig4.png)

Du kommer att se det här.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig5.png)

Det är allt för tillfället. I [Modul 1](./../module1/data-ingestion-launch-web-sdk.md) du får lära dig mer om Web SDK och hur du konfigurerar alla dess funktioner.

Klicka på i den vänstra menyn **[!UICONTROL Taggar]**.

Filtrera sökresultaten så att du kan se de två datainsamlingsegenskaperna. Öppna egenskapen för **Webb** genom att klicka på den.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig10a.png)

Du kommer då att se det här. Klicka **Tillägg**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig11.png)

På Adobe Experience Platform Web SDK-tillägget klickar du på **Konfigurera**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig12.png)

Du kommer då att se det här. För **Datastreams** visas för närvarande ett värde som är 1. Nu måste du klicka på **Välj från lista** alternativknapp. I listrutan väljer du den dataström du skapade tidigare.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig13.png)

Se till att du har valt **Datastream**. TIPS: Du kan enkelt filtrera resultaten i listrutan genom att skriva `--demoProfileLdap--`.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig14.png)

Bläddra nedåt tills du ser **Datainsamling**. Kontrollera att kryssrutan för **Aktivera klickdatainsamling** är inte aktiverat. Klicka **Spara** för att spara ändringarna.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig14a.png)

Gå till **Publiceringsflöde**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig15.png)

Klicka på **...** for **Huvud** och sedan klicka **Redigera**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig16.png)

Klicka **Lägg till alla ändrade resurser** och sedan klicka **Spara och bygg för utveckling**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig17.png)

Ändringarna publiceras nu och är klara om några minuter.

## 0.3.2 Skapa ditt datastream för mobiler

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Klicka **[!UICONTROL Datastreams]** eller **[!UICONTROL Datastreams (beta)]**.

![Klicka på Datastream-ikonen i den vänstra navigeringen](./images/edgeconfig1a.png)

I skärmens övre högra hörn väljer du namnet på sandlådan, som bör vara `--aepSandboxId--`.

![Klicka på ikonen Edge Configuration (Kantkonfiguration) i den vänstra navigeringen](./images/edgeconfig1b.png)

Klicka **[!UICONTROL Ny datastream]**.

![Klicka på Datastream-ikonen i den vänstra navigeringen](./images/edgeconfig1.png)

För **[!UICONTROL Eget namn]** och för den valfria beskrivningen anger du `--demoProfileLdap-- - Demo System Datastream (Mobile)`. För händelseschema väljer du **Demo System - händelseschema för mobilapp (Global v1.1)**. Klicka **Spara**.

Klicka **[!UICONTROL Spara]**.

![Namnge datastream och spara](./images/edgeconfig2m.png)

Du kommer då att se det här. Klicka **Lägg till tjänst**.

![Namnge datastream och spara](./images/edgeconfig3m.png)

Välj tjänsten **[!UICONTROL Adobe Experience Platform]**, som visar ytterligare fält. Du kommer då att se det här.

För händelsedatauppsättning väljer du **Demo System - händelsedatauppsättning för mobilapp (Global v1.1)** och för profildatauppsättning väljer du **Demo System - profildatauppsättning för mobilapp (Global v1.1)**. Klicka **Spara**.

![Namnge DataStream-konfigurationen och spara](./images/edgeconfig4m.png)

Du kommer då att se det här.

![Namnge DataStream-konfigurationen och spara](./images/edgeconfig5m.png)

Din datastream är nu klar att användas i din klientegenskap för Adobe Experience Platform Data Collection för mobilen.

Gå till **Taggar** och filtrera sökresultaten så att du kan se de två datainsamlingsegenskaperna. Öppna egenskapen för **Mobil** genom att klicka på den.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig10am.png)

Du kommer då att se det här. Klicka **Tillägg**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig11m.png)

På **Adobe Experience Platform Edge Network** tillägg, klicka **Konfigurera**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig12m.png)

Du kommer då att se det här. Nu måste du välja rätt sandlåda och datastream som du precis konfigurerade. Sandlådan som ska användas är `--aepSandboxId--` och datastream anropas `--demoProfileLdap-- - Demo System Datastream (Mobile)`.

För **Edge Network-domän**, använd standarddomänen som är **edge.adobedc.net**.

Klicka **Spara** för att spara ändringarna.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig13m.png)

Gå till **Publiceringsflöde**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig15m.png)

Klicka på **...** nästa **Huvud** och sedan klicka **Redigera**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig16m.png)

Klicka **Lägg till alla ändrade resurser** och sedan klicka **Spara och bygg för utveckling**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig17m.png)

Ändringarna publiceras nu och är klara om några minuter.

Nästa steg: [0.4 Använda webbplatsen](./ex4.md)

[Gå tillbaka till modul 0](./getting-started.md)

[Gå tillbaka till Alla moduler](./../../overview.md)