---
title: Datahygien i Adobe Experience Platform
description: Läs om alternativen för datahygien i Adobe Experience Platform
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
feature: Data Hygiene
role: Developer
level: Intermediate
source-git-commit: 9c15708f7300672caa963c0635179dd2855e5fed
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Självstudiekurser om datthygien

Läs mer om datahygien i Adobe Experience Platform, som bland annat omfattar:

* Aktivering av principer för minimering av data vid dataöverföring
* Justering av data som redan finns i systemet
* Borttagning av data från systemet

<!--
Data hygiene:

* Enables citizen data stewards working in Privacy or IT teams to manage customer data lifecycle.
* Provides foundational workflows for setting expiration of datasets based on corporate policies, partner
arrangements, customer commitments or regulatory needs.
* Provides foundational workflows for managing targeted treatment of identities and data belonging to consumers in a
holistic fashion.
* Provides monitoring, work order management and notifications of tasks.
* Provides the ability to log the lifecyle management tasks for auditing purposes.
-->

## Dataminimering vid intag

Funktionen för förinställningar av data hjälper dig att endast importera de fält du behöver från en datakälla.

<!-- CARDS
{cta=Watch}
* data-prep-for-data-hygiene.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Data prep for data hygiene">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="data-prep-for-data-hygiene.md" title="Dataförberedelse för datahygien" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429485/?format=jpeg&nocache=1740251397387" alt="Dataförberedelse för datahygien"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="data-prep-for-data-hygiene.md" target="_blank" rel="referrer" title="Dataförberedelse för datahygien">Dataförberedelse för datahygien</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du stöder datamängdsprinciper med dataförberedelsefunktionen i Experience Platform. Lär dig hur du bara importerar de fält som du behöver och hash-kodar data under importen.</p>
                </div>
                <a href="data-prep-for-data-hygiene.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Borttagning av data i systemet

Det finns många funktioner som kan hjälpa dig att ta bort data från systemet. Du kan ta bort hela datauppsättningar på begäran eller enligt ett schema, förfalla poster och profiler med inställningar för&quot;time-to-live&quot;, ta bort enskilda profiler och efterleva sekretesskrav.
<!-- CARDS
{cta=Watch}
* delete-datasets-and-batches.md
* ../data-lifecycle/expire-datasets.md
* pseudonymous-profile-and-event-expiration.md
* ../profiles/delete-profiles.md{description=Learn how to delete data from the Profile Store using the Real-Time Customer Profile API. By using the Profile API, you can remove data from the profile store without affecting the data lake or identity graph.}
* ../privacy/introduction-to-privacy-services.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete datasets and batches">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="delete-datasets-and-batches.md" title="Ta bort datauppsättningar och grupper" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429790/?format=jpeg&nocache=1740251397681" alt="Ta bort datauppsättningar och grupper"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="delete-datasets-and-batches.md" target="_blank" rel="referrer" title="Ta bort datauppsättningar och grupper">Ta bort datauppsättningar och grupper</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du tar bort datauppsättningar och grupper i Adobe Experience Platform.</p>
                </div>
                <a href="delete-datasets-and-batches.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Schedule dataset deletes">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../data-lifecycle/expire-datasets.md" title="Schemalägg borttagning av datauppsättning" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/345065?format=jpeg&nocache=1740251397716" alt="Schemalägg borttagning av datauppsättning"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../data-lifecycle/expire-datasets.md" target="_blank" rel="referrer" title="Schemalägg borttagning av datauppsättning">Schemalägg borttagning av datauppsättning</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du tar bort datauppsättningar med hjälp av funktionen Adobe Experience Platform Data Hygiene.</p>
                </div>
                <a href="../data-lifecycle/expire-datasets.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Pseudonymous profile and Experience Event expirations">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="pseudonymous-profile-and-event-expiration.md" title="Pseudonym profil och förfallodatum för upplevelsehändelser" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3428361?format=jpeg&nocache=1740251397705" alt="Pseudonym profil och förfallodatum för upplevelsehändelser"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="pseudonymous-profile-and-event-expiration.md" target="_blank" rel="referrer" title="Pseudonym profil och förfallodatum för upplevelsehändelser">Pseudonym profil och förfallodatum för upplevelsehändelse</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du konfigurerar förfalloinställningar för pseudonyma profiler och händelser i Experience Platform och fördelarna.</p>
                </div>
                <a href="pseudonymous-profile-and-event-expiration.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../profiles/delete-profiles.md" title="Ta bort profiler" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429807/?format=jpeg&nocache=1740251397692" alt="Ta bort profiler"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../profiles/delete-profiles.md" target="_blank" rel="referrer" title="Ta bort profiler">Ta bort profiler</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du tar bort data från profilarkivet med hjälp av Real-Time Customer Profile API. Genom att använda profil-API:t kan du ta bort data från profilarkivet utan att det påverkar datasjön eller identitetsdiagram.</p>
                </div>
                <a href="../profiles/delete-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Introduction to Privacy Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../privacy/introduction-to-privacy-services.md" title="Introduktion till Privacy Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/336074?format=jpeg&nocache=1740251397727" alt="Introduktion till Privacy Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../privacy/introduction-to-privacy-services.md" target="_blank" rel="referrer" title="Introduktion till Privacy Service">Introduktion till Privacy Service</a>
                    </p>
                    <p class="is-size-6">Läs mer om sekretessbestämmelser och hur de påverkar dataåtgärder. Läs också om hur Privacy Service hanterar dessa utmaningar.</p>
                </div>
                <a href="../privacy/introduction-to-privacy-services.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->





## Justering av data i systemet

<!-- CARDS
{cta=Watch}
* ../profiles/update-a-specific-attribute-with-upsert.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Update specific profile attributes using `upsert`">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../profiles/update-a-specific-attribute-with-upsert.md" title="Uppdatera specifika profilattribut med &quot;upsert&quot;" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3416133/?format=jpeg&nocache=1740251398874" alt="Uppdatera specifika profilattribut med &quot;upsert&quot;"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../profiles/update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" title="Uppdatera specifika profilattribut med &quot;upsert&quot;">Uppdatera specifika profilattribut med "upsert"</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du uppdaterar ett specifikt attribut för en profil med funktionen "upsert" i Adobe Experience Platform.</p>
                </div>
                <a href="../profiles/update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
