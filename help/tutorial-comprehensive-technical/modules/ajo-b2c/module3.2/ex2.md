---
title: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera en extern datakälla
description: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera en extern datakälla
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# 3.2.2 Definiera en extern datakälla

I den här övningen skapar du en anpassad extern datakälla genom att använda Adobe Journey Optimizer.

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och väljer sandlådan i listan. I det här exemplet heter sandlådan **AEP Enablement FY22**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

Bläddra nedåt på den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på knappen **Hantera** under **Datakällor**.

![Demo](./images/menudatasources.png)

Sedan visas listan **Datakällor**.
Klicka på **Skapa data-Source** för att börja lägga till din datakälla.

![Demo](./images/dshome.png)

En tom popup-meny för datakälla visas.

![Demo](./images/emptyds.png)

Innan du kan börja konfigurera det här behöver du ett konto för tjänsten **Open Weather Map**. Följ de här stegen för att skapa ditt konto och hämta API-nyckeln.

Gå till [https://openweathermap.org/](https://openweathermap.org/). Klicka på **Logga in** på hemsidan.

![WeatherMap](./images/owm.png)

Klicka på **Skapa ett konto**.

![WeatherMap](./images/owm1.png)

Fyll i detaljerna.

![WeatherMap](./images/owm2.png)

Klicka på **Skapa konto**.

![WeatherMap](./images/owm3.png)

Du omdirigeras sedan till din kontosida.

![WeatherMap](./images/owm4.png)

Klicka på **API-nycklar** på menyn för att hämta API-nyckeln som du måste konfigurera din anpassade externa datakälla för.

![WeatherMap](./images/owm5.png)

En **API-nyckel** ser ut så här: `b2c4c36b6bb59c3458d6686b05311dc3`.

Du hittar **API-dokumentationen** för **Aktuellt väder** [här](https://openweathermap.org/current).

I vårt fall kommer vi att implementera kopplingen till Open Weather Map baserat på den stad kunden är i.

![WeatherMap](./images/owm6.png)

Gå tillbaka till **Adobe Journey Optimizer**, till den tomma popup-menyn **Externa data i Source**.

![Demo](./images/emptyds.png)

Använd `--aepUserLdap--WeatherApi` som namn för datakällan. I det här exemplet är datakällans namn `vangeluwWeatherApi `.

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

Slutligen måste du definiera en **FieldGroup**, vilket i princip är den begäran du skickar till väder-API:t. I vårt fall vill vi använda namnet på staden för att begära Aktuellt väder för den staden.

![Demo](./images/fg.png)

Enligt Weather API-dokumentationen måste vi skicka en parameter `q=City`.

![Demo](./images/owmapi.png)

För att matcha förväntad API-begäran konfigurerar du FieldGroup enligt följande:

>[!IMPORTANT]
>
>Fältgruppnamnet måste vara unikt. Använd den här namnkonventionen: `--aepUserLdap--WeatherByCity` så i det här fallet ska namnet vara `vangeluwWeatherByCity`

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

Klicka på ikonen **Redigera nyttolast** .

![Demo](./images/owmapi2.png)

Du ser ett popup-fönster där du nu måste klistra in ovanstående JSON-svar.

![Demo](./images/owmapi3.png)

Klistra in ditt JSON-svar, därefter ser du detta. Klicka på **Spara**.

![Demo](./images/owmapi4.png)

Din anpassade konfiguration av datakälla är nu klar. Bläddra uppåt och klicka på **Spara**.

![Demo](./images/dssave.png)

Datakällan har skapats och ingår i listan **Datakällor**.

![Demo](./images/dslist.png)

Nästa steg: [3.2.3 Definiera en anpassad åtgärd](./ex3.md)

[Gå tillbaka till modul 3.2](journey-orchestration-external-weather-api-sms.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
