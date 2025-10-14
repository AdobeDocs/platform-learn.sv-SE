---
title: Skapa en sandlåda
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Skapa en sandlåda
description: I den här lektionen ska du skapa en sandlåda för utvecklingsmiljö som du kan använda för resten av självstudiekursen.
role: Data Architect, Data Engineer
feature: Sandboxes
jira: KT-4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Skapa en sandlåda

<!--25min-->

I den här lektionen ska du skapa en sandlåda för utvecklingsmiljö som du använder för resten av självstudiekursen.

Sandlådor har isolerade miljöer där du kan testa funktioner utan att blanda resurser och data med produktionsmiljön. Mer information finns i dokumentationen för [sandlådor](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=sv).

**Dataarkitekter** och **datatekniker** måste skapa sandlådor utanför den här självstudien.

Titta på den här korta videon för att lära dig mer om sandlådor innan du börjar övningarna:
>[!VIDEO](https://video.tv.adobe.com/v/3430296/?learn=on&enablevpops&captions=swe)

## Behörigheter krävs

I lektionen [Konfigurera behörigheter](configure-permissions.md) ställer du in alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## Skapa en sandlåda

Låt oss skapa en sandlåda:

1. Logga in i [Adobe Experience Platform](https://experience.adobe.com/platform)-gränssnittet
1. Gå till **[!UICONTROL Sandboxes]** i den vänstra navigeringen
1. Välj **[!UICONTROL Create sandbox]** överst till höger
   ![Välj Skapa sandlåda](assets/sandbox-createSandbox.png)

1. Välj **[!UICONTROL Development]** som **[!UICONTROL Type]**
1. Namnge din sandlåda `luma-tutorial` (överväg att lägga till ditt namn i slutet)
1. Ge din självstudiekurs namnet `Luma Tutorial` (överväg att lägga till ditt namn i slutet)
1. Markera knappen **[!UICONTROL Create]**
   ![Skapa din sandlåda](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >Även om du kan använda valfria godtyckliga värden för ditt sandlådenamn och din titel, rekommenderas att du följer de föreslagna värdena eftersom vi kommer att referera till dessa etiketter genom hela självstudiekursen. Om det finns flera personer i organisationen som slutför den här självstudiekursen kan du lägga till ditt namn i slutet av sandlådetiteln och namnet, till exempel luma-tutorial-igatiusjreilly.

Det tar cirka 30 sekunder att skapa sandlådor. Under den tiden visas statusen [!UICONTROL Creating]. När sandlådan är helt skapad visas den som [!UICONTROL Active]:
![&#x200B; Aktiv status &#x200B;](assets/sandbox-active.png)

Vänta tills din sandlåda är [!UICONTROL Active] innan du fortsätter med nästa övning.

## Lägg till den nya sandlådan i rollen

När sandlådan är aktiv måste du inkludera den i din roll för att kunna använda den. Så här lägger du till den i din roll (kräver behörighet som systemadministratör eller produktadministratör):

1. Gå till skärmen [!UICONTROL Permissions]
1. Öppna rollen `Luma Tutorial Platform`
1. Du kan även _ta bort_ sandlådan `Prod` från rollen
1. Lägg till sandlådan `Luma Tutorial`
1. Välj **[!UICONTROL Save]**
1. På raden [!UICONTROL Sandboxes] väljer du **[!UICONTROL Edit]**

   ![Lägg till lumatsjälvstudiekurs](assets/sandbox-addLumaTutorial.png)

1. Läs in sidan igen (eller Skift-läs in igen) och du bör nu antingen vara i sandlådan `Luma Tutorial` eller så bör den visas i din sandlådelistruta
1. Växla till sandlådan `Luma Tutorial` om du inte redan är i den

   ![Bekräfta sandlåda](assets/sandbox-confirmDropdown.png)

Bra, du har skapat din sandlåda och är redo att [konfigurera Developer Console och Postman](set-up-developer-console-and-postman.md)!
