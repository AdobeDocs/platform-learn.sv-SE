---
title: Adobe Journey Optimizer - Konfigurera en utlösarbaserad resa - orderbekräftelse
description: I det här avsnittet konfigurerar du en utlösarbaserad resa - orderbekräftelse
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1997'
ht-degree: 0%

---

# 3.4.1 Konfigurera en utlösarbaserad resa - orderbekräftelse

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och väljer sandlådan i listan. I det här exemplet heter sandlådan **AEP Enablement FY22**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.1.1 Skapa en händelse

Gå till **Konfigurationer** på menyn och klicka på **Hantera** under **Händelser**.

![Journey Optimizer](./images/oc30.png)

På skärmen **Händelser** ser du en liknande vy. Klicka på **Skapa händelse**.

![Journey Optimizer](./images/oc31.png)

Därefter visas en tom händelsekonfiguration.

![Journey Optimizer](./images/oc32.png)

Först och främst ger du evenemanget ett namn som detta: `--aepUserLdap--PurchaseEvent`, och lägger till en beskrivning som detta: `Purchase Event`.

![Journey Optimizer](./images/oc34.png)

Nästa steg är markeringen **Händelsetyp**. Välj **Enhet**.

![Journey Optimizer](./images/eventidtype1.png)

Nästa steg är **Typ av händelse-ID**. Välj **Systemgenererad**

![Journey Optimizer](./images/eventidtype.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Website (Global v1.1) v.1`.

![Journey Optimizer](./images/oc35.png)

När du har valt schemat visas ett antal fält som markeras i avsnittet **Nyttolast**. Klicka på ikonen **Redigera/Penna** om du vill lägga till fler fält i den här händelsen.

![Journey Optimizer](./images/oc36.png)

Du kommer då att se den här popup-rutan. Du måste nu markera ytterligare kryssrutor för att få tillgång till ytterligare data när den här händelsen aktiveras.

![Journey Optimizer](./images/oc37.png)

Markera kryssrutan på rad `--aepTenantId--` först.

![Journey Optimizer](./images/oc38.png)

Bläddra sedan nedåt och markera kryssrutan på raden `productListItems`.

![Journey Optimizer](./images/oc39.png)

Bläddra sedan nedåt och markera kryssrutan på raden `commerce`.

![Journey Optimizer](./images/oc391.png)

Klicka sedan på **OK**.

Därefter ser du att fler fält har lagts till i händelsen. Klicka på **Spara**.

![Journey Optimizer](./images/oc40.png)

Din nya aktivitet delas sedan och du ser din aktivitet i listan över tillgängliga händelser nu.

Klicka på aktiviteten igen för att öppna skärmen **Redigera händelse** igen.
Håll pekaren över fältet **Nyttolast** igen för att se de tre ikonerna igen. Klicka på ikonen **Visa nyttolast** .

![Journey Optimizer](./images/oc41.png)

Nu visas ett exempel på den förväntade nyttolasten. Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

![Journey Optimizer](./images/oc42.png)

Händelse-ID är det som måste skickas till Adobe Journey Optimizer för att utlösa den resa som du bygger i nästa steg. Skriv ned detta eventID, som du behöver i ett av de följande stegen.
`"eventID": "ef6dd943c94fe1b4763c098ccd1772344662f2a9f614513106cb5ada8be36857"`

Klicka på **OK**, följt av **Avbryt**.

Händelsen är nu konfigurerad och klar att användas.

## 3.4.1.2 Skapa din resa

Gå till **Resor** på menyn och klicka på **Skapa resa**.

![Journey Optimizer](./images/oc43.png)

Då ser du det här. Ge resan ett namn. Använd `--aepUserLdap-- - Order Confirmation journey`. Klicka på **OK**.

![Journey Optimizer](./images/oc45.png)

Först måste du lägga till din händelse som startpunkt för din resa. Sök efter din händelse `--aepUserLdap--PurchaseEvent` och dra och släpp den på arbetsytan. Klicka på **OK**.

![Journey Optimizer](./images/oc46.png)

Under **Åtgärder** söker du sedan efter åtgärden **E-post** och lägger till den på arbetsytan.

![Journey Optimizer](./images/oc47.png)

Ange **kategorin** till **Marknadsföring** och välj en e-postyta som gör att du kan skicka e-post. I det här fallet är e-postytan som ska väljas **E-post**. Kontrollera att kryssrutorna för **klick på e-post** och **e-post** är aktiverade.

![ACOP](./images/journeyactions1.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka på **Redigera innehåll**.

![ACOP](./images/journeyactions2.png)

Nu ser du det här. Klicka på textfältet **Ämnesrad**.

![ACOP](./images/journeyactions3.png)

Börja skriva **Tack för din beställning** i textområdet

![Journey Optimizer](./images/oc5.png)

Ämnesraden är inte färdig än. Därefter måste du hämta en personaliseringstoken för fältet **Förnamn** som lagras under `profile.person.name.firstName`. I den vänstra menyn bläddrar du nedåt för att hitta fältet **Person** > **Fullständigt namn** > **Förnamn** och klickar på ikonen **+** för att lägga till en personaliseringstoken på ämnesraden. Klicka på **Spara**.

![Journey Optimizer](./images/oc6.png)

Du kommer då tillbaka hit. Klicka på **E-posta Designer** för att skapa e-postens innehåll.

![Journey Optimizer](./images/oc7.png)

Klicka på **Designa från grunden** på nästa skärm.

![Journey Optimizer](./images/oc8.png)

På den vänstra menyn hittar du de strukturkomponenter som du kan använda för att definiera e-postmeddelandets struktur (rader och kolumner).

Dra och släpp 8 gånger en **1:1-kolumn** på arbetsytan, vilket bör ge dig följande:

![Journey Optimizer](./images/oc9.png)

Gå till **Innehållskomponenter**.

![Journey Optimizer](./images/oc10.png)

Dra och släpp en **bild**-komponent på den första raden. Klicka på **Bläddra**.

![Journey Optimizer](./images/oc11.png)

Gå till mappen **enablement-assets**, markera filen **luma-logo.png** och klicka på **Välj**.

![Journey Optimizer](./images/oc12.png)

Du är nu tillbaka här. Klicka på bilden för att markera den och använd sedan skjutreglaget **Storlek** för att göra logotypbilden lite mindre.

![Journey Optimizer](./images/oc13.png)

Gå till **Innehållskomponenter** och dra och släpp en **Bild** -komponent på den andra raden. Markera **bildkomponenten** men klicka inte på Bläddra.

![Journey Optimizer](./images/oc15.png)

Klistra in bild-URL:en i fältet **Source**: `https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/29043bedcde632a9cbe8a02a164189c9_preparing.png`. Den här bilden ligger utanför Adobe.

![Journey Optimizer](./images/oc14.png)

När du ändrar omfånget till ett annat fält återges bilden och du kommer att se följande:

![Journey Optimizer](./images/oc16.png)

Gå sedan till **Innehållskomponenter** och dra och släpp en **Text** -komponent på den tredje raden.

![Journey Optimizer](./images/oc17.png)

Markera standardtexten i komponenten **Skriv texten här.** och ersätt den med texten nedan:

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

Placera markören bredvid texten **Hej** och klicka på **Lägg till Personalization**.

![Journey Optimizer](./images/oc19.png)

Navigera till fältet **Person** > **Fullständigt namn** > **Förnamn** och klicka på ikonen **+** för att lägga till personaliseringstoken på ämnesraden. Klicka på **Spara**.

![Journey Optimizer](./images/oc20.png)

Då ser du det här:

![Journey Optimizer](./images/oc21.png)

Gå sedan till **Innehållskomponenter** och dra och släpp en **Text** -komponent på den fjärde raden.

![Journey Optimizer](./images/oc22.png)

Markera standardtexten i komponenten **Skriv texten här.** och ersätt den med texten nedan:

`Order Information`

Ändra teckenstorleken till **26px** och centrera texten i den här cellen. Då får du den här:

![Journey Optimizer](./images/oc23.png)

Gå sedan till **Innehållskomponenter** och dra och släpp en **HTML** -komponent på den femte raden. Klicka på komponenten HTML och sedan på **Visa källkoden**.

![Journey Optimizer](./images/oc24.png)

Klistra in HTML i popup-fönstret **Redigera HTML**:

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

Klicka på **Spara**.

![Journey Optimizer](./images/oc25.png)

Du får den här då. Klicka på **Spara** för att spara förloppet.

![Journey Optimizer](./images/oc26.png)

Gå till **Innehållskomponenter** och dra och släpp en **HTML** -komponent på den sjätte raden. Klicka på komponenten HTML och sedan på **Visa källkoden**.

![Journey Optimizer](./images/oc57.png)

Klistra in HTML i popup-fönstret **Redigera HTML**:

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

Då får du den här:

![Journey Optimizer](./images/oc58.png)

Du måste nu ersätta **xxx** med en referens till objektet productListItems som är en del av händelsen som utlöser resan.

![Journey Optimizer](./images/oc59.png)

Ta först bort **xxx** i HTML-koden.

![Journey Optimizer](./images/oc60.png)

Klicka på **Sammanhangsberoende attribut** på den vänstra menyn. Det här sammanhanget skickas till meddelandet från resan.

![Journey Optimizer](./images/oc601.png)

Då ser du det här. Klicka på pilen bredvid **Journey Orchestration** för att gå djupare.

![Journey Optimizer](./images/oc61.png)

Klicka på pilen bredvid **Händelser** för att gå djupare.

![Journey Optimizer](./images/oc62.png)

Klicka på pilen bredvid `--aepUserLdap--PurchaseEvent` om du vill gå djupare.

![Journey Optimizer](./images/oc63.png)

Klicka på pilen bredvid **productListItems** för att gå djupare.

![Journey Optimizer](./images/oc64.png)

Klicka på ikonen **+** bredvid **Namn** för att lägga till den på arbetsytan. Du får den här då. Du måste nu välja **.name** enligt skärmbilden nedan och sedan ta bort **.name**.

![Journey Optimizer](./images/oc65.png)

Du får den här då. Klicka på **Spara**.

![Journey Optimizer](./images/oc66.png)

Du är tillbaka i e-postprogrammet Designer nu. Klicka på **Spara** för att spara förloppet.

![Journey Optimizer](./images/oc67.png)

Gå sedan till **Innehållskomponenter** och dra och släpp en **HTML** -komponent på den sjunde raden. Klicka på komponenten HTML och sedan på **Visa källkoden**.

![Journey Optimizer](./images/oc68.png)

Klistra in HTML i popup-fönstret **Redigera HTML**:

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

Det finns två referenser till **xxx** i den här HTML-koden. Du måste nu ersätta varje **xxx** med en referens till objektet productListItems som är en del av händelsen som utlöser resan.

![Journey Optimizer](./images/oc69.png)

Ta först bort den första **xxx** i HTML-koden.

![Journey Optimizer](./images/oc71.png)

Klicka på **Sammanhangsberoende attribut** på den vänstra menyn.

![Journey Optimizer](./images/oc711.png)

Klicka på pilen bredvid **Journey Orchestration** för att gå djupare.

![Journey Optimizer](./images/oc72.png)

Klicka på pilen bredvid **Händelser** för att gå djupare.

![Journey Optimizer](./images/oc722.png)

Klicka på pilen bredvid `--aepUserLdap--PurchaseEvent` om du vill gå djupare.

![Journey Optimizer](./images/oc73.png)

Klicka på pilen bredvid **Commerce** för att gå djupare.

![Journey Optimizer](./images/oc733.png)

Klicka på pilen bredvid **Beställning** för att gå djupare.

![Journey Optimizer](./images/oc74.png)

Klicka på ikonen **+** bredvid **Prissumma** för att lägga till den på arbetsytan.

![Journey Optimizer](./images/oc75.png)

Du får den här då. Ta nu bort den andra **xxx** i HTML-koden.

![Journey Optimizer](./images/oc76.png)

Klicka på ikonen **+** bredvid **Prissumma** igen för att lägga till den på arbetsytan.

![Journey Optimizer](./images/oc77.png)

Du kan också lägga till fältet **Valuta** inifrån objektet **Ordning** på arbetsytan, vilket visas här.
När du är klar klickar du på **Spara** för att spara ändringarna.

![Journey Optimizer](./images/oc771.png)

Du kommer sedan tillbaka till Designer för e-post. Klicka på **Spara** igen.

![Journey Optimizer](./images/oc78.png)

Gå tillbaka till meddelandekontrollpanelen genom att klicka på **pilen** intill ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/oc79.png)

Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/oc79a.png)

Klicka på **OK** för att stänga e-poståtgärden.

![Journey Optimizer](./images/oc79b.png)

Klicka på **Publish** för att publicera din resa.

![Journey Optimizer](./images/oc511.png)

Klicka på **Publish** igen.

![Journey Optimizer](./images/oc512.png)

Din resa är nu publicerad.

![Journey Optimizer](./images/oc513.png)

## 3.4.1.5 Uppdatera klientegenskapen för Adobe Experience Platform Data Collection

Gå till [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) och välj **Taggar**.

Det här är egenskapssidan för Adobe Experience Platform Data Collection som du såg tidigare.

![Sidan Egenskaper](./../../../modules/datacollection/module1.1/images/launch1.png)

I modul 0 skapade Demo System två klientegenskaper åt dig: en för webbplatsen och en för mobilappen. Sök efter dem genom att söka efter `--aepUserLdap--` i rutan **[!UICONTROL Search]**. Klicka för att öppna egenskapen **Webb**.

![Sökruta](./../../../modules/datacollection/module1.1/images/property6.png)

Gå till **dataelement**. Sök efter och öppna dataelementet **XDM - Köp**.

![Journey Optimizer](./images/oc91.png)

Då ser du det här. Navigera till fältet **_experience.campaign.orchestration.eventID** och fyll i ditt eventID här. Det eventID som ska fyllas i här är det eventID som du skapade som en del av övning 10.1.2. Klicka på **Spara** eller **Spara i bibliotek**.

![Journey Optimizer](./images/oc92.png)

Spara ändringarna i din klientegenskap och publicera sedan ändringarna genom att uppdatera ditt utvecklingsbibliotek.

![Journey Optimizer](./images/oc93.png)

Ändringarna är nu distribuerade och kan testas.

## 3.4.1.6 Testa e-postmeddelandet med orderbekräftelsen på demowebbplatsen

Låt oss testa den uppdaterade resan genom att köpa en produkt på demowebbplatsen.

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Klicka på **Kör** på sidan **Screens**.

![DSN](./../../../modules/datacollection/module1.1/images/web2.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje demonstration måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

Klicka på logotypikonen för Adobe i det övre vänstra hörnet av skärmen för att öppna profilvisningsprogrammet.

![Demo](./../../../modules/datacollection/module1.2/images/pv1.png)

Ta en titt på panelen Profilvisningsprogram och kundprofilen i realtid med **Experience Cloud ID** som primär identifierare för den okända kunden.

![Demo](./../../../modules/datacollection/module1.2/images/pv2.png)

Gå till sidan Register/Login. Klicka på **SKAPA ETT KONTO**.

![Demo](./../../../modules/datacollection/module1.2/images/pv9.png)

Fyll i dina uppgifter och klicka på **Registrera**. Sedan dirigeras du om till föregående sida.

![Demo](./../../../modules/datacollection/module1.2/images/pv10.png)

Lägg till valfri produkt i kundvagnen och gå till sidan **kundvagn**. Klicka på **Fortsätt till kassan**.

![Journey Optimizer](./images/cart1.png)

Verifiera sedan fälten på utcheckningssidan och klicka på **Utcheckning**.

![Journey Optimizer](./images/cart2.png)

Du får sedan en orderbekräftelse via e-post inom några sekunder.

![Journey Optimizer](./images/oc98.png)

Du har gjort klart den här övningen.

Nästa steg: [3.4.2 Konfigurera en batchbaserad nyhetsbrevsresa](./ex2.md)

[Gå tillbaka till modul 3.4](./journeyoptimizer.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
