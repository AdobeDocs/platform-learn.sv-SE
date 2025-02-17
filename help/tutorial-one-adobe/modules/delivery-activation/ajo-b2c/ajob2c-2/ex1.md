---
title: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera en händelse
description: Adobe Journey Optimizer - External Weather API, SMS Action med mera
kt: 5342
doc-type: tutorial
exl-id: bde4290a-59d1-4471-83a7-1cad69f94ff1
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 0%

---

# 3.2.1 Definiera en händelse

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Bläddra nedåt på den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på knappen **Hantera** under **Händelser**.

![ACOP](./images/acopmenu.png)

Därefter visas en översikt över alla tillgängliga händelser. Klicka på **Skapa händelse** för att börja skapa en egen händelse.

![ACOP](./images/emptyevent.png)

Ett nytt, tomt händelsefönster öppnas sedan.
Använd `--aepUserLdap--GeofenceEntry` som namn för händelsen.

Ange Beskrivning till: `Geofence Entry Event`.

Kontrollera att **Type** är inställd på **Unitary** och välj **System Generated** för **Event ID Type** -valet.

![Demo](./images/evname.png)

Därefter måste du välja ett schema. Alla scheman som visas här är Adobe Experience Platform Schemas.

![Demo](./images/evschema.png)

Alla scheman visas inte. Det finns många fler scheman i Adobe Experience Platform.
Om du vill visa i den här listan måste ett schema ha en mycket specifik fältgrupp länkad till sig. Fältgruppen som behövs för att visas här kallas `Orchestration eventID`.

Låt oss snabbt se hur dessa scheman definieras i Adobe Experience Platform.

Gå till **Scheman** på den vänstra menyn och öppna den i en ny webbläsarflik. Gå till **Bläddra** i **Scheman** om du vill se listan över tillgängliga scheman.
Öppna schemat `Demo System - Event Schema for Website (Global v1.1)`.

![Datainmatning](./images/schemas.png)

När du har öppnat schemat ser du att fältgruppen `Orchestration eventID` är en del av schemat.
Den här fältgruppen har bara två fält, `_experience.campaign.orchestration.eventID` och `originJourneyID`.

![Datainmatning](./images/schemageo.png)

När den här fältgruppen och det här specifika händelse-ID-fältet är en del av ett schema blir det schemat tillgängligt för användning av Adobe Journey Optimizer.

Gå tillbaka till din eventkonfiguration i Adobe Journey Optimizer.

![Demo](./images/evschema.png)

I det här fallet vill du lyssna på en Geofence-händelse för att förstå om en kund finns på en viss plats, så välj nu schemat `Demo System - Event Schema for Website (Global v1.1)` som schema för händelsen.

![Demo](./images/evschema1.png)

Adobe Journey Optimizer väljer sedan automatiskt ut vissa obligatoriska fält, men du kan redigera de fält som är tillgängliga för Adobe Journey Optimizer.

Klicka på ikonen **penna** för att redigera fälten.

![Demo](./images/editfields.png)

Då visas ett popup-fönster med en schemahierarki där du kan välja fält.

![Demo](./images/popup.png)

Fält som ECID och Orchestration eventID är obligatoriska och som sådana är förmarkerade.

En marknadsförare måste dock ha flexibel åtkomst till alla datapunkter som ger kontext till en resa. Så vi ska åtminstone se till att markera följande fält (finns i kontextnoden Montera):

- Ort

När det är klart klickar du på **OK**.

![Demo](./images/popupok.png)

Adobe Journey Optimizer behöver också en identifierare som identifierar kunden. Eftersom Adobe Journey Optimizer är länkat till Adobe Experience Platform används den primära identifieraren för ett schema automatiskt som identifierare för resan.
Den primära identifieraren tar automatiskt hänsyn till Adobe Experience Platform fullständiga identitetsdiagram och länkar alla beteenden mellan alla tillgängliga identiteter, enheter och kanaler till samma profil, så att Adobe Journey Optimizer är sammanhangsberoende, relevant och konsekvent. Klicka på **Spara**.

![Demo](./images/eventidentifier.png)

Din aktivitet kommer sedan att ingå i listan över tillgängliga händelser.

![Demo](./images/eventlist.png)

Slutligen måste du återställa `Orchestration eventID` för din anpassade händelse.

Öppna aktiviteten igen genom att klicka på den i listan över händelser.
Klicka på ikonen **Visa nyttolast** bredvid **Fält** i din händelse.

![Demo](./images/fieldseyepayload.png)

Om du klickar på ikonen **Visa nyttolast** öppnas ett XDM-exempel för den här händelsen. Bläddra nedåt i **nyttolasten** tills du ser raden `eventID`.

![Demo](./images/fieldseyepayloadev.png)

Skriv ned `eventID` så som du behöver den i den sista versionen för att testa konfigurationen.

I det här exemplet är `eventID` `4df8dc10731eba7b0c37af83a9db38d4de7aa6aebcce38196d9d47929b9c598e`.

Du har definierat händelsen som ska utlösa resan vi bygger. När resan har utlösts kommer geofence-fälten, som City, och alla andra fält som du har valt (som Country, Latitude och Longitude) att göras tillgängliga för resan.

Som vi nämnt i fallbeskrivningen måste vi sedan erbjuda sammanhangsbaserade kampanjer som är beroende av vädret. För att få väderinformation måste vi definiera externa datakällor som ger oss väderinformation för den platsen. Du använder **OpenWeather API**-tjänsten för att förse oss med den informationen.

## Nästa steg

Gå till [3.2.2 Definiera en extern datakälla](./ex2.md){target="_blank"}

Gå tillbaka till [Adobe Journey Optimizer: Externa datakällor och anpassade åtgärder](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
