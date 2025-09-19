---
title: Komma igång med Adobe Commerce as a Cloud Service
description: Komma igång med Adobe Commerce as a Cloud Service
kt: 5342
doc-type: tutorial
source-git-commit: 28553f8042be7bfc0b553272a6c72e6677fe1cb3
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 14%

---

# 1.5.1 Komma igång med Adobe Commerce as a Cloud Service

Gå till [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Kontrollera att du är i rätt miljö, som bör ha namnet `--aepImsOrgName--`. Klicka på **Commerce**.

![AEM Assets](./images/accs1.png)

## 1.5.1.1 Skapa en ACCS-instans

Du borde se det här då. Klicka på **+ Lägg till instans**.

![AEM Assets](./images/accs2.png)

Fyll i fälten så här:

- **Instansnamn**: `--aepUserLdap-- - ACCS`
- **Miljö**: `Sandbox`
- **Region**: `North America`

Klicka på **Lägg till instans**.

![AEM Assets](./images/accs3.png)

Du håller på att skapas. Detta kan ta 5-10 minuter.

![AEM Assets](./images/accs4.png)

När instansen är klar klickar du på instansen för att öppna den.

![AEM Assets](./images/accs5.png)

## 1.5.1.2 Konfigurera ditt CitiSignal-arkiv

Du borde se det här då. Klicka på **Logga in med Adobe ID** och logga sedan in.

![AEM Assets](./images/accs6.png)

När du är inloggad bör du se den här hemsidan. Det första steget är att konfigurera din CitiSignal-butik i Commerce. Klicka på **Lagrar**.

![AEM Assets](./images/accs7.png)

Klicka på **Alla butiker**.

![AEM Assets](./images/accs8.png)

Klicka på **Skapa webbplats**.

![AEM Assets](./images/accs9.png)

Fyll i fälten så här:

- **Namn**: `CitiSignal`
- **Kod**: `citisignal`

Klicka på **Spara webbplats**.

![AEM Assets](./images/accs10.png)

Du borde vara tillbaka här. Klicka på **Skapa butik**.

![AEM Assets](./images/accs11.png)

Fyll i fälten så här:

- **Webbplats**: `CitiSignal`
- **Namn**: `CitiSignal`
- **Kod**: `citisignal`
- **Rotkategori**: `Default Category`

Klicka på **Spara butik**.

![AEM Assets](./images/accs12.png)

Du borde vara tillbaka här. Klicka på **Skapa butiksvy**.

![AEM Assets](./images/accs13.png)

Fyll i fälten så här:

- **Butik**: `CitiSignal`
- **Namn**: `CitiSignal`
- **Kod**: `citisignal`
- **Status**: `Enabled`

Klicka på **Spara butiksvy**.

![AEM Assets](./images/accs14.png)

Du bör då se det här meddelandet. Klicka på **OK**.

![AEM Assets](./images/accs15.png)

Du borde vara tillbaka här.

![AEM Assets](./images/accs16.png)

## 1.5.1.3 Konfigurera kategorier och produkter

Gå till **Katalog** och välj sedan **Kategorier**.

![AEM Assets](./images/accs17.png)

Välj **Standardkategori** och klicka sedan på **Lägg till underkategori**.

![AEM Assets](./images/accs18.png)

Ange namnet `Phones` och klicka sedan på **Spara**.

![AEM Assets](./images/accs19.png)

Välj **Standardkategori** och klicka sedan på **Lägg till underkategori** igen.

![AEM Assets](./images/accs20.png)

Ange namnet `Watches` och klicka sedan på **Spara**.

![AEM Assets](./images/accs21.png)

Du bör sedan skapa två kategorier.

![AEM Assets](./images/accs22.png)

Gå sedan till **Katalog** och välj **Produkter**.

![AEM Assets](./images/accs23.png)

Du borde se det här då. Klicka på **Lägg till produkt**.

![AEM Assets](./images/accs24.png)

Konfigurera din produkt så här:

- **Produktnamn**: `iPhone Air`
- **SKU**: `iPhone-Air`
- **Pris**: `999`
- **Kvantitet**: `10000`
- **Kategorier**: välj `Phones`

Klicka på **Spara**.

![AEM Assets](./images/accs25.png)

Bläddra ned till **Konfigurationer** och klicka på **Skapa konfigurationer**.

![AEM Assets](./images/accs26.png)

Du borde se det här då. Klicka på **Skapa nytt attribut**.

![AEM Assets](./images/accs27.png)

Ange **standardetiketten** till `Storage` och klicka sedan på **Lägg till alternativ** under **Hantera alternativ**.

![AEM Assets](./images/accs28.png)

Konfigurera det första alternativet med namnet `256GB` i alla tre kolumnerna och klicka sedan på **Lägg till alternativ** igen.

![AEM Assets](./images/accs29.png)

Konfigurera det andra alternativet med namnet `512GB` i alla tre kolumnerna och klicka sedan på **Lägg till alternativ** igen.

![AEM Assets](./images/accs30.png)

Konfigurera det tredje alternativet med namnet `1TB` i alla tre kolumnerna och klicka sedan på **Lägg till alternativ** igen.

![AEM Assets](./images/accs31.png)

Bläddra ned till **Egenskaper för Storefront**. Ange följande alternativ till **Ja**:

- **Använd i sökning**
- **Tillåt HTML-taggar på Storefront**
- **Visas på katalogsidor på Storefront**
- **Använd i produktlista**

![AEM Assets](./images/accs32.png)

Bläddra uppåt och klicka på **Spara attribut**.

![AEM Assets](./images/accs33.png)

Du borde se det här då. Välj båda attributen för **color** och **storage** och klicka på **Next**.

![AEM Assets](./images/accs34.png)

Du borde se det här då. Nu måste du lägga till de tillgängliga färgalternativen. Det gör du genom att klicka på **Skapa nytt värde**.

![AEM Assets](./images/accs35.png)

Ange värdet `Sky-Blue` och klicka på **Skapa nytt värde**.

![AEM Assets](./images/accs36.png)

Ange värdet `Light-Gold` och klicka på **Skapa nytt värde**.

![AEM Assets](./images/accs37.png)

Ange värdet `Cloud-White` och klicka på **Skapa nytt värde**.

![AEM Assets](./images/accs38.png)

Ange värdet `Space-Black`. Klicka på **Markera alla**

![AEM Assets](./images/accs39.png)

Välj alla tre alternativen under **Lagring** och klicka på **Nästa**.

![AEM Assets](./images/accs40.png)

Lämna standardinställningarna och klicka på **Nästa**.

![AEM Assets](./images/accs41.png)

Du borde se det här då. Klicka på **Skapa produkter**.

![AEM Assets](./images/accs42.png)

Klicka på **Spara**.

![AEM Assets](./images/accs43.png)

Bläddra ned till **Produkt på webbplatser** och markera kryssrutan för **CitiSignal**.

Klicka på **Spara**.

![AEM Assets](./images/accs44.png)

Klicka på **Bekräfta**.

![AEM Assets](./images/accs45.png)

Du borde se det här då. Klicka på **Bakåt**.

![AEM Assets](./images/accs46.png)

Du ser nu produkten **iPhone Air** och dess varianter i produktkatalogen.

![AEM Assets](./images/accs47.png)


Nästa steg: [Anslut ACCS till AEM Sites CS/EDS Storefront](./ex2.md){target="_blank"}

Gå tillbaka till [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
