---
title: Foundation - datainmatning - Konfigurera datauppsättningar
description: Foundation - datainmatning - Konfigurera datauppsättningar
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 5afd987b-ccf8-414d-98aa-a485d6130c2e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# 2.3 Konfigurera datauppsättningar

I den här övningen ska du konfigurera de nödvändiga datauppsättningarna för att hämta in och lagra profilinformation och kundbeteende. Alla datauppsättningar som du skapar i det här steget använder ett av de scheman som du skapade i föregående steg.

## Artikel

När du har definierat svaret på frågorna **Vem är den här kunden?** och **Vad gör den här kunden?** måste du nu skapa en bucket som använder den informationen för att ta emot och validera data som skickats till Adobe Experience Platform.

## 2.3.1 - Skapa datauppsättningar

Nu behöver du skapa två datauppsättningar:

- 1 datauppsättning för att samla in information som besvarar **Vem är den här kunden?** - fråga.
- 1 datauppsättning för att samla in information som besvarar **Vad gör den här kunden?** - fråga.

Logga in på Adobe Experience Platform genom att gå till denna URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](./images/home.png)

Innan du fortsätter måste du välja en **[!UICONTROL sandlåda]**. Sandlådan som ska markeras har namnet ``--module2sandbox--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Dataintag](./images/sb1.png)

I Adobe Experience Platform klickar du på **[!UICONTROL Datauppsättningar]** på menyn till vänster på skärmen.  Då ser du det här:

![Dataintag](./images/menudatasets.png)

Vi börjar med att skapa datauppsättningen för att hämta registreringsinformation för webbplatsen.

Du bör skapa en ny datauppsättning. Om du vill skapa en ny datauppsättning klickar du på knappen **[!UICONTROL + Skapa datauppsättning]**.

![Dataintag](./images/createdataset.png)

När du klickat på **[!UICONTROL + Skapa datauppsättning]** visas följande skärm.

![Dataintag](./images/datasetsetup.png)

Du måste definiera en datauppsättning från schemat som du definierade i föregående steg. Klicka på **[!UICONTROL Skapa datauppsättning från schema]** - alternativ.

![Dataintag](./images/datasetfromschema.png)

På nästa skärm måste du välja det schema som du skapade i 1, `--demoProfileLdap-- - Demo System - Profile Schema for Website`.

![Dataintag](./images/schemaselection.png)

När du har valt schemat klickar du på **[!UICONTROL Nästa]** för att fortsätta.

![Dataintag](./images/next.png)

Låt oss ge datauppsättningen ett namn.

Använd följande som namn på datauppsättningen:

`--demoProfileLdap-- - Demo System - Profile Dataset for Website`

Som ett exempel för ldap **[!UICONTROL vangeluw]** bör det vara schemats namn:

**[!UICONTROL vangeluw - demosystem - profildatauppsättning för webbplats]**

Det borde ge dig något sådant:

![Dataintag](./images/datasetname.png)

Klicka **[!UICONTROL Slutför]** för att slutföra datauppsättningskonfigurationen.

![Dataintag](./images/finish.png)

Nu ser du det här:

![Dataintag](./images/dsoverview1.png)

Gå tillbaka till [!UICONTROL Datauppsättningar] översikt. Nu visas den datauppsättning som du skapade i översikten.

![Dataintag](./images/dsoverview2.png)

Därefter ska du konfigurera en andra datauppsättning för att fånga upp webbplatsinteraktioner.

Du bör skapa en ny datauppsättning. Om du vill skapa en ny datauppsättning klickar du på knappen **[!UICONTROL + Skapa datauppsättning]**.

![Dataintag](./images/createdataset.png)

När du klickat på **[!UICONTROL + Skapa datauppsättning]** visas följande skärm.

![Dataintag](./images/datasetsetup.png)

Du måste definiera en datauppsättning från schemat som du definierade i föregående steg. Klicka på **[!UICONTROL Skapa datauppsättning från schema]** - alternativ.

![Dataintag](./images/datasetfromschema.png)

På nästa skärm måste du välja det schema som du skapade i 2.2, `--demoProfileLdap-- - Demo System - Event Schema for Website`.

![Dataintag](./images/schemaselectionee.png)

När du har valt schemat klickar du på **[!UICONTROL Nästa]** för att fortsätta.

![Dataintag](./images/next.png)

Låt oss ge datauppsättningen ett namn.

Som namn för vår datauppsättning använder vi följande:

`--demoProfileLdap-- - Demo System - Event Dataset for Website`

Som ett exempel för ldap **[!UICONTROL vangeluw]** bör det vara schemats namn:

**[!UICONTROL vangeluw - demosystem - händelsedatauppsättning för webbplats]**

Det borde ge dig något sådant:

![Dataintag](./images/datasetnameee.png)

Klicka **[!UICONTROL Slutför]** för att slutföra datauppsättningskonfigurationen.

![Dataintag](./images/finish.png)

Då ser du det här:

![Dataintag](./images/finish1.png)

Gå tillbaka till [!UICONTROL Datauppsättningar] översiktsskärm.

![Dataintag](./images/datasetsoverview.png)

Nu måste du göra det möjligt för dina datauppsättningar att ingå i Adobe Experience Platform kundprofil i realtid.

Öppna din datauppsättning `--demoProfileLdap--` - Demonstrationssystem - profildatauppsättning för webbplats genom att klicka på den.

Leta reda på [!UICONTROL Profil] växlingsikonen till höger på skärmen.

![Dataintag](./images/ds1.png)

Klicka på [!UICONTROL Profil] växla för att aktivera den här datauppsättningen för [!UICONTROL Profil].

![Dataintag](./images/ds2.png)

Klicka på **[!UICONTROL Aktivera]**.

![Dataintag](./images/ds3.png)

Din datauppsättning har nu aktiverats för [!UICONTROL Profil].

Gå tillbaka till datauppsättningsöversikten och öppna datauppsättningen `--demoProfileLdap-- - Demo System - Event Dataset` för webbplats genom att klicka på den.

Leta reda på [!UICONTROL Profil] växlingsikonen till höger på skärmen.

![Dataintag](./images/ds4.png)

Klicka på [!UICONTROL Profil] växla för att aktivera [!UICONTROL Profil].

![Dataintag](./images/ds2.png)

Klicka **[!UICONTROL Aktivera]**.

![Dataintag](./images/ds5.png)

Din datauppsättning har nu aktiverats för [!UICONTROL Profil].

Nästa steg: [2.4 Datainmatning från offlinekällor](./ex4.md)

[Gå tillbaka till modul 2](./data-ingestion.md)

[Gå tillbaka till Alla moduler](../../overview.md)
