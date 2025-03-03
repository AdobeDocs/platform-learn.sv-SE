---
title: Migrera globala variabler
description: Lär dig hur du migrerar globala variabler från tilläggskonfigurationen för Analytics till Web SDK
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-17277
exl-id: 0917e951-c7e0-4723-8354-d308890bdaac
source-git-commit: 744b26da58307f0d6f6e8715a534ca814e02371c
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# Migrera globala variabler

I den här övningen får du lära dig hur du migrerar globala variabler från Analytics-tilläggskonfigurationen till Web SDK.

## Översikt

I Adobe Analytics-tillägget finns det ett konfigurationsavsnitt som heter&quot;Globala variabler&quot;.

![Etikett för globala variabler](assets/analytics-global-variables-label.jpg)

Globala variabler är variabler som ställs in på Analytics-spårningsobjektet när det objektet initieras på sidan. Alla variabler som du anger här ställs in när spårningsobjektet skapas på varje sida.

![Global variabeluppsättning](assets/analytics-set-global-variables.jpg)

Om du anger variabler här måste vi migrera även dessa till Web SDK.

## Var lägger man in globala variabler i Web SDK

Den **sista raden** här är att det inte finns något motsvarande område i konfigurationen av tillägget för Web SDK, så det blir inte så enkelt som att bara kopiera över variablerna som vi gjorde i Utskriftsregel för standardsida.
Det korta svaret är i stället: **Skapa en ny regel som körs före de andra reglerna på varje sida och ange variablerna där.**

Om du inte behöver definierade steg gör du det så är du klar med lektionen. Om du vill ha hjälp, fortsätt ...

### Steg för migrering av globala variabler till SDK på webben

1. Öppna Adobe Analytics tilläggskonfiguration

   ![En tilläggskonfiguration](assets/configure-analytics-extension.jpg)

1. Bläddra ned till avsnittet Globala variabler (bilden ovan), öppna det och notera några eller alla variabler som ställs in. Du måste känna till dessa variabler och värden i ett senare steg.
1. Avbryt bort från Analytics-tillägget.
1. Välj **Regler** i den vänstra navigeringen och klicka på **Lägg till regel**.
1. Ge den nya regeln namnet&quot;Globala variabler&quot;.
1. Klicka på knappen Lägg till under Händelser.

   ![Global variabelregel 1](assets/global-variable-rule-1.jpg)

1. Konfigurera händelsen som ska utlösas före dina andra regler. Du måste känna till händelsetypen och den ordning som du har använt i andra regler. Exempelvärden:
   1. Ange kärnan för **tillägget**
   1. **Händelsetypen** kan vara DOM-klar, beroende på implementeringen
   1. Expandera de **avancerade alternativen**
   1. Ställ in **Order** på ett lägre antal än dina andra regler, så att den körs först.
      ![Konfigurera global variabelhändelse](assets/configure-global-variable-event.jpg)
      >[!NOTE]
      >
      >Det viktigaste här är att den här regeln utlöses innan standardregeln för sidinläsning, så att alla variabler som anges i den här regeln kan skickas till Analytics via regeln sendEvent. Vi föreslår dock att den här regeln kör **first** generellt eftersom variablerna som anges i avsnittet Globala variabler i Analytics-tillägget kan ändras i andra regler. Vi härmar den funktionen. I exemplet ovan antar vi att&quot;10&quot; är ett lägre ordernummer än någon av dina andra regler. Om det inte stämmer ändrar du numret till ett tal som är lägre än dina andra regler.
1. Välj **Behåll ändringar** om du vill spara ditt arbete.
1. Du behöver inte lägga till villkor i den här regeln, så du kan låta det avsnittet av regelgenereringen vara.
1. Klicka på plusikonen under avsnittet **Åtgärder**
1. Konfigurera den nya åtgärden
   1. Välj Adobe Experience Platform Web SDK **Extension**
   1. Välj Uppdatera variabel för **Åtgärdstyp**
   1. Till höger väljer du variabeln **Dataelement** (i den här självstudiekursen kallades det&quot;Dataelement för sidvy&quot;, men det kan variera)
   1. Välj **Analytics** under dataobjektet
   1. Fyll i variablerna som du har sparat från avsnittet Globala variabler i konfigurationen för Analytics-tillägget (i den här självstudiekursen ställer du in eVar10 på sidelementet)

   ![websdk-global-variables-action](assets/websdk-global-variables-action.jpg)

1. Behåll ändringar
1. Spara regeln i ditt arbetsbibliotek och bygg

Dina globala variabler migreras nu till Web SDK och aktiveras vid sidinläsning.
