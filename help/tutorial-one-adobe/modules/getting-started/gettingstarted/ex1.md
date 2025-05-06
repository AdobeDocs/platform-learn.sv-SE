---
title: Komma igång - Installera Chrome-tillägget för Experience League-dokumentationen
description: Komma igång - Installera Chrome-tillägget för Experience League-dokumentationen
kt: 5342
doc-type: tutorial
exl-id: 3618dacb-2203-4d19-ae51-f78415a693fd
source-git-commit: cc8efbdbcf90607f5a9bc98a2e787b61b4cd66d9
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---

# Installera Chrome-tillägget för Experience League-dokumentationen

## Om Chrome-tillägget

Den här självstudiekursen har gjorts generisk så att den enkelt kan återanvändas av vem som helst, oavsett Adobe Experience Cloud-instans.

För att dokumentationen ska kunna återanvändas introducerades **miljövariabler** i självstudiekursen, vilket betyder att du hittar **platshållarna** nedan i dokumentationen. Varje platshållare är en specifik variabel för en viss miljö, och Chrome-tillägget ändrar variabeln så att du enkelt kan kopiera kod och text från självstudiesidorna och klistra in den i de olika användargränssnitt som du kommer att använda som en del av självstudiekursen.

Ett exempel på sådana värden finns nedan. Dessa värden kan för närvarande inte användas ännu, men så fort du installerar och aktiverar Chrome-tillägget kommer dessa variabler att ändras till normal text som du kan kopiera och återanvända.

| Namn | Nyckel | Exempel |
|:-------------:| :---------------:| :---------------:|
| IMS-organisations-ID | `--aepImsOrgId--` | `907075E95BF479EC0A495C73@AdobeOrg` |
| IMS-organisationsnamn | `--aepImsOrgName--` | `Experience Platform International` |
| AEP Klient-ID | `--aepTenantId--` | `_experienceplatform` |
| Namn på AEP Sandbox | `--aepSandboxName--` | `one-adobe` |
| LDAP för lärarprofil | `--aepUserLdap--` | `vangeluw` |

I skärmbilden nedan visas till exempel en referens till `aepSandboxName`.

![DSN](./images/mod7before.png)

När tillägget har installerats ändras den texten automatiskt så att den återspeglar dina instansspecifika värden.

![DSN](./images/mod7.png)

## Installera Chrome-tillägget

Om du vill installera det Chrome-tillägget öppnar du webbläsaren i Chrome och går till: [https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi](https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi){target="_blank"}. Då ser du det här.

Klicka på **Lägg till i Chrome**.

![DSN](./images/c2.png)

Då ser du det här. Klicka på **Lägg till tillägg**.

![DSN](./images/c3.png)

Tillägget installeras sedan och ett liknande meddelande visas.

![DSN](./images/c4.png)

Klicka på ikonen **pusselbit** på menyn **extensions** och fäst tillägget **Platform Learn - Configuration** på tilläggsmenyn.

![DSN](./images/c6.png)

## Konfigurera Chrome-tillägget

Gå till [https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview){target="_blank"} och klicka sedan på tilläggsikonen för att öppna den.

![DSN](./images/tuthome.png)

Du kommer då att se den här popup-rutan. Klicka på ikonen **+**.

![DSN](./images/c7.png)

Ange de värden som anges nedan, som alla är relaterade till din Adobe Experience Platform-instans.

![DSN](./images/c8.png)

Om du är osäker på vilka värden du ska ange för de här fälten följer du riktlinjerna nedan.

**AEP IMS-organisationsnamn**

När du loggar in på din Adobe Experience Platform-instans på [https://platform.adobe.com/](https://platform.adobe.com/){target="_blank"} hittar du namnet på din instans i skärmens övre högra hörn.

![DSN](./images/aepname.png)

**AEP IMS-organisation-ID**

IMS-organisations-ID är den unika identifieraren för din Adobe Experience Cloud-instans, och den refereras till på flera platser under hela kursen.

Du kan söka efter ditt IMS-organisations-ID på flera sätt. Om du är osäker kan du söka efter ditt ID hos en av systemadministratörerna för instansen.

Du kan hitta den genom att gå till [Admin Console](https://adminconsole.adobe.com/){target="_blank"} där du kan hitta den som en del av URL:en.

![DSN](./images/aepid1.png)

Du kan också hitta den genom att gå till **Datahantering > Frågor** på AEP-menyn, där du hittar den under **Användarnamn**.

![DSN](./images/aepid2.png)

Se till att kopiera och klistra in delen **@AdobeOrg** tillsammans med ID:t.

**AEP Klient-ID**

Ditt klient-ID är den unika identifieraren för din organisations AEP-instans. När du loggar in på din Adobe Experience Platform-instans på [https://platform.adobe.com/](https://platform.adobe.com/){target="_blank"} hittar du klient-ID:t i URL:en.

![DSN](./images/aeptenantid.png)

När du anger det i Chrome-tillägget bör du se till att ett understreck läggs till som ett prefix, så i det här exemplet blir **ExperiencePlatform** **_experienceplatform**.

**AEP Sandbox-namn**

Ditt sandlådenamn är namnet på den miljö du kommer att använda i din AEP-instans. När du loggar in på din Adobe Experience Platform-instans på [https://platform.adobe.com/](https://platform.adobe.com/){target="_blank"} hittar du klient-ID:t i URL:en.

Innan du tar sandlådans namn från URL:en bör du kontrollera att du är i sandlådan som du bör använda för den här självstudiekursen. Du kan växla till den högra sandlådan genom att klicka på sandlådeväxlarmenyn i skärmens övre högra hörn.

![DSN](./images/aepsandboxsw.png)

I det här exemplet är AEP Sandbox-namnet **en-adobe**.

![DSN](./images/aepsname.png)

**Din LDAP**

Det här är användarnamnet som kommer att användas som en del av självstudiekursen. I det här exemplet baseras LDAP på den här användarens e-postadress. E-postadressen är **vangeluw@adobe.com** så LDAP blir **vangeluw**.

LDAP används för att se till att konfigurationen som du gör länkas till dig och inte hamnar i konflikt med andra användare som kanske använder samma instans och sandlåda som du använder.

Värdena bör likna dessa.
Klicka slutligen på **Skapa ny**.

![DSN](./images/c8a.png)

På den vänstra menyn i tillägget visas nu en ny ikon med miljöns initialer. Klicka på den. Du ser sedan mappningen mellan **miljövariablerna** och dina specifika Adobe Experience Platform-instansvärden. Klicka på **Aktivera konfiguration**.

![DSN](./images/c9.png)

När du har aktiverat konfigurationen visas en grön punkt bredvid initialerna för miljön. Det innebär att din miljö nu är aktiv.

![DSN](./images/c10.png)

## Verifiera självstudiekursens innehåll

Gå till [den här sidan](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-one-adobe/activation/dc/dc13/ex2){target="_blank"} som ett test.

Du bör nu se att alla **miljövariabler** på den här sidan har ersatts med sina verkliga värden, baserat på den aktiverade miljön i Chrome-tillägget.

Du bör nu ha en liknande vy som i nedanstående exempel, där miljövariabeln `aepSandboxName` har ersatts av ditt riktiga AEP Sandbox-namn, som i det här fallet är **one-adobe**.

![DSN](./images/mod7.png)

## Nästa steg

Gå till [Använd demosystemet intill för att konfigurera klientegenskapen för Adobe Experience Platform Data Collection](./ex2.md){target="_blank"}

Gå tillbaka till [Komma igång](./getting-started.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
