---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
exl-id: 587be8bc-8ebe-4f30-99d8-ba88ce40caf7
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Mål

- Förstå CJA-programtjänsten
- Lär dig placera CJA
- Förstå arbetsflödet i CJA: från dataanslutning till insikter

## 4.1.1 Vad är Customer Journey Analytics?

Customer Journey Analytics (CJA) tillhandahåller en verktygslåda till affärsintelligens- och datavetenskapsteamen för sammanfogning och analys av data över flera kanaler (online och offline). Funktionerna i CJA ger kontext och tydlighet till den komplexa flerkanaliga kundresan. Den tillhandahållna kontexten leder till användbar insikt i hur ni kan ta bort problem i kundkonverteringsprocessen och utforma och leverera exceptionella upplevelser för de ögonblick som betyder mest.

CJA lägger Analysis Workspace ovanpå Adobe Experience Platform. Adobe Experience Platform är hjärnan bakom kommunikation och samordning, och med CJA kan varumärken nu kontextualisera och visualisera alla dessa data, så att Business och Insight-team kan lära sig av dem genom att analysera hela kundresan online till offline.

Business- och Insight-teamen kan prata med CJA, ställa frågor och få svar direkt med dra-och-släpp, peka-och-klicka och användarvänliga gränssnitt i Analysis Workspace.

![demo](./images/cja-adv-analysis1.png)

## 4.1.2 Viktiga fördelar

De tre viktigaste fördelarna för kunderna är:

- Möjlighet att göra insikter tillgängliga för alla (dvs. att demokratisera dataåtkomsten)
- Förmågan att se kunden i en sammanhangsberoende resa (dvs. data kan visualiseras sekventiellt och spänna över flera kanaler både online och offline)
- Möjligheten att utnyttja data utan behov av (dvs. att låta vanliga människor använda data för att låsa upp djupgående insikter och analyser för aktivering av marknadsföringen)

## 4.1.3 Varför välja Customer Journey Analytics?

CJA är inte avsedd att ersätta ett aktuellt BI-program som Power BI, Microstrategy, Locker eller Tableau. Dessa BI-program är avsedda att visualisera data för att skapa företagsdashboards så att alla i en organisation snabbt kan se viktiga mätvärden.\
CJA:s mål är att ge marknadsförings- och affärsteamen analysmöjligheter och göra det till ett måste för de personernas analys.

Traditionellt har BI-program inte kunnat aktivera verkliga kunddata:

- De kan inte attribuera och inte göra kundreseanalyser.
- BI-program måste känna till frågan i förväg
- Interaktiva frågor begränsas av databasens struktur
- SQL-kunskaper krävs.
- BI-program ger dig inte möjlighet att fråga varför något hände.
- BI-program har ingen direktanslutning till kundens kontaktpunkter.

På grund av det ovan anförda stötte företagsanvändare och analytiker nästan omedelbart på nolltid, vilket gjorde analysen dyr, långsam, oflexibel och frånkopplad från system för åtgärder.

Med CJA kan ni få en 360-bild av kundresan, med hjälp av offline- och onlinedata, med rätt verktyg för att minska tiden för insikter, göra affärsanvändarna oberoende av varför något hände och hur de ska svara på det.

![demo](./images/cja-use-case.png)

## 4.1.4 Förstå arbetsflödet i Customer Journey Analytics

Innan du börjar nästa övning är det viktigt att förstå vilka steg som krävs för att överföra data från Adobe Experience Platform till CJA för att visualisera den och få djupgående insikter. Det är det vi kallar CJA Workflow. Låt oss titta på det:

![demo](./images/cja-work-flow.jpg)

Innan du börjar med stegen ovan ska du inte glömma steg 0, som är att förstå vilka data som finns i Adobe Experience Platform.

**Skräp in, skräp ut.** Kommer du ihåg? Du måste ha en tydlig uppfattning om vilka data som är tillgängliga och hur scheman i Adobe Experience Platform är konfigurerade. Förståelse av data i Adobe Experience Platform kommer att göra det enklare, inte bara i dataanslutningsdelen, utan även när man bygger visualiseringar och gör analyser.

## 4.1.5 Steg 0: Om Adobe Experience Platform scheman och datauppsättningar

Logga in på Adobe Experience Platform genom att gå till denna URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du loggat in kommer du till Adobe Experience Platform hemsida.

![Datainmatning](../uc1/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``Bootcamp``. Du kan göra detta genom att klicka på texten **[!UICONTROL Prod]** i skärmens övre högra hörn. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](../uc1/images/sb1.png)

Ta en titt på dessa scheman och datauppsättningar i Adobe Experience Platform.

| Datauppsättning | Schema |
| ----------------- |-------------| 
| Demo System - händelsedatauppsättning för webbplats (Global v1.1) | Demonstrationssystem - händelseschema för webbplats (Global v1.1) |
| Demo System - händelsedatauppsättning för callcenter (Global v1.1) | Demo System - händelseschema för callcenter (Global v1.1) |
| Demonstrationssystem - händelsedatauppsättning för röstassistenter (Global v1.1) | Demonstrationssystem - händelseschema för röstassistenter (Global v1.1) |

Se till att du åtminstone har kontrollerat saker som:

- Identiteter: CRMID, phoneNumber, ECID, email. Vilka identiteter är de primära identifierarna, vilka är de sekundära identifierarna?
Du kan hitta identifierarna genom att öppna ett schema och titta på objektet `_experienceplatform.identification.core`. Ta en titt på schemat [Demonstrationssystem - händelseschema för webbplats (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/identity.png)

- Utforska handelsobjektet i schemat [Demonstrationssystem - händelseschema för webbplats (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/commerce.png)

- Förhandsgranska alla [datauppsättningar](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) och ta en titt på data

Nu kan du börja använda användargränssnittet i Customer Journey Analytics.

Nästa steg: [4.2 Ansluta Adobe Experience Platform-datauppsättningar i Customer Journey Analytics](./ex2.md)

[Gå tillbaka till användarflöde 4](./uc4.md)

[Gå tillbaka till Alla moduler](../../overview.md)
