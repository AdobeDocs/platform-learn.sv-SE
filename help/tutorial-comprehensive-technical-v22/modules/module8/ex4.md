---
title: Adobe Journey Optimizer - Konfigurera och använda SMS-kanalen i Adobe Journey Optimizer
description: Adobe Journey Optimizer - Konfigurera och använda SMS-kanalen i Adobe Journey Optimizer
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 1a08f666-4ea3-43bc-ace7-5dc9854b89ad
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2261'
ht-degree: 0%

---

# 8.4 Skapa din resa och dina meddelanden

I den här övningen skapar du en resa och flera textmeddelanden genom att använda Adobe Journey Optimizer.

I det här fallet är målet att skicka olika SMS-meddelanden baserat på väderförhållandena för var kunden befinner sig. Tre scenarier har definierats:

- Färre än 10° Celsius
- Mellan 10° och 25° Celsius
- Varmare än 25° Celsius

För dessa tre villkor måste du definiera tre SMS-meddelanden i Adobe Journey Optimizer.

## 8.4.1 Skapa din resa

Logga in på Adobe Journey Optimizer genom att gå till [Adobe Experience Cloud](https://experience.adobe.com). Klicka **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Du omdirigeras till **Startsida**  i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas anropas `--aepSandboxId--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och välj sandlådan i listan. I det här exemplet heter sandlådan **AEP-aktivering FY22**. Då är du i **Startsida** vy över din sandlåda `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)


Gå till den vänstra menyn **Resor** och klicka **Skapa resa** för att börja skapa din resa.

![Demo](./images/jocreate.png)

Du bör i förväg namnge din resa.

Använd som namn för resan `--demoProfileLdap-- - Geofence Entry Journey`. I det här exemplet är resenamnet `vangeluw - Geofence Entry Journey`. Inga andra värden måste anges för tillfället. Klicka **OK**.

![Demo](./images/joname.png)

På vänster sida av skärmen kan du titta på **Händelser**. Du bör se den händelse du skapade tidigare i den listan. Markera den och dra den sedan och släpp den på arbetsytan. Din resa ser då ut så här. Klicka **OK**.

![Demo](./images/joevents.png)

Klicka på **Orchestration**. Du ser nu tillgängliga **Orchestration** funktioner. Välj **Villkor** och sedan dra och släppa den på arbetsytan på resan.

![Demo](./images/jo2.png)

Nu måste du definiera tre villkor:

- Den är kallare än 10° Celsius
- Den är mellan 10° och 25° Celsius
- Det är varmare än 25° Celsius

Vi definierar det första villkoret.

### Villkor 1: Färre än 10° Celsius

Klicka på **Villkor**.  Klicka på **Bana1** och redigera namnet på sökvägen till **Kolder än 10 C**. Klicka på **Redigera** -ikon för uttrycket för Path1.

![Demo](./images/jo5.png)

Då ser du en tom **Enkel redigerare** skärm. Din fråga kommer att bli lite mer avancerad, så du behöver **Avancerat läge**. Klicka **Avancerat läge**.

![Demo](./images/jo7.png)

Då ser du **Avancerad redigerare** som tillåter kodinmatning.

![Demo](./images/jo9.png)

Markera nedanstående kod och klistra in den i dialogrutan **Avancerad redigerare**.

`#{--demoProfileLdap--WeatherApi.--demoProfileLdap--WeatherByCity.main.temp} <= 10`

Du kommer då att se det här.

![Demo](./images/jo10.png)

För att kunna ta reda på temperaturen som en del av detta villkor måste du ange i vilken stad kunden befinner sig.
The **Ort** måste länkas till den dynamiska parametern `q`, precis som vi såg tidigare i Open Weather API Documentation.

Klicka på fältet **dynamiskt värde: q** enligt skärmbilden.

![Demo](./images/jo11.png)

Sedan måste du hitta fältet som innehåller kundens aktuella ort i någon av de tillgängliga datakällorna.

![Demo](./images/jo12.png)

Du kan hitta fältet genom att navigera till `--demoProfileLdap--GeofenceEntry.placeContext.geo.city`.

Genom att klicka på det fältet läggs det till som det dynamiska värdet för parametern `q`. Det här fältet fylls i med till exempel den geopositioneringstjänst som du har implementerat i din mobilapp. I så fall simulerar vi detta med administrationskonsolen på demowebbplatsen. Klicka **OK**.

![Demo](./images/jo13.png)

### Villkor 2: Mellan 10° och 25° Celsius

När du har lagt till det första villkoret visas den här skärmen. Klicka **Lägg till bana**.

![Demo](./images/joc2.png)

Dubbelklicka på **Bana1** och redigera sökvägen till **Mellan 10 och 25 C**. Klicka på **Redigera** -ikon för uttrycket i den här sökvägen.

![Demo](./images/joc6.png)

Då ser du en tom **Enkel redigerare** skärm. Din fråga kommer att bli lite mer avancerad, så du behöver **Avancerat läge**. Klicka **Avancerat läge**.

![Demo](./images/jo7.png)

Då ser du **Avancerad redigerare** som tillåter kodinmatning.

![Demo](./images/jo9.png)

Markera nedanstående kod och klistra in den i dialogrutan **Avancerad redigerare**.

`#{--demoProfileLdap--WeatherApi.--demoProfileLdap--WeatherByCity.main.temp} > 10 and #{--demoProfileLdap--WeatherApi.--demoProfileLdap--WeatherByCity.main.temp} <= 25`

Du kommer då att se det här.

![Demo](./images/joc10.png)

För att kunna hämta temperaturen som en del av detta villkor måste du ange i vilken stad kunden befinner sig.
The **Ort** måste länkas till den dynamiska parametern **q**, precis som vi såg tidigare i Open Weather API Documentation.

Klicka på fältet **dynamiskt värde: q** enligt skärmbilden.

![Demo](./images/joc11.png)

Sedan måste du hitta fältet som innehåller kundens aktuella ort i någon av de tillgängliga datakällorna.

![Demo](./images/jo12.png)

Du kan hitta fältet genom att navigera till `--demoProfileLdap--GeofenceEntry.placeContext.geo.city`. Genom att klicka på det fältet läggs det till som det dynamiska värdet för parametern **q**. Det här fältet fylls i med till exempel den geopositioneringstjänst som du har implementerat i din mobilapp. I så fall simulerar vi detta med administrationskonsolen på demowebbplatsen. Klicka **OK**.

![Demo](./images/jo13.png)

Sedan lägger du till det tredje villkoret.

### Villkor 3: Varmare än 25° Celsius

När du har lagt till det andra villkoret visas den här skärmen. Klicka **Lägg till bana**.

![Demo](./images/joct2.png)

Dubbelklicka på Bana1 för att ändra namnet till **Varmare än 25 C**.
Klicka sedan på **Redigera** -ikon för uttrycket i den här sökvägen.

![Demo](./images/joct6.png)

Då ser du en tom **Enkel redigerare** skärm. Din fråga kommer att bli lite mer avancerad, så du behöver **Avancerat läge**. Klicka **Avancerat läge**.

![Demo](./images/jo7.png)

Då ser du **Avancerad redigerare** som tillåter kodinmatning.

![Demo](./images/jo9.png)

Markera nedanstående kod och klistra in den i dialogrutan **Avancerad redigerare**.

`#{--demoProfileLdap--WeatherApi.--demoProfileLdap--WeatherByCity.main.temp} > 25`

Du kommer då att se det här.

![Demo](./images/joct10.png)

För att kunna hämta temperaturen som en del av detta villkor måste du ange i vilken stad kunden befinner sig.
The **Ort** måste länkas till den dynamiska parametern **q**, precis som vi såg tidigare i Open Weather API Documentation.

Klicka på fältet **dynamiskt värde: q** enligt skärmbilden.

![Demo](./images/joct11.png)

Sedan måste du hitta fältet som innehåller kundens aktuella ort i någon av de tillgängliga datakällorna.

![Demo](./images/jo12.png)

Du kan hitta fältet genom att navigera till ```--demoProfileLdap--GeofenceEntry.placeContext.geo.city```. Genom att klicka på det fältet läggs det till som det dynamiska värdet för parametern **q**. Det här fältet fylls i med till exempel den geopositioneringstjänst som du har implementerat i din mobilapp. I så fall simulerar vi detta med administrationskonsolen på demowebbplatsen. Klicka **OK**.

![Demo](./images/jo13.png)

Du har nu tre konfigurerade sökvägar. Klicka **OK**.

![Demo](./images/jo3path.png)

Eftersom det här är en resa för inlärningsändamål kommer vi nu att konfigurera några åtgärder för att visa upp de olika alternativ som marknadsförare nu behöver för att leverera meddelanden.

## 8.4.2 Skicka meddelanden för sökväg: Färre än 10° Celsius

För varje temperatursammanhang försöker vi skicka ett sms till kunden. Vi kan bara skicka ett SMS om vi har ett mobilnummer tillgängligt för en kund, så vi måste först bekräfta att vi har det.

Låt oss fokusera på **Kolder än 10 C**.

![Demo](./images/p1steps.png)

Låt oss ta en till **Villkor** och dra det enligt skärmbilden nedan. Vi kontrollerar om det finns ett mobilnummer för den här kunden.

![Demo](./images/joa1.png)

Eftersom detta bara är ett exempel konfigurerar vi bara alternativet där kunden har ett mobilnummer tillgängligt. Lägg till en etikett för **Har mobilen?**.

Klicka på **Redigera** -ikon för uttrycket för **Bana1** bana.

![Demo](./images/joa2.png)

Navigera till i Datakällor till vänster **ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number**. Du läser nu mobiltelefonnumret direkt från Adobe Experience Platform kundprofil i realtid.

![Demo](./images/joa3.png)

Markera fältet **Nummer** och sedan dra och släpp det på Villkorsytan.

Markera operatorn **är inte tom**. Klicka **OK**.

![Demo](./images/joa4.png)

Du kommer då att se det här. Klicka **OK** igen.

![Demo](./images/joa6.png)

Din resa kommer då att se ut så här. Klicka på **Åtgärder** enligt skärmbilden.

![Demo](./images/joa8.png)

Välj åtgärd **SMS** och sedan dra och släppa det efter villkoret du just lade till.

![Demo](./images/joa9.png)

Ange **Kategori** till **Marknadsföring** och välj en SMS-yta som gör att du kan skicka SMS. I det här fallet är e-postytan som ska väljas **SMS**.

![ACOP](./images/journeyactions1.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka **Redigera innehåll**.

![ACOP](./images/journeyactions2.png)

Nu visas meddelandekontrollpanelen, där du kan konfigurera texten i ditt SMS. Klicka på **Skriv meddelande** för att skapa meddelandet.

![Journey Optimizer](./images/sms3.png)

Ange följande text: `Brrrr... {{profile.person.name.firstName}}, it's freezing. 20% discount on jackets today!`. Klicka **Spara**.

![Journey Optimizer](./images/sms4.png)

Du kommer då att se det här. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/sms4a.png)

Du kommer då tillbaka hit. Klicka **OK**.

![Journey Optimizer](./images/sms4b.png)

Gå tillbaka till den vänstra menyn **Åtgärder** väljer du funktionsmakrot `--demoProfileLdap--TextSlack`och sedan dra och släppa det efter **Meddelande** åtgärd.

![Demo](./images/joa18.png)

Gå till **Åtgärdsparametrar** och klicka på **Redigera** ikon för parametern `TEXTTOSLACK`.

![Demo](./images/joa19.png)

I popup-fönstret klickar du på **Avancerat läge**.

![Demo](./images/joa20.png)

Markera nedanstående kod, kopiera den och klistra in den i **Avancerad lägesredigerare**. Klicka **OK**.

`"Brrrr..." + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " It's freezing. 20% discount on Jackets today!"`

![Demo](./images/joa21.png)

Du kommer att se den slutförda åtgärden. Klicka **OK**.

![Demo](./images/joa22.png)

Den här vägen på resan är nu färdig.

## 8.4.3 Skicka meddelanden för sökväg: Mellan 10° och 25° Celsius

För varje temperatursammanhang försöker vi skicka ett sms till kunden. Vi kan bara skicka ett SMS om vi har ett mobilnummer tillgängligt för en kund, så vi måste först bekräfta att vi har det.

Låt oss fokusera på **Mellan 10 och 25 C** bana.

![Demo](./images/p2steps.png)

Låt oss ta en till **Villkor** och dra det enligt skärmbilden nedan. Vi kontrollerar om det finns ett mobilnummer för den här kunden.

![Demo](./images/jop1.png)

Eftersom detta bara är ett exempel konfigurerar vi bara alternativet där kunden har ett mobilnummer tillgängligt. Lägg till en etikett för **Har mobilen?**.

Klicka på **Redigera** -ikon för uttrycket för **Bana1** bana.

![Demo](./images/joa2p2.png)

Navigera till i Datakällor till vänster **ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number**. Du läser nu mobiltelefonnumret direkt från Adobe Experience Platform kundprofil i realtid.

![Demo](./images/joa3.png)

Markera fältet **Nummer** och sedan dra och släpp det på Villkorsytan.

Markera operatorn **är inte tom**. Klicka **OK**.

![Demo](./images/joa4.png)

Du kommer då att se det här. Klicka **OK**.

![Demo](./images/joa6.png)

Din resa kommer då att se ut så här. Klicka på **Åtgärder** enligt skärmbilden.

![Demo](./images/jop8.png)

Välj åtgärd **SMS** och sedan dra och släppa det efter villkoret du just lade till.

![Demo](./images/jop9.png)

Ange **Kategori** till **Marknadsföring** och välj en SMS-yta som gör att du kan skicka SMS. I det här fallet är e-postytan som ska väljas **SMS**.

![ACOP](./images/journeyactions1z.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka **Redigera innehåll**.

![ACOP](./images/journeyactions2z.png)

Nu visas meddelandekontrollpanelen, där du kan konfigurera texten i ditt SMS. Klicka på **Skriv meddelande** för att skapa meddelandet.

![Journey Optimizer](./images/sms3a.png)

Ange följande text: `What a nice weather for the time of year, {{profile.person.name.firstName}} - 20% discount on Sweaters today!`. Klicka **Spara**.

![Journey Optimizer](./images/sms4az.png)

Du kommer då att se det här. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/sms4azz.png)

Nu visas den slutförda åtgärden. Klicka **OK**.

![Demo](./images/jop17.png)

Gå tillbaka till den vänstra menyn **Åtgärder** väljer du funktionsmakrot `--demoProfileLdap--TextSlack`och sedan dra och släppa det efter **Meddelande** åtgärd.

![Demo](./images/jop18.png)

Gå till **Åtgärdsparametrar** och klicka på **Redigera** ikon för parametern `TEXTTOSLACK`.

![Demo](./images/joa19z.png)

I popup-fönstret klickar du på **Avancerat läge**.

![Demo](./images/joa20.png)

Markera nedanstående kod, kopiera den och klistra in den i **Avancerad lägesredigerare**. Klicka **OK**.

`"What nice weather for the time of year, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " 20% discount on Sweaters today!"`

![Demo](./images/jop21.png)

Du kommer att se den slutförda åtgärden. Klicka **OK**.

![Demo](./images/jop22.png)

Den här vägen på resan är nu färdig.

## 8.4.4 Skicka meddelanden för sökväg: Varmare än 25° Celsius

För varje temperatursammanhang försöker vi skicka ett sms till kunden. Vi kan bara skicka ett SMS om vi har ett mobilnummer tillgängligt för en kund, så vi måste först bekräfta att vi har det.

Låt oss fokusera på **Varmare än 25 C** bana.

![Demo](./images/p3steps.png)

Låt oss ta en till **Villkor** och dra det enligt skärmbilden nedan. Du kommer att verifiera om det finns ett mobilnummer tillgängligt för den här kunden.

![Demo](./images/jod1.png)

Eftersom detta bara är ett exempel konfigurerar vi bara alternativet där kunden har ett mobilnummer tillgängligt. Lägg till en etikett för **Har mobilen?**.

Klicka på **Redigera** -ikon för uttrycket för **Bana1** bana.

![Demo](./images/joa2p3.png)

Navigera till i Datakällor till vänster **ExperiencePlatform.ProfileFieldGroup.profile.mobilePhone.number**. Du läser nu mobiltelefonnumret direkt från Adobe Experience Platform kundprofil i realtid.

![Demo](./images/joa3.png)

Markera fältet **Nummer** och sedan dra och släpp det på Villkorsytan.

Markera operatorn **är inte tom**. Klicka **OK**.

![Demo](./images/joa4.png)

Du kommer då att se det här. Klicka **OK**.

![Demo](./images/joa6.png)

Din resa kommer då att se ut så här. Klicka på **Åtgärder** enligt skärmbilden.

![Demo](./images/jod8.png)

Välj åtgärd **SMS** och sedan dra och släppa det efter villkoret du just lade till.

![Demo](./images/jod9.png)

Ange **Kategori** till **Marknadsföring** och välj en SMS-yta som gör att du kan skicka SMS. I det här fallet är e-postytan som ska väljas **SMS**.

![ACOP](./images/journeyactions1zy.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka **Redigera innehåll**.

![ACOP](./images/journeyactions2zy.png)

Nu visas meddelandekontrollpanelen, där du kan konfigurera texten i ditt SMS. Klicka på **Skriv meddelande** för att skapa meddelandet.

![Journey Optimizer](./images/sms3ab.png)

Ange följande text: `So warm, {{profile.person.name.firstName}}! 20% discount on swimwear today!`. Klicka **Spara**.

![Journey Optimizer](./images/sms4ab.png)

Du kommer då att se det här. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/sms4azzz.png)

Nu visas den slutförda åtgärden. Klicka **OK**.

![Demo](./images/jod17.png)

Gå tillbaka till den vänstra menyn **Åtgärder** väljer du funktionsmakrot `--demoProfileLdap--TextSlack`och sedan dra och släppa det efter **Meddelanden** åtgärd.

![Demo](./images/jod18.png)

Gå till **Åtgärdsparametrar** och klicka på **Redigera** ikon för parametern `TEXTTOSLACK`.

![Demo](./images/joa19zzz.png)

I popup-fönstret klickar du på **Avancerat läge**.

![Demo](./images/joa20.png)

Markera nedanstående kod, kopiera den och klistra in den i **Avancerad lägesredigerare**. Klicka **OK**.

`"So warm, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + "! 20% discount on swimwear today!"`

![Demo](./images/jod21.png)

Du kommer att se den slutförda åtgärden. Klicka **OK**.

![Demo](./images/jod22.png)

Den här vägen på resan är nu färdig.

## 8.4.5 Publicera din resa

Din resa är nu helt konfigurerad. Klicka **Publicera**.

![Demo](./images/jodone.png)

Klicka **Publicera** igen.

![Demo](./images/jopublish1.png)

Din resa är nu publicerad.

![Demo](./images/jopublish2.png)

Nästa steg: [8.5 Utlösa din resa](./ex5.md)

[Gå tillbaka till modul 8](journey-orchestration-external-weather-api-sms.md)

[Gå tillbaka till Alla moduler](../../overview.md)
