---
title: Komma igång med Firefly Services
description: Komma igång med Firefly Services
kt: 5342
doc-type: tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: c5d015fee3650d9c5a154f0b1374d27b20d2ea42
workflow-type: tm+mt
source-wordcount: '1759'
ht-degree: 0%

---

# 1.2.2 Använda Adobe-API:er i Workfront Fusion

## 1.2.2.1 Använda Firefly-text till bild-API med Workfront Fusion

Håll pekaren över den andra **Ange flera variabler**-noden och klicka på **+** för att lägga till en annan modul.

![WF Fusion](./images/wffusion48.png)

Sök efter **http** och välj sedan **HTTP**.

![WF Fusion](./images/wffusion49.png)

Välj **Gör en förfrågan**.

![WF Fusion](./images/wffusion50.png)

Välj dessa variabler:

- **URL**: `https://firefly-api.adobe.io/v3/images/generate`
- **Metod**: `POST`

Klicka på **Lägg till en rubrik**.

![WF Fusion](./images/wffusion51.png)

Du måste ange följande rubriker:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `x-api-key` | din lagrade variabel för `CONST_client_id` |
| `Authorization` | `Bearer ` + din lagrade variabel för `bearer_token` |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

Ange information för `x-api-key`. Klicka på **Lägg till**.

![WF Fusion](./images/wffusion52.png)

Klicka på **Lägg till en rubrik**.

![WF Fusion](./images/wffusion53.png)

Ange information för `Authorization`. Klicka på **Lägg till**.

![WF Fusion](./images/wffusion54.png)

Klicka på **Lägg till en rubrik**. Ange information för `Content-Type`. Klicka på **Lägg till**.

![WF Fusion](./images/wffusion541.png)

Klicka på **Lägg till en rubrik**. Ange information för `Accept`. Klicka på **Lägg till**.

![WF Fusion](./images/wffusion542.png)

Ange **Brödtyp** till **Raw**. För **innehållstyp** väljer du **JSON (program/json)**.

![WF Fusion](./images/wffusion55.png)

Klistra in den här nyttolasten i fältet **Begär innehåll**.

```json
{
  "numVariations": 1,
  "size": {
    "width": 2048,
    "height": 2048
  },
  "prompt": "Horses in a field",
  "promptBiasingLocaleCode": "en-US"
}
```

Markera kryssrutan för **Analysera svar**. Klicka på **OK**.

![WF Fusion](./images/wffusion56.png)

Klicka på **Kör en gång**.

![WF Fusion](./images/wffusion57.png)

När ditt scenario är klart bör du se det här.

![WF Fusion](./images/wffusion58.png)

Klicka på **?** på den fjärde noden, HTTP, för att se svaret. Du bör se en bildfil i svaret.

![WF Fusion](./images/wffusion59.png)

Kopiera bild-URL:en och öppna den i ett webbläsarfönster. Då ska du se något liknande:

![WF Fusion](./images/wffusion60.png)

Högerklicka på **HTTP**-objektet och byt namn på det till **Firefly T2I**.

![WF Fusion](./images/wffusion62.png)

Klicka på **Spara** för att spara ändringarna.

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2 Använda Photoshop API med Workfront Fusion

Klicka på ikonen **wrench** mellan noderna **Set Bearer Token** och **Firefly T2I**. Välj **Lägg till en router**.

![WF Fusion](./images/wffusion63.png)

Högerklicka på **Firefly T2I**-objektet och välj **Klona**.

![WF Fusion](./images/wffusion64.png)

Dra och släpp det klonade objektet nära **Router** -objektet så ansluts det automatiskt till **Router**. Du borde ha den här då.

![WF Fusion](./images/wffusion65.png)

Du har nu en identisk kopia baserad på HTTP-begäran **Firefly T2I**. Vissa av inställningarna för HTTP-begäran **Firefly T2I** liknar de som du behöver för att interagera med **Photoshop API** som är en tidsbesparande funktion. Nu behöver du bara ändra de variabler som inte är desamma, som begärande-URL:en och nyttolasten.

Ändra **URL** till `https://image.adobe.io/pie/psdService/text`.

![WF Fusion](./images/wffusion66.png)

Ersätt **Begär innehåll** med nyttolasten nedan:

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-button",
        "text": {
          "content": "Click here"
        }
      },
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Buy this stuff"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

![WF Fusion](./images/wffusion67.png)

För att **Request-innehållet** ska fungera korrekt saknas vissa variabler:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Gå tillbaka till din första nod, klicka på **Initiera konstanter** och välj sedan **Lägg till objekt** för var och en av dessa variabler.

![WF Fusion](./images/wffusion69.png)

| Nyckel | Exempelvärde |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

Du kan hitta dina variabler genom att gå tillbaka till Postman och öppna dina **miljövariabler**.

![Azure Storage](./../module1.1/images/az105.png)

Kopiera dessa värden till Workfront Fusion och lägg till ett nytt objekt för var och en av dessa fyra variabler.

Du borde ha den här då. Klicka på **OK**.

![WF Fusion](./images/wffusion68.png)

Gå sedan tillbaka till den klonade HTTP-begäran för att uppdatera **Request-innehållet**. Du kommer att lägga märke till de här svarta variablerna i **Request content** , som är de variabler som du kopierade över från Postman. Du måste nu ändra dessa variabler till de variabler du just definierade i Workfront Fusion. Ersätt varje variabel en i taget genom att ta bort den svarta texten och ersätta den med rätt variabel.

![WF Fusion](./images/wffusion70.png)

Det finns tre ändringar att göra i avsnittet **input**.

![WF Fusion](./images/wffusion71.png)

Det finns också tre ändringar att göra i avsnittet **output**. Klicka på **OK**.

![WF Fusion](./images/wffusion72.png)

Högerklicka på den klonade noden och välj **Byt namn**. Ändra namnet till **Photoshop Change Text**.

![WF Fusion](./images/wffusion73.png)

Du borde ha den här då.

![WF Fusion](./images/wffusion74.png)

Klicka på **Kör en gång**.

![WF Fusion](./images/wffusion75.png)

Klicka på ikonen **sök** på noden **Photoshop Change Text** för att visa svaret. Du bör ha ett svar som ser ut så här, med en länk till en statusfil.

![WF Fusion](./images/wffusion76.png)

Innan du fortsätter med Photoshop API-interaktionen kan vi inaktivera vägen till **Firefly T2I** -noden så att vi inte skickar onödiga API-anrop till den API-slutpunkten. Klicka på ikonen **skiftnyckel** och välj sedan **Inaktivera flöde**.

![WF Fusion](./images/wffusion77.png)

Du borde ha den här då.

![WF Fusion](./images/wffusion78.png)

Lägg sedan till en annan **Set multiple variables**-nod.

![WF Fusion](./images/wffusion79.png)

Placera den efter noden **Photoshop Change Text** .

![WF Fusion](./images/wffusion80.png)

Klicka på noden **Ange flera variabler** och välj **Lägg till objekt**. Välj variabelvärdet från svaret på föregående begäran.

| Variabelnamn | Variabelvärde |
|:-------------:| :---------------:| 
| `psdStatusUrl` | `data > _links > self > href` |

Klicka på **Lägg till**.

![WF Fusion](./images/wffusion81.png)

Klicka på **OK**.

![WF Fusion](./images/wffusion82.png)

Högerklicka på noden **Photoshop Change Text** och välj **Clone**.

![WF Fusion](./images/wffusion83.png)

Dra den klonade HTTP-begäran efter noden **Ange flera variabler** som du just skapade.

![WF Fusion](./images/wffusion83.png)

Högerklicka på den klonade HTTP-begäran, välj **Byt namn** och ändra namnet till **Photoshop Check Status**.

![WF Fusion](./images/wffusion84.png)

Klicka för att öppna HTTP-begäran. Ändra URL-adressen så att den refererar till variabeln som du skapade i föregående steg och ange **Method** till **GET**.

![WF Fusion](./images/wffusion85.png)

Ta bort **brödtexten** genom att markera det tomma alternativet.

![WF Fusion](./images/wffusion86.png)

Klicka på **OK**.

![WF Fusion](./images/wffusion87.png)

Klicka på **Kör en gång**.

![WF Fusion](./images/wffusion88.png)

Du bör sedan få ett svar som innehåller fältet **status** med statusen **running**. Det tar några sekunder för Photoshop att slutföra processen.

![WF Fusion](./images/wffusion89.png)

Nu när du vet att svaret behöver lite mer tid att slutföra, kan det vara en bra idé att lägga till en timer framför denna HTTP-begäran så att den inte körs omedelbart.

Klicka på noden **Verktyg** och välj sedan **Strömsparläge**.

![WF Fusion](./images/wffusion90.png)

Placera noden **Strömsparläge** mellan **Ange flera variabler** och **Photoshop Check Status**. Ange **Fördröjning** till **5** sekunder. Klicka på **OK**.

![WF Fusion](./images/wffusion91.png)

Du får den här då. Utmaningen med konfigurationen nedan är att 5 sekunders väntan kan vara tillräckligt, men det kanske inte räcker. I verkligheten är det bättre att ha en mer intelligent lösning som en do.. while-slinga som kontrollerar statusen var femte sekund tills statusen är lika med **Succas**. Du kommer nu att implementera en sådan taktik i nästa steg.

![WF Fusion](./images/wffusion92.png)

Klicka på ikonen **skiftnyckel** mellan **Ange flera variabler** och **viloläge**. Välj **Lägg till modul**.

![WF Fusion](./images/wffusion93.png)

Sök efter `flow` och välj sedan **Flödeskontroll**.

![WF Fusion](./images/wffusion94.png)

Välj **Upprepare**.

![WF Fusion](./images/wffusion95.png)

Ange **Upprepningar** till **20**. Klicka på **OK**.

![WF Fusion](./images/wffusion96.png)

Klicka sedan på **+** på **Photoshop Check Status** för att lägga till en annan modul.

![WF Fusion](./images/wffusion97.png)

Sök efter **flow** och välj **Flow Control**.

![WF Fusion](./images/wffusion98.png)

Välj **Matrisaggregering**.

![WF Fusion](./images/wffusion99.png)

Ange **Source Module** som **Repeater**. CLick **OK**.

![WF Fusion](./images/wffusion100.png)

Du bör då ha den här:

![WF Fusion](./images/wffusion101.png)

Klicka på ikonen **skiftnyckel** och välj **Lägg till modul**.

![WF Fusion](./images/wffusion102.png)

Sök efter **verktyg** och välj **Verktyg**.

![WF Fusion](./images/wffusion103.png)

Välj **Hämta flera variabler**.

![WF Fusion](./images/wffusion104.png)

Klicka på **+ Lägg till objekt** och ange **variabelnamnet** till `done`.

![WF Fusion](./images/wffusion105.png)

Klicka på **OK**.

![WF Fusion](./images/wffusion106.png)

Klicka på noden **Ange flera variabler** som du konfigurerade tidigare. För att kunna initiera variabeln **klar** måste du ange den till `false` här. Klicka på **+ Lägg till objekt**.

![WF Fusion](./images/wffusion107.png)

Använd `done` för **variabelnamnet**. Ett booleskt värde krävs för att ställa in status. Om du vill hitta det booleska värdet klickar du på **kugghjulsikonen** och väljer sedan `false`. Klicka på **Lägg till**.

![WF Fusion](./images/wffusion108.png)

Klicka på **OK**.

![WF Fusion](./images/wffusion109.png)

Klicka sedan på ikonen **wrench** efter noden **Hämta flera variabler** som du har konfigurerat.

![WF Fusion](./images/wffusion110.png)

Välj **Konfigurera ett filter**. Du måste nu kontrollera värdet för variabeln **klar**. Om värdet är **false** måste nästa del av slingan köras. Om värdet är **true** betyder det att processen redan har slutförts, så du behöver inte fortsätta med nästa del av slingan.

![WF Fusion](./images/wffusion111.png)

Använd **Är vi klara för etiketten?**. Ange **Villkor** med den redan befintliga variabeln **made**, ange operatorn till **Lika med** och värdet ska vara den booleska variabeln `false`. Klicka på **OK**.

![WF Fusion](./images/wffusion112.png)

Sedan kan du skapa utrymme mellan noderna **Photoshop Check Status** och **Array aggregator**. Klicka sedan på ikonen **skiftnyckel** och välj **Lägg till en router**. Du gör detta eftersom det ska finnas två sökvägar när du har kontrollerat Photoshop-filens status. Om statusen är `succeeded` ska variabeln **done** anges till `true`. Om statusen inte är lika med `succeeded` ska slingan fortsätta. Routern gör det möjligt att kontrollera och ställa in detta.

![WF Fusion](./images/wffusion113.png)

När du har lagt till routern klickar du på ikonen **skiftnyckel** och väljer **Konfigurera ett filter**.

![WF Fusion](./images/wffusion114.png)

Använd **Vi är klara** för etiketten. Ange **Villkor** med svaret från noden **Photoshop Check Status** genom att välja svarsfältet **data.outputs[].status**, operatorn ska vara **Lika med** och värdet ska vara `succeeded`. Klicka på **OK**.

![WF Fusion](./images/wffusion115.png)

Klicka sedan på den tomma noden med frågetecknet och sök efter **verktyg**. Välj sedan **Verktyg**.

![WF Fusion](./images/wffusion116.png)

Välj **Ange flera variabler**.

![WF Fusion](./images/wffusion117.png)

När den här grenen av routern används betyder det att Photoshop-filen har skapats utan fel. Det innebär att do.. while-slingan inte längre behöver fortsätta att kontrollera statusen i Photoshop, så du bör ange variabeln `done` till `true`.

Använd `done` för **variabelnamnet**. För **variabelvärdet** bör du använda det booleska värdet `true`. Klicka på **kugghjulsikonen** och välj sedan `true`. Klicka på **Lägg till**.

![WF Fusion](./images/wffusion118.png)

Klicka på **OK**.

![WF Fusion](./images/wffusion119.png)

Högerklicka sedan på noden **Ange flera variabler** som du nyss skapade och välj **Klona**.

![WF Fusion](./images/wffusion120.png)

Dra den klonade noden så att den ansluter till **arrayaggregatorn**. Högerklicka sedan på noden, välj **Byt namn** och ändra namnet till `Placeholder End`.

![WF Fusion](./images/wffusion122.png)

Ta bort den befintliga variabeln och klicka på **+ Lägg till objekt**. Använd `placeholder` för **variabelvärdet** för **använd `end`.** Klicka på **Lägg till** och sedan på **OK**.

![WF Fusion](./images/wffusion123.png)

Klicka på **Spara** för att spara ditt scenario. Klicka sedan på **Kör en gång**.

![WF Fusion](./images/wffusion124.png)

Scenariot kommer sedan att köras och slutföras. Du kommer att märka att do.. while-slingan som du konfigurerade fungerade bra. I körningen nedan ser du att **Repeater** kördes 20 gånger baserat på bubblan på noden **Verktyg > Hämta flera variabler** . Efter den noden konfigurerade du ett filter som kontrollerade statusen och bara om statusen inte var lika med **Success** kördes nästa nod. I den här körningen kördes delen efter filtret endast en gång eftersom statusen redan var **Successed** i den första körningen.

![WF Fusion](./images/wffusion125.png)

Du kan kontrollera status för skapandet av din nya Photoshop-fil genom att klicka på bubblan i HTTP-begäran **Photoshop Check Status** och gå ned till fältet **status**.

![WF Fusion](./images/wffusion126.png)

Du har nu konfigurerat den grundläggande versionen av ett repeterbart scenario som automatiserar ett antal steg. I nästa övning kommer du att fortsätta med det genom att öka komplexiteten.

Nästa steg: [1.2.3 Processautomatisering med Workfront Fusion](./ex3.md)

[Gå tillbaka till modul 1.2](./automation.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
