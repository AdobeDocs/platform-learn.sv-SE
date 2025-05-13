---
title: Frame.io och Workfront Fusion
description: Frame.io och Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 37de6ceb-833e-4e75-9201-88bddd38a817
source-git-commit: da6917ec8c4e863e80eef91280e46b20816a5426
workflow-type: tm+mt
source-wordcount: '2674'
ht-degree: 0%

---

# 1.2.5 Frame.io och Workfront Fusion

I den föregående övningen konfigurerade du scenariot `--aepUserLdap-- - Firefly + Photoshop` och konfigurerade en inkommande webkrok för att utlösa scenariot och ett webkrossvar när scenariot slutfördes. Sedan använde du Postman för att utlösa det scenariot. Postman är ett bra verktyg för testning, men i ett verkligt affärsscenario skulle företagsanvändare inte använda Postman för att utlösa ett scenario. De använder istället ett annat program och förväntar sig att ett annat program ska aktivera ett scenario i Workfront Fusion. I den här övningen är det precis vad du kommer att göra med Frame.io.

>[!NOTE]
>
>För att kunna slutföra den här övningen måste du vara en administratör i ditt Frame.io-konto. Nedanstående övning skapades för Frame.io V3 och kommer att uppdateras i ett senare skede för Frame.io V4.

## 1.2.5.1 använder Frame.io

Gå till [https://app.frame.io/projects](https://app.frame.io/projects){target="_blank"}.

Klicka på ikonen **+** för att skapa ett eget projekt i Frame.io.

![Bildruta-I/O](./images/frame1.png)

Ange namnet `--aepUserLdap--` och klicka på **Skapa projekt**.

![Bildruta-I/O](./images/frame2.png)

Sedan visas ditt projekt i den vänstra menyn.
I en av de tidigare övningarna laddade du ned [citisign-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} till skrivbordet. Markera filen och dra den sedan till den projektmapp som skapades.

![Bildruta-I/O](./images/frame3.png)

## 1.2.5.2 Workfront Fusion och Frame.io

I den föregående övningen skapade du scenariot `--aepUserLdap-- - Firefly + Photoshop`, som började med en anpassad webkrok och som slutade med ett webkrossvar. Användningen av webbhookar testades sedan med Postman, men självklart ska poängen med ett sådant scenario anropas av ett externt program. Som tidigare nämnts är Frame.io den övningen, men mellan Frame.io och `--aepUserLdap-- - Firefly + Photoshop` behövs ett annat Workfront Fusion-scenario. du kommer nu att konfigurera det scenariot.

Gå till [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Öppna **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Gå till **Scenarier** på den vänstra menyn och markera mappen `--aepUserLdap--`. Klicka på **Skapa ett nytt scenario**.

![Bildruta-I/O](./images/frame4.png)

Använd namnet `--aepUserLdap-- - Frame IO Custom Action`.

![Bildruta-I/O](./images/frame5.png)

Klicka på **frågeteckenobjektet** på arbetsytan. Ange texten `webhook` i sökrutan och klicka på **Webhooks**.

![Bildruta-I/O](./images/frame6.png)

Klicka på **Anpassad webkrok**.

![Bildruta-I/O](./images/frame7.png)

Klicka på **Lägg till** för att skapa en ny webkrok-URL.

![Bildruta-I/O](./images/frame8.png)

Använd `--aepUserLdap-- - Frame IO Custom Action Webhook` för **Webkrok-namnet**. Klicka på **Spara**.

![Bildruta-I/O](./images/frame9.png)

Du borde se det här då. Lämna den här skärmen öppen och orörd så som du behöver den i nästa steg. Du måste kopiera webboks-URL:en i ett nästa steg genom att klicka på **Kopiera adress till Urklipp**.

![Bildruta-I/O](./images/frame10.png)

Gå till [https://developer.frame.io/](https://developer.frame.io/){target="_blank"}. Klicka på **UTVECKLINGSVERKTYG** och välj sedan **Anpassade åtgärder**.

![Bildruta-I/O](./images/frame11.png)

Klicka på **Skapa en anpassad åtgärd**.

![Bildruta-I/O](./images/frame12.png)

Ange följande värden:

- **NAME**: använd `--aepUserLdap-- - Frame IO Custom Action Fusion`
- **BESKRIVNING**: använd `--aepUserLdap-- - Frame IO Custom Action Fusion`
- **EVENT**: använd `fusion.tutorial`.
- **URL**: Ange URL:en för den webkrok som du nyss skapade i Workfront Fusion
- **TEAM**: välj lämpligt Frame.io-team, i det här fallet **One Adobe Tutorial**.

Klicka på **Skicka**.

![Bildruta-I/O](./images/frame15.png)

Du borde se det här då.

![Bildruta-I/O](./images/frame14.png)

Gå tillbaka till [https://app.frame.io/projects](https://app.frame.io/projects){target="_blank"}. Uppdatera sidan.

![Bildruta-I/O](./images/frame16.png)

När du har uppdaterat sidan klickar du på de 3 punkterna **..** på resursen **citisign-fiber.psd**. Du bör sedan se den anpassade åtgärd som du skapade tidigare visas på den meny som visas. Klicka på den anpassade åtgärden `--aepUserLdap-- - Frame IO Custom Action Fusion`.

![Bildruta-I/O](./images/frame17.png)

Du bör då se en liknande **Success!**-popup. Detta popup-fönster är resultatet av kommunikationen mellan Frame.io och Workfront Fusion.

![Bildruta-I/O](./images/frame18.png)

Ändra tillbaka skärmen till Workfront Fusion. Du bör nu se **Klart fastställt** visas på det anpassade webkrobobjektet. Klicka på **OK**.

![Bildruta-I/O](./images/frame19.png)

Klicka på **Kör en gång** för att aktivera testläget och testa kommunikationen med Frame.io igen.

![Bildruta-I/O](./images/frame20.png)

Gå tillbaka till Frame.io och klicka på den anpassade åtgärden `--aepUserLdap-- - Frame IO Custom Action Fusion` igen.

![Bildruta-I/O](./images/frame21.png)

Växla tillbaka till Workfront Fusion. Du bör nu se en grön bockmarkering och en bubbla som visar **1**. Klicka på bubblan för att se informationen.

![Bildruta-I/O](./images/frame22.png)

Detaljerad vy av bubblan visar data som tagits emot från Frame.io. Du bör se olika ID:n. Fältet **resource.id** visar till exempel det unika ID:t i Frame.io för resursen **citisign-fiber.psd**.

![Bildruta-I/O](./images/frame23.png)

Nu när kommunikationen mellan Frame.io och Workfront Fusion har upprättats kan du fortsätta med konfigurationen.

## 1.2.5.3 Tillhandahåller ett anpassat formulärsvar till Frame.io

När den anpassade åtgärden anropas i Frame.io förväntar sig Frame.io att få ett svar från Workfront Fusion. Om du tänker tillbaka till det scenario du skapade i den tidigare övningen behövs ett antal variabler för att uppdatera Photoshop PSD-standardfilen. Variablerna definieras i nyttolasten som du använde:

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

För att scenariot `--aepUserLdap-- - Firefly + Photoshop` ska kunna köras krävs fält som **prompt**, **cta**, **button** och **psdTemplate**.

De första tre fälten, **prompt**, **cta**, **button**, kräver användarindata som måste samlas in i Frame.io när användaren anropar den anpassade åtgärden. Det första som behöver göras i Workfront Fusion är alltså att kontrollera om variablerna är tillgängliga eller inte och i annat fall bör Workfront Fusion svara Frame.io och begära att variablerna ska anges. Det gör man genom att använda ett formulär i Frame.io.

Gå tillbaka till Workfront Fusion och öppna ditt scenario `--aepUserLdap-- - Frame IO Custom Action`. Håll pekaren över det **anpassade webkrokobjektet** och klicka på ikonen **+** för att lägga till en annan modul.

![Bildruta-I/O](./images/frame24.png)

Sök efter `Flow Control` och klicka på **Flödeskontroll**.

![Bildruta-I/O](./images/frame25.png)

Klicka för att välja **Router**.

![Bildruta-I/O](./images/frame26.png)

Du borde se det här då.

![Bildruta-I/O](./images/frame27.png)

Klicka på **?** objekt och klicka sedan för att välja **Webhooks**.

![Bildruta-I/O](./images/frame28.png)

Välj **Webkrok-svar**.

![Bildruta-I/O](./images/frame29.png)

Du borde se det här då.

![Bildruta-I/O](./images/frame30.png)

Kopiera JSON-koden nedan och klistra in den i fältet **Brödtext**.


```json
{
  "title": "What do you want Firefly to generate?",
  "description": "Enter your Firefly prompt.",
  "fields": [
    {
      "type": "text",
      "label": "Prompt",
      "name": "Prompt",
      "value": ""
    },
    {
      "type": "text",
      "label": "CTA Text",
      "name": "CTA Text",
      "value": ""
    },
    {
      "type": "text",
      "label": "Button Text",
      "name": "Button Text",
      "value": ""
    }
  ]
}
```

Klicka på ikonen för att rensa upp och förfina JSON-koden. Klicka sedan på **OK**.

![Bildruta-I/O](./images/frame31.png)

Klicka på **Spara** för att spara ändringarna.

![Bildruta-I/O](./images/frame32.png)

Därefter måste du konfigurera ett filter för att se till att den här sökvägen för scenariot bara körs när ingen fråga är tillgänglig. Klicka på ikonen **skiftnyckel** och välj sedan **Konfigurera ett filter**.

![Bildruta-I/O](./images/frame33.png)

Konfigurera följande fält:

- **Etikett**: använd `Prompt isn't available`.
- **Villkor**: använd `{{1.data.Prompt}}`.
- **Grundläggande operatorer**: välj **Finns inte**.

>[!NOTE]
>
>Variabler i Workfront Fusion kan anges manuellt med följande syntax: `{{1.data.Prompt}}`. Talet i variabeln refererar till modulen i scenariot. I det här exemplet ser du att den första modulen i scenariot kallas **Webhooks** och har sekvensnumret **1**. Det innebär att variabeln `{{1.data.Prompt}}` kommer åt fältet **data.Prompt** från modulen med sekvensnummer 1. Sekvensnummer kan ibland vara olika, så var uppmärksam när du kopierar/klistrar in sådana variabler och kontrollera alltid att det sekvensnummer som används är det rätta.

Klicka på **OK**.

![Bildruta-I/O](./images/frame34.png)

Du borde se det här då. Klicka först på ikonen **Spara** och sedan på **Kör en gång** för att testa ditt scenario.

![Bildruta-I/O](./images/frame35.png)

Du borde se det här då.

![Bildruta-I/O](./images/frame36.png)

Gå tillbaka till Frame.io och klicka på den anpassade åtgärden `--aepUserLdap-- - Frame IO Custom Action Fusion` för resursen **citisign-fiber.psd** igen.

![Bildruta-I/O](./images/frame37.png)

Nu bör du se en uppmaning i Frame.io. Fyll inte i fälten än och skicka inte formuläret än. Den här uppmaningen visas baserat på svaret från Workfront Fusion som du precis konfigurerat.

![Bildruta-I/O](./images/frame38.png)

Växla tillbaka till Workfront Fusion och klicka på bubblan i modulen **Webkrok-svar** . Du kommer att se att under **INPUT** visas brödtexten som innehåller JSON-nyttolasten för formuläret. Klicka på **Kör en gång** igen.

![Bildruta-I/O](./images/frame40.png)

Du borde se det här igen.

![Bildruta-I/O](./images/frame41.png)

Gå tillbaka till Frame.io och fyll i fälten enligt indikationen. Klicka på **Skicka**.

![Bildruta-I/O](./images/frame39.png)

Du bör då se en **lyckad åtgärd!**-popup.

![Bildruta-I/O](./images/frame42.png)

Växla tillbaka till Workfront Fusion och klicka på bubblan i modulen **Anpassad webkrok** . I åtgärd 1, under **OUTPUT**, kan du nu se ett nytt **data** -objekt som innehåller fält som **knapptext**, **CTA-text** och **Fråga**. När de här användarindatavariablerna är tillgängliga i ditt scenario har du tillräckligt många funktioner för att fortsätta konfigurationen.

![Bildruta-I/O](./images/frame43.png)

## 1.2.5.4 Hämta filplats från Frame.io

Som tidigare nämnts behövs fält som **prompt**, **cta**, **button** och **psdTemplate** för att det här scenariot ska fungera. De första tre fälten är nu redan tillgängliga, men **psdTemplate** som ska användas saknas fortfarande. **psdTemplate** refererar nu till en Frame.io-plats eftersom filen **citisign-fiber.psd** finns i Frame.io. För att kunna hämta platsen för filen måste du konfigurera och använda anslutningen Frame.io i Workfront Fusion.

Gå tillbaka till Workfront Fusion och öppna ditt scenario `--aepUserLdap-- - Frame IO Custom Action`. Hovra över **?**-modulen klickar du på ikonen **+** för att lägga till en annan modul och söka efter `frame`. Klicka på **Frame.io**.

![Bildruta-I/O](./images/frame44.png)

Klicka på **Frame.io (äldre)**.

![Bildruta-I/O](./images/frame45.png)

Klicka på **Hämta en resurs**.

![Bildruta-I/O](./images/frame46.png)

För att kunna använda Frame.io-anslutningen måste du först konfigurera den. Klicka på **Lägg till** för att göra det.

![Bildruta-I/O](./images/frame47.png)

Öppna listrutan **Anslutningstyp**.

![Bildruta-I/O](./images/frame48.png)

Välj **API-nyckeln Frame.io** och ange namnet `--aepUserLdap-- - Frame.io Token`.

![Bildruta-I/O](./images/frame49.png)

Gå till [https://developer.frame.io/](https://developer.frame.io/){target="_blank"} om du vill hämta en API-token. Klicka på **UTVECKLINGSVERKTYG** och välj sedan **Token**.

![Bildruta-I/O](./images/frame50.png)

Klicka på **Skapa en token**.

![Bildruta-I/O](./images/frame51.png)

Använd **Beskrivning** `--aepUserLdap-- - Frame.io Token` och klicka på **Markera alla omfattningar**.

![Bildruta-I/O](./images/frame52.png)

Bläddra nedåt och klicka på **Skicka**.

![Bildruta-I/O](./images/frame53.png)

Din token har skapats. Klicka på **Kopiera** för att kopiera den till Urklipp.

![Bildruta-I/O](./images/frame54.png)

Gå tillbaka till ditt scenario i Workfront Fusion. Klistra in token i fältet **Din API-nyckel för Frame.io**. Klicka på **OK**. Din anslutning kommer nu att testas av Workfront Fusion.

![Bildruta-I/O](./images/frame55.png)

Om anslutningen har testats visas den automatiskt under **Anslutning**. Du har nu en lyckad anslutning och du måste slutföra konfigurationen för att hämta all resursinformation från Frame.io, inklusive filplatsen. Du måste ange **resurs-ID** för att kunna göra detta.

![Bildruta-I/O](./images/frame56.png)

**Resurs-ID:t** delas av Frame.io till Workfront Fusion som en del av den inledande **anpassade webkrockkommunikationen** och finns under fältet **resource.id**. Välj **resource.id** och klicka på **OK**.

![Bildruta-I/O](./images/frame57.png)

Du borde se det här nu. Spara ändringarna och klicka sedan på **Kör en gång** för att testa ditt scenario.

![Bildruta-I/O](./images/frame58.png)

Gå tillbaka till Frame.io och klicka på den anpassade åtgärden `--aepUserLdap-- - Frame IO Custom Action Fusion` för resursen **citisign-fiber.psd** igen.

![Bildruta-I/O](./images/frame37.png)

Nu bör du se en uppmaning i Frame.io. Fyll inte i fälten än och skicka inte formuläret än. Den här uppmaningen visas baserat på svaret från Workfront Fusion som du precis konfigurerat.

![Bildruta-I/O](./images/frame38.png)

Byt tillbaka till Workfront Fusion. Klicka på **Kör en gång** igen.

![Bildruta-I/O](./images/frame59.png)

Gå tillbaka till Frame.io och fyll i fälten enligt indikationen. Klicka på **Skicka**.

![Bildruta-I/O](./images/frame39.png)

Växla tillbaka till Workfront Fusion och klicka på bubblan i modulen **Frame.io - Hämta en resurs**.

![Bildruta-I/O](./images/frame60.png)

Du kan nu se en massa metadata om den specifika resursen **citisign-fiber.psd**.

![Bildruta-I/O](./images/frame61.png)

Den specifika information som behövs för det här användningsfallet är platsen för filen **citisign-fiber.psd** som du hittar genom att bläddra nedåt till fältet **Original**.

![Bildruta-I/O](./images/frame62.png)

Du har nu alla fält (**prompt**, **cta**, **button** och **psdTemplate**) tillgängliga som krävs för att det här scenariot ska fungera.

## 1.2.5.5 Anropa Workfront-scenario

I föregående övning konfigurerade du scenariot `--aepUserLdap-- - Firefly + Photoshop`. Nu behöver du göra en mindre ändring i det scenariot.

Öppna scenariot `--aepUserLdap-- - Firefly + Photoshop` på en annan flik och klicka på den första modulen **Adobe Photoshop - Tillämpa PSD-redigeringar** . Du bör nu se att indatafilen är konfigurerad att använda en dynamisk plats i Microsoft Azure. Eftersom indatafilen inte längre lagras i Microsoft Azure, utan i stället används Frame.io-lagring, måste du ändra de här inställningarna.

![Bildruta-I/O](./images/frame63.png)

Ändra **Lagring** till **Extern** och ändra **Filplats** så att endast variabeln **psdTemplate** som hämtas från den inkommande **anpassade webkrockmodulen** används. Klicka på **OK** och sedan på **Spara** för att spara ändringarna.

![Bildruta-I/O](./images/frame64.png)

Klicka på modulen **Anpassad webkrok** och sedan på **Kopiera adress till Urklipp**. Du måste kopiera URL:en som du behöver för att kunna använda den i det andra scenariot.

![Bildruta-I/O](./images/frame65.png)

Gå tillbaka till ditt scenario `--aepUserLdap-- - Frame IO Custom Action`. Håll pekaren över **Frame.io - Hämta en resurs** och klicka på ikonen **+** .

![Bildruta-I/O](./images/frame66.png)

Ange `http` och klicka sedan på **HTTP**.

![Bildruta-I/O](./images/frame67.png)

Välj **Gör en förfrågan**.

![Bildruta-I/O](./images/frame68.png)

Klistra in URL:en för den anpassade webkroken i fältet **URL**. Ange **Metod** till POST**.

![Bildruta-I/O](./images/frame69.png)

Ange **Brödtyp** till **Raw** och **Innehållstyp** till **JSON (program/json)**.
Klistra in nedanstående JSON-nyttolast i fältet **Begär innehåll** och aktivera kryssrutan för **Analysera svar**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Du har nu konfigurerat en statisk nyttolast, men den måste bli dynamisk med de tidigare insamlade variablerna.

![Bildruta-I/O](./images/frame70.png)

Ersätt den statiska variabeln **citisign-fiber.psd** med variabeln **Original** för fältet **psdTemplate**.

![Bildruta-I/O](./images/frame71.png)

Ersätt de statiska variablerna för fälten **prompt**, **cta** och **button** med de dynamiska variabler som infogades i scenariot med den inkommande webkrok-begäran från Frame.io, som är fälten **data.Prompt**, **data.CTA Text** och **data.Button Text**.

Klicka på **OK**.

![Bildruta-I/O](./images/frame72.png)

Klicka på **Spara** för att spara ändringarna.

![Bildruta-I/O](./images/frame73.png)

## 1.2.5.6 Spara ny resurs i Frame.io

När det andra Workfront Fusion-scenariot har anropats blir resultatet en ny Photoshop PSD-mall som är tillgänglig. Den PSD-filen måste sparas tillbaka i Frame.io, som är det sista steget i det här scenariot.

Hovra över **HTTP - Gör en begäran**-modul och klicka på ikonen **+** .

![Bildruta-I/O](./images/frame74.png)

Välj **Frame.io (äldre)**.

![Bildruta-I/O](./images/frame75.png)

Välj **Skapa en resurs**.

![Bildruta-I/O](./images/frame76.png)

Din Frame.io-anslutning väljs automatiskt.

![Bildruta-I/O](./images/frame77.png)

Välj följande alternativ:

- **Team-ID**: välj lämpligt Team-ID, i det här fallet `One Adobe Tutorial`.
- **Projekt-ID**: använd `--aepUserLdap--`.
- **Mapp-ID**: använd `root`.
- **Typ**: använd `File`.

![Bildruta-I/O](./images/frame78.png)

För fältet **Namn** kan du använda en variabel som **timestamp** (eller ändra det till något som du tycker är mer begripligt). Du hittar den fördefinierade variabeln **timestamp** på fliken **Datum och tid**.

![Bildruta-I/O](./images/frame79.png)

Använd JSON-koden nedan för fältet **Source URL**.

```json
{{6.data.newPsdTemplate}}
```

>[!NOTE]
>
>Variabler i Workfront Fusion kan anges manuellt med följande syntax: `{{6.data.newPsdTemplate}}`. Talet i variabeln refererar till modulen i scenariot. I det här exemplet ser du att den sjätte modulen i scenariot kallas **HTTP - Gör en begäran** och har sekvensnumret ****. Det innebär att variabeln `{{6.data.newPsdTemplate}}` kommer åt fältet **data.newPsdTemplate** från modulen med sekvensnummer 6. Sekvensnummer kan ibland vara olika, så var uppmärksam när du kopierar/klistrar in sådana variabler och kontrollera alltid att det sekvensnummer som används är det rätta.

Klicka på **OK**.

![Bildruta-I/O](./images/frame80.png)

Klicka på **Spara** för att spara ändringarna.

![Bildruta-I/O](./images/frame81.png)

Slutligen måste du konfigurera ett filter så att den här sökvägen för scenariot endast körs när en uppmaning är tillgänglig. Klicka på ikonen **skiftnyckel** och välj sedan **Konfigurera ett filter**.

![Bildruta-I/O](./images/frame82.png)

Konfigurera följande fält:

- **Etikett**: använd `Prompt is available`.
- **Villkor**: använd `{{1.data.Prompt}}`.
- **Grundläggande operatorer**: välj **finns**.

>[!NOTE]
>
>Variabler i Workfront Fusion kan anges manuellt med följande syntax: `{{1.data.Prompt}}`. Talet i variabeln refererar till modulen i scenariot. I det här exemplet ser du att den första modulen i scenariot kallas **Webhooks** och har sekvensnumret **1**. Det innebär att variabeln `{{1.data.Prompt}}` kommer åt fältet **data.Prompt** från modulen med sekvensnummer 1. Sekvensnummer kan ibland vara olika, så var uppmärksam när du kopierar/klistrar in sådana variabler och kontrollera alltid att det sekvensnummer som används är det rätta.

Klicka på **OK**.

![Bildruta-I/O](./images/frame83.png)

Klicka på **Spara** för att spara ändringarna.

![Bildruta-I/O](./images/frame84.png)

## 1.2.5.7 Testa ditt fall av användning från början till slut

Klicka på **Kör en gång** i ditt scenario `--aepUserLdap-- - Frame IO Custom Action`.

![Bildruta-I/O](./images/frame85.png)

Gå tillbaka till Frame.io och klicka på den anpassade åtgärden `--aepUserLdap-- - Frame IO Custom Action Fusion` för resursen **citisign-fiber.psd** igen.

![Bildruta-I/O](./images/frame37.png)

Nu bör du se en uppmaning i Frame.io. Fyll inte i fälten än och skicka inte formuläret än. Den här uppmaningen visas baserat på svaret från Workfront Fusion som du precis konfigurerat.

![Bildruta-I/O](./images/frame38.png)

Byt tillbaka till Workfront Fusion. Klicka på **Kör en gång** i ditt scenario `--aepUserLdap-- - Frame IO Custom Action`.

![Bildruta-I/O](./images/frame86.png)

Öppna scenariot `--aepUserLdap-- - Firefly + Photoshop` i Workfront Fusion och klicka även på **Kör en gång** i det scenariot.

![Bildruta-I/O](./images/frame87.png)

Gå tillbaka till Frame.io och fyll i fälten enligt indikationen. Klicka på **Skicka**.

![Bildruta-I/O](./images/frame39.png)

Efter 1-2 minuter visas en ny resurs automatiskt i Frame.io. Dubbelklicka på den nya resursen för att öppna den.

![Bildruta-I/O](./images/frame88.png)

Nu ser du tydligt att alla användarindatavariabler har tillämpats automatiskt.

![Bildruta-I/O](./images/frame89.png)

Du har nu slutfört den här övningen.

## Nästa steg

Gå till [1.2.6 Frame.io och Fusion till AEM Assets](./ex6.md){target="_blank"}

Gå tillbaka till [Creative Workflow Automation med Workfront Fusion](./automation.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}

