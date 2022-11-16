---
title: Importera exempeldata till Adobe Experience Platform
description: Lär dig hur du konfigurerar en sandlådemiljö i Experience Platform med exempeldata.
role: Developer
feature: API
kt: 7349
thumbnail: 7349.jpg
exl-id: da94f4bd-0686-4d6a-a158-506f2e401b4e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 0%

---

# Importera exempeldata till Adobe Experience Platform

Lär dig hur du konfigurerar en sandlådemiljö i Experience Platform med exempeldata. Med en Postman-samling kan du skapa fältgrupper, scheman, datauppsättningar och sedan importera exempeldata till Experience Platform.

## Exempel på dataanvändning

Experience Platform-användare måste ofta gå igenom en serie steg som omfattar att identifiera fältgrupper, skapa scheman, förbereda data, skapa datauppsättningar och sedan importera data innan de kan utforska de marknadsföringsfunktioner som erbjuds av Experience Platform. Den här självstudiekursen automatiserar några av stegen så att du kan hämta data till en plattformssandlåda så snabbt som möjligt.

Den här självstudiekursen fokuserar på ett fiktivt detaljhandelsmärke som kallas Luma. De investerar i Adobe Experience Platform för att kombinera lojalitet, CRM, produktkataloger och offlineköp i kundprofiler i realtid och aktivera profilerna för att ta marknadsföringen till nästa nivå. Vi har genererat exempeldata för Luma, och i resten av den här självstudiekursen kommer du att importera dessa data till någon av dina Experience Platform sandlådemiljöer.

>[!NOTE]
>
>Slutresultatet av den här självstudiekursen är en sandlåda som innehåller samma exempeldata som [Komma igång med självstudiekursen Adobe Experience Platform for Data Architects and Data Engineers](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html).


## Förutsättningar

* Du har tillgång till Experience Platform API:er och kan autentisera. Om inte, gå igenom detta [självstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html).
* Du har tillgång till en Experience Platform-utvecklingssandlåda.
* Du känner till ditt Experience Platform tenant-ID. Du kan få det genom att skapa en autentiserad [API-begäran](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#know-your-tenant_id)
eller genom att extrahera det från URL:en när du loggar in på ditt plattformskonto. I följande URL är klientorganisationen &quot;
`techmarketingdemos`&quot; `https://experience.adobe.com/#/@techmarketingdemos/sname:prod/platform/home`.

## Använda Postman {#postman}

### Ställ in miljövariabler

Kontrollera att du har hämtat [Postman](https://www.postman.com/downloads/) program.  Kom så börjar vi!

1. Ladda ned [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) som innehåller alla filer som behövs för kursen.

   >[!NOTE]
   >
   >Användardata i [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) filen är fiktiv och ska endast användas som exempel.

1. Flytta `platform-utils-main.zip` till önskad plats på datorn och packa upp den.
1. I `luma-data` mapp, öppna alla `json` filer i en textredigerare och ersätta alla förekomster av `_techmarketingdemos` med ditt eget klient-ID, föregånget av ett understreck.
1. Observera platsen för den uppzippade mappen, som du behöver den senare när du konfigurerar `FILE_PATH` Postman miljövariabel:

   >[!NOTE]
   > Om du vill hämta filsökvägen på din Mac går du till `platform-utils-main` mapp, högerklicka på mappen och välj **Visa info** alternativ.
   >
   > ![Sökväg till Mac](../assets/data-generator/images/mac-file-path.png)

   >[!NOTE]
   > Om du vill ha en filsökväg i dina fönster öppnar du platsen för den önskade mappen genom att klicka på dem och högerklickar sedan till höger om sökvägen i adressfältet. Kopiera adress för att hämta filsökvägen.
   > 
   > ![Sökväg till Windows-fil](../assets/data-generator/images/windows-file-path.png)

1. Öppna Postman och skapa en ny arbetsyta från **Arbetsytor** nedrullningsbar meny:\
   ![Skapa arbetsyta](../assets/data-generator/images/create-workspace.png)
1. Ange **Namn** och valfria **Sammanfattning** för arbetsytan och klicka **Skapa arbetsyta**. Postman växlar till den nya arbetsytan när du skapar den.
   ![Spara arbetsyta](../assets/data-generator/images/save-workspace.png)
1. Justera några inställningar för att köra Postman-samlingar på den här arbetsytan. Klicka på kugghjulsikonen i Postman sidhuvud och välj **Inställningar** för att öppna inställningarna spärrade. Du kan också använda kortkommandot (CMD/CTRL + ,) för att öppna modala bilder.
1. Under `General` uppdaterar du timeout för begäran i ms till `5000 ms` och aktivera `allow reading file outside this directory`
   ![Inställningar](../assets/data-generator/images/settings.png)

   >[!NOTE]
   > Om filer läses in från en arbetskatalog kommer de att köras smidigt på olika enheter om samma filer lagras på andra enheter. Om du vill köra filer från en plats utanför arbetskatalogen måste en inställning aktiveras för att ange samma metod. Om `FILE_PATH` är inte samma som sökvägen till Postman arbetskatalog, så det här alternativet bör aktiveras.

1. Stäng **Inställningar** -panelen.
1. Välj **Miljö** och sedan markera **Importera**:
   ![Miljöimport](../assets/data-generator/images/env-import.png)
1. Importera den hämtade JSON-miljöfilen, `DataInExperiencePlatform.postman_environment`
1. I Postman väljer du din miljö i den övre högra listrutan och klickar på ögonikonen för att visa miljövariablerna:
   ![Miljöval](../assets/data-generator/images/env-selection.png)

1. Kontrollera att följande miljövariabler är ifyllda. Om du vill veta hur du hämtar miljövariabelns värde kan du titta i [Autentisera till Experience Platform API:er](/help/platform/authentication/platform-api-authentication.md) självstudiekurs för steg-för-steg-instruktioner.

   * `CLIENT_SECRET`
   * `API_KEY`—`Client ID` i Adobe Developer Console
   * `TECHNICAL_ACCOUNT_ID`
   * `META_SCOPE`
   * `IMS`
   * `IMS_ORG`—`Organization ID` i Adobe Developer Console
   * `PRIVATE_KEY`
   * `SANDBOX_NAME`
   * `CONTAINER_ID`
   * `TENANT_ID`—se till att leda med ett understreck, till exempel `_techmarketingdemos`
   * `platform_end_point`
   * `FILE_PATH`—använd den lokala mappsökvägen där du har packat upp `platform-utils-main.zip` -fil. Se till att den innehåller mappnamnet, till exempel `/Users/dwright/Desktop/platform-utils-main`

1. **Spara** den uppdaterade miljön

### Importera Postman-samlingar

Därefter måste du importera samlingarna till Postman.

1. Välj **Samlingar** och välj sedan importalternativet:

   ![Samlingar](../assets/data-generator/images/collections.png)

1. Importera följande samlingar:

   * `0-Authentication.postman_collection.json`
   * `1-Luma-Loyalty-Data.postman_collection.json`
   * `2-Luma-CRM-Data.postman_collection.json`
   * `3-Luma-Product-Catalog.postman_collection.json`
   * `4-Luma-Offline-Purchase-Events.postman_collection.json`

   ![Import av samlingar](../assets/data-generator/images/collection-files.png)

### Autentisera

Därefter måste du autentisera och generera en användartoken. Observera att de tokengenereringsmetoder som används i den här självstudiekursen endast är lämpliga för icke-produktionsbruk. Lokal signering läser in ett JavaScript-bibliotek från en tredjepartsvärd och fjärrsignering skickar den privata nyckeln till en webbtjänst som ägs och drivs av Adobe. Även om Adobe inte lagrar den här privata nyckeln bör produktionsnycklar aldrig delas med någon.

1. Öppna `Authentication` samling, välj `IMS: JWT Generate + Auth via User Token` begär POST och klickar på `SEND` för att autentisera och hämta åtkomsttoken.

   ![Import av samlingar](../assets/data-generator/images/authentication.png)

1. Granska miljövariablerna och lägg märke till att `JWT_TOKEN` och `ACCESS_TOKEN` är nu ifyllda.

### Importera data

Nu kan du förbereda och importera data till din plattformssandlåda. De Postman-samlingar du har importerat kommer att göra allt det tunga arbetet!

1. Öppna `1-Luma-Loyalty-Data` samling och klicka **Kör** på översiktsfliken för att starta en Collection Runner.

   ![Import av samlingar](../assets/data-generator/images/loyalty.png)

1. I samlingskörningsfönstret ska du se till att välja miljön i listrutan och uppdatera **Fördröjning** till `4000ms`, kontrollera **Spara svar** och se till att körningsordningen är korrekt. Klicka på **Kör Luma-lojalitetsdata** knapp

   ![Import av samlingar](../assets/data-generator/images/loyalty-run.png)

   >[!NOTE]
   >
   >**1-Luma-Loyalty-data** skapar ett schema för kundlojalitetsdata. Schemat baseras på klassen XDM Individual Profile, standardfältgruppen samt en anpassad fältgrupp och datatyp. Samlingen skapar en datauppsättning med hjälp av schemat och överför exempelkundlojalitetsdata till Adobe Experience Platform.

   >[!NOTE]
   >
   >Om en samlingsbegäran misslyckas under Postman-samlingens körningsprogram stoppar du körningen och kör samlingsbegäran en i taget.

1. Om allt går bra, finns alla förfrågningar i `Luma-Loyalty-Data` -samlingen ska passera.

   ![Förmånsresultat](../assets/data-generator/images/loyalty-result.png)

1. Nu ska vi logga in på [Adobe Experience Platform](https://platform.adobe.com/) och navigera till datauppsättningar.
1. Öppna `Luma Loyalty Dataset` datauppsättning, och under aktivitetsfönstret för datauppsättningen, kan du visa en lyckad batchkörning som importerade 1 000 poster. Du kan också klicka på alternativet för förhandsgranskning av datauppsättning för att verifiera de poster som har importerats. Du kan behöva vänta flera minuter för att bekräfta att 1000 [!UICONTROL Nya profilfragment] skapades.
   ![Förmånsdatauppsättning](../assets/data-generator/images/loyalty-dataset.png)
1. Upprepa steg 1-3 för att köra de andra samlingarna:
   * `2-Luma-CRM-Data.postman_collection.json` skapar ett schema och en ifylld datauppsättning för kundens CRM-data. Schemat är baserat på klassen XDM Individual Profile som omfattar Demografisk information, personlig kontaktinformation, inställningsinformation och en anpassad identitetsfältgrupp.
   * `3-Luma-Product-Catalog.postman_collection.json` skapar ett schema och en ifylld datauppsättning för produktkataloginformation. Schemat är baserat på en anpassad produktkatalogklass och använder en anpassad produktkatalogfältgrupp.
   * `4-Luma-Offline-Purchase-Events.postman_collection.json` skapar ett schema och en ifylld datamängd för kunders offlineköp. Schemat är baserat på XDM ExperienceEvent-klassen och består av en anpassad identitet och fältgrupper för Commerce Details.

## Validering

Exempeldata har utformats så att kundprofiler i realtid som kombinerar data från flera system byggs när samlingarna har körts. Ett bra exempel på detta är den första posten i datamängderna för lojalitet, CRM och offlineköp. Slå upp den profilen för att bekräfta att data har importerats. I [Adobe Experience Platform](https://platform.adobe.com/):

1. Gå till **[!UICONTROL Profiler]** > **[!UICONTROL Bläddra]**
1. Välj `Luma Loyalty Id` som **[!UICONTROL Namnutrymme för identitet]**
1. Sök efter `5625458` som **[!UICONTROL Identitetsvärde]**
1. Öppna `Danny Wright` profil

![Öppna en profil](../assets/data-generator/images/validation-profile-open.png)

Genom att bläddra bland data i **[!UICONTROL Attribut]** och **[!UICONTROL Händelser]** ser du att profilen innehåller data från de olika datafilerna:
![Händelsedata från offlineinköpshändelsefilen](../assets/data-generator/images/validation-profile-events.png)

## Nästa steg

Om du vill veta mer om sammanfogningsprinciper, datastyrning, frågetjänst och segmentbyggaren går du till [lektion 11 i självstudiekursen Getting Started for Data Architects and Data Engineers](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-merge-policies.html?lang=en). I de tidigare lektionerna av den här andra självstudiekursen kan du manuellt skapa allt som just fyllts i av de här Postman-kollektionerna - du kommer snabbt igång!

Om du vill skapa en exempelimplementering av Web SDK för att länka till den här sandlådan går du igenom
[Implementera Adobe Experience Cloud med Web SDK, genomgång](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html). När du har konfigurerat lektionerna &quot;Initial Configuration&quot;, &quot;Tags Configuration&quot; och &quot;Set up Experience Platform&quot; i självstudiekursen för Web SDK loggar du in på Lumas webbplats med de första tio e-postadresserna i dialogrutan `luma-crm.json` med lösenord `test` för att se profilfragmenten sammanfogas med data som överförts i den här självstudiekursen.

Om du vill skapa ett exempel på en mobil SDK-implementering som länkar till den här sandlådan går du igenom
[Implementera Adobe Experience Cloud i mobilappar, genomgång](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html). När du har konfigurerat lektionerna&quot;Inledande konfiguration&quot;,&quot;App-implementering&quot; och&quot;Experience Platform&quot; i självstudiekursen för Web SDK loggar du in på Lumas webbplats med de första e-postadresserna i `luma-crm.json` om du vill se en profilfragmentsammanslagning med data som överförts i den här självstudiekursen.

## Återställ sandlådemiljö {#reset-sandbox}

Om du återställer en icke-produktionssandlåda tas alla resurser som är associerade med den sandlådan (scheman, datauppsättningar o.s.v.) bort, samtidigt som sandlådans namn och associerade behörigheter behålls. Den här&quot;rena&quot; sandlådan är fortfarande tillgänglig under samma namn för användare som har åtkomst till den.

Följ stegen [här](https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=en#reset-a-sandbox) för att återställa en sandlådemiljö.
