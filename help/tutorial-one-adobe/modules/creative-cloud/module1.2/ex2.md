---
title: Använda Adobe-API:er i Workfront Fusion
description: Lär dig hur du använder Adobe API:er i Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: e419f07dbef519d9cf2f0100878e4cc880ad5f94
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 0%

---

# Använda Adobe API:er i Workfront Fusion

Lär dig hur du använder Adobe API:er i Workfront Fusion.

## Använd Firefly-text till bild-API med Workfront Fusion

1. Håll pekaren över den andra **Ange flera variabler**-noden och välj **+** om du vill lägga till en annan modul.

![WF Fusion](./images/wffusion48.png)

1. Sök efter **http** och välj **HTTP**.

![WF Fusion](./images/wffusion49.png)

1. Välj **Gör en förfrågan**.

![WF Fusion](./images/wffusion50.png)

1. Välj dessa variabler:

- **URL**: `https://firefly-api.adobe.io/v3/images/generate`
- **Metod**: `POST`

1. Välj **Lägg till en rubrik**.

![WF Fusion](./images/wffusion51.png)

1. Ange följande rubriker:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `x-api-key` | din lagrade variabel för `CONST_client_id` |
| `Authorization` | `Bearer ` + din lagrade variabel för `bearer_token` |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

1. Ange information för `x-api-key`. Välj **Lägg till**.

![WF Fusion](./images/wffusion52.png)

1. Välj **Lägg till en rubrik**.

![WF Fusion](./images/wffusion53.png)

1. Ange information för `Authorization`. Välj **Lägg till**.

![WF Fusion](./images/wffusion54.png)

1. Välj **Lägg till en rubrik**. Ange information för `Content-Type`. Välj **Lägg till**.

![WF Fusion](./images/wffusion541.png)

1. Välj **Lägg till en rubrik**. Ange information för `Accept`. Välj **Lägg till**.

![WF Fusion](./images/wffusion542.png)

1. Ange **Brödtyp** till **Raw**. För **innehållstyp** väljer du **JSON (program/json)**.

![WF Fusion](./images/wffusion55.png)

1. Klistra in den här nyttolasten i fältet **Begär innehåll**.

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

1. Markera rutan för **Analysera svar**. Välj **OK**.

![WF Fusion](./images/wffusion56.png)

1. Välj **Kör en gång**.

![WF Fusion](./images/wffusion57.png)

Skärmen bör se ut så här.

![WF Fusion](./images/wffusion58.png)

1. Välj **?** på den fjärde noden, HTTP, för att se svaret. Du bör se en bildfil i svaret.

![WF Fusion](./images/wffusion59.png)

1. Kopiera bild-URL:en och öppna den i ett webbläsarfönster. Skärmen bör se ut så här:

![WF Fusion](./images/wffusion60.png)

1. Högerklicka på **HTTP** och byt namn till **Firefly T2I**.

![WF Fusion](./images/wffusion62.png)

1. Välj **Spara** om du vill spara ändringarna.

![WF Fusion](./images/wffusion61.png)

## Använda Photoshop API med Workfront Fusion

1. Välj **skiftnyckel** mellan noderna **Ange stödtoken** och **Firefly T2I**. Välj **Lägg till en router**.

![WF Fusion](./images/wffusion63.png)

1. Högerklicka på **Firefly T2I**-objektet och välj **Klona**.

![WF Fusion](./images/wffusion64.png)

1. Dra och släpp det klonade objektet nära **Router** -objektet. Det ansluter automatiskt till **Router**. Skärmen bör se ut så här:

![WF Fusion](./images/wffusion65.png)

Du har nu en identisk kopia baserad på HTTP-begäran **Firefly T2I**. Vissa av inställningarna för HTTP-begäran **Firefly T2I** liknar de som du behöver för att interagera med **Photoshop API** som är en tidsbesparande funktion. Nu behöver du bara ändra variablerna som inte är desamma, som begärande-URL:en och nyttolasten.

1. Ändra **URL** till `https://image.adobe.io/pie/psdService/text`.

![WF Fusion](./images/wffusion66.png)

1. Ersätt **Begär innehåll** med nyttolasten nedan:

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-button-text",
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
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
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

1. Gå tillbaka till din första nod, välj **Initiera konstanter** och välj sedan **Lägg till objekt** för var och en av dessa variabler.

![WF Fusion](./images/wffusion69.png)

| Nyckel | Exempelvärde |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

Du kan hitta dina variabler genom att gå tillbaka till Postman och öppna dina **miljövariabler**.

![Azure Storage](./../module1.1/images/az105.png)

1. Kopiera dessa värden till Workfront Fusion och lägg till ett nytt objekt för var och en av dessa fyra variabler.

1. Skärmen bör se ut så här. Välj **OK**.

![WF Fusion](./images/wffusion68.png)

Gå sedan tillbaka till den klonade HTTP-begäran för att uppdatera **Request-innehållet**. Observera de svarta variablerna i **Request content**, som är de variabler du kopierade över från Postman. Du måste ändra variablerna som du just definierade i Workfront Fusion. Ersätt varje variabel en i taget genom att ta bort den svarta texten och ersätta den med rätt variabel.

![WF Fusion](./images/wffusion70.png)

1. Gör dessa 3 ändringar i avsnittet **input**. Välj **OK**.

![WF Fusion](./images/wffusion71.png)

1. Gör dessa 3 ändringar i avsnittet **output**. Välj **OK**.

![WF Fusion](./images/wffusion72.png)

1. Högerklicka på den klonade noden och välj **Byt namn**. Ändra namnet till **Photoshop Change Text**.

![WF Fusion](./images/wffusion73.png)

Skärmen bör se ut så här:

![WF Fusion](./images/wffusion74.png)

1. Välj **Kör en gång**.

![WF Fusion](./images/wffusion75.png)

1. Markera ikonen **sök** på noden **Photoshop Change Text** för att visa svaret. Du bör ha ett svar som ser ut så här, med en länk till en statusfil.

![WF Fusion](./images/wffusion76.png)

1. Innan du fortsätter med Photoshop API-interaktionen inaktiverar du vägen till **Firefly T2I** -noden så att inga API-anrop skickas till API-slutpunkten som inte behövs. Markera ikonen **skiftnyckel** och välj sedan **Inaktivera flöde**.

![WF Fusion](./images/wffusion77.png)

Skärmen bör se ut så här:

![WF Fusion](./images/wffusion78.png)

1. Lägg sedan till en annan **Set multiple variables**-nod.

![WF Fusion](./images/wffusion79.png)

1. Placera den efter noden **Photoshop Change Text** .

![WF Fusion](./images/wffusion80.png)

1. Markera noden **Ange flera variabler** och välj **Lägg till objekt**. Välj variabelvärdet från svaret på föregående begäran.

| Variabelnamn | Variabelvärde |
|:-------------:| :---------------:| 
| `psdStatusUrl` | `data > _links > self > href` |

1. Välj **Lägg till**.

![WF Fusion](./images/wffusion81.png)

1. Välj **OK**.

![WF Fusion](./images/wffusion82.png)

1. Högerklicka på noden **Photoshop Change Text** och välj **Clone**.

![WF Fusion](./images/wffusion83.png)

1. Dra den klonade HTTP-begäran efter noden **Ange flera variabler** som du just skapade.

![WF Fusion](./images/wffusion83.png)

1. Högerklicka på den klonade HTTP-begäran, välj **Byt namn** och ändra namnet till **Photoshop Check Status**.

![WF Fusion](./images/wffusion84.png)

1. Välj att öppna HTTP-begäran. Ändra URL-adressen så att den refererar till variabeln som du skapade i föregående steg och ange **Method** till **GET**.

![WF Fusion](./images/wffusion85.png)

1. Ta bort **brödtexten** genom att markera det tomma alternativet.

![WF Fusion](./images/wffusion86.png)

1. Välj **OK**.

![WF Fusion](./images/wffusion87.png)

1. Välj **Kör en gång**.

![WF Fusion](./images/wffusion88.png)

Ett svar som innehåller fältet **status** med statusen **running** visas. Det tar några sekunder för Photoshop att slutföra processen.

![WF Fusion](./images/wffusion89.png)

Nu när du vet att svaret behöver lite mer tid att slutföra, kan det vara en bra idé att lägga till en timer framför denna HTTP-begäran så att den inte körs omedelbart.

1. Markera noden **Verktyg** och välj sedan **Strömsparläge**.

![WF Fusion](./images/wffusion90.png)

1. Placera noden **Strömsparläge** mellan **Ange flera variabler** och **Photoshop Check Status**. Ange **Fördröjning** till **5** sekunder. Välj **OK**.

![WF Fusion](./images/wffusion91.png)

Skärmen bör se ut så här. Utmaningen med konfigurationen nedan är att 5 sekunders väntan kan vara tillräckligt, men det kanske inte räcker. I verkligheten är det bättre att ha en mer intelligent lösning som en do.. while-slinga som kontrollerar statusen var femte sekund tills statusen är lika med **Succas**. Så du kan implementera en sådan taktik i nästa steg.

![WF Fusion](./images/wffusion92.png)

1. Välj ikonen **skiftnyckel** mellan **Ange flera variabler** och **viloläge**. Välj **Lägg till modul**.

![WF Fusion](./images/wffusion93.png)

1. Sök efter `flow` och välj sedan **Flödeskontroll**.

![WF Fusion](./images/wffusion94.png)

1. Välj **Upprepare**.

![WF Fusion](./images/wffusion95.png)

1. Ange **Upprepningar** till **20**. Välj **OK**.

![WF Fusion](./images/wffusion96.png)

1. Välj sedan **+** på **Photoshop Check Status** för att lägga till en annan modul.

![WF Fusion](./images/wffusion97.png)

1. Sök efter **flow** och välj **Flow Control**.

![WF Fusion](./images/wffusion98.png)

1. Välj **Matrisaggregering**.

![WF Fusion](./images/wffusion99.png)

1. Ange **Source Module** som **Repeater**. Välj **OK**.

![WF Fusion](./images/wffusion100.png)

Skärmen bör se ut så här:

![WF Fusion](./images/wffusion101.png)

1. Markera ikonen **skiftnyckel** och välj **Lägg till modul**.

![WF Fusion](./images/wffusion102.png)

1. Sök efter **verktyg** och välj **Verktyg**.

![WF Fusion](./images/wffusion103.png)

1. Välj **Hämta flera variabler**.

![WF Fusion](./images/wffusion104.png)

1. Välj **+ Lägg till objekt** och ange **variabelnamnet** till `done`.

![WF Fusion](./images/wffusion105.png)

1. Välj **OK**.

![WF Fusion](./images/wffusion106.png)

1. Markera noden **Ange flera variabler** som du konfigurerade tidigare. För att kunna initiera variabeln **klar** måste du ange den till `false` här. Välj **+ Lägg till objekt**.

![WF Fusion](./images/wffusion107.png)

1. Använd `done` som **variabelnamn**

1. Ett booleskt värde krävs för att ställa in status. Om du vill hitta det booleska värdet väljer du **kugghjulet** och sedan `false`. Välj **Lägg till**.

![WF Fusion](./images/wffusion108.png)

1. Välj **OK**.

![WF Fusion](./images/wffusion109.png)

1. Välj sedan ikonen **wrench** efter noden **Hämta flera variabler** som du konfigurerade.

![WF Fusion](./images/wffusion110.png)

1. Välj **Konfigurera ett filter**. Du måste nu kontrollera värdet för variabeln **klar**. Om värdet är **false** måste nästa del av slingan köras. Om värdet är **true** betyder det att processen redan har slutförts, så du behöver inte fortsätta med nästa del av slingan.

![WF Fusion](./images/wffusion111.png)

1. Använd **Är vi klara för etiketten?**. Ange **Villkor** med den redan befintliga variabeln **made**, ange operatorn till **Lika med** och värdet ska vara den booleska variabeln `false`. Välj **OK**.

![WF Fusion](./images/wffusion112.png)

1. Sedan kan du skapa utrymme mellan noderna **Photoshop Check Status** och **Array aggregator**. Välj sedan ikonen **skiftnyckel** och välj **Lägg till en router**. Du gör detta eftersom det ska finnas två sökvägar när du har kontrollerat Photoshop-filens status. Om statusen är `succeeded` ska variabeln **done** anges till `true`. Om statusen inte är lika med `succeeded` ska slingan fortsätta. Routern gör det möjligt att kontrollera och ställa in detta.

![WF Fusion](./images/wffusion113.png)

1. När du har lagt till routern markerar du ikonen **skiftnyckel** och väljer **Konfigurera ett filter**.

![WF Fusion](./images/wffusion114.png)

1. Använd **Vi är klara** för etiketten. Ange **Villkor** med svaret från noden **Photoshop Check Status** genom att välja svarsfältet **data.outputs[].status**, operatorn ska vara **Lika med** och värdet ska vara `succeeded`. Välj **OK**.

![WF Fusion](./images/wffusion115.png)

1. Markera sedan den tomma noden med frågetecknet och sök efter **verktyg**. Välj sedan **Verktyg**.

![WF Fusion](./images/wffusion116.png)

1. Välj **Ange flera variabler**.

![WF Fusion](./images/wffusion117.png)

1. När den här grenen av routern används betyder det att Photoshop-filen har skapats utan fel. Det innebär att do.. while-slingan inte längre behöver fortsätta att kontrollera statusen i Photoshop, så du bör ange variabeln `done` till `true`.

1. Använd `done` för **variabelnamnet**.

1. För **variabelvärdet** bör du använda det booleska värdet `true`. Markera ikonen **kugghjulet** och välj sedan `true`. Välj **Lägg till**.

![WF Fusion](./images/wffusion118.png)

1. Välj **OK**.

![WF Fusion](./images/wffusion119.png)

1. Högerklicka sedan på noden **Ange flera variabler** som du nyss skapade och välj **Klona**.

![WF Fusion](./images/wffusion120.png)

1. Dra den klonade noden så att den ansluter till **arrayaggregatorn**. Högerklicka sedan på noden, välj **Byt namn** och ändra namnet till `Placeholder End`.

![WF Fusion](./images/wffusion122.png)

1. Ta bort den befintliga variabeln och välj **+ Lägg till objekt**. Använd `placeholder` för **variabelvärdet** för **använd `end`.** Välj **Lägg till** och välj sedan **OK**.

![WF Fusion](./images/wffusion123.png)

1. Välj **Spara** om du vill spara ditt scenario. Nästa, välj   **Kör en gång**.

![WF Fusion](./images/wffusion124.png)

Scenariot körs sedan och bör avslutas. Observera att do.. while-slingan som du konfigurerade fungerar bra. I körningen nedan ser du att **Repeater** kördes 20 gånger baserat på bubblan på noden **Verktyg > Hämta flera variabler** . Efter den noden konfigurerade du ett filter som kontrollerade statusen och bara om statusen inte var lika med **Success** kördes nästa nod. I den här körningen kördes delen efter filtret endast en gång eftersom statusen redan var **Successed** i den första körningen.

![WF Fusion](./images/wffusion125.png)

1. Du kan kontrollera status för skapandet av din nya Photoshop-fil genom att klicka på bubblan i HTTP-begäran **Photoshop Check Status** och gå ned till fältet **status**.

![WF Fusion](./images/wffusion126.png)

Du har nu konfigurerat den grundläggande versionen av ett repeterbart scenario som automatiserar ett antal steg. I nästa övning kommer du att fortsätta med det genom att öka komplexiteten.

## Nästa steg

Gå till [Processautomatisering med Workfront Fusion](./ex3.md){target="_blank"}

Gå tillbaka till [Automatiserar Adobe Firefly-tjänster](./automation.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
