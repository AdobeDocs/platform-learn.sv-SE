---
title: Förstå kundprofil i realtid
description: I den här videon förklaras hur Adobe Experience Platform sammanställer och uppdaterar kundprofiler i realtid och hur du kan komma åt och använda dessa profiler.
feature: Profiles
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-2701
thumbnail: 27251.jpg
exl-id: 6ef5b589-f874-4687-bee3-9650c993f383
source-git-commit: 112e092df6d486d8b9103013bec57d820b8ae6d7
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Översikt över kundprofiler i realtid

I den här videon förklaras hur Adobe Experience Platform sammanställer och uppdaterar kundprofiler i realtid och hur du kan komma åt och använda dessa profiler. Mer information finns i [dokumentationen för kundprofilen i realtid](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=sv).

>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on&enablevpops)

## Arkitektur och funktioner

<!-- CARDS
* overview-diagram.md
* create-merge-policies.md
* union-schemas-overview.md
* create-a-computed-attribute-for-sum-of-purchases.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Overview Diagram of Real-Time Customer Profile">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="overview-diagram.md" title="Översikt Diagram över kundprofil i realtid" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3463973?format=jpeg&nocache=1740415066741&captions=swe" alt="Översikt Diagram över kundprofil i realtid"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="overview-diagram.md" target="_blank" rel="referrer" title="Översikt Diagram över kundprofil i realtid">Översiktsdiagram över kundprofil i realtid</a>
                    </p>
                    <p class="is-size-6">I den här videon får du en översikt som visar hur Adobe Experience Platform kundprofil kan användas i realtid.</p>
                </div>
                <a href="overview-diagram.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Create merge policies">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="create-merge-policies.md" title="Skapa sammanfogningsprinciper" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/330433?format=jpeg&nocache=1740415066765" alt="Skapa sammanfogningsprinciper"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="create-merge-policies.md" target="_blank" rel="referrer" title="Skapa sammanfogningsprinciper">Skapa sammanfogningsprinciper</a>
                    </p>
                    <p class="is-size-6">I den här videon visas hur du skapar sammanfogningsprinciper i Adobe Experience Platform. Sammanslagningsprinciper är de regler som Platform använder för att avgöra vilka data som ska användas och prioriteras när datauppsättningar från olika källor kombineras, för att skapa kundprofiler.</p>
                </div>
                <a href="create-merge-policies.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Union schemas overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="union-schemas-overview.md" title="Översikt över unionens scheman" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/329940?format=jpeg&nocache=1740415066755" alt="Översikt över unionens scheman"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="union-schemas-overview.md" target="_blank" rel="referrer" title="Översikt över unionens scheman">Översikt över unionsscheman</a>
                    </p>
                    <p class="is-size-6">Kundprofilen i realtid genomsyrar personalisering i flera kanaler i stor skala genom varje fas av kundresan. Batch- eller direktuppspelningsdata kan aktiveras för kundprofilen i realtid genom att både schemat och motsvarande datauppsättning aktiveras.</p>
                </div>
                <a href="union-schemas-overview.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Create a computed attribute for the sum of purchases">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="create-a-computed-attribute-for-sum-of-purchases.md" title="Skapa ett beräknat attribut för summan av inköp" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3443555?format=jpeg&nocache=1740415066775&captions=swe" alt="Skapa ett beräknat attribut för summan av inköp"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="create-a-computed-attribute-for-sum-of-purchases.md" target="_blank" rel="referrer" title="Skapa ett beräknat attribut för summan av inköp">Skapa ett beräknat attribut för summan av inköp</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du använder beräknade attribut för att summera de inköpsbelopp som en användare har gjort i flera försäljningskanaler.</p>
                </div>
                <a href="create-a-computed-attribute-for-sum-of-purchases.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Inhämta och hantera profildata

<!-- CARDS
* bring-data-into-the-real-time-customer-profile.md
* delete-profiles.md
* update-a-specific-attribute-with-upsert.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Bring Data into Real-Time Customer Profile">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="bring-data-into-the-real-time-customer-profile.md" title="Lägg in data i kundprofilen i realtid" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/27301?format=jpeg&nocache=1740415067018" alt="Lägg in data i kundprofilen i realtid"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="bring-data-into-the-real-time-customer-profile.md" target="_blank" rel="referrer" title="Lägg in data i kundprofilen i realtid">Hämta data till kundprofilen i realtid</a>
                    </p>
                    <p class="is-size-6">Kundprofilen i realtid genomsyrar personalisering i flera kanaler i stor skala genom varje fas av kundresan. Batch- eller direktuppspelningsdata kan aktiveras för kundprofilen i realtid genom att både schemat och motsvarande datauppsättning aktiveras.</p>
                </div>
                <a href="bring-data-into-the-real-time-customer-profile.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="delete-profiles.md" title="Ta bort profiler" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429807/?format=jpeg&nocache=1740415067005" alt="Ta bort profiler"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="delete-profiles.md" target="_blank" rel="referrer" title="Ta bort profiler">Ta bort profiler</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du tar bort data från profilarkivet med hjälp av Real-Time Customer Profile API. Genom att använda profil-API:t kan du ta bort data från profilarkivet utan att det påverkar datasjön eller identitetsdiagram. Detta kan vara praktiskt när du felsöker problem med identitetsdiagram och korrigerar tillfälliga fel i dataimporten som bara påverkar ett fåtal profiler.</p>
                </div>
                <a href="delete-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Update specific profile attributes using `upsert`">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="update-a-specific-attribute-with-upsert.md" title="Uppdatera specifika profilattribut med &quot;upsert&quot;" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3443445/?format=jpeg&nocache=1740415067029&captions=swe" alt="Uppdatera specifika profilattribut med &quot;upsert&quot;"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" title="Uppdatera specifika profilattribut med &quot;upsert&quot;">Uppdatera specifika profilattribut med "upsert"</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du uppdaterar ett specifikt attribut för en profil med funktionen "upsert" i Adobe Experience Platform.</p>
                </div>
                <a href="update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Kontoprofiler

<!-- CARDS
* view-account-profiles.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="View account profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="view-account-profiles.md" title="Visa kontoprofiler" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3446581?format=jpeg&nocache=1740415067214&captions=swe" alt="Visa kontoprofiler"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="view-account-profiles.md" target="_blank" rel="referrer" title="Visa kontoprofiler">Visa kontoprofiler</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du visar kontoprofiler i Real-Time CDP B2B edition.</p>
                </div>
                <a href="view-account-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->