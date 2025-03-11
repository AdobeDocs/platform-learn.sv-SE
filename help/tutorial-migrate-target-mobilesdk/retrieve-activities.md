---
title: Hämta Target-aktiviteter - Migrera Adobe Target-implementeringen i din mobilapp till Adobe Journey Optimizer - Beslutstillägg
description: Lär dig hur du hämtar Adobe Target-aktiviteter när du migrerar från Adobe Target till Adobe Journey Optimizer - Decisioning Mobile-tillägget.
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: d2da62ed2d36f73af1c8053be5af27feea32cb14
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Hämta målaktiviteter

Vid implementering av målmobiler används regionala kryssrutor (som nu kallas omfattningar) för att leverera innehåll från aktiviteter som använder Target formulärbaserade Experience Composer. Du måste uppdatera ditt mobilprogram så att det inkluderar omfattningar i dina nätverksanrop.

Innehållet som returneras av Target, som också kallas&quot;erbjudanden&quot;, består vanligtvis av text eller json som du behöver förbruka i programmet för att kunna återge den slutliga kundupplevelsen. Erbjudanden från Target används ofta för att

* Aktivera funktionsflaggor i programmet
* Spara alternativ text eller bilder

Om du har aktiviteter som måste köras i både Target-tillägg och Decisioning-tilläggsversioner av ditt program måste du testa noga. Om ni behöver olika erbjudanden för olika versioner av appen bör ni överväga att använda målinriktningsalternativen i gränssnittet för att leverera olika erbjudanden till olika versioner.

Se alltid till att ta med felhantering för att visa lämpliga upplevelser under felförhållanden.


## Begär och tillämpa innehåll på begäran

>[!IMPORTANT]
>
>När du har tillämpat innehåll i appen måste `displayed`-API aktiveras för att Target ska veta att besökaren har sett det alternativa innehållet eller standardinnehållet som anges i aktiviteten. Mer information finns på sidan [Spåra konverteringshändelser](track-events.md).


+++ Exempel på Android

>[!BEGINTABS]

>[!TAB Optimera SDK]

```Java
// Mboxes for Target activities
final DecisionScope decisionScope1 = DecisionScope("myTargetMbox1");
final DecisionScope decisionScope2 = new DecisionScope("myTargetMbox2");
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope1);
decisionScopes.add(decisionScope2);
 
// Prefetch the Target mboxes
Optimize.updatePropositions(decisionScopes,
                            new HashMap<String, Object>() {
                                {
                                    put("xdmKey", "xdmValue");
                                }
                            },
                            new HashMap<String, Object>() {
                                {
                                    put("dataKey", "dataValue");
                                }
                            },
                            new AdobeCallbackWithOptimizeError<Map<DecisionScope, OptimizeProposition>>() {
                                @Override
                                public void fail(AEPOptimizeError optimizeError) {
                                    // Log in case of error
                                    Log.d("Target Prefetch error", optimizeError.title);
                                }
 
                                @Override
                                public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                    // Retrieve cached propositions if prefetch succeeds
                                    Optimize.getPropositions(scopes, new AdobeCallbackWithError<Map<DecisionScope, OptimizeProposition>>() {
                                        @Override
                                      public void fail(final AdobeError adobeError) {
                                              // handle error
                                        }
 
                                        @Override
                                        public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                              if (propositionsMap != null && !propositionsMap.isEmpty()) {
                                                // get the propositions for the given decision scopes
                                                if (propositionsMap.contains(decisionScope1)) {
                                                      final OptimizeProposition proposition1 = propsMap.get(decisionScope1)
                                                      // read proposition1 offers and display them
                                                }
                                                if (propositionsMap.contains(decisionScope2)) {
                                                      final OptimizeProposition proposition2 = propsMap.get(decisionScope2)
                                                      // read proposition2 offers and display them
                                                }
                                              }
                                        }
                                      });
                                }
                            });
```

>[!ENDTABS]

+++

+++ Exempel på iOS

>[!BEGINTABS]

>[!TAB Optimera SDK]

```Swift
// Mboxes for Target activities
let decisionScope1 = DecisionScope(name: "myTargetMbox1")
let decisionScope2 = DecisionScope(name: "myTargetMbox2")
 
// Prefetch the Target mboxes
Optimize.updatePropositions(for: [decisionScope1, decisionScope2]
                            withXdm: ["xdmKey": "xdmValue"]
                            andData: ["dataKey": "dataValue"]) { data, error in
            if let error = error as? AEPOptimizeError {
                // handle error
                return
            }
            // Retrieve cached propositions if prefetch succeeds
            Optimize.getPropositions(for: [decisionScope1, decisionScope2]) { propositionsDict, error in
                if let error = error {
                    // handle error
                    return
                }
 
                if let propositionsDict = propositionsDict {
                    // get the propositions for the given decision scopes
 
                    if let proposition1 = propositionsDict[decisionScope1] {
                        // read proposition1 offers and display them
                    }
 
                    if let proposition2 = propositionsDict[decisionScope2] {
                        // read proposition2 offers and display them
                    }
                }
            }
        }
```

>[!ENDTABS]

+++



Lär dig sedan hur du [skickar Target-parametrar med hjälp av beslutstillägget](send-parameters.md).

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
