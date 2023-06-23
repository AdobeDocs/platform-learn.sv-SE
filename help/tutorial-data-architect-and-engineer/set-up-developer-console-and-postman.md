---
title: Konfigurera Developer Console och Postman
seo-title: Set up Developer Console and Postman | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Konfigurera Developer Console och Postman
description: I den här lektionen ska du skapa ett projekt i Adobe Developer Console och ge dig [!DNL Postman] Samlingar så att du kan börja använda plattforms-API:er.
role: Data Architect, Data Engineer
feature: API
jira: KT-4348
thumbnail: 4348-set-up-developer-console-and-postman.jpg
exl-id: 72b541fa-3ea1-4352-b82b-c5b79ff98491
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 0%

---

# Konfigurera Developer Console och [!DNL Postman]

<!--30min-->

I den här lektionen ska du skapa ett projekt i Adobe Developer Console och ladda ned det [!DNL Postman] samlingar så att du kan börja använda Platform API:er.

För att slutföra API-övningarna i den här självstudiekursen [hämta Postman-appen för ditt operativsystem.](https://www.postman.com/downloads/) Postman är inte nödvändigt för att kunna använda Experience Platform API:er, men underlättar API-arbetsflöden och Adobe Experience Platform tillhandahåller dussintals Postman-samlingar som hjälper dig att köra API-anrop och lära dig hur de fungerar. Resten av den här självstudiekursen bygger på en del praktiska kunskaper i Postman. Om du behöver hjälp kan du läsa [Postman-dokumentation](https://learning.postman.com/).

Plattformen är byggd för API. Även om det finns gränssnittsalternativ för alla viktiga uppgifter kan det vara bra att använda plattforms-API:t någon gång. Om du till exempel vill importera data flyttar du objekt mellan sandlådor, automatiserar rutinuppgifter eller använder nya plattformsfunktioner innan användargränssnittet har skapats.

**Dataarkitekturer** och **Datatekniker** kan behöva använda Platform API utanför den här självstudiekursen.

## Behörigheter krävs

I [Konfigurera behörigheter](configure-permissions.md) lektionen anger du alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--
* Permission item Sandboxes > `Luma Tutorial`
* Developer-role access to the `Luma Tutorial Platform` product profile
-->

## Konfigurera Adobe Developer Console

Adobe Developer Console är utvecklarmålet för att få tillgång till Adobe API:er och SDK:er, lyssna på nära nog med realtidshändelser, köra funktioner på körningsmiljön eller skapa plugin-program eller App Builder-program. Du kommer att använda den för att komma åt Experience Platform API:t. Mer information finns i [Adobe Developer Console-dokumentation](https://www.adobe.io/apis/experienceplatform/console/docs.html)

1. Skapa en mapp på din lokala dator med namnet `Luma Tutorial Assets` för filer som används i självstudiekursen.

1. Öppna [Adobe Developer Console](https://console.adobe.io){target="_blank"}

1. Logga in och bekräfta att du använder rätt Org

1. Välj **[!UICONTROL Skapa nytt projekt]** in [!UICONTROL Snabbstart] -menyn.

   ![Skapa nytt projekt](assets/adobeio-createNewProject.png)


1. I det nyskapade projektet väljer du **[!UICONTROL Redigera projekt]** knapp
1. Ändra **[!UICONTROL Projektets titel]** till `Luma Tutorial API Project` (lägg till ditt namn i slutet om flera personer från ditt företag använder den här självstudiekursen)
1. Välj **[!UICONTROL Spara]**

   ![API-konfiguration för Adobe Developer Console-projekt](assets/adobeio-renameProject.png)


1. Välj **[!UICONTROL Lägg till API]**

   ![API-konfiguration för Adobe Developer Console-projekt](assets/adobeio-addAPI.png)

1. Filtrera listan genom att välja **[!UICONTROL Adobe Experience Platform]**

1. I listan över tillgängliga API:er väljer du **[!UICONTROL Experience Platform API]** och markera **[!UICONTROL Nästa]**.

   ![API-konfiguration för Adobe Developer Console-projekt](assets/adobeio-AEPAPI.png)

1. Välj **[!UICONTROL OAuth Server-till-server]** som autentiseringsuppgifter och välj **[!UICONTROL Nästa]**.
   ![Välj OAuth Server-till-server](assets/adobeio-choose-auth.png)

1. Välj `AEP-Default-All-Users` produktprofil och välj **[!UICONTROL Spara konfigurerat API]**

   ![Välj produktprofil](assets/adobeio-selectProductProfile.png)

1. Nu har ditt Developer Console-projekt skapats!

1. I **[!UICONTROL Prova]** del av sidan, markera **[!UICONTROL Ladda ned för Postman]** och sedan markera **[!UICONTROL OAuth Server-till-server]** för att ladda ned [!DNL Postman] JSON-fil för miljö. Spara `oauth_server_to_server.postman_environment.json` i `Luma Tutorial Assets` mapp.


   ![API-konfiguration för Adobe Developer Console-projekt](assets/adobeio-io-api.png)

## Låt en systemadministratör lägga till API-autentiseringsuppgifterna i rollen

Om du vill använda API-autentiseringsuppgifterna för att interagera med Experience Platform måste du ha en systemadministratör som tilldelar API-autentiseringsuppgifterna till rollen som skapades i den föregående lektionen.  Om du inte är systemadministratör skickar du dem:

1. The [!UICONTROL Namn] API-autentiseringsuppgifter (`Credential in Luma Tutorial API Project`)
1. The [!UICONTROL E-post för tekniskt konto] av dina autentiseringsuppgifter (detta hjälper systemadministratören att hitta autentiseringsuppgifterna)

   ![[!UICONTROL Namn] och [!UICONTROL E-post för tekniskt konto] din inloggningsinformation](assets/postman-credentialDetails.png)

Här följer instruktionerna för systemadministratören:

1. Logga in [Adobe Experience Platform](https://platform.adobe.com)
1. Välj **[!UICONTROL Behörigheter]** i den vänstra navigeringen som tar dig till [!UICONTROL Roller] screen
1. Öppna `Luma Tutorial Platform` roll
   ![Öppna rollen](assets/postman-openRole.png)
1. Välj **[!UICONTROL API-autentiseringsuppgifter]** tab
1. Välj **[!UICONTROL Lägg till API-autentiseringsuppgifter]**
   ![Lägg till autentiseringsuppgifter](assets/postman-addCredential.png)
1. Hitta `Credential in Luma Tutorial API Project` autentiseringsuppgifter, filtrera med [!UICONTROL E-post för tekniskt konto] tillhandahålls av den som deltar i självstudiekursen, om listan är lång
1. Välj autentiseringsuppgifter
1. Välj **[!UICONTROL Spara]**


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
1. I [!DNL Postman]väljer du din miljö i listrutan

1. Markera ikonen om du vill visa miljövariablerna:

   ![Ändra miljö](assets/postman-changeEnvironment.png)


### Lägg till sandlådenamn och klient-ID

The `SANDBOX_NAME` och `TENANT_ID` och `CONTAINER_ID` variabler tas inte med i Adobe Developer Console-exporten, så vi lägger till dem manuellt:

1. I [!DNL Postman]öppnar du **Miljövariabler**
1. Välj **Redigera** länk till höger om miljönamnet
1. I **Lägg till nytt variabelfält**, ange `SANDBOX_NAME`
1. I båda värdefälten anger du `luma-tutorial`, namnet vi gav till vår sandlåda i föregående lektion. Om du har använt ett annat namn för sandlådan, till exempel luma-tutorial-igatiusjreilly, måste du använda det värdet.
1. I **Lägg till nytt variabelfält**, ange `TENANT_ID`
1. Byt till webbläsaren och leta upp företagets klient-ID genom att gå till Experience Platform gränssnitt och extrahera delen av URL:en *efter @-tecknet*. Min klient-ID är till exempel `techmarketingdemos` men din är annorlunda:

   ![Hämta klient-ID från plattformens gränssnitt-URL](assets/postman-getTenantId.png)

1. Kopiera det här värdet och gå tillbaka till [!DNL Postman] Skärmen Hantera miljöer
1. Klistra in ditt klient-ID i båda värdefälten
1. I **Lägg till nytt variabelfält**, ange `CONTAINER_ID`
1. Retur `global` till båda värdefälten

   >[!NOTE]
   >
   >`CONTAINER_ID` är ett fält vars värde vi ändrar flera gånger under självstudiekursen. När `global` används interagerar API med element som tillhandahålls av Adobe i ditt plattformskonto. När `tenant` används interagerar API:t med dina egna anpassade element.

1. Välj **Spara**

   ![SANDBOX_NAME-, TENANT_ID- och CONTAINER_ID-fält har lagts till som miljövariabler](assets/postman-addEnvFields.png)



## Göra API-anrop

### Hämta en åtkomsttoken

Adobe har en mängd [!DNL Postman] samlingar som hjälper dig att utforska Experience Platform API. Dessa samlingar finns i [Adobe Experience Platform Postman Samples GitHub repo](https://github.com/adobe/experience-platform-postman-samples). Du bör skapa ett bokmärke för det här svaret eftersom du kommer att använda det här flera gånger i den här självstudiekursen och senare när du implementerar Experience Platform för ditt eget företag.

Den första samlingen fungerar med Adobe Identity Management Service (IMS) API:er. Det är ett bekvämt sätt att hämta en åtkomsttoken inifrån Postman.

Så här skapar du en åtkomsttoken:

1. Ladda ned [Identity Management Service APIs-samling](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) till `Luma Tutorial Assets` mapp
1. Importera samlingen till [!DNL Postman]
1. Välj begäran **Autentisering: Åtkomsttoken för begäran** begära och markera **Skicka**
1. Du borde skaffa en `200 OK` svar med en åtkomsttoken i svaret

   ![Begär tokens](assets/postman-requestToken.png)

1. Åtkomsttoken ska lagras automatiskt som **ACCESS_TOKEN** systemvariabel för [!DNL Postman] miljö.

   ![Postman](assets/postman-config.png)


### Interagera med en plattform-API

Låt oss nu ringa ett Platform API-anrop för att bekräfta att vi har konfigurerat allt korrekt.

Öppna [Experience Platform [!DNL Postman] samlingar i GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Det finns många samlingar på den här sidan för olika plattforms-API:er. Jag rekommenderar att du bokmärker det.

Låt oss ringa vårt första API-anrop:

1. Ladda ned [API-samling för schemaregister](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Schema%20Registry%20API.postman_collection.json) till `Luma Tutorial Assets` mapp
1. Importera det till [!DNL Postman]
1. Öppna **Schema Registry API > Schemas > List schemas**
1. Titta på **Parametrar** och **Sidhuvuden** och notera hur de innehåller några av de miljövariabler som vi angav tidigare.
1. Observera att **Sidhuvuden > Acceptera värdefält** är inställd på `application/vnd.adobe.xed-id+json`. API:erna för schemaregister kräver något av dessa [angivna värden för Acceptera sidhuvud](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#accept) som ger olika format i svaret.
1. Välj **Skicka** för att göra ditt första Platform API-anrop!

Förhoppningsvis lyckas du `200 OK` svar som innehåller en lista med tillgängliga XDM-scheman från Adobe i din sandlåda, se bilden nedan.

![Första API-anrop i Postman](assets/postman-firstAPICall.png)

Om samtalet inte lyckades kan du felsöka med hjälp av felsvarsinformationen för API-anropet och granska stegen ovan. Om du fastnar ber du om hjälp i [Community-forum](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community) eller använd länken till höger på den här sidan för att logga ett problem.

Med plattformsbehörigheter, sandlåda och [!DNL Postman] konfigurera, du är redo att [modelldata i scheman](model-data-in-schemas.md)!
