---
title: Adobe Journey Optimizer - Konfigurera en batchbaserad resa
description: I det här avsnittet konfigurerar du en e-postgruppsresa för att skicka ett nyhetsbrev
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# 3.4.2 Konfigurera en gruppbaserad nyhetsbrevresa

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och väljer sandlådan i listan. I det här exemplet heter sandlådan **AEP Enablement FY22**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.2.1 Skapa nyhetsbrev

Nu kan du skapa en gruppbaserad resa. Till skillnad från den händelsebaserade resan i den föregående övningen som bygger på inkommande upplevelsehändelser eller segmentposter eller utträden för att utlösa en resa för en viss kund, riktar sig batchbaserade resor till ett helt segment med unikt innehåll som nyhetsbrev, engångskampanjer eller allmän information eller regelbundet med liknande innehåll som skickas regelbundet, till exempel födelsedagskampanjer och påminnelser.

Gå till **Resor** på menyn och klicka på **Skapa resa**.

![Journey Optimizer](./images/oc43.png)

Till höger ser du ett formulär där du måste ange resans namn och beskrivning. Ange följande värden:

- **Namn**: `--aepUserLdap-- - Newsletter Journey`. Till exempel: **vangeluw - Newsletter Journey**.
- **Beskrivning**: Månadsnyhetsbrev

Klicka på **OK**.

![Journey Optimizer](./images/batchj2.png)

Under **Orchestration** drar och släpper du **Läs segment** på arbetsytan. Det innebär att resan, när den har publicerats, börjar med att hämta hela segmentets målgrupp, som sedan blir målgrupp för resan och budskapet. Klicka på **Markera ett segment**.

![Journey Optimizer](./images/batchj3.png)

I popup-fönstret **Välj ett segment** söker du efter din ldap och väljer det segment du skapade i [Modul 2.3 - CDP i realtid - Bygg ett segment och utför åtgärden ](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md) `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. till exempel: vangeluw - Intresse i PROTEUS FITNESS JACKSHIRT. Klicka på **Spara**.

![Journey Optimizer](./images/batchj5.png)

Klicka på **OK**.

![Journey Optimizer](./images/batchj6.png)

I den vänstra menyn hittar du avsnittet **Åtgärder** och drar och släpper en **E-post** -åtgärd på arbetsytan.

![Journey Optimizer](./images/batchj7.png)

Ange **kategorin** till **Marknadsföring** och välj en e-postyta som gör att du kan skicka e-post. I det här fallet är e-postytan som ska väljas **E-post**. Kontrollera att kryssrutorna för **klick på e-post** och **e-post** är aktiverade.

![ACOP](./images/journeyactions1eee.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka på **Redigera innehåll**.

![ACOP](./images/journeyactions2.png)

Nu ser du det här. Klicka på textfältet **Ämnesrad**.

![Journey Optimizer](./images/batch4.png)

Ange den här texten för ämnesraden: `Luma Newsletter - your monthly update has arrived.`. Klicka på **Spara**.

![Journey Optimizer](./images/batch5.png)

Du kommer då tillbaka hit. Klicka på **E-posta Designer** för att börja skapa e-postinnehållet.

![Journey Optimizer](./images/batch6.png)

Då ser du det här. Klicka på **Importera HTML**.

![Journey Optimizer](./images/batch7.png)

På popup-skärmen måste du dra och släppa HTML-filen i e-postmeddelandet. Du hittar mallen [här](./../../../assets/html/ajo-newsletter.html.zip) för HTML. Ladda ned zip-filen med HTML-mallen till den lokala datorn och packa upp den på skrivbordet.

![Journey Optimizer](./images/html1.png)

Dra och släpp filen **ajo-newsletter.html** för att överföra den till Journey Optimizer. Klicka på **Importera**.

![Journey Optimizer](./images/batch8.png)

Det här e-postinnehållet är klart att användas eftersom det har all förväntad personalisering, bilder och text. Endast platshållaren för erbjudandet är tom.

Du kan få ett felmeddelande: **Fel vid försök att hämta resurser**. Det här är länkat till bilden i e-postmeddelandet.

![Journey Optimizer](./images/errorfetch.png)

Om det här felet uppstår markerar du bilden och klickar på knappen **Redigera bild** .

![Journey Optimizer](./images/errorfetch1.png)

Klicka på **Assets Essentials** för att gå tillbaka till ditt AEM Assets Essentials-bibliotek.

![Journey Optimizer](./images/errorfetch2.png)

Du kommer då att se den här popup-rutan. Navigera till mappen **enablement-assets** och markera bilden **luma-newsletterContent.png**. Klicka på **Markera**.

![Journey Optimizer](./images/errorfetch3.png)

Ditt enkla nyhetsbrev är nu klart. Klicka på **Spara**.

![Journey Optimizer](./images/ready.png)

Gå tillbaka till meddelandekontrollpanelen genom att klicka på **pilen** intill ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/batch9.png)

Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/oc79aeee.png)

Klicka på **OK** för att stänga e-poståtgärden.

![Journey Optimizer](./images/oc79beee.png)

Din nyhetsbrevsresa är nu klar att publiceras. Innan du gör det bör du lägga märke till avsnittet **Schema** där du kan växla den här resan från att vara en engångskampanj till en återkommande kampanj. Klicka på knappen **Schema**.

![Journey Optimizer](./images/batchj12.png)

Då ser du det här. Välj **En gång**.

![Journey Optimizer](./images/sch1.png)

Välj ett datum och en tid inom en timme så att du kan testa din resa. Klicka på **OK**.

>[!NOTE]
>
>Datum och tid för sändning av meddelande måste vara inom mer än en timme.

Klicka på **Publish**.

![Journey Optimizer](./images/batchj13.png)

Klicka på **Publish** igen.

![Journey Optimizer](./images/batchj14.png)

Din grundläggande nyhetsbrevsresa är nu publicerad. E-postmeddelandet med nyhetsbrevet skickas så som du har definierat det i ditt schema, och din resa stoppas så fort som det senaste e-postmeddelandet har skickats.

![Journey Optimizer](./images/batchj14eee.png)

Du har gjort klart den här övningen.

Nästa steg: [3.4.3 Tillämpa personalisering i ett e-postmeddelande](./ex3.md)

[Gå tillbaka till modul 3.4](./journeyoptimizer.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
