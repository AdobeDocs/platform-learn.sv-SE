---
title: Konfigurera behörigheter
seo-title: Configure permissions | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Konfigurera behörigheter
description: I den här lektionen ska du konfigurera Adobe Experience Platform användarbehörigheter med Adobe Admin Console.
role: Data Architect, Data Engineer
feature: Access Control
kt: 4348
thumbnail: 4348-configure-permissions.jpg
exl-id: ca01f99e-f10c-4bf0-bef2-b011ac29a565
source-git-commit: 35242a037bc79f18e90399c47e47064634d26a37
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 1%

---

# Konfigurera behörigheter

<!--30min-->

I den här lektionen ska du konfigurera Adobe Experience Platform användarbehörigheter med [!DNL Adobe's Admin Console] och [!UICONTROL Behörigheter] i plattformsgränssnittet.

Åtkomstkontroll är en viktig sekretessfunktion i Experience Platform och vi rekommenderar att behörigheter begränsas till det minimum som krävs för att människor ska kunna utföra sina arbetsuppgifter. Se [Åtkomstkontrolldokumentation](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html) för mer information.

Dataarkitekter och datatekniker är kraftfulla användare av Adobe Experience Platform och du behöver många behörigheter för att kunna slutföra den här självstudiekursen och senare i ditt dagliga arbete. Dataarkitekter är sannolikt involverade i administrationen av *andra plattformsanvändare* på deras företag som marknadsförare, analytiker och datavetare. När du är klar med den här lektionen bör du tänka på hur du kan använda de här funktionerna för att hantera andra användare på ditt företag.

**Dataarkitekturer** konfigurerar ofta behörigheter för andra användare utanför den här självstudiekursen.

>[!IMPORTANT]
>
>En systemadministratör för Adobe Experience Cloud-produkter måste slutföra några av stegen i den här lektionen, som beskrivs i avsnittsrubrikerna. Om du inte är systemadministratör kontaktar du en på ditt företag och ber dem att slutföra dessa uppgifter. Det finns också en uppgift de måste slutföra under [Konfigurera Developer Console och Postman](set-up-developer-console-and-postman.md) lektion.

## Om Admin Console

The [!DNL Admin Console] är gränssnittet som används för att administrera användaråtkomst till alla Adobe Experience Cloud-produkter. För att få tillgång till Platform måste en användare eller användare läggas till i Admin Console och sedan hanteras alla deras detaljerade behörighetsobjekt på behörighetsskärmen i Adobe Experience Platform.


Här följer en snabb sammanfattning av rollerna som finns för Platform:

* **Användare** för en produktprofil kan slutföra åtgärder i plattformens användargränssnitt enligt de behörigheter som tilldelats i produktprofilen.
* **Utvecklare** kan skapa API-autentiseringsuppgifter och projekt i Adobe Developer Console för att kunna börja använda Experience Platform API
* **Produktadministratörer** kan lägga till användare och utvecklare i Adobe Experience Platform-produkten i Adobe Admin Console, samt hantera detaljerad användaråtkomst på behörighetsskärmen i plattformsgränssnittet.
* **Systemadministratörer** kan lägga till produktadministratörer och administrera i stort sett alla behörigheter för alla Adobe Experience Cloud-produkter.

## Lägg till en användare och utvecklare i `AEP-Default-All-Users` produktprofil (kräver systemadministratör eller produktadministratör)

I den här övningen kommer du eller en systemadministratör eller produktadministratör att lägga till dig som användare och utvecklare i Adobe Experience Platform-produkten av Adobe Admin Console.

>[!NOTE]
>
>Om du är systemadministratör och hjälper en kollega att ta den här självstudiekursen bör du överväga att lägga till din kollega som systemadministratör *Produktadministratör* för Adobe Experience Platform. Som produktadministratör kan de slutföra dessa steg på egen hand och administrera andra Experience Platform-användare i framtiden.

Lägga till en deltagare i självstudiekursen som en [!UICONTROL Användare] och [!UICONTROL Utvecklare]:

1. Logga in på [Adobe Admin Console](https://adminconsole.adobe.com)
1. Välj **[!UICONTROL Produkter]** i den övre navigeringen
1. Välj **Adobe Experience Platform**
   ![Välj Adobe Experience Platform](assets/adminconsole-experiencePlatform.png)
1. Du kan ha flera profiler i din Experience Platform-instans redan. Välj `AEP-Default-All-Users` profil
   ![Välj Lägg till ny profil](assets/adminconsole-newProfile.png)

1. Gå till **[!UICONTROL Användare]** tab
1. Välj **[!UICONTROL Lägg till användare]** knapp
   ![Välj Lägg till användare](assets/adminconsole-addUser.png)
1. Slutför arbetsflödet för att lägga till självstudiekursens deltagare som en användare i produktprofilen

1. Gå till **[!UICONTROL Utvecklare]** tab
1. Välj **[!UICONTROL Lägg till utvecklare]** knapp
   ![Välj Lägg till användare](assets/adminconsole-addDeveloper.png)
1. Slutför arbetsflödet för att lägga till självstudiekursens deltagare som utvecklare i produktprofilen


## Lägg till en roll i Adobe Experience Platform (kräver en systemadministratör eller produktadministratör)

Detaljerade behörigheter för Experience Platform hanteras på Behörighetsskärmen i plattformsgränssnittet. Endast system- och produktadministratörer har åtkomst till den här skärmen, så om du inte har administratörsbehörighet behöver du hjälp av någon som har det.

Behörigheter hanteras i roller. Skapa en roll för självstudiekursen:

1. Logga in [Adobe Experience Platform](https://platform.adobe.com)
1. Välj **[!UICONTROL Behörigheter]** i den vänstra navigeringen som tar dig till [!UICONTROL Roller] screen
1. Välj **[!UICONTROL Skapa roll]**

   ![Skapa en roll i Experience Platform](assets/permissions-addRole.png)
1. Namnge rollen `Luma Tutorial Platform` (lägg till namnet på den som deltar i självstudiekursen till slutet, om flera personer från ditt företag använder den här självstudiekursen) och välj **[!UICONTROL Bekräfta]**

   ![Skapa en roll i Experience Platform](assets/permissions-nameRole.png)


1. Lägg till alla behörighetsobjekt för följande resurser med  **[!UICONTROL +]** och **[!UICONTROL Lägg till alla]**:

   1. Datamodellering
   1. Datahantering
   1. Profilhantering
   1. Identity Management
   1. Sandlådeadministration
   1. Frågetjänst
   1. Datainsamling
   1. Datastyrning
   1. Kontrollpaneler
   1. Larm

      ![Lägg till behörighetsobjekt](assets/permissions-addPermissionItems.png)

1. Lägg till behörighetsobjekten Hantera källor och Visa källor under Datainmatning.

1. När du har lagt till alla behörighetsobjekt måste du välja knappen Spara
   ![Spara behörighetsobjekt](assets/permissions-savePermissions.png)

Du kommer att göra några små uppdateringar av den här rollen efter [Skapa en sandlåda](create-a-sandbox.md) och [Konfigurera Developer Console och Postman](set-up-developer-console-and-postman.md) lektioner.

## Skapa en produktprofil för datainsamling (kräver en systemadministratör eller produktadministratör)

I den här övningen skapar du eller en systemadministratör på ditt företag en produktprofil för datainsamling (tidigare Adobe Experience Platform Launch) och lägger till dig som produktprofiladministratör.

>[!NOTE]
>
>Om du är systemadministratör och hjälper en kollega med den här självstudiekursen kan du lägga till dem som en *Produktadministratör* för datainsamling. Som produktadministratör kan de slutföra dessa steg på egen hand och administrera andra användare av datainsamling i framtiden.

Så här skapar du produktprofilen:

1. I [!DNL Adobe Admin Console] gå till Adobe Experience Platform Data Collection
1. Lägg till en ny profil med namnet `Luma Tutorial Data Collection` (lägg till namnet på den som deltar i självstudiekursen till slutet om flera personer från ditt företag använder den här självstudiekursen)
1. Stäng av **[!UICONTROL Egenskaper]** > **[!UICONTROL Ta med automatiskt]** inställning
1. Tilldela inga egenskaper eller behörigheter just nu
1. Lägg till självstudiekursens deltagare som administratör för den här profilen

När du är klar med dessa steg bör du se att `Luma Tutorial Data Collection` har konfigurerats med en administratör.
![En datainsamlingsprofil har skapats](assets/adminconsole-dc-profileCreated.png)

## Konfigurera produktprofilen för datainsamling

Nu när du är administratör för `Luma Tutorial Data Collection` produktprofil du kan konfigurera de behörigheter och roller du behöver för att slutföra självstudiekursen.

### Lägg till behörigheter

Nu ska du lägga till de enskilda behörighetsobjekten i profilen:

1. I [Adobe Admin Console](https://adminconsole.adobe.com), gå till **[!UICONTROL Produkter]** > **[!UICONTROL Datainsamling]**
1. Öppna `Luma Tutorial Data Collection` profil
1. Gå till **[!UICONTROL Behörigheter]** tab
1. Öppna **[!UICONTROL Plattformar]**
1. Se till att alla tillgängliga plattformar är markerade (du kan se olika alternativ beroende på din licens)
1. **[!UICONTROL Spara]** alla ändringar
   ![Lägg till plattformar](assets/adminconsole-launch-addPlatforms.png)
1. Öppna **[!UICONTROL Egenskaper]**
1. Se till att **[!UICONTROL Inkludera automatiskt]** växlingsknappen är Av så att du inte har tillgång till några egenskaper (vi lägger till en senare)
1. **[!UICONTROL Spara]** alla ändringar
   ![Ta bort egenskaper](assets/adminconsole-launch-removeProperties.png)
1. Öppna **[!UICONTROL Egendomsrättigheter]**
1. Välj **[!UICONTROL Lägg till alla]** för att lägga till alla egenskapsbehörigheter
1. **[!UICONTROL Spara]**
   ![Ta bort egenskaper](assets/adminconsole-launch-addPropertyRights.png)
1. Öppna **[!UICONTROL Företagsrättigheter]**
1. Lägg till **[!UICONTROL Hantera egenskaper]**
1. Välj **[!UICONTROL Spara]**
   ![Ta bort egenskaper](assets/adminconsole-launch-companyRights.png)


### Lägg till dig själv som användare

Lägg till dig själv som användare i datainsamlingsprofilen:

1. Gå till **[!UICONTROL Användare]** tab
1. Välj **[!UICONTROL Lägg till användare]** knapp
   ![Välj Lägg till användare](assets/adminconsole-launch-addUser.png)
1. Slutför arbetsflödet för att lägga till dig själv som användare i produktprofilen

Du behöver inte lägga till dig själv som utvecklare för datainsamling.

Nu har du nästan alla behörigheter som krävs för att slutföra självstudiekursen! Det kommer bara att finnas ytterligare två förbättringar som du kan göra i [!DNL Adobe Admin Console], inklusive en efter dig [skapa en sandlåda](create-a-sandbox.md)!
