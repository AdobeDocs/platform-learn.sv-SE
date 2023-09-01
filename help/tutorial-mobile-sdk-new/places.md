---
title: Platser
description: Lär dig hur du använder platsens geopositioneringstjänst i din mobilapp.
hide: true
source-git-commit: c31dd74cf8ff9c0856b29e82d9c8be2ad027df4a
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---

# Platser

Lär dig hur du använder geopositioneringstjänsten i din app.

Tjänsten Adobe Experience Platform Data Collection Places är en tjänst för geolokalisering som gör att mobilappar med platsmedvetenhet kan förstå platskontexten. Tjänsten använder avancerade och lättanvända SDK-gränssnitt tillsammans med en flexibel databas med intressepunkter (POI).

## Förutsättningar

* Alla paketberoenden finns på plats i Xcode-projektet.
* Registrerade tillägg i AppDelegate.
* MobileCore har konfigurerats för att använda ditt utvecklingsprogram-ID.
* Importerade SDK:er.
* Programmet har skapats och körts med ändringarna ovan.

## Utbildningsmål

I den här lektionen ska du

* Lär dig hur du definierar intressepunkter i tjänsten Platser.
* Uppdatera taggegenskapen med tillägget Platser.
* Uppdatera ditt schema för att hämta geopositioneringshändelser.
* Validera inställningar i Assurance.
* Uppdatera appen så att den innehåller tillägget Platser.
* Implementera geopositioneringsspårning från tjänsten Platser i din app.


## Förutsättningar

* Programmet har skapats och körts med rätt SDK installerat och konfigurerat.


## Utbildningsmål

I den här lektionen ska du

* Uppdatera Edge-konfigurationen för beslutshantering.
* Uppdatera taggegenskapen med tillägget Journey Optimizer - Decisioning.
* Uppdatera ditt schema för att hämta offerthändelser.
* Validera inställningar i Assurance.
* Skapa ett offertbeslut baserat på erbjudanden från Journey Optimizer - Beslutshantering.
* Uppdatera appen så att den innehåller tillägget Optimizer.
* Implementera erbjudanden från Beslutshantering i appen.


## Inställningar

För att platstjänsten ska fungera i din app och i Mobile SDK måste du göra några inställningar.

### Definiera platser

Du definierar några intressepunkter i tjänsten Platser.

1. I gränssnittet för datainsamling väljer du **[!UICONTROL Platser]**.
1. Välj ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg).
1. Välj **[!UICONTROL Hantera bibliotek]**.
   ![Hantera bibliotek](assets/places-manage-libraries.png)
1. I **[!UICONTROL Hantera bibliotek]** dialogruta, välja **[!UICONTROL Nytt]**.
1. I **[!UICONTROL Skapa bibliotek]** dialogruta **[!UICONTROL Namn]**, till exempel `Luma`.
1. Välj **[!UICONTROL Bekräfta]**.
   ![Skapa bibliotek](assets/places-create-library.png)
1. Stäng **[!UICONTROL Hantera bibliotek]** dialogruta, välja **[!UICONTROL Stäng]**.
1. Tillbaka in **[!UICONTROL POI-hantering]**, markera **[!UICONTROL Importera POI]**.
1. Välj **[!UICONTROL Starta]** t**[!UICONTROL Importera platser]**.
1. Välj **[!UICONTROL Luma]** från listan över bibliotek,
1. Välj **[!UICONTROL Nästa]**.
   ![Välj bibliotek](assets/places-import-select-library.png)
1. Ladda ned [Luma POIs ZIP-fil](assets/luma_pois.csv.zip) och extrahera den till en plats på datorn.
1. I **[!UICONTROL Importera platser]** dialogruta, dra och släppa den extraherade `luma_pois.csv` fil till **[!UICONTROL Välj CSV-fil - dra och släpp filen]**. Du borde se **[!UICONTROL Verifieringen lyckades]** - **[!UICONTROL CSV-filen har verifierats]**.
1. Välj **[!UICONTROL Starta import]**. Du borde se **[!UICONTROL Lyckades]** - **[!UICONTROL 6 nya POI har lagts till]**.
1. Välj **[!UICONTROL Klar]**.
1. I **[!UICONTROL POI-hantering]** ser du att sex nya Luma-butiker läggs till i listan. Du kan växla mellan ![Lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) lista och ![Karta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MapView_18_N.svg) kartvy.
   ![Platslista](assets/places-list.png).


### Tillägg för Installera platser

1. Navigera till **[!UICONTROL Taggar]** och hitta din mobila taggegenskap och öppna egenskapen.
1. Välj **[!UICONTROL Tillägg]**.
1. Välj **[!UICONTROL Katalog]**.
1. Sök efter **[!UICONTROL Adobe Journey Optimizer - beslut]** tillägg.
1. Installera tillägget. Tillägget kräver ingen ytterligare konfiguration.

   ![Lägg till beslutstillägg](assets/tag-places-extension.png)

1. I **[!UICONTROL Installera tillägg]** dialog:
   1. Välj **[!UICONTROL Luma]** från **[!UICONTROL Välj ett bibliotek]** lista.
   1. Se till att du har valt ditt arbetsbibliotek, till exempel **[!UICONTROL Inledande bygge]**.
   1. Välj **[!UICONTROL Spara i bibliotek och bygge]** från **[!UICONTROL Spara i bibliotek]**.
      ![Tillägg för Installera platser](assets/places-install-extension.png).

1. Ditt bibliotek återskapas.


### Verifiera ditt schema

Verifiera om ditt schema, enligt definitionen i [Skapa schema](create-schema.md), innehåller de fältgrupper och klasser som krävs för att samla in POI- och geolokaliseringsdata.

1. Navigera till användargränssnittet för datainsamling och välj **[!UICONTROL Scheman]** från den vänstra listen.
1. Välj **[!UICONTROL Bläddra]** i det övre fältet.
1. Välj ditt schema för att öppna det.
1. Välj **[!UICONTROL Consumer Experience Event]**.
1. Du ser en **[!UICONTROL placeContext]** objekt med objekt och fält för inhämtning av POI-interaktion och geopositioneringsdata.
   ![Schemaplatser](assets/schema-places-context.png).


### Uppdatera din tagg

Tillägget Platser innehåller funktioner för att övervaka geopositioneringshändelser och gör att du kan utlösa åtgärder som baseras på dessa händelser. Du kan använda den här funktionen för att minimera API-kodningen som du måste implementera i appen.

**Dataelement**

Först skapar du flera dataelement.

1. Gå till taggegenskapen i användargränssnittet för datainsamling.
1. Välj **[!UICONTROL Dataelement]** från den vänstra listen.
1. Välj **[!UICONTROL Lägg till dataelement]**.
1. I **[!UICONTROL Skapa dataelement]** screen, ange ett namn, till exempel `Name - Entered`.
1. Välj **[!UICONTROL Platser]** från **[!UICONTROL Tillägg]** lista.
1. Välj **[!UICONTROL Namn]** från **[!UICONTROL Dataelementtyp]** lista.
1. Välj **[!UICONTROL Aktuell POI]**under **[!UICONTROL MÅL]**.
1. Välj **[!UICONTROL Spara i bibliotek]**.
   ![Dataelement](assets/tags-create-data-element.png)

1. Upprepa steg 4-8 med hjälp av informationen från tabellen nedan för att skapa ytterligare dataelement.

   | Namn | Tillägg | Dataelementtyp | MÅL |
   |---|---|---|---|
   | `Name - Exited` | Platser | Namn | Senaste utgångna POI |
   | `Category - Current` | Platser | Kategori | Aktuell POI |
   | `Category - Exited` | Platser | Kategori | Senaste utgångna POI |
   | `City - Current` | Platser | Ort | Aktuell POI |
   | `City - Exited` | Platser | Ort | Senaste utgångna POI |

   Du bör ha följande lista över dataelement.

   ![Lista över dataelement](assets/tags-data-elements-list.png)

**Regler**

Nu ska du definiera regler för dessa dataelement.

1. Välj **[!UICONTROL Regler]** från den vänstra listen.
1. Välj **[!UICONTROL Lägg till regel]**.
1. I **[!UICONTROL Skapa regel]** på skärmen, ange ett namn för regeln, till exempel `POI - Entry`.
1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) under **[!UICONTROL HÄNDELSER]**.
   1. Välj **[!UICONTROL Platser]** från **[!UICONTROL Tillägg]** lista och markera **[!UICONTROL Ange POI]** från **[!UICONTROL Händelsetyp]** lista.
   1. Välj **[!UICONTROL Behåll ändringar]**.
      ![Tagg-händelse](assets/tags-event-mobile-core.png).
1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) under **[!UICONTROL ÅTGÄRDER]**.
   1. Välj **[!UICONTROL Mobile Core]** från **[!UICONTROL Tillägg]** lista, välj **[!UICONTROL Bifoga data]** från **[!UICONTROL Åtgärdstyp]** lista. Den här åtgärden kopplar nyttolastdata.
   1. I **[!UICONTROL JSON-nyttolast]**, klistra in följande nyttolast:

      ```json
      {
          "xdm": {
              "eventType": "location.entry",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Current%%}"
                  },
                  "POIinteraction": {
                      "poiDetail": {
                          "name": "{%%Name - Current%%}",
                          "category": "{%%Category - Current%%}"
                      },
                      "poiEntries": {
                          "value": 1
                      }
                  }
              }
          }
      }
      ```

      The `{%% ... %%}` Du kan också enkelt infoga värden genom att välja ![Data](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) bredvid dialogrutan och välja ett dataelement från dialogrutan.

   1. Välj **[!UICONTROL Behåll ändringar]**.
      ![Tagg, åtgärd](assets/tags-action-mobile-core.png)

1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) bredvid **[!UICONTROL Mobile Core - bifoga data]** åtgärd.
   1. Välj **[!UICONTROL Adobe Experience Platform Edge Network]** från **[!UICONTROL Tillägg]** lista och markera **[!UICONTROL Vidarebefordra händelse till Edge Network]**. Den här åtgärden ser till att händelsen och ytterligare nyttolastdata vidarebefordras till Edge-nätverket.
   1. Välj **[!UICONTROL Behåll ändringar]**.

1. Spara regeln genom att välja **[!UICONTROL Spara i bibliotek]**.

   ![Regel](assets/tags-rule-poi-entry.png)

Låt oss skapa en annan regel

1. I **[!UICONTROL Skapa regel]** på skärmen, ange ett namn för regeln, till exempel `POI - Exit`.
1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) under **[!UICONTROL HÄNDELSER]**.
   1. Välj **[!UICONTROL Platser]** från **[!UICONTROL Tillägg]** lista och markera **[!UICONTROL Ange POI]** från **[!UICONTROL Händelsetyp]** lista.
   1. Välj **[!UICONTROL Behåll ändringar]**.
1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) under **[!UICONTROL ÅTGÄRDER]**.
   1. Välj **[!UICONTROL Mobile Core]** från **[!UICONTROL Tillägg]** lista, välj **[!UICONTROL Bifoga data]** från **[!UICONTROL Åtgärdstyp]** lista.
   1. I **[!UICONTROL JSON-nyttolast]**, klistra in följande nyttolast:

      ```json
      {
          "xdm": {
              "eventType": "location.exit",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Exited%%}"
                  },
                  "POIinteraction": {
                      "poiExits": {
                          "value": 1
                      },
                      "poiDetail": {
                          "name": "{%%Name - Exited%%}",
                          "category": "{%%Category - Exited%%}"
                      }
                  }
              }
          }
      }
      ```

   1. Välj **[!UICONTROL Behåll ändringar]**.

1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) bredvid **[!UICONTROL Mobile Core - bifoga data]** åtgärd.
   1. Välj **[!UICONTROL Adobe Experience Platform Edge Network]** från **[!UICONTROL Tillägg]** lista och markera **[!UICONTROL Vidarebefordra händelse till Edge Network]**.
   1. Välj **[!UICONTROL Behåll ändringar]**.


För att säkerställa att alla ändringar i taggen publiceras

1. Välj **[!UICONTROL Inledande bygge]** som det bibliotek som ska byggas.
1. Välj **[!UICONTROL Bygge]**.
   ![Bygg bibliotek](assets/tags-build-library.png)




## Validera inställningar i Assurance

Så här validerar du inställningarna i Assurance:

1. Gå till försäkringsgränssnittet.
1. Om den inte redan finns i den vänstra listen. välj **[!UICONTROL Konfigurera]** i vänster rand och välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) nästa **[!UICONTROL Händelser]** och **[!UICONTROL Karta och simulera]** under **[!UICONTROL PLATSTJÄNST]**.
1. Välj **[!UICONTROL Spara]**.
1. Välj **[!UICONTROL Karta och simulera]** till vänster.
1. Välj en av POI:erna som definieras i tjänsten Platser och välj sedan i popup-fönstret ![Kugghjul](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) **[!UICONTROL Simulera anmälningshändelse]**.
   ![Simulera anmälningshändelse](assets/places-simulate.png)
1. Välj **[!UICONTROL Händelser]** från vänster spår och du bör se de händelser som du simulerade.
   ![Validering av AJO-beslut](assets/places-events.png)


## Implementera platser i din app

Som tidigare nämnts tillhandahåller installation av ett mobiltaggtillägg bara konfigurationen. Därefter måste du installera och registrera Places SDK. Om de här stegen inte är tydliga går du igenom [Installera SDK:er](install-sdks.md) -avsnitt.

>[!NOTE]
>
>Om du har slutfört [Installera SDK:er](install-sdks.md) , är platsens SDK redan installerat och du kan hoppa över det här steget.
>

1. I Xcode kontrollerar du att [AEP-platser](https://github.com/adobe/aepsdk-places-ios) läggs till i listan över paket i paketberoenden. Se [Swift Package Manager](install-sdks.md#swift-package-manager).
1. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** i Xcode Project-navigatorn.
1. Säkerställ `AEPPlaces` är en del av din lista över importer.

   `import AEPPlaces`

1. Säkerställ `Places.self` är en del av den array med tillägg som du registrerar.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. Navigera till Luma > Luma > Utils > MobileSDK i Xcode-projektnavigeraren och hitta den asynkrona funktionen processRegionEvent(regionEvent: PlacesRegionEvent, forRegion region: CLRegion). Den här funktionen är en wrapper runt [`Places.processRegionEvent`](https://developer.adobe.com/client-sdks/documentation/places/api-reference/#processregionevent) API.
1. Navigera till Luma > Luma > Vyer > Plats > GeofenceSheet i Xcodes projektnavigerare.

   1. Ange följande kod för anmälningsknappen

   ```swift
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .entry, forRegion: region)
   }
   ```

   1. Ange följande kod för knappen Avsluta:

   ```swift
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .exit, forRegion: region)
   }
   ```

Det handlar inte bara om självstudiekursen för att förklara hur positionshanteraren implementeras i iOS.


## Validera med din app

1. Öppna appen på en enhet eller i simulatorn.

1. Gå till **[!UICONTROL Plats]** -fliken.

1. Flytta runt kartan för att säkerställa att den blå cirkeln i mitten ligger ovanpå en av dina POI:n, till exempel London.

1. Tryck på den blå <img src="assets/geobutton.png" width="20" /> tills du ser kategorin och namnet längst ned till höger.

1. Tryck på etiketten för POI, som öppnar bladet Nearby POI.

   <img src="assets/appgeolocation.png" width="300" />

1. Tryck på knapparna Ingång eller Avsluta för att simulera geopositioneringshändelser från appen.

   <img src="assets/appentryexit.png" width="300" />

1. Du bör se händelserna i försäkringsgränssnittet.



## Nästa steg

Nu bör du ha alla verktyg som behövs för att börja lägga till fler funktioner i geopositioneringsfunktionerna i appen. När du har vidarebefordrat händelserna till Edge Network och via din datastream till Experience Platform bör du se upplevelsehändelserna som visas för profilen som används i appen. Dessa upplevelsehändelser kan användas för att utlösa resor i Journey Optimizer (se [push-meddelande](journey-optimizer-inapp.md) och [meddelanden i appen](journey-optimizer-push.md) med Journey Optimizer). Det vanliga exemplet med att skicka ett push-meddelande till din appanvändare när någon kommer in på en fysisk lagringsplats.

Du har sett en implementering av funktionalitet för din app, som huvudsakligen styrs av platstjänsten och dataelement och regler som du definierade i taggegenskapen. Du kan också implementera samma funktioner direkt i programmet med [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API (se [Händelser](events.md) för mer information) med en XDM-nyttolast som innehåller ett populerat placeContext-objekt.

>[!SUCCESS]
>
>Du har nu aktiverat appen för geopositioneringstjänster med tillägget Platser i Experience Platform Mobile SDK.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Mappa data till Adobe Analytics](analytics.md)**
