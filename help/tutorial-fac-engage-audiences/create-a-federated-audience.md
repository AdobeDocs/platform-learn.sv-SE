---
title: Skapa en federerad publik
seo-title: Create a federated audience | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Skapa en federerad publik
description: I den här övningen skapar vi en målgrupp från Snowflake datalager med Federated Audience Composition.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a507cab5-dba9-4bf7-a043-d7c967e9e07d
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Skapa en federerad publik

Sedan vägleder vi dig genom att skapa en målgrupp från Snowflake datalager med Federated Audience Composition. Publiken består av SecurFinancial-kunder som har en kreditpoäng på 650 eller högre och som för närvarande inte har något lån i sin SecurFinancial-portfölj.

## Steg

1. Klicka på fliken **Federerade kompositioner** på portalen **Kund > Publiker**.
2. Klicka på **Skapa komposition**.

   ![create-composition](assets/create-composition.png)

3. Märk upp kompositionen. I vårt exempel: `SecurFinancial Customers - No Loans, Good Credit`. Klicka på **Skapa**.

4. Klicka på knappen **+** på arbetsytan och välj **Skapa målgrupp**. Högerspåret visas.

5. Klicka på **Välj ett schema**, välj lämpligt schema och klicka sedan på **Bekräfta**.

6. Klicka på **Fortsätt**. Klicka på knappen **+** och sedan på **Anpassat villkor** i fönstret för frågebyggaren. Skriv villkoren. I vårt exempel används:

   `CURRENTPRODUCTS does not contain loan`
   `AND`
   `CREDITSCORE greater than or equal to 650`
   `AND`
   `CONSENTSMARKETINGPREFERRED equal to email`

   *Det sista villkoret garanterar att marknadsföringsinställningsdata används för att segmentera kunder som har valt e-post som den önskade kommunikationskanalen*.

   **Obs!** Värdefältet är skiftlägeskänsligt.

   ![query-builder](assets/query-builder.png)

7. Klicka på nästa **+**-knapp och klicka sedan på **Spara målgrupp**. Ge det här steget en etikett. I vårt exempel kommer vi att märka det som `SecurFinancial Customers - No Loans, Good Credit`.

8. Lägg till relevanta målgruppsmappningar. I detta exempel:

   - **Source målgruppsfält:** E-POST
   - **Source-målgruppsfält:** CURRENTPRODUCTS
   - **Source-målgruppsfält:** FÖRNAMN

9. Välj den primära identiteten och namnutrymmet som ska användas för profiler. Detta är de identiteter och fält som används för våra data:

   - **Primärt identitetsfält:** E-post
   - **Identitetsnamnrymd:** E-post

10. Klicka på **Spara** och sedan på **Start** för att köra frågan om kompositionen.

>[**SAMMANFATTNING**]
>
> I det här exemplet användes produkt- och kreditinformation för att skapa en större publik genom direkt åtkomst av företagsdata från Snowflake, utan att man behöver göra en kopia av den i Adobe Experience Platform. När frågan bearbetas av det externa systemet kommer endast relevanta e-postadresser, aktuella produkter och förnamnsvärden att överföras till målgruppsdefinitionen för aktivering längre fram i kedjan. Detta gäller alla destinationer som RTCDP stöder.

Mer information om målgruppssammansättning finns på [Experience League](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}.

Nu när vår federerade publik har skapats [mappar vi den till ett S3-konto](map-federated-audience-to-s3.md).
