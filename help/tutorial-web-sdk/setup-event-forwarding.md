---
title: Konfigurera en egenskap för vidarebefordring av händelser
description: Lär dig hur du använder händelsevidarebefordringsegenskap med Experience Platform Web SDK-data. Den här lektionen är en del av självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Event Forwarding
exl-id: 5a306609-2c63-42c1-8beb-efa412b8efe4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 0%

---

# Konfigurera en egenskap för vidarebefordring av händelser

Lär dig hur du använder händelsevidarebefordringsegenskap med Experience Platform Web SDK-data.

Vidarebefordran av händelser är en ny typ av egenskap som är tillgänglig i datainsamling. Med händelsevidarebefordran kan du skicka data till andra leverantörer än Adobe direkt från Adobe Experience Platform Edge Network i stället för till den traditionella webbläsaren på klientsidan. Läs mer om fördelarna med vidarebefordran av händelser i [Översikt över vidarebefordran av händelser](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en).

Om du vill använda händelsevidarebefordran i Adobe Experience Platform måste data skickas till Adobe Experience Platform Edge Network först med ett eller flera av följande tre alternativ:

* [Webb-SDK för Adobe Experience Platform](overview.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
<!--* [Server-to-Server API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)-->


>[!NOTE]
>Platform Web SDK och Platform Mobile SDK kräver inte distribution via taggar, men du bör använda taggar för att distribuera dessa SDK:er.

När du är klar med de tidigare lektionerna i den här självstudiekursen bör du skicka data till Platform Edge Network med Web SDK. När data finns i Platform Edge Network kan du aktivera vidarebefordran av händelser och använda en händelsevidarebefordringsegenskap för att skicka data till lösningar utanför Adobe.

## Utbildningsmål

I slutet av lektionen kan du:

* Skapa en egenskap för vidarebefordran av händelser
* Länka en händelsevidarebefordringsegenskap till ett Platform Web SDK-datalager
* Förstå skillnaderna mellan taggegenskapens dataelement och regler och händelsevidarebefordringens egenskapselement och regler
* Skapa ett dataelement för vidarebefordran av händelser
* Konfigurera en regel för vidarebefordran av händelser
* Verifiera att en händelsevidarebefordringsegenskap har skickat data


## Förutsättningar

* En programlicens som innehåller vidarebefordran av händelser. Vidarebefordran av händelser är en betalfunktion i datainsamling. Kontakta kontoteamet på Adobe för mer information.
* Vidarebefordran av händelser är aktiverat i din Experience Cloud-organisation.
* Användarbehörighet för vidarebefordran av händelser. (tum [Admin Console](https://adminconsole.adobe.com/), under Adobe Experience Platform Launch-produkten, behörighetsobjekt för[!UICONTROL Plattformar] > [!UICONTROL Edge] och alla [!UICONTROL Egendomsrättigheter]). När du fått det bör du se [!UICONTROL Vidarebefordran av händelser] i den vänstra navigeringen i gränssnittet för datainsamling:
   ![Egenskaper för vidarebefordran av händelser](assets/event-forwarding-menu.png)

* Adobe Experience Platform Web eller Mobile SDK har konfigurerats för att skicka data till Edge Network. Du måste ha slutfört följande lektioner i den här självstudiekursen:

   * Inledande konfiguration

      * [Konfigurera behörigheter](configure-permissions.md)
      * [Konfigurera ett XDM-schema](configure-schemas.md)
      * [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
      * [Konfigurera ett datastream](configure-datastream.md)
   * Tagginställningar

      * [Installera Web SDK-tillägg](install-web-sdk.md)
      * [Skapa dataelement](create-data-elements.md)
      * [Skapa en taggregel](create-tag-rule.md)
      * [Validera med Adobe Experience Platform debugger](validate-with-debugger.md)



## Skapa en egenskap för vidarebefordran av händelser

Börja med att skapa en händelsevidarebefordringsegenskap:

1. Öppna [Gränssnitt för datainsamling](https://experience.adobe.com/#/data-collection)
1. Välj **[!UICONTROL Vidarebefordran av händelser]** från vänster navigering
1. Välj **[!UICONTROL Ny egenskap]**.
   ![Egenskaper för vidarebefordran av händelser](assets/event-forwarding-new.png)

1. Namnge egenskapen. I detta fall `Server-Side - Web SDK Course`

1. Välj **[!UICONTROL Spara]**.
   ![spara händelsevidarebefordringsegenskap](assets/event-forwarding-save.png)

## Konfigurera datastream

För att händelsevidarebefordran ska kunna använda data som du skickar till Edge-nätverket måste du länka den nyligen skapade händelsevidarebefordringsegenskapen till samma dataström som används för att skicka data till Adobe-lösningar.

Så här konfigurerar du Target i datastream:

1. Gå till [Datainsamling](https://experience.adobe.com/#/data-collection)Gränssnittet {target=&quot;blank&quot;}
1. Välj **[!UICONTROL Datastreams]**
1. Markera tidigare skapade `Luma Web SDK` datastream

   ![Välj dataströmmen för Luma Web SDK](assets/datastream-luma-web-sdk.png)

1. Välj **[!UICONTROL Lägg till tjänst]**

   ![Lägg till en tjänst i datastream](assets/event-forwarding-datastream-addService.png)
1. Välj **[!UICONTROL Vidarebefordran av händelser]** som **[!UICONTROL Tjänst]**

1. Under **[!UICONTROL Egenskaps-ID]** väljer du namnet som du gav till egenskapen för vidarebefordran av händelser, i det här fallet `Server-Side - Web SDK Course`

1. Under **[!UICONTROL Miljö-ID]** väljer du den taggmiljö som du länkar händelsens vidarebefordringsmiljö till, i det här fallet `Development`

   >[!TIP]
   >
   >    Om du vill skicka data till en händelsevidarebefordringsmiljö utanför Adobe-organisationen väljer du **[!UICONTROL Ange ID manuellt]** och klistra in ett ID. ID:t anges när du skapar en händelsevidarebefordringsegenskap.

1. Välj **[!UICONTROL Spara]**.

   ![Aktivering av dataström för vidarebefordran av händelser](assets/event-forwarding-datastream-enable.png)

Upprepa dessa steg för staging- och produktionsdatastreams när du är redo att marknadsföra dina ändringar via publiceringsflödet.

## Vidarebefordra data från Platform Edge Network till en lösning som inte är Adobe

I den här övningen får du lära dig hur du ställer in ett dataelement för vidarebefordran av händelser, konfigurerar en regel för vidarebefordring av händelser och validerar med ett tredjedelsverktyg som kallas [Webkrok.webbplats](https://webhook.site/).

>[!NOTE]
>
>En webkrok är ett sätt att integrera olika system i halvrealtid. [Webkrok.webbplats](https://webhook.site/) är ett verktyg från tredje part som gör att du enkelt kan inspektera, testa och automatisera (med den visuella funktionen Custom Actions Builder, eller WebScript) inkommande HTTP-begäran eller e-post.

>[!IMPORTANT]
>
>Du måste redan ha skapat och mappat dataelement till ett XDM-objekt, samt konfigurerade taggregler och byggt dessa ändringar i ett bibliotek till en taggmiljö för att kunna fortsätta. Om du inte har det, se **Tagginställningar** steg i [krav](setup-event-forwarding.md#prerequisites) -avsnitt. Dessa steg säkerställer att data skickas till Platform Edge Network, och därifrån kan du konfigurera en händelsevidarebefordringsegenskap för att vidarebefordra data till en icke-Adobe-lösning.


### Skapa ett dataelement för vidarebefordran av händelser

XDM-objektet som du tidigare konfigurerade med plattformens SDK-taggtillägg blir datakällan för dataelement i en händelsevidarebefordringsegenskap. Du använder samma data som du redan har konfigurerat i taggegenskapen som en datakälla för händelsevidarebefordran.

>[!IMPORTANT]
>
>Det finns en viktig syntaxskillnad när XDM-fält refereras i händelsevidarebefordran jämfört med andra kontexter. Om du vill referera till data i en händelsevidarebefordringsegenskap måste dataelementets sökväg innehålla `arc.event` prefix:
>
> * `arc` står för Adobe Response Context.
> * Exempel: `arc.event.xdm.web.webPageDetails.URL`
>
>Om den här sökvägen anges felaktigt samlas inga data in.

I den här övningen vidarebefordrar du höjden på webbläsarens visningsruta och Experience Cloud-ID från XDM-objektet till en webkrok. Sökvägen till XDM-fältet bestäms av XDM-schemat som skapas under [Konfigurera ett XDM-schema](configure-schemas.md) lektion.

>[!TIP]
>
>Du kan också hitta sökvägen till XDM-objektet med hjälp av webbläsarens nätverksverktyg, filtrera efter `/ee` förfrågningar, öppna fyren [!UICONTROL **Nyttolast**] och går ned till den variabel du letar efter. Högerklicka sedan med musen och välj Kopiera egenskapssökväg. Här är ett exempel på webbläsarvisningsportens höjd:
> ![XDM-sökväg för händelsevidarebefordran](assets/event-forwarding-xdm-path.png)

1. Gå till **[!UICONTROL Vidarebefordran av händelser]** egenskap som du nyss skapade

1. Välj **[!UICONTROL Dataelement]**

1. Välj till **[!UICONTROL Skapa nytt dataelement]**

   ![Vidarebefordra nytt dataelement](assets/event-forwarding-new-dataelement.png)

1. **[!UICONTROL Namn]** dataelementet `environment.browserDetails.viewportHeight`

1. Under **[!UICONTROL Tillägg]**, lämna `CORE`

1. Under **[!UICONTROL Dataelementtyp]**, markera `Path`

1. Ange den XDM-objektsökväg som innehåller höjden för webbläsarvisningsrutan `arc.event.xdm.environment.browserDetails.viewportHeight`

1. Välj **[!UICONTROL Spara]**

   ![ECID-sökväg för händelsevidarebefordran](assets/event-forwarding-browser-viewpoirt-height.png)


1. Skapa ett annat dataelement

1. **[!UICONTROL Namn]** it `ecid`

1. Under **[!UICONTROL Tillägg]**, lämna `CORE`

1. Under **[!UICONTROL Dataelementtyp]**, markera `Path`

1. Ange sökvägen till XDM-objektet som innehåller Experience Cloud-ID:t `arc.event.xdm.identityMap.ECID.0.id`

1. Välj **[!UICONTROL Spara]**

   ![ECID-sökväg för händelsevidarebefordran](assets/event-forwarding-ecid.png)

   >[!CAUTION]
   >
   > Se till att inkludera `arc.event.` i sökvägen. Se även till att följa det exakta skiftläget som fältnamnet för XDM-objektet. ECID-namnutrymmet måste vara i versaler.


   >[!TIP]
   När du arbetar med din egen webbplats kan du hitta XDM-objektsökvägen med webbläsarens nätverksverktyg, filtrera efter `/ee` förfrågningar, öppna fyren [!UICONTROL **Nyttolast**] och går ned till den variabel du letar efter. Högerklicka sedan med musen och välj Kopiera egenskapssökväg. Här är ett exempel på webbläsarvisningsportens höjd:
   ![XDM-sökväg för händelsevidarebefordran](assets/event-forwarding-xdm-path.png)

### Installera tillägget Adobe Cloud Connector

Om du vill skicka data till tredjepartsplatser måste du först installera [!UICONTROL Adobe Cloud Connector] tillägg.

1. Välj **[!UICONTROL Tillägg]** till vänster

1. Välj **[!UICONTROL Katalog]** tab

1. Sök efter **[!UICONTROL Adobe Cloud Connector]**, markera **[!UICONTROL Installera]**

   ![ECID-sökväg för händelsevidarebefordran](assets/event-forwarding-adobe-cloud-connector.png)

Ingen tilläggskonfiguration behövs. Med det här tillägget kan du nu vidarebefordra data till en icke-Adobe-lösning!

### Skapa en regel för vidarebefordran av händelser

Det finns några huvudsakliga skillnader mellan att konfigurera regler i en taggegenskap och en regel i en händelsevidarebefordringsegenskap:

* **[!UICONTROL Händelser] &amp; [!UICONTROL Villkor]**:

   * **Taggar**: Alla regler aktiveras av en händelse som måste anges i regeln, till exempel: `Library Loaded - Page Top`. Villkoren är valfria.
   * **Vidarebefordran av händelser**: Det antas att varje händelse som skickas till Platform Edge Network utlöser vidarebefordran av data. Det finns därför inga [!UICONTROL Händelser] som måste väljas i regler för vidarebefordran av händelser. Om du vill hantera vilka händelser som utlöser en regel för vidarebefordran av händelser måste du konfigurera villkoren.

* **Tokenisering av dataelement**:

   * **Taggar**: Dataelementnamn tokeniseras med en `%` i början och slutet av dataelementnamnet när det används i en regel. Exempel, `%viewportHeight%`.

   * **Vidarebefordran av händelser**: Dataelementnamn tokeniseras med `{{` i början och `}}` i slutet av dataelementnamnet när det används i en regel. Exempel, `{{viewportHeight}}`.

* **Regelåtgärdssekvens**:

   * Avsnittet Åtgärder i en regel för vidarebefordran av händelser körs alltid sekventiellt. Kontrollera att åtgärdsordningen är korrekt när du sparar en regel. Den här körningssekvensen kan inte köras asynkront på samma sätt som med taggar.

<!--
  * **Tags**: Rule actions can easily be reordered using drag-and-drop functionality.
  * **Event forwarding**: Rule actions are always executed sequentially. Make sure the order of actions is correct when you save a rule.
-->

Om du vill konfigurera en regel för att vidarebefordra data till din webkrok måste du först skaffa din personliga webkrok:

1. Gå till [Webkrok.webbplats](https://webhook.site)

1. Sök **Din unika URL** kommer du att använda detta som URL-begäran i regeln för vidarebefordran av händelser

1. Välj **[!UICONTROL Kopiera till Urklipp]**

1. Lämna det här fönstret öppet så att du kan validera händelsevidarebefordringsdata i realtid som hämtas av Webkroks

   ![Kopiera webkros-URL](assets/event-forwarding-webhook.png)

1. Gå tillbaka **[!UICONTROL Datainsamling]** > **[!UICONTROL Vidarebefordran av händelser]** > **[!UICONTROL Regler]** från vänster navigering

1. Välj **[!UICONTROL Skapa ny regel]**

   ![Ny regel för vidarebefordran av händelse](assets/event-forwarding-new-rules.png)

1. Ge den ett namn `all events - ad cloud connector - webhook`

1. Lägg till en åtgärd

1. Under **[!UICONTROL Tillägg]**, markera **[!UICONTROL Adobe Cloud Connector]**

1. Under **[!UICONTROL Åtgärdstyp]**, markera **[!UICONTROL Ring för hämtning]**

1. Klistra in webkroks-URL:en i **[!UICONTROL URL]** fält

   ![Kopiera webkros-URL](assets/event-forwarding-rule.png)

1. Under **[Frågeparametrar]** lägger du till båda dataelementen som du skapade tidigare.

1. På **[!UICONTROL Nyckel]** kolumntyp i `viewPortHeight`. På **[!UICONTROL Värde]** kolumn, ange `{{environment.browserDetails.viewportHeight}}` dataelement genom att antingen skriva in det eller välja det från väljarikonen för dataelement

1. Välj [!UICONTROL **+ Lägg till ytterligare**] för att lägga till ytterligare en frågeparameter

1. På **[!UICONTROL Nyckel]** kolumntyp i `ecid`. I kolumnen Värde anger du `{{ecid}}` dataelement

1. Välj **[!UICONTROL Behåll ändringar]**

   ![Lägg till frågeparameter](assets/event-forwarding-rule-query-parameter.png)

1. Regeln ska se ut som nedan

1. Välj **[!UICONTROL Spara]**

   ![Spara regel för vidarebefordran av händelse](assets/event-forwarding-rule-save.png)

### Skapa och bygg biblioteket

Skapa ett bibliotek och bygg alla ändringar i utvecklingsmiljön för vidarebefordring av händelser på samma sätt som i en taggegenskap.

>[!NOTE]
Om du inte har länkat egenskaperna för vidarebefordran av mellanlagrings- och produktionshändelser till ditt datastam, kommer du att se Utvecklingsmiljö som det enda alternativet att skapa ett bibliotek till.

![Spara regel för vidarebefordran av händelse](assets/event-forwarding-initial-build.png)

## Validera regel för vidarebefordran av händelse

Nu kan du validera din egenskap för vidarebefordran av händelser med hjälp av Platform Debugger och Webhook.site:

1. Följ stegen för att [växla taggbibliotek](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) på [Luma Demo-webbplats](https://luma.enablementadobe.com/content/luma/us/en/men.html) till Web SDK-taggegenskapen som du mappade till för händelsevidarebefordran i datastream.

1. Innan du läser in sidan igen öppnar du felsökaren i Experience Platform **[!UICONTROL Loggar]** från vänster navigering

1. Välj **[!UICONTROL Edge]** tabbtangenten och sedan **[!UICONTROL Anslut]** för att visa förfrågningar om plattforms-Edge-nätverk

   ![Nätverkssession för klientvidarebefordrare](assets/event-forwarding-edge-session.png)

1. Läs in sidan igen

1. Du kommer att se ytterligare begäranden som ger dig synlighet i de serverförfrågningar som skickas av Platform Edge Network till WebHook

1. Begäran om fokusvalidering är den som visar den fullständigt konstruerade URL:en som skickas av Edge-nätverket

   ![Felsökning för vidarebefordring av händelser](assets/event-forwarding-debugger.png)


1. Anteckna parametrarna för frågesträngarna viewPortHeight och ecid

   ![Verifiera frågesträngar vid vidarebefordran](assets/event-forwarding-validate-data.png)

1. De matchar de data som visas i XDM-objektet

   ![Matchande data för vidarebefordran av händelser](assets/event-forwarding-matching-data.png)

1. Slutligen, validera datamatchningarna i [Webkrok.webbplats](https://webhook.site) även genom att visa det öppna Webkrok-fönstret

   ![Webbplatsdata för händelsevidarebefordran](assets/event-forwarding-webhook-data.png)

Grattis! Du har konfigurerat vidarebefordran av händelser!

[Nästa: ](conclusion.md)

>[!NOTE]
Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)