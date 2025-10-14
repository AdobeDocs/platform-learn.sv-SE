---
title: CSC-startläger - verifiera mobilapp
description: CSC-startläger - verifiera mobilapp
doc-type: multipage-overview
exl-id: 930d9487-7c39-4657-9fe4-436dc53343e1
source-git-commit: 143da6340b932563a3309bb46c1c7091e0ab2ee2
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Verifiera mobilapp

## Android

- Hämta mobilappen från [här](https://tinyurl.com/CSCBootcampApp) på din Android-enhet. Du kan hämta den på en [Android-emulator](https://developer.android.com/studio/run/emulator) eller din fysiska Android-enhet.

![Hämta app](./images/delivery-app-android-download.png)

- Öppna den hämtade filen genom att trycka på den.

![Öppna APK-filen](./images/delivery-app-android-install.png)

- Klicka på installationsknappen i popup-fönstret och bekräfta sedan genom att klicka på Installera ändå.

![Installera appen](./images/delivery-app-android-install-prompt.png)

![Lita på appen](./images/delivery-app-android-install-anyway.png)

- När appen har installerats kan du öppna den genom att klicka på knappen Öppna.

![Öppna appen](./images/delivery-app-android-open.png)


## iOS

>[!WARNING]
>
> Kontrollera att du är ansluten till Bootcamp Wifi-nätverket. Detta är viktigt eftersom programmet bara fungerar om du är i samma Wifi-nätverk.

Eftersom detta inte är en officiellt distribuerad app är iOS-konfigurationen något annorlunda än vad du är van vid.

- Hämta Expo Go-appen från [App Store](https://itunes.apple.com/app/apple-store/id982107779).

![Ladda ned programmet för export](./images/delivery-app-ios-download.png)

- I appen iPhone Camera kan du skanna den QR-kod som Adobe-teamet ska projicera på bootlägret. När du uppmanas till det klickar du på knappen som visas.

![Klicka på QR-koden](./images/delivery-app-ios-scan.png)

- Då öppnas en webbsida där du kan öppna appen på din iPhone. Klicka på knappen &quot;Expo Go&quot; för att öppna den i det program du just laddat ned.

![Klicka på knappen för att exportera &#x200B;](./images/delivery-app-ios-open-expo.png)

- I den dialogruta som öppnas väljer du&quot;Öppna&quot; så att programmet Expo Go kan läsas in med rätt information.

![Klicka på knappen Öppna](./images/delivery-app-ios-open.png)

- När programmet Expo Go har öppnats uppmanas du att söka efter enheter i det lokala nätverket. Som tidigare nämnts är detta nödvändigt så att vi kan hämta appen från våra Adobe-enheter till din telefon. Klicka på Tillåt för att läsa in det här.

![Tillåt nödvändiga behörigheter](./images/delivery-app-ios-allow.png)

- Du kan få en felsida först. Klicka bara på knappen &quot;Försök igen&quot; för att slutligen läsa in appen på din enhet. Observera att om du stänger programmet Expo Go eller kopplar från din enhet från WiFi-nätverket kommer programmet inte längre att svara.

![Försök igen om det inte fungerar](./images/delivery-app-ios-retry.png)

## Navigera i programmet

I appen kan du välja ditt team i listrutan. Detta läses dynamiskt in i innehållet som du skapade i AEM. Om du inte är nöjd med innehållet kan du alltid uppdatera det i det innehållsfragment som vi skapade tidigare och sedan publicera innehållet igen. Du ser sedan ändringarna som återspeglas i appen.

![App innan du väljer team](./images/delivery-app-initial.png)
![App efter val av team](./images/delivery-app-loaded.png)

Nästa steg: [Fas 3 - Leverans: Skapa sida i AEM](./page-in-aem.md)

[Gå tillbaka till fas 2 - produktion: Skapa mobilappsinnehåll](../production/app.md)

[Gå tillbaka till Alla moduler](../../overview.md)
