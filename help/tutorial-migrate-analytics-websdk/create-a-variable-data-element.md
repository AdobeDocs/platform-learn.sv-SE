---
title: Skapa ett variabeldataelement
description: Lägg till ett dataelement som ska byggas upp över flera regler och sedan skickas in till Edge Network och vidarebefordras till Adobe Analytics
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16759
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Skapa ett variabeldataelement

Lägg till ett dataelement som byggs upp av flera regler och skickas sedan in i Edge Network och vidarebefordras till Adobe Analytics.

Detta dataelement skapar objektet&quot;Data&quot;, som används för att skicka tillbaka Adobe Analytics-variabler (props, eVars, events osv.) till Adobe Analytics och Adobe Target. Precis som när vi bygger upp&quot;s object&quot; i en AppMeasurementen implementering i Analytics, kommer vi att bygga upp den här typen:Variable-objekt som ska vara tillgängligt och uppdateras över alla regler, och det kan användas för att fylla i props och eVars i Analytics.

1. Klicka på **Dataelement** i den vänstra navigeringen i datainsamlingsgränssnittet.

   Du kommer till landningssidan för dataelement där du kan se alla dina befintliga dataelement. Vi måste skapa ett nytt dataelement för att underlätta migreringen. Klicka på **Lägg till dataelement**.

   ![Lägg till dataelement](assets/add-new-data-alement.jpg)

1. Konfigurera dataelementet.
   1. Ge dataelementet ett namn som du vill - något som hjälper dig att komma ihåg att detta bygger ut data på sidan och att det här blir typen&quot;Variabel&quot;. Den här självstudiekursen kallas **Datavariabel för sidvy**.
   1. Välj **Adobe Experience Platform Web SDK** i listrutan Tillägg.
   1. Välj **Variabel** i listrutan **Dataelementtyp**.
   1. Markera alternativknappen **Data** på den högra panelen.
   1. Kontrollera även **Adobe Analytics**-lösningen och någon av de andra lösningarna som du migrerar, t.ex. **Adobe Target** som visas på den här skärmbilden.
1. Klicka på **Spara**.

   ![Konfigurera variabeldataelement](assets/configure-variable-data-element.jpg)
