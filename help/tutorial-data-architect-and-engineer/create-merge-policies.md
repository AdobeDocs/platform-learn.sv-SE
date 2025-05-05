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
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Skapa sammanfogningsprinciper

<!--20 min-->

I den här lektionen ska du skapa kopplingsprofiler för att prioritera hur flera datakällor sammanfogas i profiler.

Med Adobe Experience Platform kan ni samla ihop data från olika källor och kombinera dem för att få en komplett bild av varje enskild kund. När dessa data samlas avgör kopplingsprofiler hur data prioriteras och vilka data som kombineras för att skapa den enhetliga vyn.

Vi följer användargränssnittet för den här lektionen, men API-alternativ finns också för att skapa sammanfogningsprinciper.

**Dataarkitekturer** måste skapa sammanfogningsprinciper utanför den här självstudien.

Innan du börjar övningarna ska du titta på den här korta videon för att lära dig mer om kopplingsregler:
>[!VIDEO](https://video.tv.adobe.com/v/330433?learn=on&enablevpops)

## Behörigheter krävs

I lektionen [Konfigurera behörigheter](configure-permissions.md) ställer du in alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Om sammanslagningspolicyer och unionsschema

I lektionen om batchförbrukning kunde du komma ihåg att vi överförde två poster med något annorlunda information för samma kund. I [!DNL Loyalty]-data var kundens förnamn `Daniel` och han/hon bodde i `New York City`, men i CRM-data var kundens förnamn `Danny` och han/hon bodde i `Portland`. Kunddata ändras över tid. Han kanske flyttade från `Portland` till `New York City`. Andra saker ändras också, till exempel telefonnummer och e-postadresser. Med sammanfogningsprinciper kan du bestämma hur du ska hantera den här typen av konflikter när två datakällor ger olika information för samma användare.

Varför vann `Danny` som förnamn? Låt oss ta en titt:

1. Välj **[!UICONTROL Profiles]** i den vänstra navigeringen i plattformens användargränssnitt
1. Gå till fliken **[!UICONTROL Merge Polices]**
1. Standardprincipen för sammanslagning är tidstämpelordning. Eftersom du överförde CRM-data efter lojalitetsdata, uteslöts `Danny` som förnamn i profilen:

![Skärmen Kopplingsprincip](assets/mergepolicies-default.png)

När flera scheman är aktiverade för profilen skapas en [!UICONTROL Union Schema] automatiskt för alla profilaktiverade, postschemadelningar för en basklass. Du kan visa [!UICONTROL Union Schemas] genom att gå till fliken **[!UICONTROL Union Schema]**.

![Skärmen Kopplingsprincip](assets/mergepolicies-unionSchema.png)

Observera att det inte finns något unionsschema för klassen ExperienceEvent. ExperienceEvent-data fastnar fortfarande i profilen eftersom de är tidsseriebaserade, men varje händelse innehåller en tidsstämpel och id och kollisioner är inget problem.

Och om du inte gillar den standardprincipen för sammanslagning? Tänk om Luma bestämmer att deras lojalitetssystem ska vara källan till sanning när en konflikt uppstår? Därför ska vi skapa en sammanfogningspolicy.

## Skapa en kopplingsprofil i användargränssnittet

1. Välj knappen **[!UICONTROL Create Merge Policy]** i det övre högra hörnet på skärmen Sammanfogningsprofiler
1. Ange `Loyalty Prioritized` som **[!UICONTROL Name]**
1. Som **[!UICONTROL Schema]** väljer du **[!UICONTROL XDM Profile]** (observera att din anpassade klass - eftersom den är postdata - också är tillgänglig för sammanfogningsprinciper)
1. För **[!UICONTROL Id Stitching]** väljer du **[!UICONTROL Private Graph]**
1. För **[!UICONTROL Attribute Merge]** väljer du **[!UICONTROL Dataset precedence]**
1. Dra och släpp `Luma Loyalty Dataset` och `Luma CRM Dataset` på panelen **[!UICONTROL Dataset]**.
1. Se till att `Luma Loyalty Dataset` är överst genom att dra och släppa det ovanför `Luma CRM Dataset`
1. Markera knappen **[!UICONTROL Save]**
   <!--do i need to explain Private Graph? Is that GA?-->
   ![Kopplingsprincip](assets/mergepolicies-newPolicy.png)

## Validera sammanfogningsprincipen

Låt oss se om sammanfogningspolicyn gör vad vi kan förvänta oss:

1. Gå till fliken **[!UICONTROL Browse]**
1. Ändra **[!UICONTROL Merge policy]** till din nya `Loyalty Prioritized`-princip
1. Använd din `Luma CRM Id` som **[!UICONTROL Identity namespace]**
1. Som **[!UICONTROL Identity value]** använder du `112ca06ed53d3db37e4cea49cc45b71e`
1. Markera knappen **[!UICONTROL Show profile]**
1. `Daniel` är tillbaka!

![Visa en profil med en annan sammanfogningsprincip](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Skapa en sammanfogningsprincip med begränsade datauppsättningar

När du skapar sammanfogningsprinciper med datauppsättningsprioritet, inkluderas bara datauppsättningar i samma basklass som du inkluderar till höger i profilen. Låt oss skapa en annan sammanfogningspolicy

1. Välj knappen **[!UICONTROL Create Merge Policy]** i det övre högra hörnet på skärmen Sammanfogningsprofiler
1. Ange `Loyalty Only` som **[!UICONTROL Name]**
1. Som **[!UICONTROL Schema]** väljer du **[!UICONTROL XDM Profile]**
1. För **[!UICONTROL Id Stitching]** väljer du **[!UICONTROL None]**
1. För **[!UICONTROL Attribute Merge]** väljer du **[!UICONTROL Dataset precedence]**
1. Dra och släpp bara `Luma Loyalty Dataset` till panelen **[!UICONTROL Selected Dataset]**.
1. Markera knappen **[!UICONTROL Save]**

![Sammanfogningsprincip endast för lojalitet](assets/mergepolicies-loyaltyOnly.png)

## Validera sammanfogningsprincipen

Nu ska vi titta på vad den här sammanfogningspolicyn gör:

1. Gå till fliken **[!UICONTROL Browse]**
1. Ändra **[!UICONTROL Merge policy]** till din nya `Loyalty Only`-princip
1. Använd din `Luma CRM Id` som **[!UICONTROL Identity namespace]**
1. Som **[!UICONTROL Identity value]** använder du `112ca06ed53d3db37e4cea49cc45b71e`
1. Markera knappen **[!UICONTROL Show profile]**
1. Bekräfta att inga profiler hittas:
   ![Lojalitet Endast ingen CRM-ID-sökning.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

CRM-ID är ett identitetsfält i `Luma Loyalty Dataset`, men bara primära identiteter kan användas för att söka efter profiler. Så låt oss slå upp profilen med den primära identiteten `Luma Loyalty Id`

1. Ändra **[!UICONTROL Identity Namespace]** till `Luma Loyalty Id`
1. Som **[!UICONTROL Identity value]** använder du `5625458`
1. Markera knappen **[!UICONTROL Show profile]**
1. Välj profil-ID för att öppna profilen
1. Gå till fliken **[!UICONTROL Attributes]**
1. Observera att annan profilinformation från CRM-datauppsättningen, som mobiltelefonnumret och e-postadressen, inte är tillgänglig eftersom endast vi
   ![CRM-data kan inte visas i principen Endast lojalitet](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Gå till fliken **[!UICONTROL Events]**
1. ExperienceEvent-data är tillgängliga trots att de inte uttryckligen ingår i dataset för sammanfogningsprinciper:
   ![Det går att visa händelser i principen Endast lojalitet](assets/mergepolicies-loyaltyOnly-events.png)

## Mer om sammanfogningsprinciper

I profilsökningen ändrar du den sammanslagningsprincip som används tillbaka till `Default Timebased` och väljer knappen **[!UICONTROL Show profile]**. Danny är tillbaka!

![Visa en profil med en annan sammanfogningsprincip](assets/mergepolicies-backToDanny.png)

Vad är det som pågår här? Att sammanfoga profiler är inte en engångsgrej. Kundprofiler i realtid samlas ihop i farten, baserat på olika faktorer, bland annat vilken sammanfogningspolicy som används. Du kan skapa flera sammanfogningsprofiler som ska användas i olika sammanhang, beroende på vilken vy av kunden du vill ha.

Ett viktigt användningsexempel för sammanfogningsprinciper är datastyrning. Exempel: du importerar data från tredje part till plattformen som inte kan användas för personalisering, men _kan_ användas för reklamändamål. Du kan skapa en sammanfogningsprincip som utesluter den här tredjepartsdatauppsättningen och använda den här sammanfogningsprincipen för att skapa segment för dina reklamanvändningsfall.

## Ytterligare resurser

* [Dokumentation för kopplingsprofiler](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html?lang=sv-SE)
* [API-referens för sammanslagningsprinciper (ingår i kundprofils-API:t i realtid)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Låt oss nu gå vidare till [ramverket för datastyrning](apply-data-governance-framework.md).
