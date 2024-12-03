---
title: Intelligenta tjänster - Förberedelse av AI-data för kunder (Ingest)
description: Customer AI - Data Preparation (Ingest)
kt: 5342
doc-type: tutorial
exl-id: 71405859-cfc6-4991-a0b0-11c94818a0fa
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# 2.2.1 Customer AI - Data Preparation (Ingest)

För att Intelligent Services ska kunna hitta insikter från era marknadsföringshändelsedata måste data anrikas semantiskt och underhållas i en standardstruktur. Intelligent Services utnyttjar scheman från Adobe Experience Data Model (XDM) för att uppnå detta.
Alla datauppsättningar som används i Intelligent Services måste överensstämma med XDM-schemat **Consumer Experience Event** .

## Skapa schema

I den här övningen skapar du ett schema som innehåller **Consumer Experience Event mixin**, vilket krävs av **Customer AI** Intelligent Service.

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](../../datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](../../datacollection/module1.2/images/sb1.png)

Klicka på **Scheman** på den vänstra menyn och gå till **Bläddra**. Klicka på **Skapa schema**.

![Skapa nytt schema](./images/createschemabutton.png)

Välj **Manuell** på popup-menyn och klicka på **Markera**.

![Skapa nytt schema](./images/schmanual.png)

Välj sedan **Experience Event** och klicka på **Next**.

![Skapa nytt schema](./images/xdmee.png)

Du måste ange ett namn för schemat nu. Använd det här som namn för vårt schema: `--aepUserLdap-- - Demo System - Customer Experience Event` och klicka på **Slutför**.

![Skapa nytt schema](./images/schname.png)

Då ser du det här. Klicka på **+ Lägg till** under Fältgrupper.

![Skapa nytt schema](./images/xdmee1.png)

Sök efter och markera följande **fältgrupper** som ska läggas till i schemat:

- Consumer Experience Event

![Nytt CEE-schema](./images/cee1.png)

- IdentityMap

Klicka på **Lägg till fältgrupper**.

![Nytt CEE-schema](./images/cee2.png)

Då ser du det här. Välj sedan schemats namn. Du bör nu aktivera ditt schema för **profilen** genom att klicka på växlingsknappen **Profil**.

![Skapa nytt schema](./images/xdmee3.png)

Då ser du det här. Markera kryssrutan för **Data för det här schemat kommer att innehålla en primär identitet i fältet identityMap.**. Klicka på **Aktivera**.

![Skapa nytt schema](./images/xdmee4.png)

Du borde ha den här nu. Klicka på **Spara** för att spara schemat.

![Skapa nytt schema](./images/xdmee5.png)

## Skapa datauppsättning

Klicka på **Datauppsättningar** på den vänstra menyn och gå till **Bläddra**. Klicka på **Skapa datauppsättning**.

![Datauppsättning](./images/createds.png)

Klicka på **Skapa datauppsättning från schema**.

![Datauppsättning](./images/createdatasetfromschema.png)

På nästa skärm väljer du den datauppsättning som du skapade i föregående övning, med namnet **[!UICONTROL ldap - Demo System - Customer Experience Event]**. Klicka på **Nästa**.

![Datauppsättning](./images/createds1.png)

Använd `--aepUserLdap-- - Demo System - Customer Experience Event Dataset` som namn för datauppsättningen. Klicka på **Slutför**.

![Datauppsättning](./images/createds2.png)

Din datauppsättning har skapats. Aktivera växlingsknappen **Profil**.

![Datauppsättning](./images/createds3.png)

Klicka på **Aktivera**.

![Datauppsättning](./images/createds4.png)

Nu bör du ha den här:

![Datauppsättning](./images/createds5.png)

Du är nu redo att börja inhämta data från kundupplevelsehändelser och börja använda kundens AI-tjänst.

## Hämta testdata för Experience Event

När **schemat** och **datauppsättningen** har konfigurerats är du nu redo att importera Experience Event-data. Eftersom kundens AI kräver särskilda datakrav måste du importera externt förberedda data.

De data som har förberetts för upplevelsehändelserna i den här övningen måste uppfylla kraven och schemat för [Consumer Experience Event XDM Field Group](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Hämta zip-filen med demodata från den här platsen: [https://tech-insiders.s3.us-west-2.amazonaws.com/CUSTOM-CAI-EVENTS-WEB.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/CUSTOM-CAI-EVENTS-WEB.zip).

Du har nu laddat ned en fil med namnet **CUSTOM-CAI-EVENTS-WEB.zip**. Placera filen på datorns skrivbord och zippa upp den. Därefter visas en mapp med namnet **CUSTOM-CAI-EVENTS-WEB**.

![Datauppsättning](./images/ingest.png)

I den mappen hittar du flera sekvensjson-filer som alla måste importeras i nästa övning.

![Datauppsättning](./images/ingest1a.png)

## Testdata för Ingest Experience Event

I Adobe Experience Platform går du till **Datauppsättningar** och öppnar din datauppsättning, som har namnet **[!UICONTROL ldap - Demo System - Customer Experience Event Dataset]**.

![Datauppsättning](./images/ingest1.png)

Klicka på **Välj filer** i datauppsättningen för att lägga till data.

![Datauppsättning](./images/ingest2.png)

På popup-menyn markerar du filerna **WEBSITE-EE-1.json** till **WEBSITE-EE-5.json** och klickar på **Öppna**.

![Datauppsättning](./images/ingest3.png)

Upprepa den här importprocessen för filerna **WEBSITE-EE-6.json** och **WEBSITE-EE-7.json**.

Du ser sedan de data som importeras och en ny grupp skapas i läget **Inläsning**. Navigera inte bort från den här sidan förrän filen har överförts.

![Datauppsättning](./images/ingest4.png)

När filen har överförts ser du att batchstatusen har ändrats från **Inläsning** till **Bearbetning**.

![Datauppsättning](./images/ingest5.png)

Inmatning och bearbetning av data kan ta 10-20 minuter.

När dataimporten är klar ändras batchstatusen för de olika överföringarna till **Slutfört**.

![Datauppsättning](./images/ingest7.png)

Nästa steg: [2.2.2 Kundens AI - Skapa en ny instans (Konfigurera)](./ex2.md)

[Gå tillbaka till modul 2.2](./intelligent-services.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
