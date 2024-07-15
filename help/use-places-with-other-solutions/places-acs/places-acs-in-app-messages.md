---
title: Meddelanden i appen med Platstjänst
description: I det här avsnittet finns information om hur du använder push-meddelanden i Campaign Standard med meddelanden i appen i Campaign Standard.
exl-id: c80727b8-20c9-4ca0-9f2c-20ec646bb7fa
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# Meddelanden i appen med Platstjänst {#in-app-messages-loc-service}

Den här informationen hjälper dig att förstå hur du kan använda platsinformation för att skicka meddelanden i appen eller lokala meddelanden.

## Förhandskrav

Utför följande uppgifter innan du börjar:

* Ha ett mobilprogram konfigurerat med Adobe Experience Platform Mobile SDK, inklusive [Adobe Campaign Standard-tillägget](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard).

* Integrera [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) i din app.
* Lägg till [Adobe Campaign Standard-tillägget](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) i din mobilappskonfiguration.

* [Skapa en POI](/help/poi-mgmt-ui/create-a-poi-ui.md) i POI-hanteringsgränssnittet för platstjänster.

* Installera och konfigurera [platstillägget](/help/places-ext-aep-sdks/places-extension/places-extension.md) och en regionövervakningslösning ([CoreLocation-dokumentation](https://developer.apple.com/documentation/corelocation/monitoring_the_user_s_proximity_to_geographic_regions) för iOS eller [Android platsdokumentation](https://developer.android.com/training/location/geofencing)) i ditt mobilprogram.

## Skicka ett meddelande i appen baserat på en geo-fence-post eller ett avslut

1. Klicka på **[!UICONTROL Create In-App message]** i din Adobe Campaign Standard-instans.
1. Välj **[!UICONTROL Target all users of a Mobile application]** som meddelandetyp.
1. Klicka på **[!UICONTROL Next]** och skriv den allmänna informationen.
1. I den vänstra rutan kontrollerar du att du kan använda olika utlösare som är relaterade till Platstjänster.

   * Du kan välja att visa meddelandet i appen om användaren har angivit en POI-geostängsel.
   * Du kan också använda metadata som är definierade i användargränssnittet för Platstjänster för att filtrera publiken.

   I exemplet nedan kan du utlösa ett meddelande i appen som bara visas för användare som anger en av semesterresurserna som deltar i ett gratisprogram och du vill skicka en kupong till dessa användare när de kommer.

   ![&quot;Meddelandeplatser i appen&quot;](/help/assets/last-entered-vacation.png)

1. Klicka på **[!UICONTROL Next]** för att slutföra skapandet av meddelandet i appen för leverans.

   ![&quot;skapa en händelse&quot;](/help/assets/prepare-ACS.png)

   Om du vill testa leveransen av meddelanden i appen startar du programmet i Xcode- eller Android-studion och använder platssimulatorn för att välja en POI som uppfyller meddelandevillkoren.

   ![&quot;dryckeskupong&quot;](/help/assets/drink-coupon-on-app.png)

Med hjälp av Platstjänster med Adobe Campaign Standard får du ett kraftfullt verktyg för att segmentera och rikta meddelanden till användare baserat på geofence-poster och utgångar. Tack vare den här integreringen kan ni skapa mer personaliserade och sammanhangsbaserade användningsfall.

<!--I changed this embed to a link to pass validation. We should not link to youtube videos, so please upload this to MCP-->

[Platstjänst för Adobe Experience Platform med Campaign Messaging](https://www.youtube.com/watch?v=ikiTTQw9c-o)
