---
title: Konfigurera Developer Console och Postman
seo-title: Set up Developer Console and Postman | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Konfigurera Developer Console och Postman
description: I den här lektionen ska du skapa ett projekt i Adobe Developer Console och förse dig med [!DNL Postman] samlingar så att du kan börja använda Platform API:er.
role: Data Architect, Data Engineer
feature: API
jira: KT-4348
thumbnail: 4348-set-up-developer-console-and-postman.jpg
exl-id: 72b541fa-3ea1-4352-b82b-c5b79ff98491
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Konfigurera Developer Console och [!DNL Postman]

<!--30min-->

I den här lektionen ska du konfigurera ett projekt i Adobe Developer Console och hämta [!DNL Postman]-samlingar så att du kan börja använda plattforms-API:er.

För att kunna slutföra API-övningarna i den här självstudiekursen [hämtar du Postman-appen för ditt operativsystem.](https://www.postman.com/downloads/) Krävs inte för att kunna använda Experience Platform API:er, men Postman gör API-arbetsflöden enklare och Adobe Experience Platform tillhandahåller dussintals Postman-samlingar som hjälper dig att köra API-anrop och lära dig hur de fungerar. Resten av den här självstudiekursen bygger på en del praktiska kunskaper i Postman. Mer information finns i [Postman-dokumentationen](https://learning.postman.com/).

Plattformen är byggd för API. Även om det finns gränssnittsalternativ för alla viktiga uppgifter kan det vara bra att använda plattforms-API:t någon gång. Om du till exempel vill importera data flyttar du objekt mellan sandlådor, automatiserar rutinuppgifter eller använder nya plattformsfunktioner innan användargränssnittet har skapats.

**Dataarkitekter** och **datatekniker** kan behöva använda Platform API utanför den här självstudiekursen.

## Behörigheter krävs

I lektionen [Konfigurera behörigheter](configure-permissions.md) ställer du in alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--
* Permission item Sandboxes > `Luma Tutorial`
* Developer-role access to the `Luma Tutorial Platform` product profile
-->

## Konfigurera Adobe Developer Console

Adobe Developer Console är utvecklarmålet för att få tillgång till Adobe API:er och SDK:er, lyssna på händelser i realtid, köra funktioner i körningsmiljön eller bygga plugin-program eller App Builder-program. Du kommer att använda den för att komma åt Experience Platform API:t. Mer information finns i [Adobe Developer Console-dokumentationen](https://www.adobe.io/apis/experienceplatform/console/docs.html)

1. Skapa en mapp på den lokala datorn med namnet `Luma Tutorial Assets` för filer som används i självstudiekursen.

1. Öppna [Adobe Developer Console](https://console.adobe.io){target="_blank"}

1. Logga in och bekräfta att du använder rätt Org

1. Välj **[!UICONTROL Create New Project]** på menyn [!UICONTROL Quick Start].

   ![Skapa nytt projekt](assets/adobeio-createNewProject.png)


1. I det nyskapade projektet väljer du knappen **[!UICONTROL Edit Project]**
1. Ändra **[!UICONTROL Project Title]** till `Luma Tutorial API Project` (lägg till ditt namn i slutet om flera personer från ditt företag använder den här självstudiekursen)
1. Välj **[!UICONTROL Save]**

   ![Adobe Developer Console Project API-konfiguration](assets/adobeio-renameProject.png)


1. Välj **[!UICONTROL Add API]**

   ![Adobe Developer Console Project API-konfiguration](assets/adobeio-addAPI.png)

1. Filtrera listan genom att välja **[!UICONTROL Adobe Experience Platform]**

1. I listan över tillgängliga API:er väljer du **[!UICONTROL Experience Platform API]** och sedan **[!UICONTROL Next]**.

   ![Adobe Developer Console Project API-konfiguration](assets/adobeio-AEPAPI.png)

1. Välj **[!UICONTROL OAuth Server-to-Server]** som autentiseringsuppgift och välj **[!UICONTROL Next]**.
   ![Välj OAuth Server-till-server](assets/adobeio-choose-auth.png)

1. Välj produktprofilen `AEP-Default-All-Users` och välj **[!UICONTROL Save Configured API]**

   ![Välj produktprofil](assets/adobeio-selectProductProfile.png)

1. Nu har ditt Developer Console-projekt skapats!

1. I avsnittet **[!UICONTROL Try it out]** på sidan väljer du **[!UICONTROL Download for Postman]** och sedan **[!UICONTROL OAuth Server-to-Server]** för att hämta [!DNL Postman] JSON-miljöfilen. Spara `oauth_server_to_server.postman_environment.json` i mappen `Luma Tutorial Assets`.


   ![Adobe Developer Console Project API-konfiguration](assets/adobeio-io-api.png)

## Låt en systemadministratör lägga till API-autentiseringsuppgifterna i rollen

Om du vill använda API-autentiseringsuppgifterna för att interagera med Experience Platform måste du ha en systemadministratör som tilldelar API-autentiseringsuppgifterna till rollen som skapades i den föregående lektionen.  Om du inte är systemadministratör skickar du dem:

1. [!UICONTROL Name] för dina API-autentiseringsuppgifter (`Credential in Luma Tutorial API Project`)
1. [!UICONTROL Technical Account Email] av dina autentiseringsuppgifter (detta hjälper systemadministratören att hitta autentiseringsuppgifterna)

   ![[!UICONTROL Name] och [!UICONTROL Technical Account Email] av dina autentiseringsuppgifter ](assets/postman-credentialDetails.png)

Här följer instruktionerna för systemadministratören:

1. Logga in på [Adobe Experience Platform](https://platform.adobe.com)
1. Välj **[!UICONTROL Permissions]** i den vänstra navigeringen som tar dig till skärmen [!UICONTROL Roles]
1. Öppna rollen `Luma Tutorial Platform`
   ![Öppna rollen](assets/postman-openRole.png)
1. Välj fliken **[!UICONTROL API Credentials]**
1. Välj **[!UICONTROL Add API Credentials]**
   ![Lägg till autentiseringsuppgifter](assets/postman-addCredential.png)
1. Hitta autentiseringsuppgifterna `Credential in Luma Tutorial API Project`, filtrera med den [!UICONTROL Technical Account Email] som tillhandahålls av den som deltar i självstudiekursen, om listan är lång
1. Välj autentiseringsuppgifter
1. Välj **[!UICONTROL Save]**


   ![Lägg till autentiseringsuppgifter](assets/postman-findCredential.png)

## Konfigurera Postman

>[!CAUTION]
>
>Postman gränssnitt uppdateras regelbundet. Skärmbilderna i den här självstudiekursen togs med Postman v10.15.1 för Mac, men gränssnittsalternativen kan ha ändrats.


1. Hämta och installera [[!DNL Postman]](https://www.postman.com/downloads/)
1. Öppna [!DNL Postman] och skapa en arbetsyta
   ![Importmiljö](assets/postman-createWorkspace.png)

1. Importera den hämtade JSON-miljöfilen, `oauth_server_to_server.postman_environment.json`
   ![Importmiljö](assets/postman-importEnvironment.png)
1. I [!DNL Postman] väljer du din miljö i listrutan

1. Markera ikonen om du vill visa miljövariablerna:

   ![Ändra miljö](assets/postman-changeEnvironment.png)


### Lägg till sandlådenamn och klient-ID

Variablerna `SANDBOX_NAME`, `TENANT_ID` och `CONTAINER_ID` ingår inte i Adobe Developer Console-exporten, så vi lägger till dem manuellt:

1. Öppna **Miljövariabler** i [!DNL Postman]
1. Markera länken **Redigera** till höger om miljönamnet
1. I fältet **Lägg till ny variabel** anger du `SANDBOX_NAME`
1. I båda värdefälten anger du `luma-tutorial`, det namn som vi gav till vår sandlåda i föregående lektion. Om du har använt ett annat namn för sandlådan, till exempel luma-tutorial-igatiusjreilly, måste du använda det värdet.
1. I fältet **Lägg till ny variabel** anger du `TENANT_ID`
1. Växla till din webbläsare och leta upp ditt företags klientorganisations-ID genom att gå till Experience Platform-gränssnittet och extrahera delen av URL:en *efter @-tecknet*. Min klient-ID är till exempel `techmarketingdemos` men din är annorlunda:

   ![Hämtar klient-ID från plattformsgränssnittets URL](assets/postman-getTenantId.png)

1. Kopiera det här värdet och gå tillbaka till skärmen [!DNL Postman] Hantera miljöer
1. Klistra in ditt klient-ID i båda värdefälten
1. I fältet **Lägg till ny variabel** anger du `CONTAINER_ID`
1. Ange `global` i båda värdefälten

   >[!NOTE]
   >
   >`CONTAINER_ID` är ett fält vars värde vi ändrar flera gånger under självstudien. När `global` används interagerar API med element som tillhandahålls av Adobe i ditt plattformskonto. När `tenant` används interagerar API med dina egna anpassade element.

1. Välj **Spara**

   ![Fälten SANDBOX_NAME, TENANT_ID och CONTAINER_ID har lagts till som systemvariabler](assets/postman-addEnvFields.png)



## Göra API-anrop

### Hämta en åtkomsttoken

Adobe har en omfattande uppsättning [!DNL Postman] samlingar som hjälper dig att utforska Experience Platform API. De här samlingarna finns i [Adobe Experience Platform Postman Samples GitHub-repo](https://github.com/adobe/experience-platform-postman-samples). Du bör skapa ett bokmärke för det här svaret eftersom du kommer att använda det här flera gånger i den här kursen och senare när du implementerar Experience Platform för ditt eget företag.

Den första samlingen fungerar med Adobe Identity Management Service (IMS) API:er. Det är ett bekvämt sätt att hämta en åtkomsttoken inifrån Postman.

Så här skapar du en åtkomsttoken:

1. Hämta samlingen [Identity Management Service API:er](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) till din `Luma Tutorial Assets`-mapp
1. Importera samlingen till [!DNL Postman]
1. Välj begäran **Autentisering: Begär åtkomsttoken** och välj **Skicka**
1. Du bör få ett `200 OK`-svar med en åtkomsttoken i svaret

   ![Begär tokens](assets/postman-requestToken.png)

1. Åtkomsttoken ska lagras automatiskt som miljövariabeln **ACCESS_TOKEN** i [!DNL Postman]-miljön.

   ![Postman](assets/postman-config.png)


### Interagera med en plattform-API

Låt oss nu ringa ett Platform API-anrop för att bekräfta att vi har konfigurerat allt korrekt.

Öppna [Experience Platform [!DNL Postman] samlingarna i GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Det finns många samlingar på den här sidan för olika plattforms-API:er. Jag rekommenderar att du bokmärker det.

Låt oss ringa vårt första API-anrop:

1. Hämta [API-samlingen för schemaregister](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Schema%20Registry%20API.postman_collection.json) till mappen `Luma Tutorial Assets`
1. Importera den till [!DNL Postman]
1. Öppna **API för schemaregister > Scheman > Lista scheman**
1. Titta på flikarna **Parametrar** och **Sidhuvuden** och se hur de innehåller några av de miljövariabler som vi angav tidigare.
1. Observera att fältet **Sidhuvuden > Acceptera värde** är inställt på `application/vnd.adobe.xed-id+json`. API:erna för schemaregister kräver ett av dessa [angivna värden för Acceptera sidhuvud](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#accept) som har olika format i svaret.
1. Välj **Skicka** för att göra ditt första Platform API-anrop!

Förhoppningsvis har du fått ett `200 OK`-svar som innehåller en lista över tillgängliga XDM-scheman som tillhandahålls av Adobe i din sandlåda, enligt bilden nedan.

![Första API-anrop i Postman](assets/postman-firstAPICall.png)

Om samtalet inte lyckades kan du felsöka med hjälp av felsvarsinformationen för API-anropet och granska stegen ovan. Om du fastnar ber du om hjälp i [Community-forumet](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community) eller använder länken till höger på den här sidan för att logga ett problem.

Med din plattformsbehörighet, sandlåda och [!DNL Postman] konfigurerad är du redo att [modellera data i scheman](model-data-in-schemas.md)!
