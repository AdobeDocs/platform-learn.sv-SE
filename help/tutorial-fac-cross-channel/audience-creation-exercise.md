---
title: Skapa en målgrupp
seo-title: Create an audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Skapa en målgrupp
description: I den här lektionen konfigurerar vi en anslutning mellan Adobe Experience Platform och ditt företag Data Warehouse för att aktivera Federated Audience Composition.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Målgruppsövningar

Den här övningen vägleder dig genom att skapa en målgrupp från din Data Warehouse med Federated Audience Composition. Vi bygger en målgrupp för att kvalificera SecurFinancial-kunder som har en kreditpoäng på 650 eller högre och som för närvarande inte har något lån i sin SecurFinancial-portfölj.

## Steg

1. Klicka på fliken **Federerade kompositioner** på portalen **Kund > Publiker**.
2. Klicka på **Skapa komposition**.

   ![create-composition](assets/create-composition.png)

3. Ange kompositionen som `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]`. Klicka på **Skapa**.

4. Klicka på knappen **+** på arbetsytan och välj **Skapa målgrupp**. Högerspåret ska visas.

5. Klicka på **Välj ett schema** och välj **FSI_CRM**-schemat. Klicka sedan på **Bekräfta**.

6. Klicka på **Fortsätt**. Klicka på knappen **+** och sedan på **Anpassat villkor** i fönstret för frågebyggaren. Skapa följande villkor:
   - `CURRENTPRODUCTS does not contain loan`
   - `AND`
   - `CREDITSCORE greater than or equal to 650`
   - Vi använder marknadsföringsdata för att segmentera kunder som har valt e-post som den kommunikationskanal de föredrar:
   - `AND`
   - `CONSENTSMARKETINGPREFERRED equal to email`

   **Obs!** Värdefältet är skiftlägeskänsligt.

   Frågan bör nu se ut så här:

   ![query-builder](assets/query-builder.png)

7. Klicka på nästa **+**-knapp och klicka sedan på **Spara målgrupp**.

   Ge det här steget etiketten `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]`. Använd samma värde som målgruppsetiketten.

8. Lägg till följande målgruppsmappningar:
   - **Source målgruppsfält:** E-POST
   - **Source-målgruppsfält:** CURRENTPRODUCTS
   - **Source-målgruppsfält:** FÖRNAMN

9. Välj den primära identiteten och namnutrymmet som ska användas för profiler:
   - **Primärt identitetsfält:** E-post
   - **Identitetsnamnrymd:** E-post

10. Klicka på **Spara** och sedan på **Start** för att köra frågan om kompositionen som du just skapade.

**Obs!** Vi använde produkt- och kreditinformation för att skapa vår målgrupp som inte flyttade känsliga data, som kreditpoäng, till efterföljande plattformar för aktivering.

Mer information om målgruppssammansättning finns på [Experience League](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}.

Nu när vår externa målgrupp har skapats går vi vidare med att [mappa den till ett S3-konto](map-federated-audience-to-s3.md).
