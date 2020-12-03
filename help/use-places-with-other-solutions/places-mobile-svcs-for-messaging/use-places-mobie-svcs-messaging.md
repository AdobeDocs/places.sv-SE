---
title: Använda Platstjänst med Mobiltjänster för meddelanden
description: I det här avsnittet visas hur du använder Platstjänst med Mobiltjänster för meddelanden.
translation-type: tm+mt
source-git-commit: 5a21e734c0ef56c815389a9f08b445bedaae557a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 1%

---


# Adobe Mobile Services {#places-mobile-services}

Innan du kan använda mobiltjänsttillägget för meddelanden bör du kontrollera följande krav:

* Intressepunkter har skapats i Platstjänst. Mer information finns i [Skapa en POI](/help/poi-mgmt-ui/create-a-poi-ui.md).

   >[!IMPORTANT]
   >
   >Platstjänsten innehåller en ny och förbättrad POI-databas för din organisation som finns utanför det tidigare användargränssnittet för mobila tjänster. POI som finns på sidan Hantera platser i *Mobile Service* fungerar bara för version 4 av SDK.

* Här är *sidan Hantera platser* för POI-hantering i det äldre användargränssnittet för mobila tjänster för äldre versioner av SDK:

   ![Äldre gränssnitt](/help/assets/legacy-location-v4-ui.png)

* Här är användargränssnittet för platstjänster:

   ![Placerar tjänstens gränssnitt för POI-hantering](/help/assets/places-ui.png)

* ACP SDK är korrekt konfigurerad med Platstjänst och/eller Places Monitor-tillägg.

   Det innebär att data är tillgängliga som händelser och/eller villkor i regelmotorn Experience Platform Launch för din mobilapp. Mer information finns i [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md) eller [Platsmonitortillägg](/help/places-ext-aep-sdks/places-monitor-extension/using-places-monitor-extension.md).

* Bekanta dig med hur du skapar och publicerar Experience Platform Launch-regler för ACP SDK i din mobilapp.

   Mer information finns i [Regelmotorn](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine).

* dataelement från Experience Platform Launch skapas från platstillägg som ska användas i regelmotorn.

   Mer information finns i [Dataelement](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#data-elements).

## Rapportering

Innan du kan använda rapportering måste du uppfylla följande krav:

* Platstjänstdata har skickats till Adobe Analytics Report Suite.

   Mer information finns i [Använda platstjänst med Adobe Analytics](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md).

* Bli bekant med rapporter om mobila tjänster.

   Mer information finns i [Rapporter](https://docs.adobe.com/content/help/en/mobile-services/using/reports-ug/usage.html).

## Visualisering av rapportering

Du kan köra rapporter om mobila tjänster med hjälp av platsdata som skickas till Adobe Analytics. I följande exempel skickas händelser när användare har poster i en POI. I den här rapporten har ett filter för POI-händelsen lagts till i användarrapporten som är färdig:

![Rapportvisualisering](/help/assets/report-visualize.png)

Ytterligare flexibilitet när det gäller att visualisera platsdata finns i Adobe Analytics gränssnitt.

