---
title: Skapa en resa med externa målgruppsdata
seo-title: Build a journey with federated audience data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Skapa en resa med externa målgruppsdata
description: I den här lektionen ska vi använda en federerad målgrupp på en Journey Optimizer-resa.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-build-a-journey-with-federated-audience-data.jpg
hide: true
source-git-commit: b5611dccdba66d31f7dfcd96506e06d1bdd5fb3d
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Bygg en resa med Federated Audience Data

I den här lektionen får du lära dig hur en federerad publik kan användas på resor inom Adobe Journey Optimizer (AJO). Detta inkluderar att använda frågeattribut från Federated Audience Composition för att personalisera meddelanden. För att fortsätta med SecurFinancial-kundberättelsen och ta itu med kundåterannonsering och personalisering arbetar vi med en resa för kvalificerade kunder. Målet är att skicka ett personaliserat e-postmeddelande baserat på attribut som federerats från SecurFinancial&#39;s Data Warehouse.

## Steg

### Bygg en resa med en Läs publik

1. Navigera till portalen **Resor** och klicka på knappen **Skapa resa** .

   ![skapa-en-resa](assets/create-journey.png)

2. Uppdatera resans egenskaper med ett nytt namn: **`SecurFinancial - Home Loan Offer`**.

3. Klicka på **Orchestration** och dra sedan rutan **Läs målgrupp** till arbetsytan.

4. Klicka på pennikonen **bredvid rutan Målgrupp till höger på skärmen.**

5. Sök efter **`SecureFinancial Customers - No Loans, Good Credit`** i sökfältet och klicka sedan på **Spara**.

   ![skapa-en-resa](assets/select-audience.png)

6. Lämna alla inställningar som standard på den högra menyn och klicka sedan på **Spara**.

   ![save-målgruppsinställningar](assets/save-audience-settings.png)

### Anpassa e-post

1. Klicka på **Åtgärder**, klicka och dra sedan rutan **E-post** till arbetsytan.

2. Klicka på **E-postkonfiguration** på den högra menyn och välj **E-postmarknadsföring**. Klicka sedan på **Redigera innehåll**.

3. Lägg till: **`Learn more about SecurFinancial Home Loan`** på ämnesraden. Klicka sedan på **Redigera e-postbrödtext**.

4. Klicka på knappen **Innehållsmall** i det övre högra hörnet. Sök efter och markera `SecureFinancial Template` och klicka sedan på **Bekräfta**.

   ![travel-email-config](assets/journey-email-config.png)

   ![resa-email-confirm](assets/journey-email-confirm.png)

5. Granska mallen och klicka på **Använd mall**.

6. Du kommer nu att vara med i e-postprogrammet Designer. Håll muspekaren över makrot `{profile.person.name.firstName}` och klicka på **personaliseringsavataren**.

7. Gå till följande mappsökväg i anpassningsfönstret: **`[sandbox] > audienceEnrichment > CustomerAudienceUpload`**

8. Klicka i mappen **läs målgrupp**. Här finns anrikningsattributen från er externa målgrupp.

9. Välj attributet **Förnamn** för uttrycksverktyget. E-postmeddelandet uttrycker dynamiskt kundens förnamnsvärde för att personalisera e-postmeddelandet.

10. Klicka på **Spara**.

11. Nu när personaliseringen av förnamnet har lagts till lägger du till `Hi, ` framför personaliseringsvariabeln. Klicka sedan på **Spara**.

   ![resa-email-save](assets/journey-email-save.png)

12. Klicka på knappen **Bakåt** två gånger för att återgå till arbetsytan. Klicka sedan på **Spara** på menyn **Åtgärd: E-post** till höger.

   ![spara-slutresa](assets/save-final-journey.png)

Grattis! Du har skapat en resa i AJO med en federerad publik och federerade anrikningsattribut.

Nu ska vi titta på hur vi [förbättrar befintliga målgrupper](audience-enrichment-demo.md) i Experience Platform med federerade data från datalagret.
