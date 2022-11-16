---
title: Livscykeldata
description: Lär dig hur du samlar in livscykeldata i en mobilapp.
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Livscykeldata

Lär dig hur du samlar in livscykeldata i en mobilapp.

Med Adobe Experience Platform Mobile SDK Lifecycle kan du samla in livscykeldata från din mobilapp. Adobe Experience Platform Edge Network-tillägget skickar dessa livscykeldata till Platform Edge Network, där de sedan vidarebefordras till andra program och tjänster enligt din datastream-konfiguration. Läs mer om [Livscykeltillägg](https://aep-sdks.gitbook.io/docs/foundation-extensions/lifecycle-for-edge-network) i produktdokumentationen.


## Förutsättningar

* Programmet har skapats och körts med SDK:er installerade och konfigurerade.
* Assurance SDK importerades.

   ```swift
   import AEPAssurance
   ```

* Registrerat Assurance-tillägget enligt beskrivningen i [föregående lektion](install-sdks.md).

## Utbildningsmål

I den här lektionen kommer du att:

* Lägg till fältgrupp för livscykel i schemat.
* Få korrekta livscykelvärden genom att starta/pausa korrekt när appen flyttas mellan förgrunden och bakgrunden.
* Skicka data från appen till Platform Edge Network.
* Validera i Assurance.

## Lägg till fältgrupp för livscykel till schema

Fältgruppen Consumer Experience Event som du lade till i [föregående lektion](create-schema.md) innehåller redan livscykelfälten, så du kan hoppa över det här steget. Om du inte använder fältgruppen Consumer Experience Event i din egen app kan du lägga till livscykelfälten genom att göra följande:

1. Navigera till schemagränssnitt enligt beskrivningen i [föregående lektion](create-schema.md).
1. Öppna schemat&quot;Luma App&quot; och välj **[!UICONTROL Lägg till]**.
   ![välj lägg till](assets/mobile-lifecycle-add.png)
1. Skriv&quot;lifecycle&quot; i sökfältet.
1. Markera kryssrutan bredvid **[!UICONTROL Information om AEP Mobile Lifecycle]**.
1. Välj **[!UICONTROL Lägg till fältgrupper]**.
   ![lägg till fältgrupp](assets/mobile-lifecycle-lifecycle-field-group.png)
1. Välj **[!UICONTROL Spara]**.
   ![spara](assets/mobile-lifecycle-lifecycle-save.png)


## Implementeringsändringar

Nu kan du uppdatera `AppDelegate.swift` för att registrera livscykelhändelser:

1. Om appen återupptas från ett bakgrundsläge när den startas kan iOS ringa upp `applicationWillEnterForeground:` delegeringsmetod. Lägg till `lifecycleStart:`

   ```swift
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. När appen placeras i bakgrunden pausar du datainsamlingen för livscykeln från appens `applicationDidEnterBackground:` delegeringsmetod.

   ```swift
   MobileCore.lifecyclePause()
   ```

>[!NOTE]
>
>iOS 13 och senare finns i [dokumentation](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle#register-lifecycle-with-mobile-core-and-add-appropriate-start-pause-calls) för något annorlunda kod.

## Validera med Assurance

1. Granska [installationsanvisningar](assurance.md) och koppla simulatorn eller enheten till Assurance.
1. Starta programmet.
1. Skicka appen till bakgrunden. Sök efter `LifecyclePause`.
1. Ta appen till förgrunden. Sök efter `LifecycleResume`.
   ![validera livscykel](assets/mobile-lifecycle-lifecycle-assurance.png)


## Vidarebefordra data till plattforms-Edge Network

I den föregående övningen skickas för- och bakgrundshändelserna till Mobile SDK. Om du vill skicka dessa händelser till Platform Edge Network följer du de steg som anges [här](https://aep-sdks.gitbook.io/docs/foundation-extensions/lifecycle-for-edge-network#configure-a-rule-to-forward-lifecycle-metrics-to-platform). När händelserna har skickats till Platform Edge Network vidarebefordras de till andra program och tjänster enligt din datastream-konfiguration.

När du har lagt till regeln för att skicka livscykelhändelser till Platform Edge Network bör du se `Application Close (Background)` och `Application Launch (Foreground)` händelser som innehåller XDM-data i Assurance.

![validera livscykel som skickats till Platform Edge](assets/mobile-lifecycle-edge-assurance.png)



Nästa: **[Spåra händelser](events.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)