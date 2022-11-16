---
title: Skapa en sandlåda
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Skapa en sandlåda
description: I den här lektionen ska du skapa en sandlåda för utvecklingsmiljö som du kan använda för resten av självstudiekursen.
role: Data Architect, Data Engineer
feature: Sandboxes
kt: 4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Skapa en sandlåda

<!--25min-->

I den här lektionen ska du skapa en sandlåda för utvecklingsmiljö som du använder för resten av självstudiekursen.

Sandlådor har isolerade miljöer där du kan testa funktioner utan att blanda resurser och data med produktionsmiljön. Mer information finns i [dokumentation för sandlådor](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html).

**Dataarkitekturer** och **Datatekniker** måste skapa sandlådor utanför den här självstudiekursen.

Titta på den här korta videon för att lära dig mer om sandlådor innan du börjar övningarna:
>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

## Behörigheter krävs

I [Konfigurera behörigheter](configure-permissions.md) lektionen anger du alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## Skapa en sandlåda

Låt oss skapa en sandlåda:

1. Logga in på [Adobe Experience Platform](https://experience.adobe.com/platform) gränssnitt
1. Gå till **[!UICONTROL Sandlådor]** i den vänstra navigeringen
1. Välj **[!UICONTROL Skapa sandlåda]** överst till höger
   ![Välj sandlådan Skapa](assets/sandbox-createSandbox.png)

1. Välj **[!UICONTROL Utveckling]** som **[!UICONTROL Typ]**
1. Namnge din sandlåda `luma-tutorial` (överväg att lägga till ditt namn i slutet)
1. Ge din handledning en självstudiekurs `Luma Tutorial` (överväg att lägga till ditt namn i slutet)
1. Välj **[!UICONTROL Skapa]** knapp
   ![Skapa din sandlåda](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >Även om du kan använda valfria godtyckliga värden för ditt sandlådenamn och din titel, rekommenderas att du följer de föreslagna värdena eftersom vi kommer att referera till dessa etiketter genom hela självstudiekursen. Om det finns flera personer i organisationen som slutför den här självstudiekursen kan du lägga till ditt namn i slutet av sandlådetiteln och namnet, till exempel luma-tutorial-igatiusjreilly.

Det tar ca 30 sekunder att skapa sandlådor. Under tiden skapas en[!UICONTROL Skapar]&quot; visas. När sandlådan är helt skapad visas den som[!UICONTROL Aktiv]&quot;:
![Aktiv status](assets/sandbox-active.png)

Vänta tills sandlådan är[!UICONTROL Aktiv]&quot; innan man fortsätter med nästa övning.

## Lägg till den nya sandlådan i produktprofilen

När sandlådan är aktiv måste du inkludera den i din produktprofil för att kunna använda den. Så här lägger du till den i din produktprofil:

1. På en separat flik i webbläsaren loggar du in på [Admin Console](https://adminconsole.adobe.com)
1. Gå till **[!UICONTROL Produkter > Adobe Experience Platform]**
1. Öppna `Luma Tutorial Platform` profil

   ![Välj produktprofil](assets/sandbox-selectProfile.png)

1. Gå till **[!UICONTROL Behörigheter]** tab

1. På [!UICONTROL Sandlådor] rad, markera **[!UICONTROL Redigera]**

   ![Välj Redigera](assets/sandbox-selectSandboxes.png)

1. _Ta bort_ den **[!UICONTROL Prod]** sandlåda som du tilldelade profilen ursprungligen
1. Välj **[!UICONTROL +]** ikon för att lägga till den nya `Luma Tutorial` sandlåda till höger kolumn
1. Välj **[!UICONTROL Spara]** för att spara de uppdaterade behörigheterna

   ![Flytta sandlådan till den andra kolumnen](assets/sandbox-addLumaTutorial.png)

1. Gå tillbaka till webbläsarfliken med Experience Platform
1. Läs in sidan igen (eller Skift-läs in igen) och du bör nu antingen vara i `Luma Tutorial` sandlådan eller den ska visas i din sandlådelistruta
1. Växla till `Luma Tutorial` sandlåda om du inte redan finns i den

   ![Bekräfta sandlåda](assets/sandbox-confirmDropdown.png)

Bra, du har skapat din sandlåda och är redo att [Konfigurera Developer Console och Postman](set-up-developer-console-and-postman.md)!
