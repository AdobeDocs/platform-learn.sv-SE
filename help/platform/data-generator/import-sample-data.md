---
title: Importera exempeldata till Adobe Experience Platform
description: Lär dig hur du konfigurerar en sandlådemiljö i Experience Platform med exempeldata.
feature: API
role: Developer
level: Experienced
jira: KT-7349
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: da94f4bd-0686-4d6a-a158-506f2e401b4e
source-git-commit: 4db88dbae923d37884391a65ff8fc16f53e19187
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# Importera exempeldata till Adobe Experience Platform

Lär dig hur du konfigurerar en sandlådemiljö i Experience Platform med exempeldata. Med en Postman-samling kan du skapa fältgrupper, scheman, datauppsättningar och sedan importera exempeldata till Experience Platform.

## Exempel på dataanvändning

Experience Platform-användare måste ofta gå igenom en serie steg som omfattar att identifiera fältgrupper, skapa scheman, förbereda data, skapa datauppsättningar och sedan importera data innan de kan utforska de marknadsföringsfunktioner som erbjuds av Experience Platform. Den här självstudiekursen automatiserar några av stegen så att du kan hämta data till en plattformssandlåda så snabbt som möjligt.

Den här självstudiekursen fokuserar på ett fiktivt varumärke som kallas Luma. De investerar i Adobe Experience Platform för att kombinera lojalitet, CRM, produktkatalog och offlineköp i kundprofiler i realtid och aktivera profilerna för att ta marknadsföringen till nästa nivå. Vi har genererat exempeldata för Luma, och i resten av den här självstudiekursen kommer du att importera dessa data till någon av dina Experience Platform sandlådemiljöer.

>[!NOTE]
>
>Slutresultatet av den här självstudiekursen är en sandlåda som innehåller liknande data som [Komma igång med Adobe Experience Platform för dataarkitekter och datatekniker](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=sv-SE). Den uppdaterades i april 2023 för att stödja [Journey Optimizer-utmaningarna](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=sv-SE). Den uppdaterades i juni 2023 för att ändra autentiseringsmetoden till OAuth.


## Förhandskrav

* Du har tillgång till Experience Platform API:er och kan autentisera. Om inte, gå igenom den här [självstudiekursen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=sv-SE).
* Du har tillgång till en Experience Platform-utvecklingssandlåda.
* Du känner till ditt Experience Platform tenant-ID. Du kan hämta den genom att göra en autentiserad [API-begäran](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=sv-SE#know-your-tenant_id)
eller genom att extrahera det från URL:en när du loggar in på ditt plattformskonto. I följande URL är klientorganisationen till exempel `techmarketingdemos` `https://experience.adobe.com/#/@techmarketingdemos/sname:prod/platform/home`.

## Använder [!DNL Postman] {#postman}

### Ställ in miljövariabler

Kontrollera att du har hämtat programmet [Postman](https://www.postman.com/downloads/) innan du följer stegen. Kom så börjar vi!

1. Hämta filen [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) som innehåller alla filer som krävs för den här självstudiekursen.

   >[!NOTE]
   >
   >Användardata i filen [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) är fiktiva och ska endast användas i demonstrationssyfte.

1. Flytta `platform-utils-main.zip`-filen till önskad plats på datorn från hämtningsmappen och packa upp den.
1. Öppna alla `json`-filer i en textredigerare i mappen `luma-data` och ersätt alla instanser av `_yourTenantId` med ditt eget klient-ID, föregånget av ett understreck.
1. Öppna `luma-offline-purchases.json`, `luma-inventory-events.json` och `luma-web-events.json` i en textredigerare och uppdatera alla tidsstämplar så att händelserna inträffar den senaste månaden (sök till exempel efter `"timestamp":"2022-11` och ersätt år och månad)
1. Observera platsen för den uppzippade mappen, som du behöver den senare när du konfigurerar miljövariabeln `FILE_PATH` [!DNL Postman] :

   >[!NOTE]
   > Om du vill hämta filsökvägen på din Mac går du till mappen `platform-utils-main`, högerklickar på mappen och väljer alternativet **Visa info** .
   >
   > ![MAC-filsökväg](../assets/data-generator/images/mac-file-path.png)

   >[!NOTE]
   > Om du vill ha en filsökväg i dina fönster öppnar du platsen för den önskade mappen genom att klicka på dem och högerklickar sedan till höger om sökvägen i adressfältet. Kopiera adress för att hämta filsökvägen.
   > 
   > ![Windows-filsökväg](../assets/data-generator/images/windows-file-path.png)

1. Öppna [!DNL Postman] och skapa en arbetsyta från den nedrullningsbara menyn **Arbetsytor**:\
   ![Skapa arbetsyta](../assets/data-generator/images/create-workspace.png)
1. Ange ett **namn** och valfri **sammanfattning** för arbetsytan och klicka på **Skapa Workspace**. [!DNL Postman] växlar till din nya arbetsyta när du skapar den.
   ![Spara arbetsyta](../assets/data-generator/images/save-workspace.png)
1. Justera några inställningar för att köra [!DNL Postman]-samlingarna på den här arbetsytan. Klicka på kugghjulsikonen i sidhuvudet på [!DNL Postman] och välj **Inställningar** för att öppna inställningarna modal. Du kan också använda kortkommandot (CMD/CTRL + ,) för att öppna modala bilder.
1. Under fliken `General` uppdaterar du timeout för begäran i ms till `5000 ms` och aktiverar `allow reading file outside this directory`
   ![Inställningar](../assets/data-generator/images/settings.png)

   >[!NOTE]
   > Om filer läses in från en arbetskatalog kommer de att köras smidigt på olika enheter om samma filer lagras på andra enheter. Om du vill köra filer från en plats utanför arbetskatalogen måste en inställning aktiveras för att ange samma metod. Om `FILE_PATH` inte är samma som arbetskatalogsökvägen för [!DNL Postman] bör det här alternativet aktiveras.

1. Stäng panelen **Inställningar**.
1. Markera **miljöerna** och välj sedan **Importera**:
   ![Miljöimport](../assets/data-generator/images/env-import.png)
1. Importera den hämtade JSON-miljöfilen, `DataInExperiencePlatform.postman_environment`
1. I Postman väljer du din miljö i den övre högra listrutan och klickar på ögonikonen för att visa miljövariablerna:
   ![Miljöval](../assets/data-generator/images/env-selection.png)

1. Kontrollera att följande miljövariabler är ifyllda. Om du vill lära dig hur du hämtar miljövariabelns värde kan du gå till självstudiekursen [Autentisera till Experience Platform-API:er](/help/platform/authentication/platform-api-authentication.md) för steg-för-steg-instruktioner.

   * `CLIENT_SECRET`
   * `API_KEY`—`Client ID` i Adobe Developer Console
   * `SCOPES`
   * `TECHNICAL_ACCOUNT_ID`
   * `IMS`
   * `IMS_ORG`—`Organization ID` i Adobe Developer Console
   * `SANDBOX_NAME`
   * `TENANT_ID` - se till att leda med ett understreck, till exempel `_techmarketingdemos`
   * `CONTAINER_ID`
   * `platform_end_point`
   * `FILE_PATH` - använd den lokala mappsökvägen där du har packat upp `platform-utils-main.zip`-filen. Kontrollera att den innehåller mappnamnet, till exempel `/Users/dwright/Desktop/platform-utils-main`

1. **Spara** den uppdaterade miljön

### Importera Postman-samlingar

Därefter måste du importera samlingarna till Postman.

1. Markera **Samlingar** och välj sedan importalternativet:

   ![Samlingar](../assets/data-generator/images/collections.png)

1. Importera följande samlingar:

   * `0-Authentication.postman_collection.json`
   * `1-Luma-Loyalty-Data.postman_collection.json`
   * `2-Luma-CRM-Data.postman_collection.json`
   * `3-Luma-Product-Catalog.postman_collection.json`
   * `4-Luma-Offline-Purchase-Events.postman_collection.json`
   * `5-Luma-Product-Inventory-Events.postman_collection.json`
   * `6-Luma-Test-Profiles.postman_collection.json`
   * `7-Luma-Web-Events.postman_collection.json`

   ![Samlingar, import](../assets/data-generator/images/collection-files.png)

### Autentisera

Därefter måste du autentisera och generera en användartoken. Observera att de tokengenereringsmetoder som används i den här självstudiekursen endast är lämpliga för icke-produktionsbruk. Lokal signering läser in ett JavaScript-bibliotek från en tredjepartsvärd och fjärrsignering skickar den privata nyckeln till en webbtjänst som ägs och drivs av Adobe. Även om Adobe inte lagrar den här privata nyckeln bör produktionsnycklar aldrig delas med någon.

1. Öppna samlingen `0-Authentication`, markera `OAuth: Request Access Token`-begäran och klicka på `SEND` för att autentisera och hämta åtkomsttoken.

   ![Samlingar, import](../assets/data-generator/images/authentication.png)

1. Granska miljövariablerna och observera att `ACCESS_TOKEN` nu är ifylld.

### Importera data

Nu kan du förbereda och importera data till din plattformssandlåda. De Postman-samlingar du har importerat kommer att göra allt det tunga arbetet!

1. Öppna samlingen `1-Luma-Loyalty-Data` och klicka på **Kör** på översiktsfliken för att starta en samlingskörare.

   ![Samlingar, import](../assets/data-generator/images/loyalty.png)

1. I samlingskörningsfönstret ska du se till att välja miljön i listrutan, uppdatera **Fördröjning** till `4000ms`, kontrollera alternativet **Spara svar** och se till att körningsordningen är korrekt. Klicka på knappen **Kör Luma-lojalitetsdata**

   ![Samlingar, import](../assets/data-generator/images/loyalty-run.png)

   >[!NOTE]
   >
   >**1-Luma-Loyalty-Data** skapar ett schema för kundlojalitetsdata. Schemat baseras på klassen XDM Individual Profile, standardfältgruppen samt en anpassad fältgrupp och datatyp. Samlingen skapar en datauppsättning med hjälp av schemat och överför exempelkundlojalitetsdata till Adobe Experience Platform.

   >[!NOTE]
   >
   >Om en samlingsbegäran misslyckas under Postman-samlingens körningsprogram stoppar du körningen och kör samlingsbegäran en i taget.

1. Om allt fungerar bra bör alla begäranden i samlingen `Luma-Loyalty-Data` skickas.

   ![Förmånsresultat](../assets/data-generator/images/loyalty-result.png)

1. Nu ska vi logga in på [Adobe Experience Platform-gränssnittet](https://platform.adobe.com/) och navigera till datauppsättningar.
1. Öppna datauppsättningen `Luma Loyalty Dataset`, och under aktivitetsfönstret för datauppsättningen kan du visa en lyckad batchkörning som kapslade 1 000 poster. Du kan också klicka på alternativet för förhandsgranskning av datauppsättning för att verifiera de poster som har importerats. Du kan behöva vänta flera minuter för att bekräfta att 1000 [!UICONTROL New Profile Fragments] skapades.
   ![Förmånsdatauppsättning](../assets/data-generator/images/loyalty-dataset.png)
1. Upprepa steg 1-3 för att köra de andra samlingarna:
   * `2-Luma-CRM-Data.postman_collection.json` skapar ett schema och en ifylld datauppsättning för CRM-data för kunder. Schemat är baserat på klassen XDM Individual Profile som omfattar Demografisk information, personlig kontaktinformation, inställningsinformation och en anpassad identitetsfältgrupp.
   * `3-Luma-Product-Catalog.postman_collection.json` skapar ett schema och en ifylld datamängd för produktkataloginformation. Schemat är baserat på en anpassad produktkatalogklass och använder en anpassad produktkatalogfältgrupp.
   * `4-Luma-Offline-Purchase-Events.postman_collection.json` skapar ett schema och en ifylld datamängd för kunders offlineinköpshändelsedata. Schemat baseras på klassen XDM ExperienceEvent och består av en anpassad identitet och fältgrupper för Commerce Details.
   * `5-Luma-Product-Inventory-Events.postman_collection.json` skapar ett schema och en ifylld datamängd för händelser som är relaterade till produkter som kommer in och ut ur lagret. Schemat baseras på en anpassad affärshändelseklass och en anpassad fältgrupp.
   * `6-Luma-Test-Profiles.postman_collection.json` skapar ett schema och en ifylld datauppsättning med testprofiler som ska användas i Adobe Journey Optimizer
   * `7-Luma-Web-Events.postman_collection.json` skapar ett schema och en ifylld datauppsättning med enkla historiska webbdata.


## Validering

Exempeldata har utformats så att kundprofiler i realtid som kombinerar data från flera system byggs när samlingarna har körts. Ett bra exempel på detta är den första posten i datamängderna för lojalitet, CRM och offlineköp. Slå upp den profilen för att bekräfta att data har importerats. I [Adobe Experience Platform-gränssnittet](https://experience.adobe.com/platform/):

1. Gå till **[!UICONTROL Profiles]** > **[!UICONTROL Browse]**
1. Välj `Luma Loyalty Id` som **[!UICONTROL Identity namespace]**
1. Sök efter `5625458` som **[!UICONTROL Identity value]**
1. Öppna profilen `Daniel Wright`

>[!TIP]
>
>Om du inte ser profilen kontrollerar du sidan [!UICONTROL Datasets] för att bekräfta att alla datauppsättningar har skapats och importerats. Om det ser bra ut kan du vänta i femton minuter och se om profilen är tillgänglig i visningsprogrammet.  Om det uppstår problem med dataimporten kontrollerar du felmeddelandena för att försöka hitta problemet. Du kan också försöka aktivera feldiagnostik på sidan [!UICONTROL Datasets] och dra och släppa JSON-datafilen för att importera data igen.


![Öppnar en profil](../assets/data-generator/images/validation-profile-open.png)

Genom att bläddra igenom data på flikarna **[!UICONTROL Attributes]** och **[!UICONTROL Events]** bör du se att profilen innehåller data från de olika datafilerna:
![Händelsedata från offlineinköpshändelsefilen ](../assets/data-generator/images/validation-profile-events.png)

## Nästa steg

Om du vill veta mer om Adobe Journey Optimizer innehåller den här sandlådan allt du behöver för att hantera [Journey Optimizer-utmaningar](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=sv-SE)

Om du vill lära dig mer om sammanfogningsprinciper, datastyrning, frågetjänst och segmentbyggaren går du till [lektion 11 i självstudiekursen Komma igång för dataarkitekter och datatekniker](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-merge-policies.html?lang=sv-SE). I de tidigare lektionerna av den här andra självstudiekursen kan du manuellt skapa allt som just fyllts i av de här Postman-kollektionerna - du kommer snabbt igång!

Om du vill skapa en exempelimplementering av Web SDK för att länka till den här sandlådan går du igenom
[Implementera Adobe Experience Cloud med Web SDK, självstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=sv-SE). När du har konfigurerat lektionerna&quot;Inledande konfiguration&quot;,&quot;Taggkonfiguration&quot; och&quot;Konfigurera Experience Platform&quot; i självstudiekursen för Web SDK loggar du in på Lumas webbplats med hjälp av de första tio e-postadresserna i filen `luma-crm.json` med hjälp av lösenordet `test` för att se profilfragmenten sammanfogas med data som överförts i den här självstudiekursen.

Om du vill skapa ett exempel på en mobil SDK-implementering som länkar till den här sandlådan går du igenom
[Implementera Adobe Experience Cloud i mobilappar, genomgång](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=sv-SE). När du har konfigurerat lektionerna&quot;Inledande konfiguration&quot;,&quot;App-implementering&quot; och&quot;Experience Platform&quot; i självstudiekursen för Web SDK loggar du in på Lumas webbplats med de första e-postadresserna i filen `luma-crm.json` för att se en profilfragmentsammanslagning med data som överförts i den här självstudiekursen.

## Återställ sandlådemiljö {#reset-sandbox}

Om du återställer en icke-produktionssandlåda tas alla resurser som är associerade med den sandlådan (scheman, datauppsättningar o.s.v.) bort, samtidigt som sandlådans namn och associerade behörigheter behålls. Den här&quot;rena&quot; sandlådan är fortfarande tillgänglig under samma namn för användare som har åtkomst till den.

Följ stegen [här](https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=sv-SE#reset-a-sandbox) för att återställa en sandlådemiljö.
