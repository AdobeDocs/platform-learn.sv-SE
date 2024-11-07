---
title: Komma igång - Installera Chrome-tillägget för dokumentationen för Experience League
description: Komma igång - Installera Chrome-tillägget för dokumentationen för Experience League
kt: 5342
doc-type: tutorial
source-git-commit: 8d595675c09a4347c04e900414d94b6c674e20f7
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 0.1 Installera Chrome-tillägget för dokumentationen för Experience League

## 0.1.1 Varför har vi skapat ett Chrome-tillägg?

Dokumentationen har gjorts generisk så att den enkelt kan återanvändas av vem som helst, med valfri Adobe Experience Platform-instans.
Genom att göra dokumentationen återanvändbar introducerades **miljövariabler** i dokumentationen, vilket innebär att du hittar **nycklarna** nedan i dokumentationen. Varje nyckel är en specifik variabel för en viss miljö, och Chrome-tillägget ändrar variabeln åt dig och gör det därför enkelt för dig att kopiera kod och text från självstudiesidorna och klistra in den i de olika användargränssnitt som du kommer att använda som en del av självstudiekursen.

Ett exempel på sådana värden finns nedan. Dessa värden kan för närvarande inte användas än, men så fort du installerar och aktiverar Chrome-tillägget ändras dessa variabler till &quot;normal&quot; text som du kan kopiera och återanvända.

| Namn | Nyckel |
|:-------------:| :---------------:|
| AEP IMS-organisations-ID | `--aepImsOrgId--` |
| Klient-ID för AEP | `--aepTenantId--` |
| Namn på AEP-sandlåda | `--aepSandboxName--` |
| LDAP för lärarprofil | `--aepUserLdap--` |

I skärmbilden nedan visas till exempel en referens till `--aepTenantId--`.

![DSN](./images/mod7before.png)

När tillägget har installerats ändras den texten automatiskt så att den återspeglar dina instansspecifika värden.

![DSN](./images/mod7.png)

Tillägget gör det även möjligt för dig att:

- Registrera dig för självstudiekursen

## 0.1.2 Installera Chrome-tillägget

Om du vill installera det Chrome-tillägget öppnar du webbläsaren i Chrome och går till: [https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0](https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0). Då ser du det här.

Klicka på **Lägg till i Chrome**.

![DSN](./images/c2.png)

Då ser du det här. Klicka på **Lägg till tillägg**.

![DSN](./images/c3.png)

Tillägget installeras sedan och ett liknande meddelande visas.

![DSN](./images/c4.png)

Klicka på ikonen **pusselbit** på menyn **extensions** och fäst tillägget **Platform Learn - Configuration** på tilläggsmenyn.

![DSN](./images/c6.png)

## 0.1.2 Konfigurera Chrome-tillägget

Gå till [https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en) och klicka sedan på tilläggsikonen för att öppna den.

![DSN](./images/tuthome.png)

Du kommer då att se den här popup-rutan. Klicka på ikonen **+**.

![DSN](./images/c7.png)

Ange ditt namn och det konfigurations-ID som skapades för din Adobe Experience Platform-miljö. Klicka på **Skapa ny**.

>[!IMPORTANT]
>
>Om du är Adobe-anställd: du hittar det konfigurations-ID som ska användas på den interna Github-repon (https://git.corp.adobe.com/vangeluw/platformenablement).
>
>Om du är Adobe Solution Partner kontaktar du din Solution Partner-kontakt eller mejlar **spphelp@adobe.com**.

![DSN](./images/c8.png)

På den vänstra menyn i tillägget visas nu en ikon med dina initialer. Klicka på den. Du ser sedan mappningen mellan **miljövariablerna** och dina specifika Adobe Experience Platform-instansvärden. Klicka på **Aktivera konfiguration**.

![DSN](./images/c9.png)

När du har aktiverat konfigurationen visas en grön punkt bredvid dina initialer. Detta innebär att ditt konfigurations-ID nu är aktivt. Du kommer även att se ett antal ytterligare menyalternativ.

![DSN](./images/c10.png)

Nu finns det två alternativ:

- Om du är en befintlig användare av aktiveringen med en befintlig konfiguration går du till **0.1.3 Befintlig användare - Logga in**
- Om du är en helt ny användare som startar den här självstudiekursen för första gången går du till **0.1.4 Registrering** och hoppar över **0.1.3 Befintlig användare - Inloggning**

## 0.1.3 Befintlig användare - inloggning

>[!IMPORTANT]
>
>Utför **0.1.3 Befintlig användare - Inloggning** fungerar bara om du är en befintlig användare som tidigare har registrerat sig för den här självstudien.

Om du är en befintlig användare som konfigurerar det här Chrome-tillägget för första gången klickar du på den lila ikonen i den vänstra menyn. Då ser du det här.

![DSN](./images/chromeret1.png)

Fyll i värdena efter behov.

>[!IMPORTANT]
>
>**LDAP** är det viktigaste fältet: du bör använda samma LDAP som du använde när du först registrerade dig för kursen. Detta säkerställer att dina förlopp läses in. Om du är osäker på vad din ldap är kan du titta på din e-postadress. Använd texten före @-symbolen i din e-postadress som LDAP. Om din e-postadress är **techinsiders@adobe.com** bör den LDAP du anger här vara **vangeluw**).

![DSN](./images/chromeret2.png)

Klicka på **OK**.

![DSN](./images/chromeret3.png)

Efter 30 sek-1 minut ändras skärmen och du återställs till **Hem**, där du ser följande:

![DSN](./images/chromeret4.png)

Ditt Chrome-tillägg är nu konfigurerat och du kan nu kontrollera om allt fungerar som det ska.

## 0.1.4 Ny användare - Registrering

>[!IMPORTANT]
>
>Utgång **0.1.4 Ny användare - Registrering** är avsedd för nya användare som startar den här självstudiekursen för första gången.

Om du är en ny användare som registrerar sig för kursen första gången klickar du på den gula ikonen på menyn. Då ser du det här.

![DSN](./images/c11.png)

Fyll i fälten efter behov. Klicka på **Spara**.

>[!IMPORTANT]
>
>**LDAP** är det viktigaste fältet. Om du är osäker på vad din ldap är kan du titta på din e-postadress. Använd texten före @-symbolen i din e-postadress som LDAP. Om din e-postadress är **techinsiders@adobe.com** bör den LDAP du anger här vara **vangeluw**).

![DSN](./images/chrome1.png)

Efter 30 sek-1 minut ändras skärmen och du återställs till **Hem**, där du ser följande:

![DSN](./images/chrome2.png)

Ditt Chrome-tillägg är nu konfigurerat och du kan nu kontrollera om allt fungerar som det ska.

## 0.1.5 Bekräfta självstudiekursens innehåll

Gå till [den här sidan](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/module4/ex3.html?lang=en) som ett test.

Du bör nu se att alla **miljövariabler** har ersatts med sina verkliga värden, baserat på konfigurations-ID:t i Chrome-tillägget.

Du bör nu ha en liknande vy som i nedanstående exempel, där miljövariablerna `--aepTenantId--` har ersatts av ditt riktiga klient-ID, som i det här fallet är **_experienceplatform**.

![DSN](./images/c12.png)

Nästa steg: [0.2 Använd demonstrationssystemet bredvid för att konfigurera klientegenskapen för Adobe Experience Platform Data Collection](./ex2.md)

[Gå tillbaka till modul 0](./getting-started.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
