---
title: Komma igång med AJO Translation Services
description: Komma igång med AJO Translation Services
kt: 5342
doc-type: tutorial
exl-id: ee0b8650-a59f-4888-8228-4caafe4143e4
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# 3.2.1 Översättningsleverantör

## 3.2.1.1 Konfigurera Microsoft Azure Translator

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

## 3.2.1.2 Språkordlista

Gå till [https://experience.adobe.com/](https://experience.adobe.com/). Klicka på **Journey Optimizer**.

![Översättningar](./images/ajolp1.png)

Gå till **Översättningar** på den vänstra menyn och gå sedan till **Språkordlista**. Om det här meddelandet visas klickar du på **Lägg till standardspråk**.

![Översättningar](./images/locale1.png)

Du borde se det här då.

![Översättningar](./images/locale2.png)

## 3.2.1.3 Konfigurera översättningsprovider i AJO

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

## 3.2.1.4 Konfigurera översättningsprojekt

Gå till [https://experience.adobe.com/](https://experience.adobe.com/). Klicka på **Journey Optimizer**.

![Översättningar](./images/ajolp1.png)

Gå till **Översättningar** på den vänstra menyn och gå sedan till **Språkordlista**. Om det här meddelandet visas klickar du på **Skapa projekt**.

![Översättningar](./images/ajoprovider1.png)

Ange namnet `--aepUserLdap-- - Translations`, ställ in **Source Locale** på `[en-US] English - United States` och markera kryssrutan för att aktivera **Publicera godkända översättningar automatiskt**. Klicka sedan på **+ Lägg till en språkinställning**.

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

Du har gjort klart den här övningen.

## Nästa steg

Gå till [3.2.2 Skapa din kampanj](./ex2.md)

Gå tillbaka till [Modul 3.2](./ajotranslationsvcs.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}