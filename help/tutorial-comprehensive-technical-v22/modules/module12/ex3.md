---
title: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector - Ansluta GCP och BigQuery till Adobe Experience Platform
description: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector - Ansluta GCP och BigQuery till Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b2b29cb7-dd5c-48f2-b881-3e10d9f1a0df
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 0%

---

# 12.3 Anslut GCP och BigQuery till Adobe Experience Platform

## Mål

- Utforska API och tjänster i Google Cloud Platform
- Bekanta dig med OAuth Playground för att testa Google API:er
- Skapa din första BigQuery-anslutning i Adobe Experience Platform

## Kontext

Adobe Experience Platform tillhandahåller en anslutning inom **Källor** som hjälper dig att överföra BigQuery-datauppsättningar till Adobe Experience Platform. Denna dataanslutning baseras på Google BigQuery API. Därför är det viktigt att förbereda Google Cloud Platform och BigQuery-miljön för att kunna ta emot API-anrop från Adobe Experience Platform.

För att konfigurera BigQuery Source Connector i Adobe Experience Platform behöver du följande fyra värden:

- projekt
- clientId
- clientSecret
- refreshToken

Än så länge har du bara den första, **Projekt-ID**. Detta **Projekt-ID** är ett slumpmässigt ID som genererades av Google när du skapade ditt BigQuery-projekt under övning 12.1.

Kopiera projekt-ID i en separerad textfil.

| Autentiseringsuppgifter | Namngivning | Exempel |
| ----------------- |-------------| -------------|
| Projekt-ID | random | sammansatt-uppgift-306413 |

Du kan när som helst kontrollera ditt projekt-ID genom att klicka på **Projektnamn** i den övre menyraden:

![demo](./images/ex1/projectMenu.png)

Du kommer att se ditt projekt-ID till höger:

![demo](./images/ex1/projetcselection.png)

I den här övningen får du lära dig hur du får de tre andra obligatoriska fälten:

- clientId
- clientSecret
- refreshToken

## 12.3.1 API och tjänster för Google Cloud

Börja med att gå tillbaka till startsidan för Google Cloud Platform. Det gör du genom att klicka på logotypen i det övre vänstra hörnet på skärmen.

![demo](./images/ex2/5.png)

När du är på startsidan går du till den vänstra menyn och klickar på **API:er och tjänster** och sedan klicka på **Kontrollpanel**.

![demo](./images/ex2/4.png)

Nu ser du **API:er och tjänster** hemsida.

![demo](./images/ex2/6.png)

På den här sidan kan du se hur olika Google API-anslutningar används. Om du vill konfigurera en API-anslutning så att Adobe Experience Platform kan läsa från BigQuery måste du göra följande:

- Först måste du skapa en OAuth-tillståndsskärm för att kunna aktivera framtida autentiseringar. Google säkerhetsskäl kräver också att en människa gör den första autentiseringen innan en programmatisk åtkomst tillåts.
- För det andra behöver du API-autentiseringsuppgifter (clientId och clientSecret) som ska användas för API-autentisering och åtkomst till BigQuery Connector.

## 12.3.2 OAuth-godkännandeskärm

Låt oss börja med att skapa OAuth-godkännandeskärmen. I den vänstra menyn på **API:er och tjänster** hemsida, klicka **OAuth-godkännandeskärm**.

![demo](./images/ex2/6-1a.png)

Då ser du det här:

![demo](./images/ex2/6-1.png)

Välj användartyp: **Extern**. Klicka på **SKAPA**.

![demo](./images/ex2/6-2.png)

Då är du på **Konfiguration av OAuth Consent Screen** -fönstret.

Det enda som behöver göras här är att ange namnet på godkännandeskärmen i **Programnamn** och välj **E-post till användarsupport**. Använd den här namnkonventionen för programnamnet:

| Namngivning | Exempel |
| ----------------- |-------------| 
| `--demoProfileLdap-- - AEP BigQuery Connector` | vangeluw - AEP BigQuery Connector |

![demo](./images/ex2/6-3.png)

Bläddra nedåt tills du ser **Kontaktinformation för utvecklare** och fylla i en e-postadress.

![demo](./images/ex2/6-3a.png)

Klicka **SPARA OCH FORTSÄTT**.

![demo](./images/ex2/6-4.png)

Du kommer då att se det här. Klicka **SPARA OCH FORTSÄTT**.

![demo](./images/ex2/o1.png)

Du kommer då att se det här. Klicka **SPARA OCH FORTSÄTT**.

![demo](./images/ex2/o2.png)

Du kommer då att se det här. Klicka **TILLBAKA TILL KONTROLLPANELEN**.

![demo](./images/ex2/o3.png)

Du kommer då att se det här. Klicka **PUBLICERA APP**.

![demo](./images/ex2/o4.png)

Klicka **BEKRÄFTA**.

![demo](./images/ex2/o5.png)

Du kommer då att se det här.

![demo](./images/ex2/o6.png)

I nästa steg avslutar du API-konfigurationen och får dina API-autentiseringsuppgifter.

## 12.3.3 Google API-autentiseringsuppgifter: Klienthemlighet och klient-ID

Klicka på **Autentiseringsuppgifter**. Då ser du det här:

![demo](./images/ex2/7.png)

Klicka på **+ SKAPA AUTENTISERINGSUPPGIFTER** -knappen.

![demo](./images/ex2/9.png)

Du kommer att se tre alternativ. Klicka på **OAuth-klient-ID**:

![demo](./images/ex2/11.png)

På nästa skärm väljer du **Webbprogram**.

![demo](./images/ex2/12.png)

Flera nya fält visas. Nu måste du ange **Namn** för OAuth-klient-ID och ange **Auktoriserade omdirigerings-URI:er**.

Följ den här namnkonventionen:

| Fält | Värde | Exempel |
| ----------------- |-------------| -------------| 
| Namn | ldap - AEP BigQuery Connector | vangeluw - Platform BigQuery Connector |
| Auktoriserade omdirigerings-URI:er | https://developers.google.com/oauthplayground | https://developers.google.com/oauthplayground |

The **Auktoriserade omdirigerings-URI:er** fältet är ett mycket viktigt fält eftersom du behöver det senare för att få den RefreshToken som du behöver för att slutföra konfigurationen av BigQuery Source Connector i Adobe Experience Platform.

![demo](./images/ex2/12-1.png)

Innan du fortsätter måste du trycka på **Retur** efter att du angett URL:en för att lagra värdet i **Auktoriserade omdirigerings-URI:er** fält. Om du inte klickar på **Retur** kommer du att stöta på problem i ett senare skede i **OAuth 2.0 Playground**.

Klicka på **Skapa**:

![demo](./images/ex2/19.png)

Nu visas ditt klient-ID och din klienthemlighet.

![demo](./images/ex2/20.png)

Kopiera dessa två fält och klistra in dem i en textfil på skrivbordet. Du kan alltid komma åt dessa autentiseringsuppgifter i ett senare skede, men det är enklare om du sparar dem i en textfil bredvid ditt BigQuery-projekt-ID.

I Adobe Experience Platform finns nu följande värden tillgängliga:

| Referenser för BigQuery Connector | Värde |
| ----------------- |-------------| 
| Projekt-ID | ditt eget projekt-ID (t.ex.: composition-task-306413) |
| klientid | dinclientid |
| cilenthemlighet | din klienthemlighet |


Du saknar fortfarande **refreshToken**. refreshToken är ett krav på grund av säkerhetsskäl. I API:ernas värld går tokens normalt ut var 24:e timme. Så **refreshToken** behövs för att uppdatera säkerhetstoken var 24:e timme, så att konfigurationen av Source Connector kan fortsätta ansluta till Google Cloud Platform och BigQuery.

## 12.3.4 BigQuery API och refreshToken

Det finns många sätt att få en refreshToken för att få åtkomst till API:er för Google Cloud-plattformen. Ett av dessa alternativ är exempelvis att använda Postman.
Google har dock byggt något som är enklare att testa och spela med API:erna, ett verktyg som kallas **OAuth 2.0 Playground**.

För åtkomst **OAuth 2.0 Playground**, gå till [https://developers.google.com/oauthplayground](https://developers.google.com/oauthplayground).

Då ser du **OAuth 2.0 Playground** hemsida.

![demo](./images/ex2/22.png)

Klicka på **växel** ikonen längst upp till höger på skärmen:

![demo](./images/ex2/22-1.png)

Kontrollera att inställningarna är desamma som i bilden ovan.

Kontrollera inställningarna så att de är 100 % säkra.

När du är klar markerar du kryssrutan för **Använd dina egna OAuth-autentiseringsuppgifter**

![demo](./images/ex2/22-2.png)

Två fält ska visas och du har värdet för dem.

![demo](./images/ex2/23.png)

Fyll i fälten efter denna tabell:

| Inställningar för uppspelnings-API | Dina Google API-autentiseringsuppgifter |
| ----------------- |-------------| 
| OAuth-klient-ID | ditt eget klient-ID (i textfilen på skrivbordet) |
| OAuth-klienthemlighet | din egen klienthemlighet (i textfilen på skrivbordet) |

![demo](./images/ex2/23-a.png)

Kopiera **Klient-ID** och **Klienthemlighet** från textfilen som du skapade på skrivbordet.

![demo](./images/ex2/20.png)

När du fyllt i dina uppgifter klickar du **Stäng**

![demo](./images/ex2/23-1.png)

På den vänstra menyn kan du se alla tillgängliga Google API:er. Sök efter **BigQuery API v2**.

![demo](./images/ex2/27.png)

Välj sedan det omfång som anges i bilden nedan:

![demo](./images/ex2/26.png)

När du har valt dem bör du se en blå knapp som säger **Auktorisera API:er**. Klicka på den.

![demo](./images/ex2/28.png)

Välj det Google-konto du använde för att konfigurera GCP och BigQuery.

En stor varning kan visas: **Den här appen har inte verifierats**. Detta beror på att din Platform BigQuery Connector inte har granskats formellt än, så Google vet inte om det är en autentisk app eller inte. Du bör bortse från det här meddelandet.

Klicka **Avancerat**.

![demo](./images/ex2/32.png)

Klicka på **Gå till ldap - AEP BigQuery Connector (osäker)**.

![demo](./images/ex2/33.png)

Du omdirigeras till den OAuth-godkännandeskärm som du skapade.

![demo](./images/ex2/29.png)

Om du använder tvåfaktorsautentisering (2FA) anger du den verifieringskod som skickas till dig.

![demo](./images/ex2/30.png)

Google visar nu åtta olika **Behörighet** uppmaningar. Klicka **Tillåt** för alla åtta behörighetsbegäranden. (Detta är en procedur som måste följas och bekräftas en gång av en riktig människa, innan API:t tillåter programmatiska begäranden)

Igen, **åtta olika popup-fönster** visas inte, du måste klicka **Tillåt** för alla.

![demo](./images/ex2/29.png)

Efter de åtta behörighetsbegärandena visas den här översikten. Klicka **Tillåt** för att slutföra processen.

![demo](./images/ex2/35.png)

Efter den sista **Tillåt**-click, you will be sent back to the OAuth 2.0 Playground and you will see this:

![demo](./images/ex2/36.png)

Klicka **Exchange-auktoriseringskod för tokens**.

![demo](./images/ex2/36-1.png)

Efter några sekunder har **Steg 2 - Exchange-auktoriseringskod för tokens** vyn stängs automatiskt och du ser **Steg 3 - Konfigurera begäran till API**.

Du måste gå tillbaka till **Steg 2 Verifieringskod för Exchange för tokens** så klicka på **Steg 2 Verifieringskod för Exchange för tokens** igen för att visualisera **Uppdatera token**.

![demo](./images/ex2/37.png)

Nu ser du **Uppdatera token**.

![demo](./images/ex2/38.png)

Kopiera **Uppdatera token** och klistra in den i textfilen på skrivbordet tillsammans med de andra autentiseringsuppgifterna för BigQuery-källkopplingen:

| Referenser för BigQuery-källkoppling | Värde |
| ----------------- |-------------| 
| Projekt-ID | ett eget slumpmässigt projekt-ID (t.ex.: apt-sommar-273608) |
| klientid | dinclientid |
| cilenthemlighet | din klienthemlighet |
| uppdateringstoken | din uppdateringstoken |

Sedan ställer vi in Source Connector i Adobe Experience Platform.

## Exercise 12.3.5 - Connect Platform with your own BigQuery table

Logga in på Adobe Experience Platform genom att gå till denna URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Dataintag](../module2/images/sb1.png)

Gå till Källor på den vänstra menyn. Då ser du **Källor** hemsida. I **Källor** meny, klicka på **Databaser**. Klicka på **Google BigQuery** kort. Klicka på **Konfigurera** eller **+ Konfigurera**.

![demo](./images/1.png)

Nu bör du skapa en ny anslutning.

Klicka på **Nytt konto**. Nu måste du fylla i alla nedanstående fält, baserat på de inställningar du gjorde i GCP och BigQuery.

![demo](./images/3.png)

Vi börjar med att namnge anslutningen:

Använd den här namnkonventionen:

| Referenser för BigQuery Connector | Värde | Exempel |
| ----------------- |-------------| -------------| 
| Kontonamn | `--demoProfileLdap-- - BigQuery Connection` | vangeluw - BigQuery Connection |
| Beskrivning | `--demoProfileLdap-- - BigQuery Connection` | vangeluw - BigQuery Connection |

Det borde ge dig något sådant här:

![demo](./images/ex2/39-a.png)

Fyll sedan i GCP- och BigQuery API **Kontoautentisering**-information som du lagrade i en textfil på skrivbordet:

| Referenser för BigQuery Connector | Värde |
| ----------------- |-------------| 
| Projekt-ID | ett eget slumpmässigt projekt-ID (t.ex.: apt-sommar-273608) |
| clientId | ... |
| cilentSecret | ... |
| refreshToken | ... |

Dina **Kontoautentisering**-details ska nu se ut så här:

![demo](./images/ex2/39-xx.png)

När du har fyllt i alla dessa fält klickar du på **Anslut till källa**.

![demo](./images/ex2/39-2.png)

Om **Kontoautentisering** informationen har fyllts i korrekt bör du nu se en visuell bekräftelse på att anslutningen fungerar som den ska genom att se **Ansluten** bekräftelse.

![demo](./images/ex2/projectid.png)

Nu när du har skapat anslutningen klickar du på **Nästa**:

![demo](./images/42.png)

Du kommer nu att se den BigQuery-datauppsättning som du skapade under övning 12.2.

![demo](./images/datasets.png)

Bra gjort! I nästa övning läser du in data från den tabellen och mappar den mot ett schema och en datauppsättning i Adobe Experience Platform.

Nästa steg: [12.4 Läs in data från BigQuery till Adobe Experience Platform](./ex4.md)

[Gå tillbaka till modul 12](./customer-journey-analytics-bigquery-gcp.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
