---
title: Optimera din Firefly-process med Microsoft Azure och försignerade URL:er
description: Lär dig hur du optimerar din Firefly-process med Microsoft Azure och försignerade URL:er
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: 45f6f9db7d5b3e79e10d508a44a532261bd9cdb3
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 0%

---

# 1.1.2 Optimera din Firefly-process med Microsoft Azure och försignerade URL:er

Lär dig hur du optimerar din Firefly-process med Microsoft Azure och försignerade URL:er.

## 1.1.2.1 Skapa en Azure-prenumeration

>[!NOTE]
>
>Om du redan har en befintlig Azure-prenumeration kan du hoppa över det här steget. Fortsätt med nästa övning i så fall.

Gå till [https://portal.azure.com](https://portal.azure.com){target="_blank"} och logga in med ditt Azure-konto. Om du inte har någon, använd din personliga e-postadress för att skapa ditt Azure-konto.

![Azure Storage](./images/02azureportalemail.png){zoomable="yes"}

När inloggningen är klar visas följande skärm:

![Azure Storage](./images/03azureloggedin.png){zoomable="yes"}

På den vänstra menyn väljer du **Alla resurser**. Azure-prenumerationsskärmen visas om du inte har prenumererat ännu.

Om du inte prenumererar väljer du **Starta med en kostnadsfri provversion av Azure**.

![Azure Storage](./images/04azurestartsubscribe.png){zoomable="yes"}

Fyll i Azure-prenumerationsformuläret och ange din mobiltelefon och ditt kreditkort för aktivering (du har en kostnadsfri nivå i 30 dagar och du debiteras inte om du inte uppgraderar).

När prenumerationen är klar är du redo att gå.

![Azure Storage](./images/06azuresubscriptionok.png){zoomable="yes"}

## 1.1.2.2 Skapa Azure Storage-konto

Sök efter `storage account` och välj sedan **Lagringskonton**.

![Azure Storage](./images/azs1.png){zoomable="yes"}

Välj **+ Skapa**.

![Azure Storage](./images/azs2.png){zoomable="yes"}

Välj din **prenumeration** och välj (eller skapa) en **resursgrupp**.

Under **Lagringskontots namn** använder du `--aepUserLdap--`.

Välj **Granska + skapa**.

![Azure Storage](./images/azs3.png){zoomable="yes"}

Välj **Skapa**.

![Azure Storage](./images/azs4.png){zoomable="yes"}

Välj **Gå till resursen** när du har bekräftat.

![Azure Storage](./images/azs5.png){zoomable="yes"}

Ditt Azure Storage-konto är nu klart att användas.

![Azure Storage](./images/azs6.png){zoomable="yes"}

Välj **Datalagring** och gå sedan till **Behållare**. Välj **+ behållare**.

![Azure Storage](./images/azs7.png){zoomable="yes"}

Använd `--aepUserLdap--` som namn och välj **Skapa**.

![Azure Storage](./images/azs8.png){zoomable="yes"}

Behållaren är nu klar att användas.

![Azure Storage](./images/azs9.png){zoomable="yes"}

## 1.1.2.3 Installera Azure Storage Explorer

[Hämta Microsoft Azure Storage Explorer för att hantera dina filer](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}. Välj rätt version för ditt specifika operativsystem, hämta och installera det.

![Azure Storage](./images/az10.png){zoomable="yes"}

Öppna programmet och välj **Logga in med Azure**.

![Azure Storage](./images/az11.png){zoomable="yes"}

Välj **Prenumeration**.

![Azure Storage](./images/az12.png){zoomable="yes"}

Välj **Azure** och sedan **Next**.

![Azure Storage](./images/az13.png){zoomable="yes"}

Välj ditt Microsoft Azure-konto och slutför autentiseringsprocessen.

![Azure Storage](./images/az14.png){zoomable="yes"}

Efter autentiseringen visas det här meddelandet.

![Azure Storage](./images/az15.png){zoomable="yes"}

Gå tillbaka till Microsoft Azure Storage Explorer-appen, välj din prenumeration och välj **Öppna Utforskaren**.

>[!NOTE]
>
>Om ditt konto inte visas klickar du på **kugghjulsikonen** bredvid din e-postadress och väljer **Avfiltrera**.

![Azure Storage](./images/az16.png){zoomable="yes"}

Ditt lagringskonto visas under **Lagringskonton**.

![Azure Storage](./images/az17.png){zoomable="yes"}

Öppna **Blobbehållare** och markera sedan den behållare som du skapade i föregående övning.

![Azure Storage](./images/az18.png){zoomable="yes"}

## 1.1.2.4 Manuell filöverföring och användning av en bildfil som formatreferens

Överför en bildfil eller [den här filen](./images/gradient.jpg){target="_blank"} till behållaren.

![Azure Storage](./images/gradient.jpg)

När du har överfört den kan du se den i behållaren:

![Azure Storage](./images/az19.png){zoomable="yes"}

Högerklicka på `gradient.jpg` och välj sedan **Hämta signatur för delad åtkomst**.

![Azure Storage](./images/az20.png){zoomable="yes"}

Under **Behörigheter** krävs bara **Läs**. Välj **Skapa**.

![Azure Storage](./images/az21.png){zoomable="yes"}

Kopiera din försignerade URL för den här bildfilen för nästa API-begäran till Firefly.

![Azure Storage](./images/az22.png){zoomable="yes"}

Gå tillbaka i Postman och öppna begäran **POST - Firefly - T2I (styleref) V3**.
Detta visas i **Brödtext**.

![Azure Storage](./images/az23.png){zoomable="yes"}

Ersätt platshållarens URL med den försignerade URL:en för bildfilen och välj **Skicka**.

![Azure Storage](./images/az24.png){zoomable="yes"}

Öppna Firefly Services nya bild i webbläsaren.

![Azure Storage](./images/az25.png){zoomable="yes"}

En annan bild visas med `horses in a field`, men den här gången liknar stilen den bildfil som du angav som stilreferens.

![Azure Storage](./images/az26.png){zoomable="yes"}

## 1.1.2.5 Programmatisk filöverföring

Om du vill använda programmatisk filöverföring med Azure Storage-konton måste du skapa en ny **SAS**-token (Shared Access Signature) med behörighet att skriva en fil.

Högerklicka på din behållare i Azure Storage Explorer och välj **Hämta signatur för delad åtkomst**.

![Azure Storage](./images/az27.png){zoomable="yes"}

Välj följande nödvändiga behörigheter under **Behörigheter**:

- **Läs**
- **Lägg till**
- **Skapa**
- **Skriv**
- **Lista**

Välj **Skapa**.

![Azure Storage](./images/az28.png){zoomable="yes"}

När du har tagit emot din **SAS-token** väljer du **Kopiera**.

![Azure Storage](./images/az29.png){zoomable="yes"}

Använd **SAS-token** för att överföra en fil till ditt Azure Storage-konto.

Gå tillbaka till Postman, markera mappen **FF - Firefly Services Tech Insiders**, markera **..** i mappen **Firefly** och välj sedan **Lägg till begäran**.

![Azure Storage](./images/az30.png){zoomable="yes"}

Ändra namnet på den tomma begäran till **Överför fil till Azure Storage-konto**, ändra **begärantyp** till **PUT** och klistra in SAS-token-URL:en i URL-avsnittet och välj sedan **Brödtext**.

![Azure Storage](./images/az31.png){zoomable="yes"}

Välj sedan en fil från den lokala datorn eller använd en annan bildfil som finns [här](./images/gradient2-p.jpg){target="_blank"}.

![Övertoningsfil](./images/gradient2-p.jpg)

I **Brödtext** väljer du **binär**, sedan **Välj fil** och sedan **+ Ny fil från den lokala datorn**.

![Azure Storage](./images/az32.png){zoomable="yes"}

Välj önskad fil och välj **Öppna**.

![Azure Storage](./images/az33.png){zoomable="yes"}

Ange sedan filnamnet som ska användas i ditt Azure Storage-konto genom att placera markören framför frågetecknet **?** i URL:en så här:

![Azure Storage](./images/az34.png){zoomable="yes"}

URL:en ser för närvarande ut så här, men måste ändras.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

Ändra filnamnet till `gradient2-p.jpg` och ändra URL:en så att filnamnet inkluderas:

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Azure Storage](./images/az34a.png){zoomable="yes"}

Gå sedan till **Sidhuvuden** och lägg till en ny rubrik manuellt så här:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Azure Storage](./images/az35.png){zoomable="yes"}

Gå till **Auktorisering** och ange **Autentiseringstyp** till **Ingen autentisering** och välj **Skicka**.

![Azure Storage](./images/az36.png){zoomable="yes"}

Därefter visas det tomma svaret i Postman, vilket innebär att filöverföringen är bra.

![Azure Storage](./images/az37.png){zoomable="yes"}

I Azure Storage Explorer uppdateras innehållet i din mapp och den nyligen överförda filen visas.

![Azure Storage](./images/az38.png){zoomable="yes"}

## 1.1.2.6 Programmatisk filanvändning

Om du vill läsa filer från Azure Storage-konton programmatiskt på lång sikt måste du skapa en ny **SAS**-token (Shared Access Signature) med behörighet att läsa en fil. Tekniskt sett kan du använda den SAS-token som skapades i föregående övning, men det är bäst att ha en separat token med bara **läsbehörighet** och en separat token med endast **skrivbehörighet**.

### Långsiktig Läs SAS-token

Gå tillbaka till Azure Storage Explorer, högerklicka på din behållare och välj sedan **Hämta signatur för delad åtkomst**.

![Azure Storage](./images/az27.png){zoomable="yes"}

Välj följande nödvändiga behörigheter under **Behörigheter**:

- **Läs**
- **Lista**

Ange **Förfallotid** till 1 år från och med nu.

Välj **Skapa**.

![Azure Storage](./images/az100.png){zoomable="yes"}

Kopiera URL:en och skriv ned den i en fil på datorn för att få din SAS-token med läsbehörighet.

![Azure Storage](./images/az101.png){zoomable="yes"}

URL:en ska se ut så här:

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

Du kan härleda ett par värden från ovanstående URL:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### Långsiktig Write SAS-token

Gå tillbaka till Azure Storage Explorer, högerklicka på din behållare och välj **Hämta signatur för delad åtkomst**.

![Azure Storage](./images/az27.png){zoomable="yes"}

Välj följande nödvändiga behörigheter under **Behörigheter**:

- **Läs**
- **Lista**
- **Lägg till**
- **Skapa**
- **Skriv**

Ange **Förfallotid** till 1 år från och med nu.

Välj **Skapa**.

![Azure Storage](./images/az102.png){zoomable="yes"}

Kopiera URL:en och skriv ned den i en fil på datorn för att få din SAS-token med läsbehörighet.

![Azure Storage](./images/az103.png){zoomable="yes"}

URL:en ska se ut så här:

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Du kan härleda ett par värden från ovanstående URL:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Variabler i Postman

Som du kan se i avsnittet ovan finns det några vanliga variabler i både läs- och skrivtoken.

Därefter måste du skapa variabler i Postman som lagrar de olika elementen i SAS-tokens ovan. Det finns vissa värden som är desamma i båda URL-adresserna:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

För framtida API-interaktioner är det viktigaste som ändras resursnamnet, medan variablerna ovan förblir desamma. I så fall är det bra att skapa variabler i Postman så att du inte behöver ange dem manuellt varje gång.

I Postman väljer du **Miljö**, öppnar **Alla variabler** och väljer **Miljö**.

![Azure Storage](./images/az104.png){zoomable="yes"}

Skapa dessa fyra variabler i tabellen som visas och ange dina specifika personliga värden för kolumnerna **Startvärde** och **Aktuellt värde**.

- `AZURE_STORAGE_URL`: din URL
- `AZURE_STORAGE_CONTAINER`: ditt behållarnamn
- `AZURE_STORAGE_SAS_READ`: din SAS-lästoken
- `AZURE_STORAGE_SAS_WRITE`: din SAS-skrivtoken

Välj **Spara**.

![Azure Storage](./images/az105.png){zoomable="yes"}

### Variabler i PostBuster

Som du kan se i avsnittet ovan finns det några vanliga variabler i både läs- och skrivtoken.

Därefter måste du skapa variabler i PostBuster som lagrar de olika elementen i SAS-tokens ovan. Det finns vissa värden som är desamma i båda URL-adresserna:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Öppna PostBuster. Välj **Basmiljö** och klicka sedan på ikonen **redigera** för att öppna basmiljön.

![Azure Storage](./images/pbbe1.png)

Därefter visas fyra tomma variabler. Ange din Azure Storage-kontoinformation här.

![Azure Storage](./images/pbbe2.png)

Basmiljöfilen bör nu se ut så här. Klicka på **Stäng**.

![Azure Storage](./images/pbbe3.png)

### Testa konfigurationen

I en av de föregående övningarna såg **Body** för din begäran **Firefly - T2I (styleref) V3** ut så här:

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![Azure Storage](./images/az24.png){zoomable="yes"}

Ändra URL:en till:

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

Välj **Skicka** för att testa ändringarna du gjort.

![Azure Storage](./images/az106.png){zoomable="yes"}

Om variablerna har konfigurerats korrekt returneras en bild-URL.

![Azure Storage](./images/az107.png){zoomable="yes"}

Öppna bildens URL för att verifiera bilden.

![Azure Storage](./images/az108.jpg)

## Nästa steg

Gå till [Arbeta med Photoshop API:er](./ex3.md){target="_blank"}

Gå tillbaka till [Översikt över Adobe Firefly Services](./firefly-services.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}