---
title: Datainsamling - FAC - Skapa scheman, datamodell och länkar
description: Foundation - FAC - Skapa scheman, datamodell och länkar
kt: 5342
doc-type: tutorial
exl-id: 42004cb9-60b3-4ca8-97d9-3d169735c98f
source-git-commit: 50622dc6698a7e1384c4803ea40682a060a08617
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# 3.1.2 Skapa scheman, datamodell och länkar

Nu kan du konfigurera din federerade databas i Adobe Experience Platform.

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./images/sb1.png)

## 3.1.2.1 Konfigurera en Federated databas i AEP

Klicka på **Federated databaser** på den vänstra menyn. Klicka sedan på **Lägg till federerad databas**.

![FAC](./images/fdb1.png)

Använd **Label** som `--aepUserLdap-- - CitiSignal Snowflake` och välj **Snowflake** som typ.

Under Mer information måste du fylla i dina inloggningsuppgifter, som ser ut så här:

![FAC](./images/fdb2.png)

**Server**:

Gå till **Admin > Konton** i Snowflake. Klicka på den 3 **..** bredvid ditt konto och klicka på **Hantera URL:er**.

![FAC](./images/fdburl1.png)

Då ser du det här. Kopiera den **aktuella URL:en** och klistra in den i fältet **Server** i AEP.

![FAC](./images/fdburl2.png)

**Användare**: det användarnamn du skapade tidigare, i övning 1.3.1.1
**Lösenord**: det lösenord du skapade tidigare, i övning 1.3.1.1
**Database**: use **CITISIGNAL**

Till slut borde du ha den här. Klicka på **Testa anslutning**. Om testet lyckas klickar du på **Distribuera funktioner**, som skapar funktioner på Snowflake-sidan som är nödvändiga för arbetsflödesmotorn.

När anslutningen har testats och funktioner har distribuerats lagras konfigurationen.

![FAC](./images/fdb3.png)

När du sedan går tillbaka till menyn **Federerade databaser** visas anslutningen där.

![FAC](./images/fdb4.png)

## 3.1.2.2 Skapa scheman i AEP

Klicka på **Modeller** på den vänstra menyn och gå sedan till **Scheman**. Klicka på **Skapa schema**.

![FAC](./images/fdb5.png)

Välj din federerade databas och klicka på **+ Lägg till tabeller**.

![FAC](./images/fdb6.png)

Då ser du det här. Markera de fem tabeller du har skapat i Snowflake tidigare:

- `--aepUserLdap--_HOUSEHOLDS`
- `--aepUserLdap--_MOBILE_DATA_USAGE`
- `--aepUserLdap--_MONTHLY_DATA_USAGE`
- `--aepUserLdap--_PERSONS`
- `--aepUserLdap--_USERS`

Klicka på **Lägg till**.

![FAC](./images/fdb7.png)

AEP läser sedan in informationen för varje tabell och visar den i användargränssnittet.

För varje tabell kan du:

- ändra schemats etikett
- lägg till en beskrivning
- byta namn på alla fält och ange deras synlighet
- välj primärnyckel för schemat

För denna övning behövs inga ändringar.

Klicka på **Skapa**.

![FAC](./images/fdb8.png)

Då ser du det här. Du kan klicka på ett schema och granska informationen. Klicka till exempel på **—aepUserLdap—_PERSONS**.

![FAC](./images/fdb9.png)

Du kommer då att se detta med möjlighet att redigera konfigurationen. Klicka på **Data** om du vill visa ett exempel på data som finns i Snowflake-databasen.

![FAC](./images/fdb10.png)

Sedan visas ett exempel på data.

![FAC](./images/fdb11.png)

## 3.1.2.3 Skapa en modell i AEP

Gå till **Modeller** på den vänstra menyn och gå sedan till **Datamodell**. Klicka på **Skapa datamodell**.

![FAC](./images/fdb12.png)

Använd `--aepUserLdap-- - CitiSignal Snowflake Data Model` för etiketten. Klicka på **Skapa**.

![FAC](./images/fdb13.png)

Klicka på **Lägg till scheman**.

![FAC](./images/fdb14.png)

Markera dina scheman och klicka på **Lägg till**.

![FAC](./images/fdb15.png)

Då ser du det här. Klicka på **Spara**.

### `--aepUserLdap--_USERS` - `--aepUserLdap--_PERSONS`

Nu kan du börja definiera länkar mellan scheman. Om du vill börja definiera en länk måste du klicka på **Skapa länkar**.

![FAC](./images/fdb16.png)

Först definierar vi länken mellan tabellen `--aepUserLdap--_USERS` och `--aepUserLdap--_PERSONS`.

Klicka på **Lägg till**.

![FAC](./images/fdb18.png)


### `--aepUserLdap--_HOUSEHOLDS` - `--aepUserLdap--_PERSONS`

Du kommer då tillbaka hit. Klicka på **Skapa länkar** om du vill skapa en annan länk.

![FAC](./images/fdb17.png)

Sedan definierar vi länken mellan tabellen `--aepUserLdap--_HOUSEHOLDS` och `--aepUserLdap--_PERSONS`.

![FAC](./images/fdb19.png)

### `--aepUserLdap--_USERS` - `--aepUserLdap--_MONTHLY_DATA_USAGE`

Du kommer då tillbaka hit. Klicka på **Skapa länkar** om du vill skapa en annan länk.

![FAC](./images/fdb20.png)

Sedan definierar vi länken mellan tabellen `--aepUserLdap--_USERS` och `--aepUserLdap--_MONTHLY_DATA_USAGE`.

![FAC](./images/fdb21.png)


### `--aepUserLdap--_USERS` - `--aepUserLdap--_HOUSEHOLDS`

Du kommer då tillbaka hit. Klicka på **Skapa länkar** om du vill skapa en annan länk.

![FAC](./images/fdb22.png)

Sedan definierar vi länken mellan tabellen `--aepUserLdap--_USERS` och `--aepUserLdap--_HOUSEHOLDS`.

![FAC](./images/fdb23.png)

### `--aepUserLdap--_USERS` - `--aepUserLdap--_MOBILE_DATA_USAGE`

Du kommer då tillbaka hit. Klicka på **Skapa länkar** om du vill skapa en annan länk.

![FAC](./images/fdb24.png)

Sedan definierar vi länken mellan tabellen `--aepUserLdap--_USERS` och `--aepUserLdap--_MOBILE_DATA_USAGE`.

![FAC](./images/fdb25.png)

Du borde se det här då. Klicka på **Spara**.

![FAC](./images/fdb26.png)

Din konfiguration i AEP är nu klar. Nu kan ni börja använda era federerade data i en federerad målgruppskomposition.

Nästa steg: [3.1.3 Skapa en federerad komposition](./ex3.md)

[Gå tillbaka till modul 3.1](./fac.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
