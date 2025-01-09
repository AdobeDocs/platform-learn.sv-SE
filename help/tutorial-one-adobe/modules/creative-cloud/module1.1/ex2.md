---
title: Komma igång med Firefly Services
description: Komma igång med Firefly Services
kt: 5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: 6c344db00b8296c8ea6d31c83cefd8edcddb51b1
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---

# 1.1.2 Optimera Firefly-processen med Microsoft Azure och försignerade URL:er

## 1.1.2.1 Skapa en Azure-prenumeration

>[!NOTE]
>
>Om du redan har en befintlig Azure-prenumeration kan du hoppa över det här steget. Fortsätt med nästa övning i så fall.

Gå till [https://portal.azure.com](https://portal.azure.com) och logga in med ditt Azure-konto. Om du inte har någon, använd din personliga e-postadress för att skapa ditt Azure-konto.

![Azure Storage](./images/02azureportalemail.png)

När inloggningen är klar visas följande skärm:

![Azure Storage](./images/03azureloggedin.png)

Klicka på menyn till vänster och välj **Alla resurser**. Azure-prenumerationsskärmen visas om du inte har prenumererat ännu. I så fall väljer du **Starta med en kostnadsfri Azure-utvärderingsversion**.

![Azure Storage](./images/04azurestartsubscribe.png)

Fyll i Azure-prenumerationsformuläret, ange din mobiltelefon och ditt kreditkort för aktivering (du har en kostnadsfri nivå i 30 dagar och du debiteras inte om du inte uppgraderar).

När prenumerationsprocessen är klar är du redo att gå:

![Azure Storage](./images/06azuresubscriptionok.png)

## 1.1.2.2 Skapa Azure Storage-konto

Sök efter `storage account` och klicka sedan på **Lagringskonton**.

![Azure Storage](./images/azs1.png)

Klicka på **+ Skapa**.

![Azure Storage](./images/azs2.png)

Fyll i följande information:

- Välj din **prenumeration**
- Välj (eller skapa) en **resursgrupp**
- **Lagringskontots namn**: använd `--aepUserLdap--`

Klicka på **Granska + skapa**.

![Azure Storage](./images/azs3.png)

Klicka på **Skapa**.

![Azure Storage](./images/azs4.png)

Du får då en liknande bekräftelse. Klicka på **Gå till resursen**.

![Azure Storage](./images/azs5.png)

Ditt Azure Storage-konto är nu klart att användas.

![Azure Storage](./images/azs6.png)

Klicka på **Datalagring** och gå sedan till **Behållare**. Klicka på **+ behållare**.

![Azure Storage](./images/azs7.png)

Använd `--aepUserLdap--` som namn. Klicka på **Skapa**.

![Azure Storage](./images/azs8.png)

Behållaren är nu klar att användas.

![Azure Storage](./images/azs9.png)

## 1.1.2.3 Installera Azure Storage Explorer

Du använder Microsoft Azure Storage Explorer för att hantera dina filer. Du kan hämta den via [den här länken](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4). Välj rätt version för ditt specifika operativsystem, hämta den och installera den.

![Azure Storage](./images/az10.png)

Öppna programmet när det har installerats. Du kommer att se något liknande. Klicka på **Logga in med Azure**.

![Azure Storage](./images/az11.png)

Klicka på **Prenumeration**.

![Azure Storage](./images/az12.png)

Välj **Azure** och klicka på **Nästa**.

![Azure Storage](./images/az13.png)

Välj ditt Microsoft Azure-konto och slutför autentiseringsprocessen.

![Azure Storage](./images/az14.png)

När det är autentiserat visas ett meddelande som detta.

![Azure Storage](./images/az15.png)

Växla tillbaka till Microsoft Azure Storage Explorer-appen. Välj din prenumeration och klicka på **Öppna Utforskaren**.

![Azure Storage](./images/az16.png)

Du hittar sedan ditt lagringskonto under **Lagringskonton**.

![Azure Storage](./images/az17.png)

Öppna **Blobbehållare** och klicka sedan på behållaren som du skapade i föregående övning.

![Azure Storage](./images/az18.png)

## 1.1.2.4 Manuell filöverföring och användning av en bildfil som formatreferens

Du bör nu överföra en bildfil som du väljer till behållaren. Du kan använda valfri bildfil eller så kan du använda [den här filen](./images/gradient.jpg) genom att hämta den till datorn.

![Azure Storage](./images/gradient.jpg)

Släpp bildfilen i din behållare i Azure Storage Explorer.

När du har överfört den visas den i behållaren:

![Azure Storage](./images/az19.png)

Högerklicka på filen `gradient.jpg` och klicka sedan på **Hämta signatur för delad åtkomst**.

![Azure Storage](./images/az20.png)

Under **Behörigheter** krävs bara **Läs**. Klicka på **Skapa**.

![Azure Storage](./images/az21.png)

Du kommer då att se din försignerade URL för den här bildfilen. Kopiera den som du behöver den för nästa API-begäran till Firefly.

![Azure Storage](./images/az22.png)

Gå tillbaka till Postman. Öppna begäran **POST - Firefly - T2I (styleref) V3**. Du kommer då att se detta i **Body**.

![Azure Storage](./images/az23.png)

Ersätt platshållarens URL med den försignerade URL-adressen för bildfilen som du kopierade från Azure Storage Explorer. Du får den här då. Klicka på **Skicka**.

![Azure Storage](./images/az24.png)

Du får sedan ett svar från Firefly Services igen, med en ny bild. Öppna bildfilen i webbläsaren.

![Azure Storage](./images/az25.png)

Du kommer då att se en annan bild med `horses in a field`, men den här gången liknar stilen den bildfil som du angav som stilreferens.

![Azure Storage](./images/az26.png)

## 1.1.2.5 Programmatisk filöverföring

Om du vill använda programmatisk filöverföring med Azure Storage-konton måste du skapa en ny **SAS**-token (Shared Access Signature) med behörighet att skriva en fil.

Gå tillbaka till Azure Storage Explorer om du vill göra det. Högerklicka på behållaren och klicka sedan på **Hämta signatur för delad åtkomst**.

![Azure Storage](./images/az27.png)

Under **Behörigheter** krävs följande behörigheter:

- **Läs**
- **Lägg till**
- **Skapa**
- **Skriv**
- **Lista**

Klicka på **Skapa**.

![Azure Storage](./images/az28.png)

Du får då din **SAS-token**. Klicka på **Kopiera**.

![Azure Storage](./images/az29.png)

Du kan nu använda denna **SAS-token** för att överföra en fil till ditt Azure Storage-konto. Gå tillbaka till Postman för att göra det.

Klicka för att markera mappen **FF - Firefly Services Tech Insiders**, klicka sedan på 3 punkter **..** i mappen **Firefly** och klicka sedan på **Lägg till begäran**.

![Azure Storage](./images/az30.png)

Du får då en tom förfrågan. Ändra namnet på begäran till **Överför fil till Azure Storage-konto**, ändra **begärantyp** till **PUT** och klistra in SAS-token-URL:en i URL-avsnittet.

Klicka sedan på **Brödtext**.

![Azure Storage](./images/az31.png)

Du måste nu välja en fil på den lokala datorn. Du kan använda en ny bildfil eller använda en annan bildfil som du hittar [här](./images/gradient2-p.jpg).

![Övertoningsfil](./images/gradient2-p.jpg)

I **Brödtext** väljer du **binär** och klickar sedan på **Välj fil** och sedan på **+ Ny fil från den lokala datorn**.

![Azure Storage](./images/az32.png)

Välj önskad fil och klicka på **Öppna**.

![Azure Storage](./images/az33.png)

Då ser du det här. Nästa sak du ska göra är att ange filnamnet som ska användas i ditt Azure Storage-konto. Om du vill göra det måste du placera markörerna framför frågetecknet **?** i URL:en. Du kan för närvarande se detta:

![Azure Storage](./images/az34.png)

URL:en ser för närvarande ut så här, men måste ändras.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

Det filnamn som ska användas är `gradient2-p.jpg`, vilket innebär att URL:en måste ändras så att filnamnet inkluderas:

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Azure Storage](./images/az34a.png)

Gå sedan till **Sidhuvuden** där du måste lägga till en ny rubrik manuellt. Använd detta:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Azure Storage](./images/az35.png)

Gå till **Auktorisering** och ange **Autentiseringstyp** till **Ingen autentisering**. Klicka på **Skicka**.

![Azure Storage](./images/az36.png)

Du kommer då att se det tomma svaret i Postman, vilket innebär att din filöverföring gick bra.

![Azure Storage](./images/az37.png)

Om du sedan går tillbaka till Azure Storage Explorer och uppdaterar innehållet i din mapp, kommer du nu att hitta den nyligen överförda filen där.

![Azure Storage](./images/az38.png)

## 1.1.2.5 Programmatisk filanvändning

Om du vill använda programmässig läsning av filer från Azure Storage-konton måste du skapa en ny **SAS**-token (Shared Access Signature) med behörighet att läsa en fil. Du kan tekniskt använda den SAS-token som du skapade i föregående övning, men det är bäst att ha en separat token med bara **läsbehörighet**.

Gå tillbaka till Azure Storage Explorer om du vill göra det. Högerklicka på behållaren och klicka sedan på **Hämta signatur för delad åtkomst**.

![Azure Storage](./images/az27.png)

Under **Behörigheter** krävs följande behörigheter:

- **Läs**
- **Lägg till**
- **Skapa**
- **Skriv**
- **Lista**

Klicka på **Skapa**.

![Azure Storage](./images/az28.png)


Nästa steg: [1.1.3 ...](./ex3.md)

[Gå tillbaka till modul 1.1](./firefly-services.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
