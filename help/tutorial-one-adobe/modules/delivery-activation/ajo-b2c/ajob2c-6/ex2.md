---
title: Landningssidor i Adobe Journey Optimizer
description: Landningssidor i Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
exl-id: bf499aad-91d0-4fb5-a38c-db8fcd56480b
source-git-commit: 83e8418b1a9e5e0e37f97473d2c7539ccd3fd803
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 8%

---

# 3.6.2 Landing Pages

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.6.2.1 prenumerationslistor

Landningssidor i Adobe Journey Optimizer fungerar tillsammans med **prenumerationslistor**. För att kunna konfigurera landningssidor måste du först konfigurera **prenumerationslistor**.

CitiSignal vill fråga sina kunder om deras intresse för följande domäner:

- Smart Home
- Arbeta hemifrån
- Onlinespel

När en kund har anmält sitt intresse för någon av dessa domäner, bör kunden läggas till i en viss lista så att den kan målinriktas med specifikt innehåll efteråt som en del av kommande kampanjer.

Du kommer nu att skapa 3 prenumerationslistor.

Gå till **Prenumerationslistor** på den vänstra menyn. Klicka på **Skapa prenumerationslista**.

![Landningssidor](./images/lp1.png)

Använd **för** Titel`--aepUserLdap--_SL_Interest_in_Smart_Home`.
Använd **för** Beskrivning`Interest in Smart Home`.

Klicka på **Skicka**.

![Landningssidor](./images/lp2.png)

Klicka på **Skapa prenumerationslista** om du vill skapa en annan lista.

![Landningssidor](./images/lp3.png)

Använd **för** Titel`--aepUserLdap--_SL_Interest_WFH`.
Använd **för** Beskrivning`Interest in Work From Home`.

Klicka på **Skicka**.

![Landningssidor](./images/lp4.png)

Klicka på **Skapa prenumerationslista** om du vill skapa en annan lista.

![Landningssidor](./images/lp5.png)

Använd **för** Titel`--aepUserLdap--_SL_Interest_Online_Gaming`.
Använd **för** Beskrivning`Interest in Online Gaming`.

Klicka på **Skicka**.

![Landningssidor](./images/lp6.png)

Du har nu skapat de tre listor du behöver.

![Landningssidor](./images/lp7.png)

## 3.6.2.2 förinställning för landningssida

För att kunna använda landningssidor i Adobe Journey Optimizer måste en förinställning skapas.

Gå till **Administration** > **Kanaler** på den vänstra menyn och välj sedan **Förinställningar för startsida**.

Klicka på **Skapa förinställning för landningssida**.

![Landningssidor](./images/lp8.png)

För fältet **Namn** använder du: `--aepUserLdap-- - CitiSignal LP` och väljer den underdomän som är tillgänglig i din instans.

>[!NOTE]
>
>Om du inte ser någon underdomän i din instans kontaktar du AJO-administratören för att få en.

Klicka på **Skicka**.

![Landningssidor](./images/lp9.png)

Din förinställning för landningssidan har nu skapats.

![Landningssidor](./images/lp10.png)

## Startsida för 3.6.2.3

Nu kan du skapa en landningssida. Gå till **Innehållshantering** > **Landing Pages** på den vänstra menyn.

Klicka på **Skapa landningssida**.

![Landningssidor](./images/lp11.png)

Använd **för fältet** Titel`vangeluw - CitiSignal Interests`. Välj sedan den **förinställning för landningssida** som du konfigurerade i föregående steg.

Klicka på **Skapa**.

![Landningssidor](./images/lp12.png)

Du borde se det här då.

![Landningssidor](./images/lp13.png)

Ändra fältet **Sidnamn** till `--aepUserLdap-- - CitiSignal Interests`.

Ange det här anpassade namnet under **Åtkomstinställningar**: `--aepUserLdap---citisignal-interests`.

Klicka på **Öppna Designer**.

![Landningssidor](./images/lp14.png)

Välj **Design från grunden**.

![Landningssidor](./images/lp15.png)

Du borde se det här då.

![Landningssidor](./images/lp16.png)

Lägg till en strukturkomponent **1:1 kolumn** på arbetsytan.

![Landningssidor](./images/lp17.png)

Lägg till innehållskomponenten **Form** på arbetsytan.

![Landningssidor](./images/lp18.png)

Uppdatera fältet **Etikett** för **Kryssruta 1** till `Keep me updated about CitiSignal's offering for Smart Home`.

Kontrollera att kryssrutan **Inaktivera om du har markerat** är aktiverad och att **prenumerationslista** är markerad.

Klicka sedan på **Välj prenumerationslista**.

![Landningssidor](./images/lp19.png)

Markera sedan listan `--aepUserLdap--_SL_Interest_in_Smart_Home` och klicka på **Välj**.

![Landningssidor](./images/lp20.png)

Klicka på **+ Lägg till fält** och välj sedan **Kryssruta**.

![Landningssidor](./images/lp21.png)

Du borde se det här då.

![Landningssidor](./images/lp22.png)

Uppdatera fältet **Etikett** för **Kryssruta 2** till `Keep me updated about CitiSignal's offering for Work From Home`.

Kontrollera att kryssrutan **Inaktivera om du har markerat** är aktiverad och att **prenumerationslista** är markerad.

Klicka sedan på **Välj prenumerationslista**.

![Landningssidor](./images/lp23.png)

Markera sedan listan `--aepUserLdap--_SL_Interest_WFH` och klicka på **Välj**.

![Landningssidor](./images/lp24.png)

Klicka på **+ Lägg till fält** och välj sedan **Kryssruta**.

![Landningssidor](./images/lp25.png)

Du borde se det här då.

![Landningssidor](./images/lp26.png)

Uppdatera fältet **Etikett** för **Kryssruta 3** till `Keep me updated about CitiSignal's offering for Online Gaming`.

Kontrollera att kryssrutan **Inaktivera om du har markerat** är aktiverad och att **prenumerationslista** är markerad.

Klicka sedan på **Välj prenumerationslista**.

![Landningssidor](./images/lp27.png)

Markera sedan listan `--aepUserLdap--_SL_Interest_Online_Gaming` och klicka på **Välj**.

![Landningssidor](./images/lp28.png)

Du borde se det här då.

![Landningssidor](./images/lp29.png)

Gå till formulärfältet **CALL TO ACTION**.

Uppdatera följande fält:

- **Text** - Knappetikett: `Save`.
- **Bekräftelseåtgärd**: välj **Bekräftelsetext**.
- **Bekräftelsetext**: använd: `Thanks for updating your preferences!`
- **Felåtgärd**: välj **Feltext**.
- **I feltexten**: använd: `There was an error updating your preferences.`

Klicka på **Spara** och sedan på pilen i det övre vänstra hörnet för att gå tillbaka till föregående skärm.

![Landningssidor](./images/lp30.png)

Klicka på **Publicera**.

![Landningssidor](./images/lp31.png)

Klicka på **Publicera** igen.

![Landningssidor](./images/lp32.png)

Din landningssida är nu publicerad och kan användas i ett e-postmeddelande.

![Landningssidor](./images/lp33.png)

## 3.6.2.4 Inkludera landningssida i e-post

I övning 3.1 skapade du en resa som kallas `--aepUserLdap-- - Registration Journey`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/published.png)

Du bör nu uppdatera e-postmeddelandet under den resan så att det innehåller länken till landningssidan.

Gå till **Resor** på den vänstra menyn och klicka för att öppna resan `--aepUserLdap-- - Registration Journey`.

![Landningssidor](./images/lp34.png)

Klicka på **Mer..** och välj sedan **Skapa en ny version**.

![Landningssidor](./images/lp35.png)

Klicka på **Skapa en ny version**.

![Landningssidor](./images/lp36.png)

Klicka för att välja åtgärden **E-post** och välj sedan **Redigera innehåll**.

![Landningssidor](./images/lp37.png)

Klicka på **Redigera e-postbrödtext**.

![Landningssidor](./images/lp38.png)

Då borde du se något sådant här. Lägg till en ny strukturkomponent, **1:1, kolumn**, på arbetsytan.

![Landningssidor](./images/lp39.png)

Lägg till den nya innehållskomponenten **Text** i den strukturkomponent som skapades nyligen.

![Landningssidor](./images/lp40.png)

Klistra in följande text i innehållskomponenten **Text**.

`Would you like to hear from us about Smart Home news? Do you work from home and would you like to hear our tips? Or are you an avid online gamer and do you want to receive our game reviews? Click here to update your preferences and interests!`

Formatera texten så att den ser ut så här och markera sedan ordet `here`. Klicka på ikonen **link** .

Ange länkens **typ** till **landningssida** och ställ in fältet **Mål** till **Tom**.

Klicka på ikonen **redigera** för att markera den landningssida som ska länkas.

![Landningssidor](./images/lp41.png)

Välj landningssidan `--aepUserLdap-- - CitiSignal Interests`. Klicka på **Markera**.

![Landningssidor](./images/lp42.png)

Du borde se det här då. Klicka på **Spara**.

![Landningssidor](./images/lp43.png)

Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till föregående skärm.

![Landningssidor](./images/lp44.png)

Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till föregående skärm igen.

![Landningssidor](./images/lp45.png)

Klicka på **Spara**.

![Landningssidor](./images/lp46.png)

Klicka på **Publicera**.

![Landningssidor](./images/lp47.png)

Klicka på **Publicera** igen.

![Landningssidor](./images/lp48.png)

Ändringarna har publicerats och du kan testa din resa.

![Landningssidor](./images/lp49.png)

## 3.6.2.5 Testa din resa och landningssida

Gå till [https://dsn.adobe.com](https://dsn.adobe.com). När du har loggat in med din Adobe ID ser du det här. Klicka på de tre punkterna **..** i webbplatsprojektet och klicka sedan på **Kör** för att öppna det.

![DSN](./../../datacollection/dc1.1/images/web8.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje övning måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen. Gå till **Logga in**

![DSN](../../../getting-started/gettingstarted/images/web7.png)

Klicka på **SKAPA ETT KONTO**. Fyll i dina uppgifter och klicka på **Registrera**.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv9.png)

Du kommer nu att omdirigeras till hemsidan. Öppna profilvisarpanelen och gå till kundprofilen i realtid. På panelen Profilvisningsprogram ska du se alla dina personuppgifter visas, som dina nya e-post- och telefonidentifierare.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv10.png)

1 minut efter att du har skapat ditt konto får du ett e-postmeddelande från Adobe Journey Optimizer om att du har skapat kontot.

Klicka på länken i e-postmeddelandet för att uppdatera dina inställningar.

![Starta installationsprogrammet](./images/email.png)

Du bör då se formuläret som du skapade. Aktivera några kryssrutor och klicka på **Spara**.

![Starta installationsprogrammet](./images/email1.png)

Därefter visas ett bekräftelsemeddelande.

![Starta installationsprogrammet](./images/email2.png)

## Rapportering av prenumerationslista för 3.6.2.6

Om du vill visa tillgängliga rapporter om prenumerationslistor går du till **Prenumerationslistor** på den vänstra menyn och klickar för att öppna en PDF-fil av de prenumerationslistor du konfigurerade tidigare.

![Landningssidor](./images/lp50.png)

Klicka på **Rapport**.

![Landningssidor](./images/lp51.png)

Du bör då se översikten över listan med det antal personer som har prenumererat eller avbrutit prenumerationen.

![Landningssidor](./images/lp52.png)

## Nästa steg

Gå till [3.6.3 AJO och GenStudio for Performance Marketing](./ex3.md)

Gå tillbaka till [Adobe Journey Optimizer: Innehållshantering](./ajocontent.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
