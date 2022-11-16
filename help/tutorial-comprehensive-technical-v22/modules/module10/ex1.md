---
title: Adobe Journey Optimizer - Konfigurera en utlösarbaserad resa - orderbekräftelse
description: I det här avsnittet konfigurerar du en utlösarbaserad resa - orderbekräftelse
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 69bb9eca-3942-4c31-a3d2-0b218143e1eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 0%

---

# 10.1 Konfigurera en utlösarbaserad resa - orderbekräftelse

Logga in på Adobe Journey Optimizer genom att gå till [Adobe Experience Cloud](https://experience.adobe.com). Klicka **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Du omdirigeras till **Startsida**  i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas anropas `--aepSandboxId--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och välj sandlådan i listan. I det här exemplet heter sandlådan **AEP-aktivering FY22**. Då är du i **Startsida** vy över din sandlåda `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.1.1 Skapa din aktivitet

Gå till menyn **Konfigurationer** och klicka **Hantera** under **Händelser**.

![Journey Optimizer](./images/oc30.png)

På **Händelser** visas en liknande vy. Klicka **Skapa händelse**.

![Journey Optimizer](./images/oc31.png)

Därefter visas en tom händelsekonfiguration.

![Journey Optimizer](./images/oc32.png)

Först och främst ger du evenemanget ett namn som detta: `--demoProfileLdap--PurchaseEvent`och lägg till en beskrivning enligt följande: `Purchase Event`.

![Journey Optimizer](./images/oc34.png)

Nästa är **Händelsetyp** markering. Välj **Unitary**.

![Journey Optimizer](./images/eventidtype1.png)

Nästa är **Typ av händelse-ID** markering. Välj **Systemgenererat**

![Journey Optimizer](./images/eventidtype.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Website (Global v1.1) v.1`.

![Journey Optimizer](./images/oc35.png)

När du har valt schemat visas ett antal fält i **Nyttolast** -avsnitt. Klicka på **Redigera/Penna** om du vill lägga till fler fält till den här händelsen.

![Journey Optimizer](./images/oc36.png)

Du kommer då att se den här popup-rutan. Du måste nu markera ytterligare kryssrutor för att få tillgång till ytterligare data när den här händelsen aktiveras.

![Journey Optimizer](./images/oc37.png)

Först markerar du kryssrutan på raden `--aepTenantId--`.

![Journey Optimizer](./images/oc38.png)

Bläddra nedåt och markera kryssrutan på raden `productListItems`.

![Journey Optimizer](./images/oc39.png)

Bläddra nedåt och markera kryssrutan på raden `commerce`.

![Journey Optimizer](./images/oc391.png)

Klicka på **OK**.

Därefter ser du att fler fält har lagts till i händelsen. Klicka **Spara**.

![Journey Optimizer](./images/oc40.png)

Din nya aktivitet delas sedan och du ser din aktivitet i listan över tillgängliga händelser nu.

Klicka på aktiviteten igen för att öppna **Redigera händelse** skärm igen.
Hovra över **Nyttolast** om du vill visa de tre ikonerna igen. Klicka på **Visa nyttolast** ikon.

![Journey Optimizer](./images/oc41.png)

Nu visas ett exempel på den förväntade nyttolasten. Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

![Journey Optimizer](./images/oc42.png)

Händelse-ID är det som måste skickas till Adobe Journey Optimizer för att utlösa den resa som du bygger i nästa steg. Skriv ned detta eventID, som du behöver i ett av de följande stegen.
`"eventID": "ef6dd943c94fe1b4763c098ccd1772344662f2a9f614513106cb5ada8be36857"`

Klicka **OK**, följt av **Avbryt**.

Händelsen är nu konfigurerad och klar att användas.

## 10.1.2 Skapa din resa

Gå till menyn **Resor** och klicka **Skapa resa**.

![Journey Optimizer](./images/oc43.png)

Du kommer då att se det här. Ge resan ett namn. Använd `--demoProfileLdap-- - Order Confirmation journey`. Klicka **OK**.

![Journey Optimizer](./images/oc45.png)

Först måste du lägga till din händelse som startpunkt för din resa. Sök efter din aktivitet `--demoProfileLdap--PurchaseEvent` och dra och släpp det på arbetsytan. Klicka **OK**.

![Journey Optimizer](./images/oc46.png)

Nästa, under **Åtgärder**, sök efter **E-post** och lägg till det på arbetsytan.

![Journey Optimizer](./images/oc47.png)

Ange **Kategori** till **Marknadsföring** och välj en e-postyta som gör att du kan skicka e-post. I det här fallet är e-postytan som ska väljas **E-post**. Se till att kryssrutorna för **Klicka på e-post** och **e-post öppnas** båda är aktiverade.

![ACOP](./images/journeyactions1.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka **Redigera innehåll**.

![ACOP](./images/journeyactions2.png)

Nu ser du det här. Klicka på **Subject line** textfält.

![ACOP](./images/journeyactions3.png)

Börja skriva i textområdet **Tack för din beställning,**

![Journey Optimizer](./images/oc5.png)

Ämnesraden är inte färdig än. Därefter måste du ta in en personaliseringstoken för fältet **Förnamn** som lagras under `profile.person.name.firstName`. Bläddra nedåt i den vänstra menyn för att hitta **Person** > **Fullständigt namn** >  **Förnamn** och klicka på **+** om du vill lägga till en personaliseringstoken på ämnesraden. Klicka **Spara**.

![Journey Optimizer](./images/oc6.png)

Du kommer då tillbaka hit. Klicka **E-postdesigner** för att skapa e-postens innehåll.

![Journey Optimizer](./images/oc7.png)

På nästa skärm klickar du på **Designa från grunden**.

![Journey Optimizer](./images/oc8.png)

På den vänstra menyn hittar du de strukturkomponenter som du kan använda för att definiera e-postmeddelandets struktur (rader och kolumner).

Dra och släpp 8 gånger **1:1-kolumn** på arbetsytan, som bör ge dig följande:

![Journey Optimizer](./images/oc9.png)

Gå till **Innehållskomponenter**.

![Journey Optimizer](./images/oc10.png)

Dra och släpp en **Bild** -komponenten på första raden. Klicka **Bläddra**.

![Journey Optimizer](./images/oc11.png)

Gå till mappen **enablement-assets** markerar du filen **luma-logo.png** och klicka **Välj**.

![Journey Optimizer](./images/oc12.png)

Du är nu tillbaka här. Klicka på bilden för att markera den och använd sedan **Storlek** för att göra logotypbilden lite mindre.

![Journey Optimizer](./images/oc13.png)

Gå till **Innehållskomponenter** och dra och släppa **Bild** -komponenten på den andra raden. Välj **Bildkomponent** men klicka inte på Bläddra.

![Journey Optimizer](./images/oc15.png)

Klistra in bildens URL-adress i fältet **Källa**: `https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/29043bedcde632a9cbe8a02a164189c9_preparing.png`. Den här bilden ligger utanför Adobe.

![Journey Optimizer](./images/oc14.png)

När du ändrar omfånget till ett annat fält återges bilden och du ser detta:

![Journey Optimizer](./images/oc16.png)

Nästa, gå till **Innehållskomponenter** och dra och släppa **Text** -komponenten på den tredje raden.

![Journey Optimizer](./images/oc17.png)

Markera standardtexten i den komponenten **Skriv texten här.** och ersätta den med texten nedan:

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

Placera markören bredvid texten **Hej** och klicka **Lägg till personalisering**.

![Journey Optimizer](./images/oc19.png)

Navigera till **Person** > **Fullständigt namn** > **Förnamn** och klicka på **+** om du vill lägga till en personaliseringstoken på ämnesraden. Klicka **Spara**.

![Journey Optimizer](./images/oc20.png)

Då ser du det här:

![Journey Optimizer](./images/oc21.png)

Nästa, gå till **Innehållskomponenter** och dra och släppa **Text** på fjärde raden.

![Journey Optimizer](./images/oc22.png)

Markera standardtexten i den komponenten **Skriv texten här.** och ersätta den med texten nedan:

`Order Information`

Ändra teckenstorleken till **26px** och centrera texten i den här cellen. Då får du den här:

![Journey Optimizer](./images/oc23.png)

Nästa, gå till **Innehållskomponenter** och dra och släppa **HTML** på femte raden. Klicka på komponenten HTML och sedan på **Visa källkoden**.

![Journey Optimizer](./images/oc24.png)

I **Redigera HTML** popup, klistra in HTML:

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

Klicka **Spara**.

![Journey Optimizer](./images/oc25.png)

Du får den här då. Klicka **Spara** för att spara förloppet.

![Journey Optimizer](./images/oc26.png)

Gå till **Innehållskomponenter** och dra och släppa **HTML** på sjätte raden. Klicka på komponenten HTML och sedan på **Visa källkoden**.

![Journey Optimizer](./images/oc57.png)

I **Redigera HTML** popup, klistra in HTML:

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

Då får du den här:

![Journey Optimizer](./images/oc58.png)

Nu måste du ersätta **xxx** med en referens till objektet productListItems som är en del av händelsen som utlöser resan.

![Journey Optimizer](./images/oc59.png)

Först, ta bort **xxx** i HTML-koden först.

![Journey Optimizer](./images/oc60.png)

Klicka på **Sammanhangsberoende attribut**. Det här sammanhanget skickas till meddelandet från resan.

![Journey Optimizer](./images/oc601.png)

Du kommer då att se det här. Klicka på pilen bredvid **Journey Orchestration** fördjupa dig.

![Journey Optimizer](./images/oc61.png)

Klicka på pilen bredvid **Händelser** fördjupa dig.

![Journey Optimizer](./images/oc62.png)

Klicka på pilen bredvid `--demoProfileLdap--PurchaseEvent` fördjupa dig.

![Journey Optimizer](./images/oc63.png)

Klicka på pilen bredvid **productListItems** fördjupa dig.

![Journey Optimizer](./images/oc64.png)

Klicka på **+** ikon bredvid **Namn** för att lägga till den på arbetsytan. Du får den här då. Du måste nu välja  **.name** som anges i skärmbilden nedan och sedan bör du ta bort **.name**.

![Journey Optimizer](./images/oc65.png)

Du får den här då. Klicka **Spara**.

![Journey Optimizer](./images/oc66.png)

Du är tillbaka i e-postdesignern nu. Klicka **Spara** för att spara förloppet.

![Journey Optimizer](./images/oc67.png)

Nästa, gå till **Innehållskomponenter** och dra och släppa **HTML** på den sjunde raden. Klicka på komponenten HTML och sedan på **Visa källkoden**.

![Journey Optimizer](./images/oc68.png)

I **Redigera HTML** popup, klistra in HTML:

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

Det finns två referenser till **xxx** i den här HTML-koden. Nu måste du ersätta varje **xxx** med en referens till objektet productListItems som är en del av händelsen som utlöser resan.

![Journey Optimizer](./images/oc69.png)

Ta först bort den första **xxx** i HTML-koden.

![Journey Optimizer](./images/oc71.png)

Klicka på **Sammanhangsberoende attribut**.

![Journey Optimizer](./images/oc711.png)

Klicka på pilen bredvid **Journey Orchestration** fördjupa dig.

![Journey Optimizer](./images/oc72.png)

Klicka på pilen bredvid **Händelser** fördjupa dig.

![Journey Optimizer](./images/oc722.png)

Klicka på pilen bredvid `--demoProfileLdap--PurchaseEvent` fördjupa dig.

![Journey Optimizer](./images/oc73.png)

Klicka på pilen bredvid **Handel** fördjupa dig.

![Journey Optimizer](./images/oc733.png)

Klicka på pilen bredvid **Order** fördjupa dig.

![Journey Optimizer](./images/oc74.png)

Klicka på **+** ikon bredvid **Prissumma** för att lägga till den på arbetsytan.

![Journey Optimizer](./images/oc75.png)

Du får den här då. Ta bort den andra **xxx** i HTML-koden.

![Journey Optimizer](./images/oc76.png)

Klicka på **+** ikon bredvid **Prissumma** igen för att lägga till den på arbetsytan.

![Journey Optimizer](./images/oc77.png)

Du kan också lägga till fältet **Valuta** inifrån **Order** på arbetsytan, som du ser här.
När du är klar klickar du på **Spara** för att spara ändringarna.

![Journey Optimizer](./images/oc771.png)

Du kommer sedan tillbaka till e-postdesignern. Klicka **Spara** igen.

![Journey Optimizer](./images/oc78.png)

Gå tillbaka till meddelandekontrollpanelen genom att klicka på **pil** bredvid texten på ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/oc79.png)

Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/oc79a.png)

Klicka **OK** för att stänga e-poståtgärden.

![Journey Optimizer](./images/oc79b.png)

Klicka **Publicera** för att publicera din resa.

![Journey Optimizer](./images/oc511.png)

Klicka **Publicera** igen.

![Journey Optimizer](./images/oc512.png)

Din resa är nu publicerad.

![Journey Optimizer](./images/oc513.png)

## 10.1.5 Uppdatera klientegenskapen för Adobe Experience Platform Data Collection

Gå till [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) och markera **Taggar**.

Det här är egenskapssidan för Adobe Experience Platform Data Collection som du såg tidigare.

![Egenskapssida](../module1/images/launch1.png)

I modul 0 skapade Demo System två klientegenskaper: en för webbplatsen och en för mobilappen. Hitta dem genom att söka efter `--demoProfileLdap--` i **[!UICONTROL Sök]** box. Klicka för att öppna **Webb** -egenskap.

![Sökruta](../module1/images/property6.png)

Gå till **Dataelement**. Söka efter och öppna dataelementet **XDM - Inköp**.

![Journey Optimizer](./images/oc91.png)

Du kommer då att se det här. Navigera till fältet **_experience.campaign.orchestration.eventID** och fyll i ditt eventID här. Det eventID som ska fyllas i här är det eventID som du skapade som en del av övning 10.1.2. Klicka **Spara** eller **Spara i bibliotek**.

![Journey Optimizer](./images/oc92.png)

Spara ändringarna i din klientegenskap och publicera sedan ändringarna genom att uppdatera ditt utvecklingsbibliotek.

![Journey Optimizer](./images/oc93.png)

Ändringarna är nu distribuerade och kan testas.

## 10.1.6 Testa e-postmeddelandet med orderbekräftelsen på demowebbplatsen

Låt oss testa den uppdaterade resan genom att köpa en produkt på demowebbplatsen.

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](../module0/images/web8.png)

På **Skärmar** sida, klicka **Kör**.

![DSN](../module1/images/web2.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../module0/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../module0/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../module0/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../module0/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje demonstration måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](../module0/images/web7.png)

Klicka på logotypikonen för Adobe i det övre vänstra hörnet av skärmen för att öppna profilvisningsprogrammet.

![Demo](../module2/images/pv1.png)

Ta en titt på panelen Profilvisningsprogram och kundprofilen i realtid med **Experience Cloud ID** som primär identifierare för den här okända kunden.

![Demo](../module2/images/pv2.png)

Gå till sidan Register/Login. Klicka **SKAPA ETT KONTO**.

![Demo](../module2/images/pv9.png)

Fyll i detaljerna och klicka **Registrera** därefter omdirigeras du till föregående sida.

![Demo](../module2/images/pv10.png)

Lägg valfri produkt i kundvagnen och gå till **Kundvagn** sida. Klicka **Gå till kassan**.

![Journey Optimizer](./images/cart1.png)

Verifiera sedan fälten på utcheckningssidan och klicka på **Utcheckning**.

![Journey Optimizer](./images/cart2.png)

Du får sedan en orderbekräftelse via e-post inom några sekunder.

![Journey Optimizer](./images/oc98.png)

Du har gjort klart den här övningen.

Nästa steg: [10.2 Konfigurera en batchbaserad nyhetsbrevsresa](./ex2.md)

[Gå tillbaka till modul 10](./journeyoptimizer.md)

[Gå tillbaka till Alla moduler](../../overview.md)
