---
title: CDP i realtid - destinationer SDK
description: CDP i realtid - destinationer SDK
kt: 5342
doc-type: tutorial
exl-id: c18acbf5-92f5-4cd2-a5aa-a5e9debb98c9
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# 2.3.6 Destinationer SDK

## Konfigurera ditt Adobe I/O-projekt

I den här övningen kommer du att använda Adobe I/O igen för att ställa frågor till Adobe Experience Platform API:er. Om du inte har konfigurerat ditt Adobe I/O-projekt ännu går du tillbaka till [Exercise 3 i Module 2.1](../rtcdpb2c-1/ex3.md) och följer instruktionerna där.

>[!IMPORTANT]
>
>Om du är Adobe-anställd följer du instruktionerna här för att använda [PostBuster](./../../../../modules/getting-started/gettingstarted/ex8.md).

## Autentisering till Adobe I/O

I den här övningen kommer du att använda Postman igen för att ställa frågor till Adobe Experience Platform API:er. Om du inte har konfigurerat ditt Postman-program ännu går du tillbaka till [Exercise 3 i Module 2.1](../rtcdpb2c-1/ex3.md) och följer instruktionerna där.

>[!IMPORTANT]
>
>Om du är Adobe-anställd följer du instruktionerna här för att använda [PostBuster](./../../../../modules/getting-started/gettingstarted/ex8.md).

## Definiera slutpunkt och format

För den här övningen behöver du en slutpunkt för att konfigurera så att kvalificeringshändelsen kan direktuppspelas till den slutpunkten när en målgrupp kvalificerar sig. I den här övningen använder du en exempelslutpunkt med [https://pipedream.com/requestbin](https://pipedream.com/requestbin). Gå till [https://pipedream.com/requestbin](https://pipedream.com/requestbin), skapa ett konto och skapa sedan en arbetsyta. När arbetsytan har skapats ser du något liknande.

Klicka på **kopiera** för att kopiera URL:en. Du måste ange den här URL:en i nästa övning. URL:en i det här exemplet är `https://eodts05snjmjz67.m.pipedream.net`.

![Datainmatning](./images/webhook1.png)

När det gäller formatet kommer vi att använda en standardmall som strömmar målgruppskvalifikationer eller icke-kvalifikationer tillsammans med metadata som kundidentifierare. Mallar kan anpassas så att de uppfyller förväntningarna för specifika slutpunkter, men i den här övningen återanvänder vi en standardmall, vilket resulterar i en sådan här nyttolast som kommer att direktuppspelas till slutpunkten.

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

## Skapa en server- och mallkonfiguration

Det första steget för att skapa ett eget mål i Adobe Experience Platform är att skapa en server- och mallkonfiguration med Postman.

Det gör du genom att öppna ditt Postman-program och gå till **Målredigerings-API**, till **Målservrar och mallar** och klicka för att öppna begäran **POST - Skapa en målserverkonfiguration**.

>[!NOTE]
>
>Om du inte har den Postman-samlingen går du tillbaka till [Exercise 3 i Module 2.1](../rtcdpb2c-1/ex3.md) och följer instruktionerna där för att konfigurera Postman med de medföljande Postman-samlingarna.

Då ser du det här. Under **Sidhuvuden** måste du uppdatera värdet för nyckeln **x-sandbox-name** manuellt och ange den till `--aepSandboxName--`. Välj värdet **{{SANDBOX_NAME}}**.

![Datainmatning](./images/sdkpm1.png)

Ersätt den med `--aepSandboxName--`.

![Datainmatning](./images/sdkpm2.png)

Gå sedan till **Brödtext**. välj platshållaren **{{body}}**.

![Datainmatning](./images/sdkpm3.png)

Du måste nu ersätta platshållaren **{{body}}** med följande kod:

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

När du har klistrat in ovanstående kod måste du uppdatera fältet **urlBasedDestination.url.value** manuellt, och du måste ange det till webbadressen för den webkrok du skapade i det föregående steget, som var `https://eodts05snjmjz67.m.pipedream.net` i det här exemplet.

![Datainmatning](./images/sdkpm4.png)

När fältet **urlBasedDestination.url.value** har uppdaterats bör det se ut så här. Klicka på **Skicka**.

![Datainmatning](./images/sdkpm5.png)

>[!NOTE]
>
>Glöm inte att du måste ha en giltig `access_token` innan du skickar en begäran till Adobe I/O. Om du vill hämta en giltig `access_token` kör du begäran **POST - Get Access Token** i samlingen **Adobe IO - OAuth**.

När du har klickat på **Skicka** skapas servermallen och som en del av svaret visas ett fält med namnet **instanceId**. Skriv ned det så som du behöver det i nästa steg. I det här exemplet är **instanceId**
`52482c90-8a1e-42fc-b729-7f0252e5cebd`.

![Datainmatning](./images/sdkpm6.png)

## Skapa din destinationskonfiguration

I Postman, under **Målredigerings-API**, går du till **Målkonfigurationer** och klickar för att öppna begäran **POST - Skapa en målkonfiguration**. Då ser du det här. Under **Sidhuvuden** måste du uppdatera värdet för nyckeln **x-sandbox-name** manuellt och ange den till `--aepSandboxName--`. Markera värdet **{{SANDBOX_NAME}}** och ersätt det med `--aepSandboxName--`.

![Datainmatning](./images/sdkpm7.png)

Gå sedan till **Brödtext**. välj platshållaren **{{body}}**.

![Datainmatning](./images/sdkpm9.png)

Du måste nu ersätta platshållaren **{{body}}** med följande kod:

```json
{
    "name": "--aepUserLdap-- - Webhook",
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
        "documentationLink": "https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=sv-SE",
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

![Datainmatning](./images/sdkpm11.png)

När du har klistrat in ovanstående kod måste du uppdatera fältet **destinationDelivery manuellt. destinationServerId**, och du måste ange det till **instanceId** för målservermallen som du skapade i föregående steg, som var `52482c90-8a1e-42fc-b729-7f0252e5cebd` i det här exemplet. Klicka sedan på **Skicka**.

![Datainmatning](./images/sdkpm10.png)

Du kommer då att se det här svaret.

![Datainmatning](./images/sdkpm12.png)

Målet har skapats i Adobe Experience Platform. Vi går dit och kollar det.

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Gå till **Destinationer** på den vänstra menyn, klicka på **Katalog** och bläddra nedåt till kategorin **Direktuppspelning**. Du kommer att se ditt mål där nu.

![Datainmatning](./images/destsdk1.png)

## Länka målgruppen till er målgrupp

I **Destinationer** > **Katalog** klickar du på **Konfigurera** på destinationen för att börja lägga till målgrupper till det nya målet.

![Datainmatning](./images/destsdk2.png)

Ange ett slumpmässigt värde för **innehavartoken**, som **1234**. Klicka på **Anslut till mål**.

![Datainmatning](./images/destsdk3.png)

Då ser du det här. Använd `--aepUserLdap-- - Webhook` som namn på målet. Välj en valfri slutpunkt, i det här exemplet **EU**. Klicka på **Nästa**.

![Datainmatning](./images/destsdk4.png)

Du kan också välja en datastyrningspolicy. Klicka på **Nästa**.

![Datainmatning](./images/destsdk5.png)

Välj målgruppen som du skapade tidigare, med namnet `--aepUserLdap-- - Interest in Galaxy S24`. Klicka på **Nästa**.

![Datainmatning](./images/destsdk6.png)

Då ser du det här. Se till att mappa **SOURCE FIELD** `--aepTenantId--.identification.core.ecid` till fältet `Identity: ecid`. Klicka på **Nästa**.

![Datainmatning](./images/destsdk7.png)

Klicka på **Slutför**.

![Datainmatning](./images/destsdk8.png)

Din destination är nu live, nya målgruppskvalifikationer kommer att strömmas till din anpassade webkrok nu.

![Datainmatning](./images/destsdk9.png)

## Testa målgruppsaktiveringen

Gå till [https://dsn.adobe.com](https://dsn.adobe.com). När du har loggat in med din Adobe ID ser du det här. Klicka på de tre punkterna **..** i webbplatsprojektet och klicka sedan på **Kör** för att öppna det.

![DSN](./../../datacollection/dc1.1/images/web8.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje övning måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](../../../getting-started/gettingstarted/images/web7.png)

I det här exemplet vill du svara en viss kund som tittar på en viss produkt.
Gå till **Telefoner och enheter** på startsidan för **Citi Signal** och klicka på produkten **Galaxy S24**.

![Datainmatning](./images/homegalaxy.png)

Produktsidan för Galaxy S24 har nu visats, så din målgrupp kvalificerar sig för din profil under de följande minuterna.

![Datainmatning](./images/homegalaxy1.png)

När du öppnar profilvisningsprogrammet och går till **Publiker** får du se målgruppen kvalificera sig.

![Datainmatning](./images/homegalaxydsdk.png)

Gå nu tillbaka till din öppna webbkrok på [https://eodts05snjmjz67.m.pipedream.net](https://eodts05snjmjz67.m.pipedream.net), där du bör se en ny inkommande begäran, som kommer från Adobe Experience Platform och som innehåller publikens kvalificeringshändelse.

![Datainmatning](./images/destsdk10.png)

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [CDP i realtid - Bygg en målgrupp och vidta åtgärder](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
