---
title: Komma igång med AJO Translation Services
description: Komma igång med AJO Translation Services
kt: 5342
doc-type: tutorial
exl-id: 28c925dd-8a7b-4b9a-a128-ecbfbfbeaf04
source-git-commit: 7438a1289689c5c3fb3deb398aa9898d7ac26cf8
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 3.5.1 Översättningsleverantör

## 3.5.1.1 Konfigurera Microsoft Azure Translator

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home).

![Översättningar](./images/transl1.png)

Ange `translators` i sökfältet. Klicka sedan på **+ Skapa**.

![Översättningar](./images/transl2.png)

Välj **Skapa översättare**.

![Översättningar](./images/transl3.png)

Välj ditt **prenumerations-ID** och **resursgrupp**.
Ange **Region** till **Global**.
Ange **prisnivån** till **kostnadsfri F0**.

Välj **Granska + skapa**.

![Översättningar](./images/transl4.png)

Välj **Skapa**.

![Översättningar](./images/transl5.png)

Välj **Gå till resursen**.

![Översättningar](./images/transl6.png)

Gå till **Resurshantering** > **Tangenter och slutpunkt** på den vänstra menyn. Klicka för att kopiera nyckeln.

![Översättningar](./images/transl7.png)

## 3.5.1.2 Språkordlista

Gå till [https://experience.adobe.com/](https://experience.adobe.com/). Klicka på **Journey Optimizer**.

![Översättningar](./images/ajolp1.png)

Gå till **Översättningar** på den vänstra menyn och gå sedan till **Språkordlista**. Om det här meddelandet visas klickar du på **Lägg till standardspråk**.

![Översättningar](./images/locale1.png)

Du borde se det här då.

![Översättningar](./images/locale2.png)

## 3.5.1.3 Konfigurera översättningsprovider i AJO

Gå till [https://experience.adobe.com/](https://experience.adobe.com/). Klicka på **Journey Optimizer**.

![Översättningar](./images/ajolp1.png)

Gå till **Översättningar** på den vänstra menyn och gå sedan till **Providers**. Klicka på **Lägg till provider**.

![Översättningar](./images/transl8.png)

Under **Providers** väljer du **Microsoft Translator**. Markera kryssrutan för att aktivera användningen av översättningsprovidern. Klistra in nyckeln som du kopierade från Microsoft Azure Translators. Klicka sedan på **Verifiera autentiseringsuppgifter**.

![Översättningar](./images/transl9.png)

Dina autentiseringsuppgifter bör sedan valideras. Om de är det, bläddrar du nedåt för att välja språk för översättning.

![Översättningar](./images/transl10.png)

Välj `[en-US] English`, `[es] Spanish`, `[fr] French`, `[nl] Dutch`.

![Översättningar](./images/transl11.png)

Bläddra uppåt och klicka på **Spara**.

![Översättningar](./images/transl12.png)

**Översättningsprovidern** är nu klar att användas.

![Översättningar](./images/transl13.png)

## 3.5.1.4 Konfigurera översättningsprojekt

Gå till [https://experience.adobe.com/](https://experience.adobe.com/). Klicka på **Journey Optimizer**.

![Översättningar](./images/ajolp1.png)

Gå till **Översättningar** på den vänstra menyn och gå sedan till **Språkordlista**. Om det här meddelandet visas klickar du på **Skapa projekt**.

![Översättningar](./images/ajoprovider1.png)

Ange namnet `--aepUserLdap-- - Translations`, ställ in **Source Locale** på `[en-US] English - United States` och markera kryssrutorna för att aktivera både **Publicera automatiskt godkända översättningar** och **Aktivera granskningsarbetsflöde**. Klicka sedan på **+ Lägg till en språkinställning**.

![Översättningar](./images/ajoprovider1a.png)

Sök efter `fr`, aktivera kryssrutan för `[fr] French` och aktivera sedan kryssrutan för **Microsoft Translator**. Klicka på **+ Lägg till en språkinställning**.

![Översättningar](./images/ajoprovider2.png)

Sök efter `es`, aktivera kryssrutan för `[es] Spanish` och aktivera sedan kryssrutan för **Microsoft Translator**. Klicka på **+ Lägg till en språkinställning**.

![Översättningar](./images/ajoprovider3.png)

Sök efter `nl`, aktivera kryssrutan för `[nl] Spanish` och aktivera sedan kryssrutan för **Microsoft Translator**. Klicka på **+ Lägg till en språkinställning**.

![Översättningar](./images/ajoprovider6.png)

Klicka på **Spara**.

![Översättningar](./images/ajoprovider8.png)

Ditt **översättningsprojekt** är nu klart att användas.

![Översättningar](./images/ajoprovider9.png)

## 3.5.1.5 Konfigurera språkinställningar

Gå till **Kanaler** > **Allmänna inställningar** > **Språkinställningar**. Klicka på **Skapa språkinställningar**.

![Journey Optimizer](./images/camploc6.png)

Använd namnet `--aepUserLdap--_translations`. Välj **Översättningsprojekt**. Klicka sedan på ikonen **redigera** .

![Journey Optimizer](./images/camploc7.png)

Välj det översättningsprojekt som du skapade i föregående steg. Klicka på **Markera**.

![Journey Optimizer](./images/camploc8.png)

Du borde se det här då. Ange **Återställningsinställningen** till **Engelska - USA**. Klicka för att välja **Välj profilspråkets attribut**, vilket avgör vilket fält i kundprofilen som ska användas för att läsa in översättningarna. Klicka sedan på ikonen **redigera** för att välja vilket fält som ska användas.

![Journey Optimizer](./images/camploc9.png)

Ange **önskat språk** i sökfältet och markera sedan fältet **Önskat språk**.

![Journey Optimizer](./images/camploc10.png)

Klicka på ikonen **edit** för både **English - United States** och **Dutch** för att granska konfigurationen.

![Journey Optimizer](./images/camploc11.png)

Här är konfigurationen för **engelska - USA**. Klicka på **Avbryt**.

![Journey Optimizer](./images/camploc12.png)

Klicka för att visa konfigurationen för **Dutch**. Klicka på **Avbryt**.

![Journey Optimizer](./images/camploc13.png)

Bläddra uppåt och klicka på **Skicka**.

![Journey Optimizer](./images/camploc14.png)

Dina språkinställningar har nu konfigurerats.

![Journey Optimizer](./images/camploc15.png)

Du har gjort klart den här övningen.

## Nästa steg

Gå till [3.5.2 Skapa din kampanj](./ex2.md)

Gå tillbaka till [Modul 3.5](./ajotranslationsvcs.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
