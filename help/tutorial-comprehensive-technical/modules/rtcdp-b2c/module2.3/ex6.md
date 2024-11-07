---
title: CDP i realtid - externa målgrupper
description: CDP i realtid - externa målgrupper
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1974'
ht-degree: 0%

---

# 2.3.6 Externa målgrupper

I många fall kanske ditt företag vill använda befintliga segment från andra program för att förbättra kundprofilen i Adobe Experience Platform.
Dessa externa målgrupper kan ha definierats baserat på en datavetenskapsmodell eller externa dataplattformar.

Med funktionen för externa målgrupper i Adobe Experience Platform kan ni fokusera på att ta in externa målgrupper och deras aktivering utan att behöva definiera om motsvarande segmentdefinition i detalj i Adobe Experience Platform.

Den övergripande processen är uppdelad i tre huvudsteg:

- Importera externa målgruppsmetadata: det här steget är avsett att importera externa målgruppsmetadata, som målgruppens namn, till Adobe Experience Platform.
- Tilldela det externa målgruppsmedlemskapet till kundprofilen: det här steget ska berika kundprofilen med det externa segmentmedlemskapsattributet.
- Skapa segmenten i Adobe Experience Platform: det här steget är tänkt att skapa åtgärdbara segment baserat på det externa målgruppsmedlemskapet.

## 2.3.6.1 Metadata

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

>[!IMPORTANT]
>
>Sandlådan som ska användas för den här övningen är ``--module2sandbox--``!

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--module2sandbox--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./images/sb1.png)

Medan segmentdata definierar villkoret för att en profil ska vara en del av ett segment, är segmentets metadata information om segmentet, till exempel namn, beskrivning och status för segmentet. När de externa målgruppsmetadata lagras i Adobe Experience Platform måste du använda ett identitetsnamnutrymme för att importera metadata i Adobe Experience Platform.

## 2.3.6.1.1 Identitetsnamnutrymme för externa målgrupper

Ett identitetsnamnområde har redan skapats för användning med **externa målgrupper**.
Om du vill visa identiteten som redan har skapats går du till **Identiteter** och söker efter **Extern**. Klicka på&quot;External Audiences&quot;.

Observera:

- Identitetssymbolen **externa målgrupper** används i nästa steg för att referera till den externa målgruppsidentiteten.
- Typen **Identifierare för icke-personer** används för det här identitetsnamnområdet, eftersom det här namnområdet inte är avsett att identifiera kundprofiler utan segment.

![Identitet för externa målgrupper](images/extAudIdNS.png)

## 2.3.6.1.2 Skapa ett schema med metadata för externa målgrupper

De externa målgruppsmetadata baseras på **segmentdefinitionsschemat**. Mer information finns i [XDM Github-databasen](https://github.com/adobe/xdm/blob/master/docs/reference/classes/segmentdefinition.schema.md).

Gå till Scheman på den vänstra menyn. Klicka på **+ Skapa schema** och sedan på **Bläddra**.

![Metadataschema för externa målgrupper 1](images/extAudMDXDM1.png)

Om du vill tilldela en klass söker du efter **segmentdefinitionen**. Markera klassen **Segmentdefinition** och klicka på **Tilldela klass**.

![Metadataschema för externa målgrupper 2](images/extAudMDXDM2.png)

Då ser du det här. Klicka på **Avbryt**.

![Metadataschema för externa målgrupper 3](images/extAudMDXDM3.png)

Då ser du det här. Markera fältet **_id**. Bläddra nedåt i den högra menyn och aktivera kryssrutorna **Identitet** och **Primär identitet**. Markera identitetsnamnområdet **Externa målgrupper**. Klicka på **Använd**.

![Metadataschema för externa målgrupper 4](images/extAudMDXDM4.png)

Välj sedan schemanamnet **Namnlöst schema**. Ändra namnet till `--aepUserLdap-- - External Audiences Metadata`.

![Metadata för externa målgrupper 5](images/extAudMDXDM5.png)

Aktivera alternativet **Profil** och bekräfta. Klicka slutligen på **Spara**.

![Metadata för externa målgrupper 5](images/extAudMDXDM6.png)

## 2.3.6.1.3 Skapa datamängden för metadata för externa målgrupper

Gå till **Bläddra** i **Scheman**. Sök och klicka på det `--aepUserLdap-- - External Audiences Metadata`-schema som du skapade i föregående steg. Klicka sedan på **Skapa datauppsättning från schema**.

![Metadata för externa målgrupper DS 1](images/extAudMDDS1.png)

Ange `--aepUserLdap-- - External Audience Metadata` för fältet **Namn**. Klicka på **Skapa datauppsättning**.

![Metadata för externa målgrupper DS 2](images/extAudMDDS2.png)

Då ser du det här. Glöm inte att aktivera växeln **Profil**!

![Metadata för externa målgrupper DS 3](images/extAudMDDS3.png)

## 2.3.6.1.4 Skapa en HTTP API Source Connection

Därefter måste du konfigurera HTTP API Source Connector som du använder för att importera metadata till datauppsättningen.

Gå till **Källor**. Ange **HTTP** i sökfältet. Klicka på **Lägg till data**.

![Metadata för externa målgrupper http 1](images/extAudMDhttp1.png)

Ange följande information:

- **Kontotyp**: välj **Nytt konto**
- **Kontonamn**: ange `--aepUserLdap-- - External Audience Metadata`
- Markera kryssrutan **XDM-kompatibel ruta**

Klicka sedan på **Anslut till källa**.

![Metadata för externa målgrupper http 2](images/extAudMDhttp2.png)

Då ser du det här. Klicka på **Nästa**.

![Metadata för externa målgrupper http 2](images/extAudMDhttp2a.png)

Välj **Befintlig datauppsättning** och sök efter och markera datauppsättningen `--aepUserLdap-- - External Audience Metadata` i listrutan.

Verifiera **dataflödesinformationen** och klicka sedan på **Nästa**.

![Metadata för externa målgrupper http: 3](images/extAudMDhttp3.png)

Då ser du det här.

Steget **Mappning** i guiden är tomt eftersom du kommer att hämta en XDM-kompatibel nyttolast till HTTP API Source Connector, så ingen mappning krävs. Klicka på **Nästa**.

![Metadata för externa målgrupper http: 3](images/extAudMDhttp3a.png)

I steget **Granska** kan du granska anslutningen och mappningsinformationen om du vill. Klicka på **Slutför**.

![Metadata för externa målgrupper http 4](images/extAudMDhttp4.png)

Då ser du det här.

![Metadata för externa målgrupper http 4](images/extAudMDhttp4a.png)

## 2.3.6.1.5 Metadata för externa målgrupper

På översiktsfliken för Source Connector klickar du på **..** och sedan på **Kopiera schemanyttolast**.

![Metadatastr 1](images/extAudMDstr1a.png) för externa målgrupper

Öppna textredigeringsprogrammet på datorn och klistra in den nyttolast som du just kopierade. Den ser ut så här. Därefter måste du uppdatera objektet **xdmEntity** i den här nyttolasten.

![Metadatastr 1](images/extAudMDstr1b.png) för externa målgrupper

Objektet **xdmEntity** måste ersättas med nedanstående kod. Kopiera koden nedan och klistra in den i textfilen genom att ersätta objektet **xdmEntity** i textredigeraren.

```
"xdmEntity": {
    "_id": "--aepUserLdap---extaudience-01",
    "description": "--aepUserLdap---extaudience-01 description",
    "segmentIdentity": {
      "_id": "--aepUserLdap---extaudience-01",
      "namespace": {
        "code": "externalaudiences"
      }
    },
    "segmentName": "--aepUserLdap---extaudience-01 name",
    "segmentStatus": "ACTIVE",
    "version": "1.0"
  }
```

Du bör då se det här:

![Metadatastr 1](images/extAudMDstr1.png) för externa målgrupper

Öppna sedan ett nytt **Terminal**-fönster. Kopiera all text i textredigeraren och klistra in den i terminalfönstret.

![Metadatastr 1](images/extAudMDstr1d.png) för externa målgrupper

Tryck sedan på **Enter**.

Sedan visas en bekräftelse på ditt datainmatningsproblem i terminalfönstret:

![Metadatastr 1](images/extAudMDstr1e.png) för externa målgrupper

Uppdatera skärmen för HTTP API Source Connector där du nu ser att data bearbetas:

![Metadatastr för externa målgrupper 2](images/extAudMDstr2.png)

## 2.3.6.1.6 Validera inmatning av metadata för externa målgrupper

När bearbetningen är klar kan du kontrollera datatillgängligheten i datauppsättningen med hjälp av frågetjänsten.

Gå till **Datauppsättningar** på den högra menyn och välj den `--aepUserLdap-- - External Audience Metadata` datauppsättning som du skapade tidigare.

![Metadatastr för externa målgrupper 3](images/extAudMDstr3.png)

Gå till Frågor på den högra menyn och klicka på **Skapa fråga**.

![Metadata för externa målgrupper 4](images/extAudMDstr4.png)

Ange följande kod och tryck sedan på **SKIFT + ENTER**:

```
select * from --aepUserLdap--_external_audience_metadata
```

I frågeresultatet ser du den externa målgruppens metadata som du har inkapslat.

![Metadatastr för externa målgrupper 5](images/extAudMDstr5.png)

## 2.3.6.2 Segmentmedlemskap

Med externa målgruppsmetadata tillgängliga kan ni nu importera segmentmedlemskapet för en viss kundprofil.

Nu måste du förbereda en profildatamängd som har anrikats mot segmentmedlemskapsschemat. Mer information finns i [XDM Github-databasen](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/segmentmembership.schema.md).

## 2.3.6.2.1 Skapa ett medlemsschema för externa målgrupper

Gå till **Scheman** på den högra menyn. Klicka på **Skapa schema** och sedan på **XDM-individuell profil**.

![Schema för externa målgruppsprofiler ](images/extAudPrXDM1.png)

I popup-fönstret **Lägg till fältgrupper** söker du efter **Profilkärna**. Välj fältgruppen **Profilkärna v2**.

![Schema för externa målgruppsprofiler ](images/extAudPrXDM2.png)

I popup-fönstret **Lägg till fältgrupper** söker du efter **Segmentmedlemskap**. Markera fältgruppen **Information om segmentmedlemskap**. Klicka sedan på **Lägg till fältgrupper**.

![Externt målgruppsprofilschema 3](images/extAudPrXDM3.png)

Då ser du det här. Navigera till fältet `--aepTenantId--.identification.core`. Klicka på fältet **crmId**. Bläddra nedåt i den högra menyn och markera kryssrutorna **Identitet** och **Primär identitet**. För **Identity Namespace** väljer du **Demo System - CRMID**.

Klicka på **Använd**.

![Externt målgruppsprofilschema 4](images/extAudPrXDM4.png)

Välj sedan schemanamnet **Namnlöst schema**. Ange `--aepUserLdap-- - External Audiences Membership` i fältet för visningsnamn.

![Externt målgruppsprofilschema 5](images/extAudPrXDM5a.png)

Aktivera sedan växlingsknappen **Profil** och bekräfta. Klicka på **Spara**.

![Externt målgruppsprofilschema 5](images/extAudPrXDM5.png)

## 2.3.6.2.2 Skapa datauppsättningen External Audiences Membership

Gå till **Bläddra** i **Scheman**. Sök och klicka på det `--aepUserLdap-- - External Audiences Membership`-schema som du skapade i föregående steg. Klicka sedan på **Skapa datauppsättning från schema**.

![Metadata för externa målgrupper DS 1](images/extAudPrDS1.png)

Ange `--aepUserLdap-- - External Audiences Membership` för fältet **Namn**. Klicka på **Skapa datauppsättning**.

![Metadata för externa målgrupper DS 2](images/extAudPrDS2.png)

Då ser du det här. Glöm inte att aktivera växeln **Profil**!

![Metadata för externa målgrupper DS 3](images/extAudPrDS3.png)

## 2.3.6.2.3 Skapa en HTTP API Source Connection


Därefter måste du konfigurera HTTP API Source Connector som du använder för att importera metadata till datauppsättningen.

Gå till **Källor**. Ange **HTTP** i sökfältet. Klicka på **Lägg till data**.

![Metadata för externa målgrupper http 1](images/extAudMDhttp1.png)

Ange följande information:

- **Kontotyp**: välj **Nytt konto**
- **Kontonamn**: ange `--aepUserLdap-- - External Audience Membership`
- Markera kryssrutan **XDM-kompatibel ruta**

Klicka sedan på **Anslut till källa**.

![Metadata för externa målgrupper http 2](images/extAudPrhttp2.png)

Då ser du det här. Klicka på **Nästa**.

![Metadata för externa målgrupper http 2](images/extAudPrhttp2a.png)

Välj **Befintlig datauppsättning** och sök efter och markera datauppsättningen `--aepUserLdap-- - External Audiences Membership` i listrutan.

Verifiera **dataflödesinformationen** och klicka sedan på **Nästa**.

![Metadata för externa målgrupper http: 3](images/extAudPrhttp3.png)

Då ser du det här.

Steget **Mappning** i guiden är tomt eftersom du kommer att hämta en XDM-kompatibel nyttolast till HTTP API Source Connector, så ingen mappning krävs. Klicka på **Nästa**.

![Metadata för externa målgrupper http: 3](images/extAudPrhttp3a.png)

I steget **Granska** kan du granska anslutningen och mappningsinformationen om du vill. Klicka på **Slutför**.

![Metadata för externa målgrupper http 4](images/extAudPrhttp4.png)

Då ser du det här.

![Metadata för externa målgrupper http 4](images/extAudPrhttp4a.png)

## 2.3.6.2.4 Information om medlemskap för externa målgrupper

På översiktsfliken för Source Connector klickar du på **..** och sedan på **Kopiera schemanyttolast**.

![Metadatastr 1](./images/extAudPrstr1a.png) för externa målgrupper

Öppna textredigeringsprogrammet på datorn och klistra in den nyttolast som du just kopierade. Den ser ut så här. Därefter måste du uppdatera objektet **xdmEntity** i den här nyttolasten.

![Metadatastr 1](images/extAudPrstr1b.png) för externa målgrupper

Objektet **xdmEntity** måste ersättas med nedanstående kod. Kopiera koden nedan och klistra in den i textfilen genom att ersätta objektet **xdmEntity** i textredigeraren.

```
  "xdmEntity": {
    "_id": "--aepUserLdap---profile-test-01",
    "_experienceplatform": {
      "identification": {
        "core": {
          "crmId": "--aepUserLdap---profile-test-01"
        }
      }
    },
    "personID": "--aepUserLdap---profile-test-01",
    "segmentMembership": {
      "externalaudiences": {
        "--aepUserLdap---extaudience-01": {
          "status": "realized",
          "lastQualificationTime": "2022-03-05T00:00:00Z"
        }
      }
    }
  }
```

Du bör då se det här:

![Metadatastr 1](images/extAudPrstr1.png) för externa målgrupper

Öppna sedan ett nytt **Terminal**-fönster. Kopiera all text i textredigeraren och klistra in den i terminalfönstret.

![Metadatastr 1](images/extAudPrstr1d.png) för externa målgrupper

Tryck sedan på **Enter**.

Sedan visas en bekräftelse på ditt datainmatningsproblem i terminalfönstret:

![Metadatastr 1](images/extAudPrstr1e.png) för externa målgrupper

Uppdatera skärmen för HTTP API Source Connector där du efter några minuter kommer att se att data bearbetas:

![Metadatastr för externa målgrupper 2](images/extAudPrstr2.png)

## 2.3.6.2.5 Validera externa målgruppers medlemskap

När bearbetningen är klar kan du kontrollera datatillgängligheten i datauppsättningen med hjälp av frågetjänsten.

Gå till **Datauppsättningar** på den högra menyn och välj den `--aepUserLdap-- - External Audiences Membership ` datauppsättning som du skapade tidigare.

![Metadatastr för externa målgrupper 3](images/extAudPrstr3.png)

Gå till Frågor på den högra menyn och klicka på **Skapa fråga**.

![Metadata för externa målgrupper 4](images/extAudPrstr4.png)

Ange följande kod och tryck sedan på **SKIFT + ENTER**:

```
select * from --aepUserLdap--_external_audiences_membership
```

I frågeresultatet ser du den externa målgruppens metadata som du har inkapslat.

![Metadatastr för externa målgrupper 5](images/extAudPrstr5.png)

## 2.3.6.3 Skapa ett segment

Nu är ni redo att agera utifrån de externa målgrupperna.
Adobe Experience Platform satsar på åtgärder genom att skapa segment, fylla respektive målgrupper och dela dessa målgrupper med målgrupperna.
Nu kan du skapa ett segment med hjälp av den externa målgrupp du just skapade.

Gå till **Segment** på den vänstra menyn och klicka på **Skapa segment**.

![Externa målgrupper SegBuilder 1](images/extAudSegUI2.png)

Gå till **Publiker**. Då ser du det här. Klicka på **Externa målgrupper**.

![Externa målgrupper SegBuilder 1](images/extAudSegUI2a.png)

Välj den externa målgrupp som du skapade tidigare, med namnet `--aepUserLdap---extaudience-01`. Dra och släpp målgruppen på arbetsytan.

![Externa målgrupper SegBuilder 1](images/extAudSegUI2b.png)

Ge segmentet ett namn, använd `--aepUserLdap-- - extaudience-01`. Klicka på **Spara och stäng**.

![Externa målgrupper SegBuilder 1](images/extAudSegUI1.png)

Då ser du det här. Du kommer också att märka att profilen som du importerade segmentmedlemskapet för nu visas i listan med **Exempelprofiler**.

![Externa målgrupper SegBuilder 1](images/extAudSegUI3.png)

Ditt segment är klart nu och kan skickas till en destination för aktivering.

## 2.3.6.4 Visualisera kundprofil

Nu kan du även visualisera segmentkvalificeringen i din kundprofil. Gå till **Profiler**, använd identitetsnamnrymden **Demo System - CRMID** och ange identiteten `--aepUserLdap---profile-test-01` som du använde som en del av övning 6.6.2.4, och klicka på **Visa**. Klicka sedan på **profil-ID** för att öppna profilen.

![Externa målgrupper SegBuilder 1](images/extAudProfileUI1.png)

Gå till **Segmentmedlemskap** där du ser din externa målgrupp visas.

![Externa målgrupper SegBuilder 1](images/extAudProfileUI2.png)

Nästa steg: [2.3.7 Destinations SDK](./ex7.md)

[Gå tillbaka till modul 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
