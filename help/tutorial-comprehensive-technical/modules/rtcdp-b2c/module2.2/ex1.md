---
title: Intelligenta tjänster - Förberedelse av AI-data för kunder (Ingest)
description: Customer AI - Data Preparation (Ingest)
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# 2.2.1 Customer AI - Data Preparation (Ingest)

För att Intelligent Services ska kunna hitta insikter från era marknadsföringshändelsedata måste data anrikas semantiskt och underhållas i en standardstruktur. Intelligent Services utnyttjar scheman från Adobe Experience Data Model (XDM) för att uppnå detta.
Alla datauppsättningar som används i Intelligent Services måste överensstämma med XDM-schemat **Consumer Experience Event** .

## 2.2.1.1 Skapa schema

I den här övningen skapar du ett schema som innehåller **Consumer Experience Event mixin**, vilket krävs av **Customer AI** Intelligent Service.

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](../../datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--module10sandbox--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](../../datacollection/module1.2/images/sb1.png)

Klicka på **Scheman** på den vänstra menyn och gå till **Bläddra**. Klicka på **Skapa schema**.

![Skapa nytt schema](./images/create-schema-button.png)

Välj **XDM ExperienceEvent** på popup-menyn.

![Skapa nytt schema](./images/xdmee.png)

Då ser du det här.

![Skapa nytt schema](./images/xdmee1.png)

Sök efter och välj följande **Mixins** som ska läggas till i schemat:

- Consumer Experience Event

  ![Nytt CEE-schema](./images/cee.png)

- Information om slutanvändar-ID

  ![Nytt CEE-schema](./images/identitymap.png)

Klicka på **Lägg till fältgrupper**.

![Identitetsnyckeldefinition](./images/addmixin.png)

Då ser du det här. Välj **Information om** för blandat användar-ID.

![Skapa nytt schema](./images/eui1.png)

Navigera till fältet **endUserID:n._experience.emailid.id**.

![Skapa nytt schema](./images/eui2.png)

I den högra menyn för fältet **endUserIDs._experience.emailid.id**, rulla nedåt och markera kryssrutan för **Identitet**, markera kryssrutan för **Primär identitet** och markera **Identitetsnamnrymden** för **E-post**.

![Skapa nytt schema](./images/eui3.png)

Navigera till fältet **endUserID:n._experience.mcid.id**. Markera kryssrutan för **Identitet** och markera **Identitetsnamnrymden** för **ECID**. Klicka på **Använd**.

![Skapa nytt schema](./images/eui4.png)

Ge schemat ett namn nu.

Som namn för vårt schema ska du använda följande:

- `--aepUserLdap-- - Demo System - Customer Experience Event`

För ldap **vangeluw** bör det här till exempel vara schemats namn:

- **vangeluw - Demo System - Customer Experience Event**

Det borde ge dig något såhär. Klicka på knappen **+ Lägg till** för att lägga till nya **mixar**.

![Skapa nytt schema](./images/xdmee2.png)

Välj namnet på schemat. Du bör nu aktivera ditt schema för **profilen** genom att klicka på växlingsknappen **Profil**.

![Skapa nytt schema](./images/xdmee3.png)

Då ser du det här. Klicka på **Aktivera**.

![Skapa nytt schema](./images/xdmee4.png)

Du borde ha den här nu. Klicka på **Spara** för att spara schemat.

![Skapa nytt schema](./images/xdmee5.png)

## 2.2.1.2 Skapa datauppsättning

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

## 2.2.1.3 Hämta testdata för Experience Event

När **schemat** och **datauppsättningen** har konfigurerats är du nu redo att importera Experience Event-data. Eftersom kundens AI kräver data på minst **kvartal** 2 måste du importera externt förberedda data.

Data som har förberetts för upplevelsehändelser måste uppfylla kraven och schemat för [Consumer Experience Event XDM Mixin](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Hämta filen som innehåller exempeldata från den här platsen: [https://dashboard.adobedemo.com/data](https://dashboard.adobedemo.com/data). Klicka på knappen **Hämta**.

![Datauppsättning](./images/dsn1.png)

Om du inte kan komma åt länken ovan kan du även hämta filen från den här platsen: [https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip](https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip).

Du har nu laddat ned en fil med namnet **retail-v1-dec2020-xl.json.zip**. Placera filen på datorns skrivbord och zippa upp den. Därefter visas filen **retail-v1.json**. Du kommer att behöva den här filen i nästa övning.

![Datauppsättning](./images/ingest.png)

## 2.2.1.4 Testdata för händelsen Ingest Experience

I Adobe Experience Platform går du till **Datauppsättningar** och öppnar din datauppsättning, som har namnet **[!UICONTROL ldap - Demo System - Customer Experience Event Dataset]**.

![Datauppsättning](./images/ingest1.png)

Klicka på **Välj filer** i datauppsättningen för att lägga till data.

![Datauppsättning](./images/ingest2.png)

På popup-menyn markerar du filen **retail-v1.json** och klickar på **Öppna**.

![Datauppsättning](./images/ingest3.png)

Du ser sedan de data som importeras och en ny grupp skapas i läget **Inläsning**. Navigera inte bort från den här sidan förrän filen har överförts.

![Datauppsättning](./images/ingest4.png)

När filen har överförts ser du att batchstatusen har ändrats från **Inläsning** till **Bearbetning**.

![Datauppsättning](./images/ingest5.png)

Inmatning och bearbetning av data kan ta 10-20 minuter.

När dataimporten är klar ändras batchstatusen till **Slutfört**.

![Datauppsättning](./images/ingest7.png)

![Datauppsättning](./images/ingest8.png)

Nästa steg: [2.2.2 Kundens AI - Skapa en ny instans (Konfigurera)](./ex2.md)

[Gå tillbaka till modul 2.2](./intelligent-services.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
