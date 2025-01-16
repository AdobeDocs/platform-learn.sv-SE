---
title: Processautomatisering med Workfront Fusion
description: Processautomatisering med Workfront Fusion
kt: 5342
doc-type: tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: a4933bd49988cd16c4382ad4327d01ae58b52bbb
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# 1.2.3 Processautomatisering med Workfront Fusion

Ditt scenario ser nu ut så här.

![WF Fusion](./images/wffusion200.png)

## 1.2.3.1 Iterera över flera värden

Hittills har du ändrat text i en Photoshop-fil med ett statiskt värde. Om du vill skala och automatisera arbetsflödena för att skapa innehåll måste du iterera över en lista med värden och infoga dessa värden dynamiskt i Photoshop-filen. I nästa steg ska du lägga till en funktion för att iterera över värden i ditt befintliga scenario.

Mellan noden **Router** och noden **Photoshop Change Text** klickar du på ikonen **wrench** och väljer **Lägg till en modul**.

![WF Fusion](./images/wffusion201.png)

Sök efter `flow` och välj **Flödeskontroll**.

![WF Fusion](./images/wffusion202.png)

Välj **Iterator**.

![WF Fusion](./images/wffusion203.png)

Du borde ha den här då.

![WF Fusion](./images/wffusion204.png)

Även om det går att läsa indatafiler som CSV-filer måste du för närvarande använda en grundläggande version av en CSV-fil genom att definiera en textsträng och dela upp textfilen.

Du kan hitta funktionen **split** genom att klicka på ikonen **T** , där du ser alla tillgängliga funktioner för att ändra textvärden. Klicka på funktionen **split** så ser du det här.

![WF Fusion](./images/wffusion206.png)

Delningsfunktionen förväntar sig en array med värden före semikolon och förväntar sig att du anger avgränsaren efter semikolon. För det här testet bör du använda en enkel array med två fält, **Köp nu** och **Klicka här**, och avgränsaren är **,**.

Ange detta i fältet **Array** genom att ersätta den för närvarande tomma funktionen **split**: `{{split("Buy now, Click here "; ",")}}`. Klicka på **OK**.

![WF Fusion](./images/wffusion205.png)

Din iterator är nu konfigurerad och om du kör ditt scenario nu kommer det att köras två gånger. Det finns dock fortfarande ett problem eftersom du använder statiska värden i noden **Photoshop Change Text** . Klicka på **Photoshop Change Text** om du vill lägga till vissa variabler i stället för statiska värden för in- och utdatafälten.

![WF Fusion](./images/wffusion207.png)

I **Request content** visas texten **Click here**. Den här texten måste ersättas med värden som kommer från arrayen.

![WF Fusion](./images/wffusion208.png)

Ta bort texten **Klicka här** och ersätt den genom att välja variabeln **Value** från noden **Intervator**. Då uppdateras texten på knappen i Photoshop-dokumentet dynamiskt.

![WF Fusion](./images/wffusion209.png)

Du måste också uppdatera filnamnet som används för att skriva filen i ditt Azure Storage-konto. Om filnamnet är statiskt skriver varje ny upprepning helt enkelt över den tidigare filen, och därför förlorar du de anpassade filerna. Det aktuella statiska filnamnet är **sevoi-psd-changed-text.psd** och du måste nu uppdatera det. Placera markören bakom ordet `text`.

![WF Fusion](./images/wffusion210.png)

Lägg först till ett bindestreck `-` och markera sedan värdet **Paketordningsposition**. Detta säkerställer att Workfront Fusion för första gången lägger till `-1` i filnamnet, för andra upprepningen `-2` och så vidare. Klicka på **OK**.

![WF Fusion](./images/wffusion211.png)

Spara ditt scenario och klicka sedan på **Kör en gång**.

![WF Fusion](./images/wffusion212.png)

När scenariot har körts går du tillbaka till Azure Storage Explorer och uppdaterar mappen. Du bör sedan se de två nyskapade filerna.

![WF Fusion](./images/wffusion213.png)

Hämta och öppna varje fil. Du bör då se de olika texterna på knapparna. Det här är filen `sevoi-psd-changed-text-1.psd`.

![WF Fusion](./images/wffusion214.png)

Det här är filen `sevoi-psd-changed-text-2.psd`.

![WF Fusion](./images/wffusion215.png)

## 1.2.3.2 Aktivera ditt scenario med en webkrok

Hittills har du kört ditt scenario manuellt för att testa. Nu uppdaterar vi ditt scenario med en webkrok, så att det kan aktiveras från en extern miljö.

Klicka på ikonen **+**, sök efter **webkrok** och välj sedan **Webhooks**.

![WF Fusion](./images/wffusion216.png)

Välj **Anpassad webkrok**.

Dra och anslut noden **Anpassad webkrok** så att den ansluter till den första noden på arbetsytan, som kallas **Initiera konstanter**.

![WF Fusion](./images/wffusion217.png)

Klicka på noden **Anpassad webkrok**. Klicka sedan på **Lägg till**.

![WF Fusion](./images/wffusion218.png)

Ange **Webkrok-namnet** till `--aepUserLdap-- - Tutorial 1.2`.

![WF Fusion](./images/wffusion219.png)

Markera kryssrutan för **Hämta begäranderubriker**. Klicka på **Spara**.

![WF Fusion](./images/wffusion220.png)

Din webkroks-URL är nu tillgänglig. Kopiera URL-adressen.

![WF Fusion](./images/wffusion221.png)

Öppna Postman och lägg till en ny mapp i samlingen **FF - Firefly Services Tech Insiders**.

![WF Fusion](./images/wffusion222.png)

Namnge mappen `--aepUserLdap-- - Workfront Fusion`.

![WF Fusion](./images/wffusion223.png)

Klicka på de tre punkterna **..** i mappen som du just skapade och välj **Lägg till begäran**.

![WF Fusion](./images/wffusion224.png)

Ange **Metodtypen** till **POST** och klistra in webbkrokens URL i adressfältet.

![WF Fusion](./images/wffusion225.png)

Du måste skicka en anpassad brödtext så att variabelelementen kan tillhandahållas från en extern källa till ditt Workfront Fusion-scenario. Gå till **Brödtext** och välj **Raw**.

![WF Fusion](./images/wffusion226.png)

Klistra in texten nedan i texten i din begäran. Klicka på **Skicka**.

```json
{
    "psdTemplate": "placeholder",
    "xlsFile": "placeholder"
}
```

![WF Fusion](./images/wffusion229.png)

Gå tillbaka till Workfront Fusion. Du kommer nu att se ett meddelande på din anpassade webkrok som säger: **Klart fastställt**.

![WF Fusion](./images/wffusion227.png)

Klicka på **Spara** och sedan på **Kör en gång**. Scenariot kommer nu att vara aktivt men kan inte köras förrän du klickar på **Skicka** igen i Postman.

![WF Fusion](./images/wffusion230.png)

Gå till Postman och klicka på **Skicka** igen.

![WF Fusion](./images/wffusion228.png)

Scenariot körs sedan igen och de två filerna skapas precis som förut.

![WF Fusion](./images/wffusion232.png)

Äntligen ändrar du namnet på din Postman-begäran till `POST - Send Request to Workfront Fusion Webhook`.

![WF Fusion](./images/wffusion233.png)

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 1.2](./automation.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
