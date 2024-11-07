---
title: Komma igång - Skapa ditt dataflöde
description: Komma igång - Skapa ditt dataflöde
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# 0.3 Skapa ditt datastream

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Efter föregående övning har du nu två egenskaper för datainsamling: en för webben och en för mobilen.

![DSN](./images/launchprop.png)

Dessa egenskaper är nästan klara att användas, men innan du kan börja samla in data med dessa egenskaper måste du konfigurera en datastream. Du får mer information om vad ett datastream är och vad det betyder i Exercise 1.2.

Följ dessa steg tills vidare.

## 0.3.1 Skapa ditt datastream för webben

Klicka på **[!UICONTROL Datastreams]** eller **[!UICONTROL Datastreams (Beta)]**.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1a.png)

I skärmens övre högra hörn väljer du namnet på sandlådan, som ska vara `--aepSandboxName--`.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1b.png)

Klicka på **[!UICONTROL New Datastream]**.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1.png)

Ange `--aepUserLdap-- - Demo System Datastream` för **[!UICONTROL Friendly Name]** och den valfria beskrivningen. För händelseschema väljer du **Demonstrationssystem - händelseschema för webbplatsen (Global v1.1)**. Klicka på **Spara**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig2.png)

Då ser du det här. Klicka på **Lägg till tjänst**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig3.png)

Välj tjänsten **[!UICONTROL Adobe Experience Platform]**, som visar ytterligare fält. Då ser du det här.

För händelsedatauppsättning väljer du **Demonstrationssystem - händelsedatauppsättning för webbplats (Global v1.1)** och för profildatauppsättning väljer du **Demonstrationssystem - profildatauppsättning för webbplats (Global v1.1)**. Klicka på **Spara**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig4.png)

Du kommer att se det här.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig5.png)

Det är allt för tillfället. I [Modul 1.1](./../../../modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md) får du lära dig mer om Web SDK och hur du konfigurerar alla dess funktioner.

Klicka på **[!UICONTROL Tags]** på den vänstra menyn.

Filtrera sökresultaten så att du kan se de två datainsamlingsegenskaperna. Öppna egenskapen för **webben** genom att klicka på den.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig10a.png)

Då ser du det här. Klicka på **Tillägg**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig11.png)

Klicka på **Konfigurera** i Adobe Experience Platform Web SDK-tillägget.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig12.png)

Då ser du det här. För **datastreams** visas för närvarande ett värde som är 1 för &quot;dummy&quot;. Du måste nu klicka på alternativknappen **Välj från listan**. I listrutan väljer du den dataström du skapade tidigare.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig13.png)

Se till att du har valt din **datastream**. TIPS: Du kan enkelt filtrera resultaten i listrutan genom att skriva `--aepUserLdap--`.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig14.png)

Bläddra nedåt tills du ser **Datainsamling**. Kontrollera att kryssrutan för **Aktivera klickdatainsamling** inte är aktiverad. Klicka på **Spara** för att spara ändringarna.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig14a.png)

Gå till **Publiceringsflöde**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig15.png)

Klicka på **..** för **Main** och klicka sedan på **Edit**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig16.png)

Klicka på **Lägg till alla ändrade resurser** och sedan på **Spara och skapa för utveckling**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig17.png)

Ändringarna publiceras nu och är klara om några minuter.

## 0.3.2 Skapa ditt datastream för mobiler

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Klicka på **[!UICONTROL Datastreams]** eller **[!UICONTROL Datastreams (Beta)]**.

![Klicka på Datastream-ikonen i den vänstra navigeringen](./images/edgeconfig1a.png)

I skärmens övre högra hörn väljer du namnet på sandlådan, som ska vara `--aepSandboxName--`.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1b.png)

Klicka på **[!UICONTROL New Datastream]**.

![Klicka på Datastream-ikonen i den vänstra navigeringen](./images/edgeconfig1.png)

Ange `--aepUserLdap-- - Demo System Datastream (Mobile)` för **[!UICONTROL Friendly Name]** och den valfria beskrivningen. För händelseschema väljer du **Demonstrationssystem - händelseschema för mobilapp (Global v1.1)**. Klicka på **Spara**.

Klicka på **[!UICONTROL Save]**.

![Namnge dataströmmen och spara](./images/edgeconfig2m.png)

Då ser du det här. Klicka på **Lägg till tjänst**.

![Namnge dataströmmen och spara](./images/edgeconfig3m.png)

Välj tjänsten **[!UICONTROL Adobe Experience Platform]**, som visar ytterligare fält. Då ser du det här.

För händelsedatauppsättning väljer du **Demonstrationssystem - händelsedatauppsättning för mobilapp (Global v1.1)** och för profildatauppsättning väljer du **Demonstrationssystem - profildatauppsättning för mobilapp (Global v1.1)**. Klicka på **Spara**.

![Namnge dataströmskonfigurationen och spara](./images/edgeconfig4m.png)

Då ser du det här.

![Namnge dataströmskonfigurationen och spara](./images/edgeconfig5m.png)

Din datastream är nu klar att användas i din klientegenskap för Adobe Experience Platform Data Collection för mobilen.

Gå till **Taggar** och filtrera sökresultaten så att du kan se de två datainsamlingsegenskaperna. Öppna egenskapen för **Mobile** genom att klicka på den.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig10am.png)

Då ser du det här. Klicka på **Tillägg**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig11m.png)

Klicka på **Konfigurera** på tillägget **Adobe Experience Platform Edge Network**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig12m.png)

Då ser du det här. Nu måste du välja rätt sandlåda och datastream som du precis konfigurerade. Sandlådan som ska användas är `--aepSandboxName--` och datastream kallas `--aepUserLdap-- - Demo System Datastream (Mobile)`.

Använd standarddomänen **edge.adobedc.net** för **Edge Network-domänen**.

Klicka på **Spara** för att spara ändringarna.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig13m.png)

Gå till **Publiceringsflöde**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig15m.png)

Klicka på **..** bredvid **Huvudsida** och klicka sedan på **Redigera**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig16m.png)

Klicka på **Lägg till alla ändrade resurser** och sedan på **Spara och skapa för utveckling**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig17m.png)

Ändringarna publiceras nu och är klara om några minuter.

Nästa steg: [0.4 Använd webbplatsen](./ex4.md)

[Gå tillbaka till modul 0](./getting-started.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)