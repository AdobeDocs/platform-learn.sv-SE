---
title: Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
description: Kom igång med Adobe Experience Platform for Data Architects and Data Engineers.
breadcrumb-title: Översikt
role: Data Architect, Data Engineer
jira: KT-4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: 63987fb652a653283a05a5f35f7ce670127ae905
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Getting Started with Adobe Experience Platform for Data Architects and Data Engineers

<!--5min-->

_Komma igång med Adobe Experience Platform för dataarkitekter och datatekniker_ är den perfekta startpunkten för att komma i kontakt med Experience Platform.


<!--How do we address ETL-->

## Utbildningsmål

Dataarkitekter och datatekniker måste samarbeta nära för en framgångsrik driftsättning i Experience Platform. Den här praktiska självstudiekursen lär dig de viktigaste uppgifter som utförs av _båda rollerna_ så att du vet hur du börjar implementera Platform för ditt eget företag. Du får hjälp med övningar som presenterar nyckelterminologi, funktioner, gränssnitt och API:er för Experience Platform. Kunder som använder Adobe Experience Cloud-program som Real-time Customer Data Platform, Customer Journey Analytics och Journey Optimizer tycker också att det här innehållet är användbart eftersom plattformstjänster är en viktig grund för dessa program.

![Adobe Experience Cloud Marknadsföring framhäver de plattformstjänster som ingår i den här självstudiekursen: Identitet, Profil, Segmentering, Ingestion, Query och Governance](assets/marketecture.png)

Ämnen:

* Konfigurera användarbehörigheter
* Skapa sandlådor
* Konfigurera ett Developer Console-projekt och använda Platform API
* Datahantering - inklusive att skapa scheman, datauppsättningar, identiteter, sammanfogningsprinciper och datastyrning
* Inläsning av data med batchläge och direktuppspelningsläge
* Hämta webbdata med Adobe Experience Platform Web SDK
* Skapa kundprofiler i realtid
* Validera data och extrahera data med frågetjänsten
* Bygga segment

## Affärsscenario

Adobe Experience Platform är en teknisk plattform som hjälper er att uppnå era marknadsföringsmål. Användningsexemplen bör styra hur du utformar och implementerar tekniken. Den här självstudiekursen fokuserar på ett fiktivt varumärke som kallas Luma. Luma driver tegelhus i flera länder och har också en onlinenärvaro med en webbplats och mobilappar. De investerar i Adobe Experience Platform för att kombinera kundlojalitet, CRM, webb och offlineköp i kundprofiler i realtid och aktivera profilerna för att ta marknadsföringen till nästa nivå. Affärsmålen för Luma kanske inte överensstämmer med företagets mål, men du bör kunna koppla de konkreta stegen i den här självstudiekursen till dina egna affärsmål.

## Krav

* Du har tittat på [Introduktionen till Adobe Experience Platform-spellistan](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction) på Experience League och känner till plattformsfunktionerna
* Du har tillgång till ett konto som etablerats med Adobe Experience Platform (eller ett plattformsbaserat program som Real-Time CDP eller Journey Optimizer) och Data Collection (tidigare Launch).
* Du är systemadministratör för det kontot eller kan ha en [konfigurera användarbehörigheter](configure-permissions.md) åt dig.

## Använda den här självstudiekursen

I den här självstudiekursen kombineras uppgifter för både datatekniker och dataarkitekter. Eftersom det är en självstudiekurs på introduktionsnivå bör du kunna slutföra uppgifterna för båda rollerna. Eftersom många av lektionerna bygger på det som implementerades i tidigare lektioner bör du gå igenom lektionerna i ordning. Jag ska ta reda på vilka lektioner som kan hoppas över.

När du skapar olika plattformselement under den här självstudiekursen kan du försöka hålla dig till de namn jag rekommenderar så mycket som möjligt. Det finns dock några högnivåelementnamn som du kanske vill anpassa om det finns flera personer på din organisation som tar den här självstudiekursen samtidigt. Du kan till exempel kalla plattformssandlådan&quot;Luma Tutorial Platform - Ignatius J Reilly&quot; i stället för bara&quot;Luma Tutorial Platform&quot;.

Om du fastnar kan du försöka läsa instruktionerna igen först och sedan använda länken ![Logga ett problem](https://experienceleague.adobe.com/assets/img/feedback.svg) på sidofältet på varje sida för att kontakta mig.

## Teknisk information

### Sandlådemiljöer

I självstudiekursen skapar du en sandlådemiljö och använder den för att slutföra övningarna. Sandlådemiljön gör det säkert för dig att slutföra övningarna och experimentera utan att behöva oroa dig för att dina produktionsdata ska äventyras.

### API

Plattformen är byggd för API. Det finns gränssnittsarbetsflöden för alla större plattformsarbetsflöden och de kommer att användas främst, men självstudiekursen innehåller vissa API-orienterade övningar. Jag vägleder dig genom de grundläggande projektinställningarna i Adobe Developer Console och ger dig [!DNL Postman] miljöer och samlingar för att komma igång med Platform API. När du är klar med självstudiekursen kanske du tycker att det är värdefullt att känna till Platform API och använda den i din egen distribution.

### Tredjepartstekniker

Även om du kommer att använda flera olika tekniker i den här självstudiekursen finns du nästan bara kvar i Adobe ekosystem. I er egen plattformsimplementering är det troligt att ni integrerar Platform med specifika tredjepartstekniker. För att den här självstudiekursen ska vara relevant för alla kunder använder vi en mer generisk implementering.

## Självstudiekursuppdateringar

* Juni 2023: Uppdaterat för att inkludera ett nytt behörighetsarbetsflöde och för att använda API-autentiseringsuppgifter för OAuth Server-till-Server


Låt oss nu gå vidare till den första lektionen -[konfigurera behörigheter](configure-permissions.md).
