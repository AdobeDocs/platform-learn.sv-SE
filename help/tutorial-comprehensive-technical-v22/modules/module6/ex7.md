---
title: CDP i realtid - Destinations SDK
description: CDP i realtid - Destinations SDK
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 9585f858-569b-421e-a21d-aa623cd6c819
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 0%

---

# 6.7 Destinations-SDK

## 6.7.1 Konfigurera ditt Adobe I/O-projekt

>[!IMPORTANT]
>
>Om du har skapat ditt Adobe I/O-projekt efter december 2021 kan du återanvända det projektet, hoppa över den här övningen och gå direkt till övning 6.7.2.
>
>Om du skapade ditt Adobe I/O-projekt före december 2021 skapar du ett nytt projekt som är kompatibelt med API:t för målredigering.

I den här övningen kommer du att använda Adobe I/O intensivt för att ställa frågor mot plattformens API:er. Följ stegen nedan för att konfigurera Adobe I/O.

Gå till [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)

![Adobe I/O New Integration](../module3/images/iohome.png)

Se till att du väljer rätt Adobe Experience Platform-instans i skärmens övre högra hörn. Din instans är `--envName--`.

![Adobe I/O New Integration](../module3/images/iocomp.png)

Klicka **Skapa nytt projekt**.

![Adobe I/O New Integration](../module3/images/adobe_io_new_integration.png) eller
![Adobe I/O New Integration](../module3/images/adobe_io_new_integration1.png)

Välj **+ Lägg till i projekt** och markera **API**.

![Adobe I/O New Integration](../module3/images/adobe_io_access_api.png)

Då ser du det här:

![Adobe I/O New Integration](../module3/images/api1.png)

Klicka på **Adobe Experience Platform** ikon.

![Adobe I/O New Integration](../module3/images/api2.png)

Klicka **Experience Platform API**.

![Adobe I/O New Integration](../module3/images/api3.png)

Klicka på **Nästa**.

![Adobe I/O New Integration](../module3/images/next.png)

Nu kan du välja att antingen låta Adobe I/O generera ditt nyckelpar eller överföra ett befintligt.

Välj **Alternativ 1 - Generera ett nyckelpar**.

![Adobe I/O New Integration](../module3/images/api4.png)

Klicka **Generera nyckelpar**.

![Adobe I/O New Integration](../module3/images/generate.png)

Du får se en snurra i cirka 30 sekunder.

![Adobe I/O New Integration](../module3/images/spin.png)

Du kommer då att se detta och det nyckelpar som genereras kommer att laddas ned som en zip-fil: **config.zip**.

Zippa upp filen **config.zip** på skrivbordet visas två filer:

![Adobe I/O New Integration](../module3/images/zip.png)

- **certificate_pub.crt** är ditt certifikat för offentlig nyckel. Ur säkerhetssynpunkt är detta det certifikat som fritt används för att konfigurera integreringar med onlineprogram.
- **private.key** är din privata nyckel. Det här ska aldrig delas med någon. Den privata nyckeln är det du använder för att autentisera din API-implementering och ska vara en hemlighet. Om du delar din privata nyckel med vem som helst kan de komma åt implementeringen och missbruka API:t för att importera skadliga data till Platform och extrahera alla data som finns i Platform.

![Adobe I/O New Integration](../module3/images/config.png)

Spara **config.zip** på en säker plats, eftersom du behöver detta för nästa steg och för framtida åtkomst till API:er för Adobe I/O och Adobe Experience Platform.

Klicka på **Nästa**.

![Adobe I/O New Integration](../module3/images/next.png)

Du måste nu välja **Produktprofil(er)** för er integrering.

Välj önskade produktprofiler.

**FYI**: i din Adobe Experience Platform-instans kommer produktprofilerna att ha ett annat namn. Du måste välja minst en produktprofil med rätt åtkomsträttigheter, som är konfigurerad i Adobe Admin Console.

![Adobe I/O New Integration](../module3/images/api9.png)

Klicka **Spara konfigurerat API**.

![Adobe I/O New Integration](../module3/images/saveconfig.png)

Du får se en snurra i några sekunder.

![Adobe I/O New Integration](../module3/images/api10.png)

Och sedan ser du integreringen.

![Adobe I/O New Integration](../module3/images/api11.png)

Klicka på **Ladda ned för Postman** och klicka sedan på **Tjänstkonto (JWT)** för att ladda ned en Postman-miljö (vänta tills miljön har laddats ned kan det ta några sekunder).

![Adobe I/O New Integration](../module3/images/iopm.png)

Bläddra nedåt tills du ser **Tjänstkonto (JWT)**, där du hittar all integreringsinformation som används för att konfigurera integreringen med Adobe Experience Platform.

![Adobe I/O New Integration](../module3/images/api12.png)

IO-projektet har för närvarande ett generiskt namn. Du måste ge integreringen ett eget namn. Klicka på **Projekt 1** (eller liknande namn) som anges

![Adobe I/O New Integration](../module3/images/api13.png)

Klicka **Redigera projekt**.

![Adobe I/O New Integration](../module3/images/api14.png)

Ange ett namn och en beskrivning för integreringen. Som namnkonvention kommer vi att använda `AEP API --demoProfileLdap--`. Ersätt ldap med din ldap.
Om din ldap till exempel är vangeluw blir namnet och beskrivningen av din integrering AEP API-vangeluw.

Retur `AEP API --demoProfileLdap--` som **Projektets titel**. Klicka **Spara**.

![Adobe I/O New Integration](../module3/images/api15.png)

Integreringen av Adobe I/O är nu klar.

![Adobe I/O New Integration](../module3/images/api16.png)

## 6.7.2 Postman-autentisering till Adobe I/O

Gå till [https://www.getpostman.com/](https://www.getpostman.com/).

Klicka på **Kom igång**.

![Adobe I/O New Integration](../module3/images/getstarted.png)

Ladda sedan ned och installera Postman.

![Adobe I/O New Integration](../module3/images/downloadpostman.png)

Starta programmet när du har installerat Postman.

I Postman finns det två koncept: Miljöer och samlingar.

- Miljön innehåller alla dina miljövariabler som är mer eller mindre konsekventa. I miljön hittar du saker som IMSOrg i vår plattformsmiljö, tillsammans med säkerhetsreferenser som din privata nyckel och andra. Miljöfilen är den du laddade ned under installationen av Adobe I/O i den tidigare övningen, den har följande namn: **service.postman_environment.json**.

- Samlingen innehåller ett antal API-begäranden som du kan använda. Vi kommer att använda 2 samlingar
   - 1 samling för autentisering till Adobe I/0
   - 1 Samling för övningar i denna modul
   - 1 samling för övningarna i Real-Time CDP-modulen, för målredigering

Hämta filen [postman.zip](../../assets/postman/postman_profile.zip) till din lokala dator.

I den här **postman.zip** hittar du följande filer:

- `_Adobe I-O - Token.postman_collection.json`
- `_Adobe Experience Platform Enablement.postman_collection.json`
- `Destination_Authoring_API.json`

Zippa upp **postman.zip** lagra dessa tre filer i en mapp på skrivbordet tillsammans med den nedladdade Postman-miljön från Adobe I/O. Du måste ha dessa fyra filer i den mappen:

![Adobe I/O New Integration](../module3/images/pmfolder.png)

Gå tillbaka till Postman. Klicka **Importera**.

![Adobe I/O New Integration](../module3/images/postmanui.png)

Klicka **Överför filer**.

![Adobe I/O New Integration](../module3/images/choosefiles.png)

Navigera till den mapp på skrivbordet där du extraherade de 4 hämtade filerna. Markera de här fyra filerna samtidigt och klicka på **Öppna**.

![Adobe I/O New Integration](../module3/images/selectfiles.png)

Efter att ha klickat **Öppna** visas en översikt över den miljö och de samlingar du håller på att importera. Klicka **Importera**.

![Adobe I/O New Integration](../module3/images/impconfirm.png)

Nu har du allt du behöver i Postman för att börja interagera med Adobe Experience Platform via API:erna.

Det första du behöver göra är att se till att du är rätt autentiserad. Du måste begära en åtkomsttoken för att kunna autentiseras.

Kontrollera att du har valt rätt miljö innan du kör någon begäran. Du kan kontrollera den valda miljön genom att verifiera listrutan Miljö i det övre högra hörnet.

Den valda miljön ska ha ett namn som liknar det här:

![Postman](../module3/images/envselemea.png)

Klicka på **ögat** ikonen och klicka sedan på **Redigera** om du vill uppdatera den privata nyckeln i miljöfilen.

![Postman](../module3/images/gear.png)

Du kommer då att se det här. Alla fält är förifyllda, utom fältet **PRIVATE_KEY**.

![Postman](../module3/images/pk2.png)

Den privata nyckeln har genererats när du skapade ditt Adobe I/O-projekt. Den hämtades som en zip-fil med namnet **config.zip**. Extrahera zip-filen till skrivbordet.

![Postman](../module3/images/pk3.png)

Öppna mappen **config** och öppna filen **private.key** med valfri textredigerare.

![Postman](../module3/images/pk4.png)

Du kommer då att se något liknande, kopiera all text till Urklipp.

![Postman](../module3/images/pk5.png)

Gå tillbaka till Postman och klistra in den privata nyckeln i fälten bredvid variabeln **PRIVATE_KEY**, för båda kolumnerna **URSPRUNGLIGT VÄRDE** och **AKTUELLT VÄRDE**. Klicka **Spara**.

![Postman](../module3/images/pk6.png)

Din Postman-miljö och dina samlingar är nu konfigurerade och fungerar. Nu kan du autentisera från Postman till Adobe I/O.

För att göra det måste du läsa in ett externt bibliotek som hanterar kryptering och dekryptering av kommunikation. Om du vill läsa in det här biblioteket måste du köra begäran med namnet **INIT: Läs in krypteringsbibliotek för RS256**. Välj den här förfrågan i **Adobe I/O - tokensamling** och du ser den mitt på skärmen.

![Postman](../module3/images/iocoll.png)

![Postman](../module3/images/cryptolib.png)

Klicka på den blå **Skicka** -knappen. Efter några sekunder visas ett svar i **Brödtext** i Postman:

![Postman](../module3/images/cryptoresponse.png)

Med kryptobiblioteket inläst kan vi autentisera till Adobe I/O.

I **\_Adobe I/O - Token-samling** markerar du begäran med namnet **IMS: JWT Generate + Auth**. Återigen visas informationen om begäran mitt på skärmen.

![Postman](../module3/images/ioauth.png)

Klicka på den blå **Skicka** -knappen. Efter några sekunder visas ett svar i **Brödtext** i Postman:

![Postman](../module3/images/ioauthresp.png)

Om konfigurationen lyckades bör du se ett liknande svar som innehåller följande information:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| token_type | **innehavare** |
| access_token | **eyJ4NXUiOiJpbXNfbmEx...QT7mqZkumN1tdsPEioOEl4087Dg** |
| förfaller_in | **86399973** |

Adobe I/O har gett dig en **innehavare**-token, med ett specifikt värde (denna mycket långa åtkomsttoken) och ett förfallofönster.

Den token vi har fått gäller nu i 24 timmar. Det innebär att om du efter 24 timmar vill använda Postman för att autentisera till Adobe I/O måste du generera en ny token genom att köra denna begäran igen.

## 6.7.3 Definiera slutpunkt och format

För den här övningen behöver du en slutpunkt för att konfigurera så att kvalificeringshändelsen kan direktuppspelas till den slutpunkten när ett segment kvalificerar sig. I den här övningen ska du använda en exempelslutpunkt med [https://webhook.site/](https://webhook.site/). Gå till [https://webhook.site/](https://webhook.site/)där du ser något liknande. Klicka **Kopiera till Urklipp** för att kopiera URL:en. Du måste ange den här URL:en i nästa övning. URL:en i det här exemplet är `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a`.

![Dataintag](./images/webhook1.png)

När det gäller formatet kommer vi att använda en standardmall som direktuppspelar segmentens kvalifikationer eller kvalifikationer tillsammans med metadata som kundidentifierare. Mallar kan anpassas så att de uppfyller förväntningarna för specifika slutpunkter, men i den här övningen återanvänder vi en standardmall, vilket resulterar i en sådan här nyttolast som kommer att direktuppspelas till slutpunkten.

```json
{
  "profiles": [
    {
      "identities": [
        {
          "type": "ecid",
          "id": "64626768309422151580190219823409897678"
        }
      ],
      "AdobeExperiencePlatformSegments": {
        "add": [
          "f58c723c-f1e5-40dd-8c79-7bb4ab47f041"
        ],
        "remove": []
      }
    }
  ]
}
```

## 6.7.4 Skapa en server- och mallkonfiguration

Det första steget för att skapa ett eget mål i Adobe Experience Platform är att skapa en server- och mallkonfiguration.

Om du vill göra det går du till **API för målredigering**, till **Målservrar och mallar** och klicka för att öppna begäran **POST - Skapa en målserverkonfiguration**. Du kommer då att se det här. Under **Sidhuvuden** måste du uppdatera värdet för nyckeln manuellt **x-sandbox-name** och ange `--aepSandboxId--`. Välj värdet **{{SANDBOX_NAME}}**.

![Dataintag](./images/sdkpm1.png)

Ersätt den med `--aepSandboxId--`.

![Dataintag](./images/sdkpm2.png)

Nästa, gå till **Brödtext**. markera platshållaren **{{body}}**.

![Dataintag](./images/sdkpm3.png)

Nu måste du ersätta platshållaren **{{body}}** efter koden nedan:

```json
{
    "name": "Custom HTTP Destination",
    "destinationServerType": "URL_BASED",
    "urlBasedDestination": {
        "url": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "yourURL"
        }
    },
    "httpTemplate": {
        "httpMethod": "POST",
        "requestBody": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{\n    \"profiles\": [\n    {%- for profile in input.profiles %}\n        {\n            \"identities\": [\n            {%- for idMapEntry in profile.identityMap -%}\n            {%- set namespace = idMapEntry.key -%}\n                {%- for identity in idMapEntry.value %}\n                {\n                    \"type\": \"{{ namespace }}\",\n                    \"id\": \"{{ identity.id }}\"\n                }{%- if not loop.last -%},{%- endif -%}\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\n            {% endfor %}\n            ],\n            \"AdobeExperiencePlatformSegments\": {\n                \"add\": [\n                {%- for segment in profile.segmentMembership.ups | added %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ],\n                \"remove\": [\n                {#- Alternative syntax for filtering segments by status: -#}\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ]\n            }\n        }{%- if not loop.last -%},{%- endif -%}\n    {% endfor %}\n    ]\n}"
        },
        "contentType": "application/json"
    }
}
```

När du har klistrat in koden ovan måste du uppdatera fältet manuellt **urlBasedDestination.url.value** och du måste ange den till webbadressen för den webkrok du skapade i föregående steg, som `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a` i det här exemplet.

![Dataintag](./images/sdkpm4.png)

När fältet har uppdaterats **urlBasedDestination.url.value**, det borde se ut så här. Klicka **Skicka**.

![Dataintag](./images/sdkpm5.png)

Efter klickning **Skicka** skapas servermallen och som en del av svaret visas ett fält med namnet **instanceId**. Skriv ned det så som du behöver det i nästa steg. I det här exemplet **instanceId** är
`eb0f436f-dcf5-4993-a82d-0fcc09a6b36c`.

![Dataintag](./images/sdkpm6.png)

## 6.7.5 Skapa en destinationskonfiguration

I Postman, under **API för målredigering**, gå till **Målkonfigurationer** och klicka för att öppna begäran **POST - Skapa en målkonfiguration**. Du kommer då att se det här. Under **Sidhuvuden** måste du uppdatera värdet för nyckeln manuellt **x-sandbox-name** och ange `--aepSandboxId--`. Välj värdet **{{SANDBOX_NAME}}**.

![Dataintag](./images/sdkpm7.png)

Ersätt den med `--aepSandboxId--`.

![Dataintag](./images/sdkpm8.png)

Nästa, gå till **Brödtext**. markera platshållaren **{{body}}**.

![Dataintag](./images/sdkpm9.png)

Nu måste du ersätta platshållaren **{{body}}** efter koden nedan:

```json
{
    "name": "--demoProfileLdap-- - Webhook",
    "description": "Exports segment qualifications and identities to a custom webhook via Destination SDK.",
    "status": "TEST",
    "customerAuthenticationConfigurations": [
        {
            "authType": "BEARER"
        }
    ],
    "customerDataFields": [
        {
            "name": "endpointsInstance",
            "type": "string",
            "title": "Select Endpoint",
            "description": "We could manage several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
            "isRequired": true,
            "enum": [
                "US",
                "EU",
                "APAC",
                "NZ"
            ]
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en",
        "category": "streaming",
        "connectionType": "Server-to-server",
        "frequency": "Streaming"
    },
    "identityNamespaces": {
        "ecid": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": false
        }
    },
    "segmentMappingConfig": {
        "mapExperiencePlatformSegmentName": true,
        "mapExperiencePlatformSegmentId": true,
        "mapUserInput": false
    },
    "aggregation": {
        "aggregationType": "BEST_EFFORT",
        "bestEffortAggregation": {
            "maxUsersPerRequest": "1000",
            "splitUserById": false
        }
    },
    "schemaConfig": {
        "profileRequired": false,
        "segmentRequired": true,
        "identityRequired": true
    },
    "destinationDelivery": [
        {
            "authenticationRule": "NONE",
            "destinationServerId": "yourTemplateInstanceID"
        }
    ]
}
```

![Dataintag](./images/sdkpm11.png)

När du har klistrat in koden ovan måste du uppdatera fältet manuellt **destinationDelivery. destinationServerId**, och du måste ange det till **instanceId** för målservermallen som du skapade i föregående steg, som `eb0f436f-dcf5-4993-a82d-0fcc09a6b36c` i det här exemplet. Nästa, klicka **Skicka**.

![Dataintag](./images/sdkpm10.png)

Du kommer då att se det här svaret.

![Dataintag](./images/sdkpm12.png)

Målet har skapats i Adobe Experience Platform. Vi går dit och kollar det.

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Dataintag](../module2/images/sb1.png)

Gå till den vänstra menyn **Destinationer**, klicka **Katalog** och rulla ned till kategorin **Direktuppspelning**. Du kommer att se ditt mål där nu.

![Dataintag](./images/destsdk1.png)

## 6.7.6 Länka segmentet till målplatsen

I **Destinationer** > **Katalog**, klicka **Konfigurera** på destinationen för att börja lägga till segment till den nya destinationen.

![Dataintag](./images/destsdk2.png)

Ange en oanvändbar innehavartoken, som **1234**. Klicka **Anslut till mål**.

![Dataintag](./images/destsdk3.png)

Du kommer då att se det här. Använd `--demoProfileLdap-- - Webhook`. Välj en valfri slutpunkt, i det här exemplet **EU**. Klicka på **Nästa**.

![Dataintag](./images/destsdk4.png)

Du kan också välja en datastyrningspolicy. Klicka på **Nästa**.

![Dataintag](./images/destsdk5.png)

Markera segmentet som du skapade tidigare och som har namnet `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Klicka på **Nästa**.

![Dataintag](./images/destsdk6.png)

Du kommer då att se det här. Se till att mappa **KÄLLFÄLT** `--aepTenantId--.identification.core.ecid` till fältet `Identity: ecid`. Klicka på **Nästa**.

![Dataintag](./images/destsdk7.png)

Klicka **Slutför**.

![Dataintag](./images/destsdk8.png)

Din destination är nu aktiv, nya segmentkvalifikationer kommer att strömmas till din anpassade webkrok nu.

![Dataintag](./images/destsdk9.png)

## 6.7.7 Testa aktiveringen av segmentet

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](../module0/images/web8.png)

Nu kan du följa nedanstående flöde för att komma åt webbplatsen. Klicka **Integreringar**.

![DSN](../module0/images/web1.png)

På **Integreringar** måste du välja den datainsamlingsegenskap som skapades i övning 0.1.

![DSN](../module0/images/web2.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../module0/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../module0/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../module0/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../module0/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje demonstration måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](../module0/images/web7.png)

Från **Luma** startsida, gå till **Män** och klicka på produkten **PROTEUS FITNESS JACKSHIRT**.

![Dataintag](./images/homenadia.png)

Du har nu besökt produktsidan för **PROTEUS FITNESS JACKSHIRT**, vilket innebär att du nu är berättigad till det segment du skapade tidigare i den här övningen.

![Dataintag](./images/homenadiapp.png)

När du öppnar profilvisningsprogrammet går du till **Segment** ser du att segmentet är kvalificerat.

![Dataintag](./images/homenadiapppb.png)

Gå tillbaka till din öppna webkrok på [https://webhook.site/](https://webhook.site/), där du ska se en ny inkommande begäran som kommer från Adobe Experience Platform och som innehåller segmentkvalificeringshändelsen.

![Dataintag](./images/destsdk10.png)

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 6](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../overview.md)
