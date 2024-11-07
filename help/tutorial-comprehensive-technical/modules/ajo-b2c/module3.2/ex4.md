---
title: Adobe Journey Optimizer - Konfigurera och använda SMS-kanalen i Adobe Journey Optimizer
description: Adobe Journey Optimizer - Konfigurera och använda SMS-kanalen i Adobe Journey Optimizer
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '2300'
ht-degree: 0%

---

# 3.2.4 Skapa din resa och dina meddelanden

I den här övningen skapar du en resa och flera textmeddelanden genom att använda Adobe Journey Optimizer.

I det här fallet är målet att skicka olika SMS-meddelanden baserat på väderförhållandena för var kunden befinner sig. Tre scenarier har definierats:

- Färre än 10° Celsius
- Mellan 10° och 25° Celsius
- Varmare än 25° Celsius

För dessa tre villkor måste du definiera tre SMS-meddelanden i Adobe Journey Optimizer.

## 3.2.4.1 Skapa din resa

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och väljer sandlådan i listan. I det här exemplet heter sandlådan **AEP Enablement FY22**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)


Gå till **Resor** på den vänstra menyn och klicka på **Skapa resa** för att börja skapa din resa.

![Demo](./images/jocreate.png)

Du bör i förväg namnge din resa.

Använd `--aepUserLdap-- - Geofence Entry Journey` som namn för resan. I det här exemplet är resenamnet `vangeluw - Geofence Entry Journey`. Inga andra värden måste anges för tillfället. Klicka på **OK**.

![Demo](./images/joname.png)

Titta på **Händelser** till vänster på skärmen. Du bör se den händelse du skapade tidigare i den listan. Markera den och dra den sedan och släpp den på arbetsytan. Din resa ser då ut så här. Klicka på **OK**.

![Demo](./images/joevents.png)

Klicka sedan på **Orchestration**. Nu ser du de tillgängliga **Orchestration**-funktionerna. Välj **Villkor** och dra och släpp det på arbetsytan på resan.

![Demo](./images/jo2.png)

Nu måste du definiera tre villkor:

- Den är kallare än 10° Celsius
- Den är mellan 10° och 25° Celsius
- Det är varmare än 25° Celsius

Vi definierar det första villkoret.

### Villkor 1: Färger än 10° Celsius

Klicka på **Villkor**.  Klicka på **Sökväg1** och redigera namnet på sökvägen till **Färg än 10 C**. Klicka på ikonen **Redigera** för uttrycket för Path1.

![Demo](./images/jo5.png)

Du ser då en tom skärm i **Enkel redigerare**. Din fråga kommer att vara lite mer avancerad, så du behöver **avancerat läge**. Klicka på **Avancerat läge**.

![Demo](./images/jo7.png)

Du kommer då att se **Avancerad redigerare** som tillåter kodinmatning.

![Demo](./images/jo9.png)

Markera nedanstående kod och klistra in den i **Avancerad redigerare**.

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} <= 10`

Då ser du det här.

![Demo](./images/jo10.png)

För att kunna ta reda på temperaturen som en del av detta villkor måste du ange i vilken stad kunden befinner sig.
**City** måste länkas till den dynamiska parametern `q`, precis som vi såg tidigare i Open Weather API-dokumentationen.

Klicka på fältet **dynamiskt val: q** som anges i skärmbilden.

![Demo](./images/jo11.png)

Sedan måste du hitta fältet som innehåller kundens aktuella ort i någon av de tillgängliga datakällorna.

![Demo](./images/jo12.png)

Du kan hitta fältet genom att gå till `--aepUserLdap--GeofenceEntry.placeContext.geo.city`.

Genom att klicka på det fältet läggs det till som dynamiskt värde för parametern `q`. Det här fältet fylls i med till exempel den geopositioneringstjänst som du har implementerat i din mobilapp. I så fall simulerar vi detta med administrationskonsolen på demowebbplatsen. Klicka på **OK**.

![Demo](./images/jo13.png)

### Villkor 2: 10-25° Celsius

När du har lagt till det första villkoret visas den här skärmen. Klicka på **Lägg till sökväg**.

![Demo](./images/joc2.png)

Dubbelklicka på **Sökväg1** och redigera sökvägen till **Mellan 10 och 25 C**. Klicka på ikonen **Redigera** för uttrycket med den här sökvägen.

![Demo](./images/joc6.png)

Du ser då en tom skärm i **Enkel redigerare**. Din fråga kommer att vara lite mer avancerad, så du behöver **avancerat läge**. Klicka på **Avancerat läge**.

![Demo](./images/jo7.png)

Du kommer då att se **Avancerad redigerare** som tillåter kodinmatning.

![Demo](./images/jo9.png)

Markera nedanstående kod och klistra in den i **Avancerad redigerare**.

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} > 10 and #{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} <= 25`

Då ser du det här.

![Demo](./images/joc10.png)

För att kunna hämta temperaturen som en del av detta villkor måste du ange i vilken stad kunden befinner sig.
**City** måste länkas till den dynamiska parametern **q**, precis som vi såg tidigare i Open Weather API-dokumentationen.

Klicka på fältet **dynamiskt val: q** som anges i skärmbilden.

![Demo](./images/joc11.png)

Sedan måste du hitta fältet som innehåller kundens aktuella ort i någon av de tillgängliga datakällorna.

![Demo](./images/jo12.png)

Du kan hitta fältet genom att gå till `--aepUserLdap--GeofenceEntry.placeContext.geo.city`. Genom att klicka på det fältet läggs det till som dynamiskt värde för parametern **q**. Det här fältet fylls i med till exempel den geopositioneringstjänst som du har implementerat i din mobilapp. I så fall simulerar vi detta med administrationskonsolen på demowebbplatsen. Klicka på **OK**.

![Demo](./images/jo13.png)

Sedan lägger du till det tredje villkoret.

### Villkor 3: Varmare än 25° Celsius

När du har lagt till det andra villkoret visas den här skärmen. Klicka på **Lägg till sökväg**.

![Demo](./images/joct2.png)

Dubbelklicka på Path1 om du vill ändra namnet till **Varmare än 25 C**.
Klicka sedan på ikonen **Redigera** för uttrycket som den här sökvägen gäller.

![Demo](./images/joct6.png)

Du ser då en tom skärm i **Enkel redigerare**. Din fråga kommer att vara lite mer avancerad, så du behöver **avancerat läge**. Klicka på **Avancerat läge**.

![Demo](./images/jo7.png)

Du kommer då att se **Avancerad redigerare** som tillåter kodinmatning.

![Demo](./images/jo9.png)

Markera nedanstående kod och klistra in den i **Avancerad redigerare**.

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} > 25`

Då ser du det här.

![Demo](./images/joct10.png)

För att kunna hämta temperaturen som en del av detta villkor måste du ange i vilken stad kunden befinner sig.
**City** måste länkas till den dynamiska parametern **q**, precis som vi såg tidigare i Open Weather API-dokumentationen.

Klicka på fältet **dynamiskt val: q** som anges i skärmbilden.

![Demo](./images/joct11.png)

Sedan måste du hitta fältet som innehåller kundens aktuella ort i någon av de tillgängliga datakällorna.

![Demo](./images/jo12.png)

Du kan hitta fältet genom att gå till ```--aepUserLdap--GeofenceEntry.placeContext.geo.city```. Genom att klicka på det fältet läggs det till som dynamiskt värde för parametern **q**. Det här fältet fylls i med till exempel den geopositioneringstjänst som du har implementerat i din mobilapp. I så fall simulerar vi detta med administrationskonsolen på demowebbplatsen. Klicka på **OK**.

![Demo](./images/jo13.png)

Du har nu tre konfigurerade sökvägar. Klicka på **OK**.

![Demo](./images/jo3path.png)

Eftersom det här är en resa för inlärningsändamål kommer vi nu att konfigurera några åtgärder för att visa upp de olika alternativ som marknadsförare nu behöver för att leverera meddelanden.

## 3.2.4.2 Skicka meddelanden för sökväg: Färre än 10° Celsius

För varje temperatursammanhang försöker vi skicka ett sms till kunden. Vi kan bara skicka ett SMS om vi har ett mobilnummer tillgängligt för en kund, så vi måste först bekräfta att vi har det.

Vi fokuserar på **Kolder än 10 C**.

![Demo](./images/p1steps.png)

Låt oss ta ett annat **Condition** -element och dra det enligt skärmbilden nedan. Vi kommer att verifiera om det finns ett mobilnummer tillgängligt för den här kunden.

![Demo](./images/joa1.png)

Eftersom detta bara är ett exempel konfigurerar vi bara alternativet där kunden har ett mobilnummer tillgängligt. Lägg till etiketten **Har mobil?**.

Klicka på ikonen **Redigera** för uttrycket för sökvägen **Path1**.

![Demo](./images/joa2.png)

Navigera till **ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number** i de datakällor som visas till vänster. Du läser nu mobiltelefonnumret direkt från Adobe Experience Platform kundprofil i realtid.

![Demo](./images/joa3.png)

Markera fältet **Nummer** och dra och släpp det på villkorsarbetsytan.

Markera operatorn **som inte är tom**. Klicka på **OK**.

![Demo](./images/joa4.png)

Då ser du det här. Klicka på **OK** igen.

![Demo](./images/joa6.png)

Din resa kommer då att se ut så här. Klicka på **Åtgärder** enligt skärmbilden.

![Demo](./images/joa8.png)

Välj åtgärden **SMS** och dra och släpp den efter villkoret som du just lade till.

![Demo](./images/joa9.png)

Ange **kategori** till **marknadsföring** och välj en SMS-yta som gör att du kan skicka SMS. I det här fallet är e-postytan som ska väljas **SMS**.

![ACOP](./images/journeyactions1.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka på **Redigera innehåll**.

![ACOP](./images/journeyactions2.png)

Nu visas meddelandekontrollpanelen, där du kan konfigurera texten i ditt SMS. Klicka på området **Disponera meddelande** för att skapa meddelandet.

![Journey Optimizer](./images/sms3.png)

Ange följande text: `Brrrr... {{profile.person.name.firstName}}, it's freezing. 20% discount on jackets today!`. Klicka på **Spara**.

![Journey Optimizer](./images/sms4.png)

Då ser du det här. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/sms4a.png)

Du kommer då tillbaka hit. Klicka på **OK**.

![Journey Optimizer](./images/sms4b.png)

Gå tillbaka till **Åtgärder** på den vänstra menyn, markera åtgärden `--aepUserLdap--TextSlack` och dra och släpp den sedan efter åtgärden **Meddelande** .

![Demo](./images/joa18.png)

Gå till **åtgärdsparametrar** och klicka på ikonen **Redigera** för parametern `TEXTTOSLACK`.

![Demo](./images/joa19.png)

Klicka på **Avancerat läge** i popup-fönstret.

![Demo](./images/joa20.png)

Markera nedanstående kod, kopiera den och klistra in den i **redigeraren för avancerat läge**. Klicka på **OK**.

`"Brrrr..." + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " It's freezing. 20% discount on Jackets today!"`

![Demo](./images/joa21.png)

Du kommer att se den slutförda åtgärden. Klicka på **OK**.

![Demo](./images/joa22.png)

Den här vägen på resan är nu färdig.

## 3.2.4.3 Skicka meddelanden för sökväg: mellan 10° och 25° Celsius

För varje temperatursammanhang försöker vi skicka ett sms till kunden. Vi kan bara skicka ett SMS om vi har ett mobilnummer tillgängligt för en kund, så vi måste först bekräfta att vi har det.

Vi fokuserar på **Mellan 10 och 25 C**-sökvägar.

![Demo](./images/p2steps.png)

Låt oss ta ett annat **Condition** -element och dra det enligt skärmbilden nedan. Vi kommer att verifiera om det finns ett mobilnummer tillgängligt för den här kunden.

![Demo](./images/jop1.png)

Eftersom detta bara är ett exempel konfigurerar vi bara alternativet där kunden har ett mobilnummer tillgängligt. Lägg till etiketten **Har mobil?**.

Klicka på ikonen **Redigera** för uttrycket för sökvägen **Path1**.

![Demo](./images/joa2p2.png)

Navigera till **ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number** i de datakällor som visas till vänster. Du läser nu mobiltelefonnumret direkt från Adobe Experience Platform kundprofil i realtid.

![Demo](./images/joa3.png)

Markera fältet **Nummer** och dra och släpp det på villkorsarbetsytan.

Markera operatorn **som inte är tom**. Klicka på **OK**.

![Demo](./images/joa4.png)

Då ser du det här. Klicka på **OK**.

![Demo](./images/joa6.png)

Din resa kommer då att se ut så här. Klicka på **Åtgärder** enligt skärmbilden.

![Demo](./images/jop8.png)

Välj åtgärden **SMS** och dra och släpp den efter villkoret som du just lade till.

![Demo](./images/jop9.png)

Ange **kategori** till **marknadsföring** och välj en SMS-yta som gör att du kan skicka SMS. I det här fallet är e-postytan som ska väljas **SMS**.

![ACOP](./images/journeyactions1z.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka på **Redigera innehåll**.

![ACOP](./images/journeyactions2z.png)

Nu visas meddelandekontrollpanelen, där du kan konfigurera texten i ditt SMS. Klicka på området **Disponera meddelande** för att skapa meddelandet.

![Journey Optimizer](./images/sms3a.png)

Ange följande text: `What a nice weather for the time of year, {{profile.person.name.firstName}} - 20% discount on Sweaters today!`. Klicka på **Spara**.

![Journey Optimizer](./images/sms4az.png)

Då ser du det här. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/sms4azz.png)

Nu visas den slutförda åtgärden. Klicka på **OK**.

![Demo](./images/jop17.png)

Gå tillbaka till **Åtgärder** på den vänstra menyn, markera åtgärden `--aepUserLdap--TextSlack` och dra och släpp den sedan efter åtgärden **Meddelande** .

![Demo](./images/jop18.png)

Gå till **åtgärdsparametrar** och klicka på ikonen **Redigera** för parametern `TEXTTOSLACK`.

![Demo](./images/joa19z.png)

Klicka på **Avancerat läge** i popup-fönstret.

![Demo](./images/joa20.png)

Markera nedanstående kod, kopiera den och klistra in den i **redigeraren för avancerat läge**. Klicka på **OK**.

`"What nice weather for the time of year, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " 20% discount on Sweaters today!"`

![Demo](./images/jop21.png)

Du kommer att se den slutförda åtgärden. Klicka på **OK**.

![Demo](./images/jop22.png)

Den här vägen på resan är nu färdig.

## 3.2.4.4 Skicka meddelanden för sökväg: Varmare än 25° Celsius

För varje temperatursammanhang försöker vi skicka ett sms till kunden. Vi kan bara skicka ett SMS om vi har ett mobilnummer tillgängligt för en kund, så vi måste först bekräfta att vi har det.

Vi fokuserar på **Varmare än 25 C**-sökvägar.

![Demo](./images/p3steps.png)

Låt oss ta ett annat **Condition** -element och dra det enligt skärmbilden nedan. Du kommer att verifiera om det finns ett mobilnummer tillgängligt för den här kunden.

![Demo](./images/jod1.png)

Eftersom detta bara är ett exempel konfigurerar vi bara alternativet där kunden har ett mobilnummer tillgängligt. Lägg till etiketten **Har mobil?**.

Klicka på ikonen **Redigera** för uttrycket för sökvägen **Path1**.

![Demo](./images/joa2p3.png)

Navigera till **ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number** i de datakällor som visas till vänster. Du läser nu mobiltelefonnumret direkt från Adobe Experience Platform kundprofil i realtid.

![Demo](./images/joa3.png)

Markera fältet **Nummer** och dra och släpp det på villkorsarbetsytan.

Markera operatorn **som inte är tom**. Klicka på **OK**.

![Demo](./images/joa4.png)

Då ser du det här. Klicka på **OK**.

![Demo](./images/joa6.png)

Din resa kommer då att se ut så här. Klicka på **Åtgärder** enligt skärmbilden.

![Demo](./images/jod8.png)

Välj åtgärden **SMS** och dra och släpp den efter villkoret som du just lade till.

![Demo](./images/jod9.png)

Ange **kategori** till **marknadsföring** och välj en SMS-yta som gör att du kan skicka SMS. I det här fallet är e-postytan som ska väljas **SMS**.

![ACOP](./images/journeyactions1zy.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka på **Redigera innehåll**.

![ACOP](./images/journeyactions2zy.png)

Nu visas meddelandekontrollpanelen, där du kan konfigurera texten i ditt SMS. Klicka på området **Disponera meddelande** för att skapa meddelandet.

![Journey Optimizer](./images/sms3ab.png)

Ange följande text: `So warm, {{profile.person.name.firstName}}! 20% discount on swimwear today!`. Klicka på **Spara**.

![Journey Optimizer](./images/sms4ab.png)

Då ser du det här. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/sms4azzz.png)

Nu visas den slutförda åtgärden. Klicka på **OK**.

![Demo](./images/jod17.png)

Gå tillbaka till **Åtgärder** på den vänstra menyn, markera åtgärden `--aepUserLdap--TextSlack` och dra och släpp den sedan efter åtgärden **Meddelanden**.

![Demo](./images/jod18.png)

Gå till **åtgärdsparametrar** och klicka på ikonen **Redigera** för parametern `TEXTTOSLACK`.

![Demo](./images/joa19zzz.png)

Klicka på **Avancerat läge** i popup-fönstret.

![Demo](./images/joa20.png)

Markera nedanstående kod, kopiera den och klistra in den i **redigeraren för avancerat läge**. Klicka på **OK**.

`"So warm, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + "! 20% discount on swimwear today!"`

![Demo](./images/jod21.png)

Du kommer att se den slutförda åtgärden. Klicka på **OK**.

![Demo](./images/jod22.png)

Den här vägen på resan är nu färdig.

## 3.2.4.5 Publish din resa

Din resa är nu helt konfigurerad. Klicka på **Publish**.

![Demo](./images/jodone.png)

Klicka på **Publish** igen.

![Demo](./images/jopublish1.png)

Din resa är nu publicerad.

![Demo](./images/jopublish2.png)

Nästa steg: [3.2.5 Utlösa din resa](./ex5.md)

[Gå tillbaka till modul 3.2](journey-orchestration-external-weather-api-sms.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
