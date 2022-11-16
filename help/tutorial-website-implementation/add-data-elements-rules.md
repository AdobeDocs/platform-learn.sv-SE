---
title: Lägga till ett dataelement, en regel och ett bibliotek
description: Lär dig hur du skapar dataelement, regler och ett bibliotek i taggar. Den här lektionen är en del av självstudiekursen Implementera Experience Cloud på webbplatser.
exl-id: 4d9eeb52-144a-4876-95d3-83d8eec4832f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 2%

---

# Lägga till ett dataelement, en regel och ett bibliotek

I den här lektionen skapar du ditt första dataelement, regel och bibliotek.

Dataelement och regler är de grundläggande byggstenarna för taggar. Data Elements lagrar de attribut du vill skicka till dina marknadsförings- och annonslösningar, medan Regler skickar förfrågningar till dessa lösningar under rätt förhållanden.  Bibliotek är de JavaScript-filer som läses in på sidan för att göra allt arbete. I den här lektionen ska du använda alla tre för att få vår exempelsida att göra något.

>[!NOTE]
>
>Adobe Experience Platform Launch håller på att integreras i Adobe Experience Platform som en serie datainsamlingstekniker. Flera terminologiska förändringar har introducerats i gränssnittet som du bör vara medveten om när du använder det här innehållet:
>
> * platforma launchen (klientsidan) är nu **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)**
> * platform launch Server Side is now **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge-konfigurationer är nu **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**


## Utbildningsmål

När lektionen är klar kan du:

* Skapa ett dataelement
* Skapa en regel
* Skapa ett bibliotek
* Lägga till ändringar i ett bibliotek
* Verifiera att biblioteket läses in i webbläsaren
* Arbeta effektivare med funktionen &quot;Arbetsbibliotek&quot;

## Skapa ett dataelement för sidnamn

Dataelement är taggarnas version av ett datalager. De kan lagra värden från ditt eget datalager, cookies, lokala lagringsobjekt, frågesträngsparametrar, sidelement, metataggar osv. I den här övningen skapar du ett dataelement för Sidnamn, som du kommer att använda senare i dina Target- och Analytics-implementeringar.

**Skapa ett dataelement**

1. Klicka på **[!UICONTROL Dataelement]**

1. Eftersom du inte har skapat några dataelement än i den här egenskapen visas en kort video med ytterligare information om det här avsnittet. Titta på den här videon, om du vill.

1. Klicka på **[!UICONTROL Skapa nytt dataelement]** knapp:

   ![Klicka på knappen Skapa nytt dataelement](images/launch-newDataElement.png)

1. Namnge dataelementet, t.ex. `Page Name`

1. Använd [!UICONTROL JavaScript-variabel] Dataelementtyp som pekar på ett värde i exempelsidans datalager: `digitalData.page.pageInfo.pageName`

1. Markera rutorna för **[!UICONTROL Använd gemener]** och **[!UICONTROL Rensa text]** standardisera ärendet och ta bort ovidkommande utrymmen

1. Lämna **[!UICONTROL Ingen]** som **[!UICONTROL Lagringstid]** eftersom det här värdet vanligtvis är olika på alla sidor

1. Klicka på **[!UICONTROL Spara]** knapp för att spara dataelementet

   ![Skapa dataelementet Sidnamn](images/launch-dataElement.png).

>[!NOTE]
>
>Dataelementsfunktioner _kan utökas med tillägg_. Med tillägget ContextHub kan du till exempel lägga till dataelement med hjälp av tilläggsfunktioner.

## Skapa en regel

Därefter använder du det här dataelementet i en enkel regel. Regler är en av de mest kraftfulla funktionerna i taggar och gör att du kan ange vad som ska hända när besökaren interagerar med webbplatsen. När villkoren som beskrivs i reglerna är uppfyllda utlöser regeln den åtgärd som du har angett.

Du ska skapa en regel som skickar dataelementvärdet för sidnamnet till webbläsarkonsolen.

**Skapa en regel**

1. Klicka på **[!UICONTROL Regler]**

1. Eftersom du inte har skapat några regler än i den här egenskapen visas en kort video med ytterligare information om ämnet. Titta på den här videon, om du vill.

1. Klicka på **[!UICONTROL Skapa ny regel]** knapp:

   ![Klicka på knappen Skapa ny regel](images/launch-newRule.png)

1. Namnge regeln `All Pages - Library Loaded`. Den här namnkonventionen anger var och när regeln kommer att utlösas, vilket gör det enklare att identifiera och återanvända när taggegenskapen mognar.

1. Klicka på under Händelser **[!UICONTROL Lägg till]**. Händelsen talar om för taggar när regeln ska utlösas och kan vara många saker, bland annat en sidinläsning, ett klick, en anpassad JavaScript-händelse osv.

   ![Namnge regeln och lägg till en händelse](images/launch-addEventToRule.png)

   1. Som händelsetyp väljer du **[!UICONTROL Bibliotek inläst (sidan ovanpå)]**. Observera att när du väljer händelsetyp fylls ett namn för händelsen i automatiskt med taggen. Observera också att standardordningen för händelsen är 50. Ordning är en kraftfull funktion i taggar som ger dig exakt kontroll över sekvensen av åtgärder när du har flera regler som aktiveras av samma händelse. Du kommer att använda den här funktionen senare i självstudiekursen.

   1. Klicka på **[!UICONTROL Behåll ändringar]** knapp

   ![Välj en händelse](images/launch-ruleSelectEvent.png)

1. Eftersom den här regeln ska starta på alla sidor kan du lämna **[!UICONTROL Villkor]** tom. Om du öppnar modala villkor kan du se att villkor kan lägga till både begränsningar och undantag baserat på en mängd olika alternativ, bland annat URL:er, dataelementvärden, datumintervall och mycket annat.

1. Klicka på under Åtgärder **[!UICONTROL Lägg till]**

1. Välj **[!UICONTROL Åtgärdstyp > Anpassad kod]**, vilket i det här skedet är det enda alternativet. Senare i självstudiekursen, när du lägger till tillägg, finns det fler alternativ.

1. Välj **[!UICONTROL &lt;/> Öppna redigeraren]** för att öppna kodredigeraren

   ![Välj en åtgärd](images/launch-selectAction.png)

1. Lägg till följande i kodredigeraren. Den här koden skickar värdet för dataelementet Sidnamn till webbläsarkonsolen så att du kan bekräfta att det fungerar:

   ```javascript
   console.log('The page name is '+_satellite.getVar('Page Name'));
   ```

1. Spara kodredigeraren

   ![Ange egen kod](images/launch-customCodeAction.png)

1. På skärmen Åtgärdskonfiguration klickar du på **[!UICONTROL Behåll ändringar]**

1. Klicka **[!UICONTROL Spara]** för att spara regeln

På sidan Regler ska du se din nya regel:
![Regeln visas på sidan](images/launch-savedRule.png)

## Spara ändringarna i ett bibliotek

När du har konfigurerat en samling tillägg, dataelement och regler i gränssnittet för datainsamling måste du paketera dessa funktioner och logik i en uppsättning JavaScript-kod som du kan distribuera på webbplatsen så att marknadsföringstaggarna utlöses när besökarna kommer till webbplatsen. Ett bibliotek är den uppsättning JavaScript-kod som ska göra detta.

I en tidigare lektion implementerade du inbäddningskoden för utvecklingsmiljön på exempelsidan. När du läste in exempelsidan returnerades ett 404-fel för inbäddningskodens URL eftersom ett taggbibliotek ännu inte har skapats och tilldelats miljön. Nu ska du placera ditt nya dataelement och linjera i ett bibliotek så att exempelsidan kan göra något.

**Lägga till och skapa ett bibliotek**

1. Klicka på **[!UICONTROL Publiceringsflöde]**

1. Klicka **[!UICONTROL Lägg till nytt bibliotek]**

   ![Lägg till nytt bibliotek](images/launch-addNewLibrary.png)

1. Namnge biblioteket, t.ex. `Initial Setup`

1. Välj **[!UICONTROL Miljö > Utveckling]**

1. Klicka **[!UICONTROL Lägg till alla ändrade resurser]**

   ![Lägg till alla ändrade resurser](images/launch-addAllChangedResources.png)

1. Observera att efter att du klickat **[!UICONTROL Lägg till alla ändrade resurser]** -taggar sammanfattar de ändringar du just har gjort.

1. Klicka **[!UICONTROL Spara och bygg för utveckling]**

   ![Spara och bygg för utveckling](images/launch-saveAndBuild.png)

Efter en stund blir statuspunkten grön vilket anger att biblioteket har skapats.

![Library Built](images/launch-libraryBuilt.png)

## Validera ditt arbete

Verifiera nu att regeln fungerar som förväntat.

Läs in exempelsidan igen. Om du tittar på fliken Utvecklarverktyg -> Nätverk bör du nu se ett svar från 200 för ditt taggbibliotek!

![Biblioteksladdningar med 200 svar](images/samplepage-200.png)

Om du tittar på Developer Tools -> Console bör du se texten&quot;The page name is home&quot;

![Konsolmeddelande](images/samplepage-console.png)

Grattis! Du har skapat ditt första dataelement och regel och byggt upp ditt första taggbibliotek!

## Använda funktionen Arbetsbibliotek

När du gör många ändringar i taggar är det inte praktiskt att behöva gå till fliken Publicera, lägga till ändringar och skapa biblioteket varje gång du vill se resultatet.  Nu när du har skapat ditt bibliotek för&quot;Inledande konfiguration&quot; kan du använda funktionen&quot;Arbetsbibliotek&quot; för att snabbt spara ändringarna och återskapa biblioteket i ett enda steg.

Gör en liten ändring i regeln &quot;Alla sidor - Biblioteksinläsning&quot;. Klicka på **[!UICONTROL Regler]** och klicka sedan på `All Pages - Library Loaded` regel som öppnar den.

![Öppna regeln igen](images/launch-reopenRule.png)

På `Edit Rule` klickar du på ***[!UICONTROL Arbetsbibliotek]*** listruta och välj `Initial Setup` bibliotek.

![Välj Inledande konfiguration som arbetsbibliotek](images/launch-setWorkingLibrary.png)

När du har valt biblioteket bör du se att **[!UICONTROL Spara]** knappen är nu standard till **[!UICONTROL Spara i bibliotek]**. När du ändrar taggar kan du använda det här alternativet för att automatiskt lägga till ändringen direkt i ditt arbetsbibliotek och/eller återskapa den.

Testa det. Öppna åtgärden Egen kod och lägg bara till ett kolon efter texten&quot;Sidnamnet är&quot; så att hela kodblocket läser:

```javascript
console.log('The page name is: '+_satellite.getVar('Page Name'));
```

Spara koden, behåll ändringarna i funktionsmakrot och klicka nu på **[!UICONTROL Spara i bibliotek och bygge]** -knappen.

![Alternativet Spara och skapa finns nu](images/launch-workingLibrary-saveAndBuild.png)

Vänta ett ögonblick tills den gröna punkten visas igen bredvid [!UICONTROL Arbetsbibliotek] listruta. Läs nu in exempelsidan igen så bör du se ändringen i konsolmeddelandet (du kanske måste rensa webbläsarens cache och läsa in den igen för att kunna se ändringen på sidan):

![Konsolmeddelande med kolon](images/samplepage-consoleWithColon.png)

Det här är ett mycket snabbare sätt att arbeta och du kommer att använda den här metoden för resten av självstudiekursen.

[Nästa&quot;Byt miljö med Experience Cloud Debugger&quot; >](switch-environments.md)
