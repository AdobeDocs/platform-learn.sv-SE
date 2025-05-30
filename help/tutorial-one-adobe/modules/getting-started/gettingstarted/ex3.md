---
title: Komma igång - Skapa ditt dataflöde
description: Komma igång - Skapa ditt dataflöde
kt: 5342
doc-type: tutorial
exl-id: d36057b4-64c6-4389-9612-d3c9cf013117
source-git-commit: cc8efbdbcf90607f5a9bc98a2e787b61b4cd66d9
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# Skapa ditt datastream

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/){target="_blank"}.

![DSN](./images/launchprop.png)

Innan du fortsätter kontrollerar du att du har valt rätt miljö med hjälp av miljöväljaren i skärmens övre högra hörn. Rätt miljö att använda kallas `--aepImsOrgName--`.

>[!NOTE]
>
> På skärmbilden nedan visas en viss organisation som valts. När du går igenom den här självstudiekursen är det troligt att din organisation har ett annat namn. När du registrerade dig för den här självstudiekursen fick du den information om miljön som du skulle använda. Följ dessa instruktioner.


![DSN](./images/org.png)

Klicka på **[!UICONTROL Tags]** på den vänstra menyn. Efter föregående övning har du nu tre egenskaper för datainsamling: en för webben, en för mobilen och en för CX-appen.

![DSN](./images/launchprop1.png)

Dessa egenskaper är nästan klara att användas, men innan du kan börja samla in data med dessa egenskaper måste du konfigurera en datastream. Du får mer information om vad ett datastream är och vad det innebär i en senare övning i datainsamlingsmodulen.

Följ dessa steg tills vidare.

## Skapa ett datastream för webben

Klicka på **[!UICONTROL Datastreams]**.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1a.png)

I skärmens övre högra hörn väljer du namnet på sandlådan, som ska vara `--aepSandboxName--`.

>[!NOTE]
>
> Skärmbilden nedan visar att en viss sandlåda har valts. När du går igenom den här självstudiekursen är det troligt att din sandlåda har ett annat namn. När du registrerade dig för den här självstudiekursen fick du den information om miljön som du skulle använda. Följ dessa instruktioner.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1b.png)

Klicka på **[!UICONTROL New Datastream]**.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1.png)

Ange `--aepUserLdap-- - One Adobe Datastream` för **Namn** och den valfria beskrivningen. För **Mappningsschema** väljer du **Demonstrationssystem - händelseschema för webbplatsen (Global v1.1)**. Klicka på **Spara**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig2.png)

Då ser du det här. Klicka på **Lägg till tjänst**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig3.png)

Välj tjänsten **[!UICONTROL Adobe Experience Platform]**, som visar ytterligare fält. Då ser du det här.

För händelsedatauppsättning väljer du **Demonstrationssystem - händelsedatauppsättning för webbplats (Global v1.1)** och för profildatauppsättning väljer du **Demonstrationssystem - profildatauppsättning för webbplats (Global v1.1)**. Klicka på **Spara**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig4.png)

Du kommer att se det här.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig5.png)

Klicka på **[!UICONTROL Tags]** på den vänstra menyn.

Filtrera sökresultaten så att du kan se dina datainsamlingsegenskaper. Öppna egenskapen för **webben** genom att klicka på den.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig10a.png)

Då ser du det här. Klicka på **Tillägg**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig11.png)

Klicka först på Adobe Experience Platform Web SDK-tillägget och sedan på **Konfigurera**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig12.png)

Då ser du det här. Titta närmare på menyn **Datastreams** och se till att rätt sandlåda är markerad, som i ditt fall ska vara `--aepSandboxName--`.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig12a.png)

Öppna listrutan **Datastreams** och välj den datastream som du skapade tidigare.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig13.png)

Se till att du har valt din **datastream** i alla tre olika miljöer. Klicka sedan på **Spara**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig14.png)

Gå till **Publiceringsflöde**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig15.png)

Klicka på **..** för **Main** och klicka sedan på **Edit**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig16.png)

Klicka på **Lägg till alla ändrade resurser** och sedan på **Spara och skapa för utveckling**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig17.png)

Ändringarna publiceras nu och är klara om några minuter. Därefter visas den gröna punkten intill **Main**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig17a.png)

## Skapa ditt datastream för mobilen

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/){target="_blank"}.

Klicka på **[!UICONTROL Datastreams]**.

![Klicka på Datastream-ikonen i den vänstra navigeringen](./images/edgeconfig1a.png)

I skärmens övre högra hörn väljer du namnet på sandlådan, som ska vara `--aepSandboxName--`.

>[!NOTE]
>
> Skärmbilden nedan visar att en viss sandlåda har valts. När du går igenom den här självstudiekursen är det troligt att din sandlåda har ett annat namn. När du registrerade dig för den här självstudiekursen fick du den information om miljön som du skulle använda. Följ dessa instruktioner.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1b.png)

Klicka på **[!UICONTROL New Datastream]**.

![Klicka på Datastream-ikonen i den vänstra navigeringen](./images/edgeconfig1.png)

Ange `--aepUserLdap-- - One Adobe Datastream (Mobile)` för **[!UICONTROL Friendly Name]** och den valfria beskrivningen. För **Mappningsschema** väljer du **Demonstrationssystem - händelseschema för mobilapp (Global v1.1)**. Klicka på **Spara**.

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

Klicka på tillägget **Adobe Experience Platform Edge Network** och sedan på **Konfigurera**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig12m.png)

Då ser du det här. Nu måste du välja rätt sandlåda och datastream som du precis konfigurerade. Sandlådan som ska användas är `--aepSandboxName--` och datastream kallas `--aepUserLdap-- - One Adobe Datastream (Mobile)`.

Använd standarddomänen för **Edge Network**.

Klicka på **Spara** för att spara ändringarna.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig13m.png)

Gå till **Publiceringsflöde**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig15m.png)

Klicka på **..** bredvid **Huvudsida** och klicka sedan på **Redigera**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig16m.png)

Klicka på **Lägg till alla ändrade resurser** och sedan på **Spara och skapa för utveckling**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig17m.png)

Ändringarna publiceras nu och är klara om några minuter. Därefter visas den gröna punkten intill **Main**.

![Namnge Edge-konfigurationen och spara](./images/edgeconfig17ma.png)

## Nästa steg

Gå till [Använd webbplatsen](./ex4.md){target="_blank"}

Gå tillbaka till [Komma igång](./getting-started.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}