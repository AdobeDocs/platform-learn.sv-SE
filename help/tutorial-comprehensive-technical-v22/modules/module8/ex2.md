---
title: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera en extern datakälla
description: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera en extern datakälla
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: e3e04415-4258-4ad7-a227-0e68dfcba235
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 1%

---

# 8.2 Definiera en extern datakälla

I den här övningen skapar du en anpassad extern datakälla genom att använda Adobe Journey Optimizer.

Logga in på Adobe Journey Optimizer genom att gå till [Adobe Experience Cloud](https://experience.adobe.com). Klicka **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Du omdirigeras till **Startsida**  i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas anropas `--aepSandboxId--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och välj sandlådan i listan. I det här exemplet heter sandlådan **AEP-aktivering FY22**. Då är du i **Startsida** vy över din sandlåda `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

Bläddra nedåt i den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på **Hantera** knapp under **Datakällor**.

![Demo](./images/menudatasources.png)

Då ser du **Datakällor** lista.
Klicka **Skapa datakälla** för att börja lägga till datakällan.

![Demo](./images/dshome.png)

En tom popup-meny för datakälla visas.

![Demo](./images/emptyds.png)

Innan du kan börja konfigurera detta behöver du ett konto hos **Öppna väderkarta** service. Följ de här stegen för att skapa ditt konto och hämta API-nyckeln.

Gå till [https://openweathermap.org/](https://openweathermap.org/). På hemsidan klickar du på **Logga in**.

![WeatherMap](./images/owm.png)

Klicka **Skapa ett konto**.

![WeatherMap](./images/owm1.png)

Fyll i detaljerna.

![WeatherMap](./images/owm2.png)

Klicka **Skapa konto**.

![WeatherMap](./images/owm3.png)

Du omdirigeras sedan till din kontosida.

![WeatherMap](./images/owm4.png)

Klicka på **API-nycklar** för att hämta API-nyckeln, som du måste konfigurera din anpassade externa datakälla för.

![WeatherMap](./images/owm5.png)

An **API-nyckel** ser ut så här: `b2c4c36b6bb59c3458d6686b05311dc3`.

Du hittar **API-dokumentation** för **Aktuellt väder** [här](https://openweathermap.org/current).

I vårt fall kommer vi att implementera kopplingen till Open Weather Map baserat på den stad kunden är i.

![WeatherMap](./images/owm6.png)

Gå tillbaka till **Adobe Journey Optimizer** till tomma **Extern datakälla** popup.

![Demo](./images/emptyds.png)

Använd som namn för datakällan `--demoProfileLdap--WeatherApi`. I det här exemplet är datakällans namn `vangeluwWeatherApi `.

Ange Beskrivning till: `Access to the Open Weather Map`.

URL:en för Open Weather Map API är: **http://api.openweathermap.org/data/2.5/weather?units=metric**

![Demo](./images/dsname.png)

Därefter måste du välja den autentisering som ska användas.

Använd dessa variabler:

| Fält | Värde |
|:-----------------------:| :-----------------------|
| Typ | **API-nyckel** |
| Namn | **APPID** |
| Värde | **din API-nyckel** |
| Plats | **Frågeparameter** |

![Demo](./images/dsauth.png)

Slutligen måste du definiera en **FieldGroup**, vilket i princip är den begäran du kommer att skicka till väder-API:t. I vårt fall vill vi använda namnet på staden för att begära Aktuellt väder för den staden.

![Demo](./images/fg.png)

Enligt Weather API Documentation måste vi skicka en parameter `q=City`.

![Demo](./images/owmapi.png)

För att matcha förväntad API-begäran konfigurerar du FieldGroup enligt följande:

>[!IMPORTANT]
>
>Fältgruppnamnet måste vara unikt. Använd den här namnkonventionen: `--demoProfileLdap--WeatherByCity` så i det här fallet ska namnet `vangeluwWeatherByCity`

![Demo](./images/fg1.png)

För svarsnyttolasten måste du klistra in ett exempel på det svar som ska skickas av väder-API:t.

Du hittar det förväntade API JSON-svaret på API-dokumentationssidan [här](https://openweathermap.org/current).

![Demo](./images/owmapi1.png)

Du kan också kopiera JSON-svaret härifrån:

```json
{"coord": { "lon": 139,"lat": 35},
  "weather": [
    {
      "id": 800,
      "main": "Clear",
      "description": "clear sky",
      "icon": "01n"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 281.52,
    "feels_like": 278.99,
    "temp_min": 280.15,
    "temp_max": 283.71,
    "pressure": 1016,
    "humidity": 93
  },
  "wind": {
    "speed": 0.47,
    "deg": 107.538
  },
  "clouds": {
    "all": 2
  },
  "dt": 1560350192,
  "sys": {
    "type": 3,
    "id": 2019346,
    "message": 0.0065,
    "country": "JP",
    "sunrise": 1560281377,
    "sunset": 1560333478
  },
  "timezone": 32400,
  "id": 1851632,
  "name": "Shuzenji",
  "cod": 200
}
```

Kopiera JSON-svaret ovan till Urklipp och gå sedan till konfigurationsskärmen för din anpassade datakälla.

Klicka på **Redigera nyttolast** ikon.

![Demo](./images/owmapi2.png)

Ett popup-fönster visas där du nu måste klistra in ovanstående JSON-svar.

![Demo](./images/owmapi3.png)

Klistra in ditt JSON-svar, därefter ser du detta. Klicka **Spara**.

![Demo](./images/owmapi4.png)

Din anpassade konfiguration av datakälla har slutförts. Bläddra uppåt och klicka **Spara**.

![Demo](./images/dssave.png)

Datakällan har skapats och är en del av **Datakällor** lista.

![Demo](./images/dslist.png)

Nästa steg: [8.3 Definiera en anpassad åtgärd](./ex3.md)

[Gå tillbaka till modul 8](journey-orchestration-external-weather-api-sms.md)

[Gå tillbaka till Alla moduler](../../overview.md)
