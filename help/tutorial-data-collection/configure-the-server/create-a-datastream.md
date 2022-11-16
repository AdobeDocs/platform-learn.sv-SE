---
title: Skapa ett datastream
description: Skapa ett datastream
exl-id: 4a33a7f3-8bd8-4d28-9ae4-a0609444485f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Skapa ett datastream

De data du skickar från din webbplats med Platform Web SDK når en uppsättning Adobe-servrar som kallas [Adobe Experience Platform Edge Network](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Det här nätverket kan skicka dina data till [Adobe Experience Platform dataset du skapade tidigare](create-a-schema.md) och andra produkter i Adobe Experience Cloud. Dessa Adobe-produkter kan också svara på data på din webbsida. Edge Network kan till exempel returnera personaliseringsinnehåll från Adobe Target.

Om du vill konfigurera vilka Adobe-produkter Edge Network skickar data till och från måste du skapa ett datastream. När Edge Network tar emot data från din webbsida, konsulterar den dataström du har skapat, läser dess konfiguration och vidarebefordrar data till rätt Adobe-produkter.

![Datastream-produktkonfiguration](../assets/datastream-diagram.png)

1. Om du vill skapa ett datastream måste du först navigera till användargränssnittet i datainsamlingen. I det övre högra hörnet av plattformen klickar du på **[!UICONTROL Programväljare]** och markera **[!UICONTROL Datainsamling]** i listrutan.
   ![Meny för datainsamling](../assets/data-collection-menu.png)
1. När gränssnittet för datainsamling visas väljer du **[!UICONTROL Datastreams]** i den vänstra navigeringen och sedan **[!UICONTROL Ny datastream]** i det övre högra hörnet.
1. Ange ett namn för datastream, välj [schemat som du skapade tidigare](create-a-schema.md) som **[!UICONTROL Händelsedatauppsättning]** och markera **[!UICONTROL Spara]** (mappningen beskrivs senare).
   ![Namn och beskrivning för dataström](../assets/datastream-name-description.png)

## Lägg till tjänst i datastream

På nästa skärm kan du lägga till vilka Adobe-produkter och -tjänster som ska ta emot data som du skickar från din webbplats.

1. Välj **[!UICONTROL Lägg till tjänst]** -kommando. Aktivera endast Adobe Experience Platform genom att välja [den datauppsättning du skapade tidigare](create-a-dataset.md) och markera **[!UICONTROL Spara]** i det övre högra hörnet. Ditt datastream har skapats.
   ![Datastream-produktkonfiguration](../assets/datastream-product-configuration.png)

## Datastream-miljöer

Företagen har vanligtvis en kampanjväg för alla webbplatsuppdateringar. Någon på företaget (en marknadsförare eller tekniker, beroende på ändringarna) testar vanligtvis sina ändringar i en utvecklingsmiljö som bara den personen använder. När de känner sig bekväma med ändringarna befordras ändringarna till en staging-miljö där de får ytterligare testning. Äntligen publiceras ändringarna på produktionens webbplats. Datastreams stöder det här kampanjmönstret.

Om du stöder plattformsbaserade program som CDP, Journey Optimizer eller Customer Journey Analytics i realtid måste ytterligare datastreams skapas i de separata plattformssandlådor som motsvarar dessa miljöer.

Om du inte är en plattformskund kan du skapa flera datastreams i en enda sandlåda och använda funktionen för datastream-kopiering för att duplicera inställningar.

Servern är nu helt konfigurerad för att ta emot data från din webbsida.

[Nästa: ](../configure-the-client/whats-a-data-layer.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om datainsamling. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
