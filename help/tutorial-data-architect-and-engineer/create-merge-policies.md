---
title: Skapa sammanfogningsprinciper
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Skapa sammanfogningsprinciper
description: I den här lektionen ska du skapa sammanfogningsprinciper som avgör hur data sammanfogas i profiler.
role: Data Architect, Data Engineer
feature: Profiles
jira: KT-4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: 915502e54365eedb09b12a92aa3b1af71f6de1f4
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Skapa sammanfogningsprinciper

<!--20 min-->

I den här lektionen ska du skapa kopplingsprofiler för att prioritera hur flera datakällor sammanfogas i profiler.

Med Adobe Experience Platform kan ni samla ihop data från olika källor och kombinera dem för att få en komplett bild av varje enskild kund. När dessa data samlas avgör kopplingsprofiler hur data prioriteras och vilka data som kombineras för att skapa den enhetliga vyn.

Vi följer användargränssnittet för den här lektionen, men API-alternativ finns också för att skapa sammanfogningsprinciper.

**Dataarkitekturer** måste skapa kopplingsprofiler utanför den här självstudiekursen.

Innan du börjar övningarna ska du titta på den här korta videon för att lära dig mer om kopplingsregler:
>[!VIDEO](https://video.tv.adobe.com/v/330433?learn=on)

## Behörigheter krävs

I [Konfigurera behörigheter](configure-permissions.md) lektionen anger du alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Om sammanslagningspolicyer och unionsschema

I lektionen om batchförbrukning kunde du komma ihåg att vi överförde två poster med något annorlunda information för samma kund. I [!DNL Loyalty] data, kundens förnamn var `Daniel` och han bodde i `New York City`men i CRM-data var kundens förnamn `Danny` och han bodde i `Portland`. Kunddata ändras över tid. Han kanske flyttade från `Portland` till `New York City`. Andra saker ändras också, till exempel telefonnummer och e-postadresser. Med sammanfogningsprinciper kan du bestämma hur du ska hantera den här typen av konflikter när två datakällor ger olika information för samma användare.

Så varför gjorde `Danny` vinner du som förnamn? Låt oss ta en titt:

1. I användargränssnittet för plattformen väljer du **[!UICONTROL Profiler]** till vänster navigering
1. Gå till **[!UICONTROL Sammanfoga profiler]** tab
1. Standardprincipen för sammanslagning är tidstämpelordning. Eftersom du överförde CRM-data efter lojalitetsdata, `Danny` uteslöts som förnamn i profilen:

![Skärm för sammanfogningsprincip](assets/mergepolicies-default.png)

När flera scheman är aktiverade för profilen, [!UICONTROL Unionens schema] skapas automatiskt för alla profilaktiverade postschemadelningar i en basklass. Du kan visa [!UICONTROL Unionens system] genom att gå till **[!UICONTROL Unionens schema]** -fliken.

![Skärm för sammanfogningsprincip](assets/mergepolicies-unionSchema.png)

Observera att det inte finns något unionsschema för klassen ExperienceEvent. ExperienceEvent-data fastnar fortfarande i profilen eftersom de är tidsseriebaserade, men varje händelse innehåller en tidsstämpel och id och kollisioner är inget problem.

Och om du inte gillar den standardprincipen för sammanslagning? Tänk om Luma bestämmer att deras lojalitetssystem ska vara källan till sanning när en konflikt uppstår? Därför ska vi skapa en sammanfogningspolicy.

## Skapa en kopplingsprofil i användargränssnittet

1. På skärmen Sammanfogningsprofiler väljer du **[!UICONTROL Skapa kopplingsprofil]** längst upp till höger
1. Som **[!UICONTROL Namn]**, ange `Loyalty Prioritized`
1. Som **[!UICONTROL Schema]**, markera **[!UICONTROL XDM-profil]** (Observera att din anpassade klass - eftersom den är postdata - också är tillgänglig för sammanfogningsprinciper)
1. För **[!UICONTROL ID-textning]**, markera **[!UICONTROL Privat diagram]**
1. För **[!UICONTROL Koppla attribut]**, markera **[!UICONTROL Datauppsättningsprioritet]**
1. Dra och släppa `Luma Loyalty Dataset` och `Luma CRM Dataset` till **[!UICONTROL Datauppsättning]** -panelen.
1. Kontrollera att `Luma Loyalty Dataset` ligger överst genom att dra och släppa det ovanför `Luma CRM Dataset`
1. Välj **[!UICONTROL Spara]** knapp
   <!--do i need to explain Private Graph? Is that GA?-->
   ![Kopplingsprincip](assets/mergepolicies-newPolicy.png)

## Validera sammanfogningsprincipen

Låt oss se om sammanfogningspolicyn gör vad vi kan förvänta oss:

1. Gå till **[!UICONTROL Bläddra]** tab
1. Ändra **[!UICONTROL Kopplingsprincip]** till dina nya `Loyalty Prioritized` policy
1. Som **[!UICONTROL Namnutrymme för identitet]** använder du `Luma CRM Id`
1. Som **[!UICONTROL Identitetsvärde]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Välj **[!UICONTROL Visa profil]** knapp
1. `Daniel` är tillbaka!

![Visa en profil med en annan sammanfogningsprincip](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Skapa en sammanfogningsprincip med begränsade datauppsättningar

När du skapar sammanfogningsprinciper med datauppsättningsprioritet, inkluderas bara datauppsättningar i samma basklass som du inkluderar till höger i profilen. Låt oss skapa en annan sammanfogningspolicy

1. På skärmen Sammanfogningsprofiler väljer du **[!UICONTROL Skapa kopplingsprofil]** längst upp till höger
1. Som **[!UICONTROL Namn]**, ange  `Loyalty Only`
1. Som **[!UICONTROL Schema]**, markera **[!UICONTROL XDM-profil]**
1. För **[!UICONTROL ID-textning]**, markera **[!UICONTROL Ingen]**
1. För **[!UICONTROL Koppla attribut]**, markera **[!UICONTROL Datauppsättningsprioritet]**
1. Dra och släpp endast `Luma Loyalty Dataset` till **[!UICONTROL Markerad datauppsättning]** -panelen.
1. Välj **[!UICONTROL Spara]** knapp

![Sammanfogningspolicy endast för lojalitet](assets/mergepolicies-loyaltyOnly.png)

## Validera sammanfogningsprincipen

Nu ska vi titta på vad den här sammanfogningspolicyn gör:

1. Gå till **[!UICONTROL Bläddra]** tab
1. Ändra **[!UICONTROL Kopplingsprincip]** till dina nya `Loyalty Only` policy
1. Som **[!UICONTROL Namnutrymme för identitet]** använder du `Luma CRM Id`
1. Som **[!UICONTROL Identitetsvärde]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Välj **[!UICONTROL Visa profil]** knapp
1. Bekräfta att inga profiler hittas:
   ![Endast lojalitet Ingen CRM-ID-sökning.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

CRM-ID är ett identitetsfält i `Luma Loyalty Dataset`, men bara primära identiteter kan användas för att söka efter profiler. Låt oss slå upp profilen med den primära identiteten, `Luma Loyalty Id`&quot;

1. Ändra **[!UICONTROL Identitetsnamnutrymme]** till `Luma Loyalty Id`
1. Som **[!UICONTROL Identitetsvärde]** use `5625458`
1. Välj **[!UICONTROL Visa profil]** knapp
1. Välj profil-ID för att öppna profilen
1. Gå till **[!UICONTROL Attribut]** tab
1. Observera att annan profilinformation från CRM-datauppsättningen, som mobiltelefonnumret och e-postadressen, inte är tillgänglig eftersom endast vi
   ![CRM-data kan inte visas i principen Endast lojalitet](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Gå till **[!UICONTROL Händelser]** tab
1. ExperienceEvent-data är tillgängliga trots att de inte uttryckligen ingår i dataset för sammanfogningsprinciper:
   ![Händelser kan visas i principen Endast lojalitet](assets/mergepolicies-loyaltyOnly-events.png)

## Mer om sammanfogningsprinciper

Ändra den sammanfogningsprincip som används i profilsökningen till `Default Timebased` och väljer **[!UICONTROL Visa profil]** -knappen. Danny är tillbaka!

![Visa en profil med en annan sammanfogningsprincip](assets/mergepolicies-backToDanny.png)

Vad är det som pågår här? Att sammanfoga profiler är inte en engångsgrej. Kundprofiler i realtid samlas ihop i farten, baserat på olika faktorer, bland annat vilken sammanfogningspolicy som används. Du kan skapa flera sammanfogningsprofiler som ska användas i olika sammanhang, beroende på vilken vy av kunden du vill ha.

Ett viktigt användningsexempel för sammanfogningsprinciper är datastyrning. Exempel: du importerar data från tredje part till plattformen som inte kan användas för personalisering, men _kan_ användas för reklamändamål. Du kan skapa en sammanfogningsprincip som utesluter den här tredjepartsdatauppsättningen och använda den här sammanfogningsprincipen för att skapa segment för dina reklamanvändningsfall.

## Ytterligare resurser

* [Dokumentation för kopplingsprofiler](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [API-referens för sammanslagningsprinciper (ingår i kundprofils-API i realtid)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Nu går vi vidare till [ramverk för datastyrning](apply-data-governance-framework.md).
