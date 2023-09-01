---
title: Livscykeldata
description: Lär dig hur du samlar in livscykeldata i en mobilapp.
hide: true
source-git-commit: 4101425bd97e271fa6cc15157a7be435c034e764
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---

# Livscykeldata

Lär dig hur du samlar in livscykeldata i en mobilapp.

Med Adobe Experience Platform Mobile SDK Lifecycle kan du samla in livscykeldata från din mobilapp. Adobe Experience Platform Edge Network-tillägget skickar dessa livscykeldata till Platform Edge Network, där de sedan vidarebefordras till andra program och tjänster enligt din datastream-konfiguration. Läs mer om [Livscykeltillägg](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) i produktdokumentationen.


## Förutsättningar

* App med SDK:er har installerats och konfigurerats.
* Registrerat Assurance-tillägget enligt beskrivningen i [föregående lektion](install-sdks.md).

## Utbildningsmål

I den här lektionen kommer du att:

<!--
* Add lifecycle field group to the schema.
* -->
* Få korrekta livscykelvärden genom att starta/pausa korrekt när appen flyttas mellan förgrunden och bakgrunden.
* Skicka data från appen till Platform Edge Network.
* Validera i Assurance.

<!--
## Add lifecycle field group to schema

The Consumer Experience Event field group you added in the [previous lesson](create-schema.md) already contains the lifecycle fields, so you can skip this step. If you don't use Consumer Experience Event field group in your own app, you can add the lifecycle fields by doing the following:

1. Navigate to the schema interface as described in the [previous lesson](create-schema.md).
1. Open the **Luma Mobile App Event Schema** schema and select **[!UICONTROL Add]** next to Field groups.
    ![select add](assets/lifecycle-add.png)
1. In the search bar, enter "lifecycle".
1. Select the checkbox next to **[!UICONTROL AEP Mobile Lifecycle Details]**.
1. Select **[!UICONTROL Add field groups]**.
    ![add field group](assets/lifecycle-lifecycle-field-group.png)
1. Select **[!UICONTROL Save]**.
    ![save](assets/lifecycle-lifecycle-save.png)
-->

## Implementeringsändringar

Nu kan du uppdatera projektet för att registrera livscykelhändelserna.

1. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL SceneDelegate]** i Xcode Project-navigatorn.

1. Om appen återupptas från ett bakgrundsläge när den startas kan iOS ringa `sceneWillEnterForeground:` delegeringsmetod och här vill du aktivera en start-händelse för livscykel. Lägg till koden i `func sceneWillEnterForeground(_ scene: UIScene)`:

   ```swift
   // When in foreground start lifecycle data collection
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. När appen placeras i bakgrunden vill du pausa datainsamlingen i livscykeln från appens `sceneDidEnterBackground:` delegeringsmetod. Lägg till koden i  `func sceneDidEnterBackground(_ scene: UIScene)`:

   ```swift
   // When in background pause lifecycle data collection
   MobileCore.lifecyclePause()
   }
   ```

## Validera med Assurance

1. Granska [installationsanvisningar](assurance.md) och koppla simulatorn eller enheten till Assurance.
1. Starta programmet.
1. Skicka appen till bakgrunden. Sök efter **[!UICONTROL LifecyclePause]** händelser i försäkringsgränssnittet.
1. Ta appen till förgrunden. Sök efter **[!UICONTROL LivscykelÅteruppta]** händelser i försäkringsgränssnittet.
   ![validera livscykel](assets/lifecycle-lifecycle-assurance.png)


## Vidarebefordra data till plattforms-Edge Network

I föregående övning skickas för- och bakgrundshändelserna till Adobe Experience Platform Mobile SDK. Så här vidarebefordrar du dessa händelser till Platform Edge Network:

1. Välj **[!UICONTROL Regler]** i användargränssnittet för datainsamling.
   ![Skapa regel](assets/rule-create.png)
1. Välj **[!UICONTROL Inledande bygge]** som det bibliotek som ska användas.
1. Välj **[!UICONTROL Skapa ny regel]**.
   ![Skapa ny regel](assets/rules-create-new.png)
1. I **[!UICONTROL Skapa regel]** skärm, ange `Application Status` for **[!UICONTROL Namn]**.
1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Lägg till]** nedan **[!UICONTROL HÄNDELSER]**.
   ![Dialogrutan Skapa regel](assets/rule-create-name.png)
1. I **[!UICONTROL Händelsekonfiguration]** steg:
   1. Välj **[!UICONTROL Mobile Core]** som **[!UICONTROL Tillägg]**.
   1. Välj **[!UICONTROL Förgrund]** som **[!UICONTROL Händelsetyp]**.
   1. Välj **[!UICONTROL Behåll ändringar]**.
      ![Regelhändelsekonfiguration](assets/rule-event-configuration.png)
1. Tillbaka i **[!UICONTROL Skapa regel]** skärm, välja ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Lägg till]** nästa **[!UICONTROL Mobile Core - förgrund]**.
   ![Konfiguration av nästa händelse](assets/rule-event-configuration-next.png)
1. I **[!UICONTROL Händelsekonfiguration]** steg:
   1. Välj **[!UICONTROL Mobile Core]** som **[!UICONTROL Tillägg]**.
   1. Välj **[!UICONTROL Bakgrund]** som **[!UICONTROL Händelsetyp]**.
   1. Välj **[!UICONTROL Behåll ändringar]**.
      ![Regelhändelsekonfiguration](assets/rule-event-configuration-background.png)
      ![Lägg till åtgärd i regel](assets/rule-action-button.png)
1. I **[!UICONTROL Åtgärdskonfiguration]** steg:
   1. Välj **[!UICONTROL Adobe Experience Edge Network]** som **[!UICONTROL Tillägg]**.
   1. Välj **[!UICONTROL Vidarebefordra händelse till Edge Network]** som **[!UICONTROL Åtgärdstyp]**.
   1. Välj **[!UICONTROL Behåll ändringar]**.
      ![Regelåtgärdskonfiguration](assets/rule-action-configuration.png)
1. Välj **[!UICONTROL Spara i bibliotek]**.
   ![Regel - spara i bibliotek](assets/rule-save-to-library.png)
1. Välj **[!UICONTROL Bygge]** för att återskapa biblioteket.
   ![Regel - bygge](assets/rule-build.png)

När du har skapat egenskapen skickas händelserna till Platform Edge Network och händelserna vidarebefordras till andra program och tjänster enligt din datastream-konfiguration.

Du borde se **[!UICONTROL Stäng program (bakgrund)]** och **[!UICONTROL Programstart (förgrund)]** händelser som innehåller XDM-data i Assurance.

![validera livscykel som skickats till Platform Edge](assets/lifecycle-edge-assurance.png)

>[!SUCCESS]
>
>Du har nu konfigurerat din app så att den skickar programtillståndshändelser (förgrund, bakgrund) till Adobe Experience Platform Edge Network och alla tjänster som du har definierat i din datastam.<br>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Spåra händelser](events.md)**
