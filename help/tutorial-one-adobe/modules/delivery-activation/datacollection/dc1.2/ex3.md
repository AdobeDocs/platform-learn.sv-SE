---
title: Foundation - datainmatning - Konfigurera datauppsättningar
description: Foundation - datainmatning - Konfigurera datauppsättningar
kt: 5342
doc-type: tutorial
exl-id: 322aaaaa-50f7-4da4-bc4b-1b7edfe17e54
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# 1.2.3 Konfigurera datauppsättningar

I den här övningen ska du konfigurera datauppsättningar för att hämta in och lagra profilinformation och kundbeteende. Alla datauppsättningar som du skapar i det här steget använder ett av de scheman som du skapade i föregående steg.

## Kontext

När du har definierat svaret på frågorna **Vem är den här kunden?** och **Vad gör den här kunden?** ska se ut som om du nu måste skapa en bucket som använder den informationen för att ta emot och validera data som skickats till Adobe Experience Platform.

## Skapa datauppsättningar

Nu behöver du skapa två datauppsättningar:

- 1 datauppsättning för att hämta information som besvarar **Vem är den här kunden?** - fråga.
- 1 datauppsättning för att hämta information som besvarar **Vad gör den här kunden?** - fråga.

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./images/home.png)

Innan du fortsätter måste du välja en **[!UICONTROL sandbox]**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./images/sb1.png)

Klicka på **[!UICONTROL Datasets]** på menyn till vänster på skärmen i Adobe Experience Platform.  Då ser du det här:

![Datainmatning](./images/menudatasets.png)

Vi börjar med att skapa datauppsättningen för att hämta registreringsinformation för webbplatsen.

Du bör skapa en ny datauppsättning. Om du vill skapa en ny datauppsättning klickar du på knappen **[!UICONTROL + Create Dataset]**.

![Datainmatning](./images/createdataset.png)

Du måste definiera en datauppsättning från schemat som du definierade i föregående steg. Klicka på alternativet **[!UICONTROL Create Dataset from Schema]** -.

![Datainmatning](./images/datasetfromschema.png)

På nästa skärm måste du välja det schema som du skapade i , `--aepUserLdap-- - Demo System - Profile Schema for Website`.

Klicka på **Nästa**.

![Datainmatning](./images/schemaselection.png)

Låt oss ge datauppsättningen ett namn.

Använd följande som namn på datauppsättningen:

`--aepUserLdap-- - Demo System - Profile Dataset for Website`

Klicka på **Slutför**.

![Datainmatning](./images/datasetname.png)

Nu ser du det här:

![Datainmatning](./images/dsoverview1.png)

Gå tillbaka till översikten för [!UICONTROL Datasets]. Nu visas den datauppsättning som du skapade i översikten.

![Datainmatning](./images/dsoverview2.png)

Därefter ska du konfigurera en andra datauppsättning för att fånga upp webbplatsinteraktioner.

Klicka på **[!UICONTROL + Create Dataset]**.

![Datainmatning](./images/createdataset.png)


Du måste definiera en datauppsättning från schemat som du definierade i föregående steg. Klicka på alternativet **[!UICONTROL Create Dataset from Schema]** -.

![Datainmatning](./images/datasetfromschema.png)

På nästa skärm måste du välja det schema som du skapade tidigare, `--aepUserLdap-- - Demo System - Event Schema for Website`.

Klicka på **Nästa**.

![Datainmatning](./images/schemaselectionee.png)

Låt oss ge datauppsättningen ett namn.

Använd följande som namn på datauppsättningen:

`--aepUserLdap-- - Demo System - Event Dataset for Website`

Klicka på **Slutför**.

![Datainmatning](./images/datasetnameee.png)

Då ser du det här:

![Datainmatning](./images/finish1ee.png)

Gå tillbaka till översiktsskärmen [!UICONTROL Datasets].

![Datainmatning](./images/datasetsoverview.png)

Nu måste du aktivera dina datauppsättningar som en del av Adobe Experience Platform kundprofil i realtid.

Öppna datauppsättningen `--aepUserLdap-- - Demo System - Profile Dataset for Website` genom att klicka på den.

Leta reda på växlingsikonen [!UICONTROL Profile] till höger på skärmen.
Klicka på växlingsknappen [!UICONTROL Profile] för att aktivera den här datauppsättningen för [!UICONTROL Profile].

![Datainmatning](./images/ds1.png)

Klicka på **[!UICONTROL Enable]**.

![Datainmatning](./images/ds3.png)

Din datauppsättning har nu aktiverats för [!UICONTROL Profile].

Gå tillbaka till översikten över datauppsättningarna och öppna datauppsättningen `--aepUserLdap-- - Demo System - Event Dataset` för webbplatsen genom att klicka på den.

Leta reda på växlingsikonen [!UICONTROL Profile] till höger på skärmen. Klicka på [!UICONTROL Profile] för att aktivera [!UICONTROL Profile].

![Datainmatning](./images/ds4.png)

Klicka på **[!UICONTROL Enable]**.

![Datainmatning](./images/ds5.png)

Din datauppsättning har nu aktiverats för [!UICONTROL Profile].

## Nästa steg

Gå till [1.2.4 Datainmatning från offlinekällor](./ex4.md){target="_blank"}

Gå tillbaka till [datainmatning](./data-ingestion.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
