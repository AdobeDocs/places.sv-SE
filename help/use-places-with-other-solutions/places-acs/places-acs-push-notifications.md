---
title: Push-meddelanden med Platstjänst
description: I det här avsnittet finns information om hur du använder platstjänsten med push-meddelanden i Campaign Standarden.
exl-id: 4b50f552-deb8-49cd-9221-fbbf33aaa5f9
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 2%

---

# Push-meddelanden med platstjänst {#push-notifications}

I det här avsnittet får du lära dig hur du använder historisk geolokaliseringsinformation för att rikta push-meddelanden som levereras via Adobe Campaign Standard.

## Förhandskrav

Utför följande uppgifter innan du börjar:

* Ha ett mobilprogram konfigurerat med Adobe Experience Platform Mobile SDK, inklusive [Adobe Campaign Standard-tillägget](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard).

* Integrera [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) i din app.
* Lägg till [Adobe Campaign Standard-tillägget](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) i din mobilappskonfiguration.

* [Skapa en POI](/help/poi-mgmt-ui/create-a-poi-ui.md) i POI-hanteringsgränssnittet för platstjänster.

* Aktivera och installera tillägget [Platser](/help/places-ext-aep-sdks/places-extension/places-extension.md).


## Skapa dataelement i Experience Platform Launch

När du har verifierat att Platstillägget och en regionövervakningslösning ([CoreLocation-dokumentation](https://developer.apple.com/documentation/corelocation/monitoring_the_user_s_proximity_to_geographic_regions) för iOS, eller [Android platsdokumentation](https://developer.android.com/training/location/geofencing)) fungerar korrekt i ditt program, måste du skapa dataelement i Experience Platform Launch. Med dataelement kan du läsa den information som tillhandahölls av tilläggen som kom via händelsehubben Mobile SDK och agera som ett alias för att hämta data från klientprogrammet. Om du vill hämta data från platstilläggen och skicka informationen om platstjänster till Campaign måste du skapa några dataelement.

Så här skapar du ett dataelement:

1. Klicka på fliken **[!UICONTROL Data Elements]** i din mobila Experience Platform Launch-egenskap och klicka på **[!UICONTROL Add Data Element]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places Service]**.
1. I listrutan **[!UICONTROL Data Element Type]** väljer du **[!UICONTROL Name]**.
1. I den högra rutan kan du välja **[!UICONTROL Current POI]** som hämtar namnet på det POI som användaren finns i.

   **[!UICONTROL Last Entered]** hämtar namnet på den POI som användaren senast angav och **[!UICONTROL Last Exited]** anger namnet på den POI som användaren senast lämnade. I det här exemplet har vi markerat **[!UICONTROL Last Entered]** och skrivit ett namn för dataelementet, till exempel **[!UICONTROL Last Entered POI Name]** och klickat **[!UICONTROL Save]**.

   ![&quot;Push messaging in Campaign Standard&quot;](/help/assets/ACS_Push1.png)

1. Upprepa stegen 1-4 ovan och skapa dataelement för *senaste angivna POI-latitud*, *Senaste angivna POI-longitud* och *Senaste angivna POI-radie*.

Förutom dataelementen för Platstjänst måste du skapa dataelement för Mobile Core för *program-ID* och *Experience Cloud-ID*.

## Skapa en regel för att skicka platsdata till Adobe Campaign Standard

Med regler i Experience Platform Launch kan du skapa komplexa arbetsflöden med flera lösningar som baseras på händelseutlösare. Med hjälp av regler kan du skapa nya regler eller ändra befintliga regler och distribuera uppdateringarna dynamiskt till dina mobilprogram. I följande exempel aktiveras regeln när en användare anger en geofenad POI. När regeln har utlösts skickas en uppdatering till Campaign Standarden för att spela in en post till en viss POI för en viss användare baserat på Experience Cloud-ID:t.

1. Klicka på **[!UICONTROL Add Rule]** på fliken **[!UICONTROL Rules]** i din mobila Experience Platform Launch-egenskap.
1. Klicka på **[!UICONTROL +]** under avsnittet **[!UICONTROL Events]** och välj **[!UICONTROL Places Service]** som tillägg.
1. För **[!UICONTROL Event Type]** väljer du **[!UICONTROL Enter POI]**.
1. Namnge regeln, till exempel **Användaren angav POI**.
1. Klicka på **[!UICONTROL Keep Changes]**.
1. Lämna avsnittet **[!UICONTROL Conditions]** tomt.

   I det här avsnittet kan du filtrera eller placera begränsningar för när den här regeln ska utlösas.

1. Klicka på **[!UICONTROL +]** under avsnittet **[!UICONTROL Actions]**.
1. Välj **[!UICONTROL Mobile Core]** i listrutan **[!UICONTROL Extension]** och välj **[!UICONTROL Send Postback]** i listrutan **[!UICONTROL Action Type]**.
1. I **[!UICONTROL URL]** måste du skapa slutpunkten för Campaign Standardens platser.

   URL:en ska se ut ungefär som `https:///rest/head/mobileAppV5//locations/`.
Se till att du använder rätt dataelement som du skapade tidigare för Campaign-servern och pKey.

1. Klicka på rutan för att lägga till en inläggstext och skicka följande:

   ```
   {
    "locationData": {
    "distances": "{%%Last Entered POI Radius%%}",
    "poiLabel": "{%%Last Entered POI Name%%}",
    "latitude": "{%%Last Entered POI Lat%%}",
    "longitude": "{%%Last Entered POI Long%%}",
    "appId": "{%%AppID%%}",
    "marketingCloudId": “{%%ecid%%}”
    }
   }
   ```

1. Se till att du använder dataelement som du skapade i föregående avsnitt.
1. Skriv **[!UICONTROL application/json]** i **[!UICONTROL Content Type]**.
1. Klicka på **[!UICONTROL Keep Changes]**.

>[!IMPORTANT]
>
>* Det kan vara praktiskt att ha en webbok i Slack som är konfigurerad som en extra åtgärd för att validera att poster aktiveras och att rätt data samlas in.
>* Kom ihåg att publicera de senaste ändringarna av appen för att säkerställa att regeln och alla dataelement är distribuerade som en del av konfigurationen. När du har publicerat ska du starta mobilprogrammet igen för att få de senaste konfigurationsuppdateringarna.

## Använd platsdata för att rikta Campaign-meddelanden

Nu när vi har platsdata i Campaign kan vi använda POI som målgruppsverktyg.

1. Klicka på **[!UICONTROL Create Push Notification]** i din Adobe Campaign Standard-instans.
1. Välj **[!UICONTROL Send push to Campaign profiles]** för typen av push-meddelanden.
1. Klicka på **[!UICONTROL Next]** och skriv den allmänna informationen.
1. På målgruppsskärmen klickar du på **[!UICONTROL Count]** för att avgöra hur många användare push-meddelandet ska skickas.

   >[!TIP]
   >
   >I det här exemplet är antalet 3 eftersom det finns tre installerade enheter som programmet testas på.

1. Expandera fliken **[!UICONTROL Profile]** i den vänstra rutan och dra filtret **[!UICONTROL POI location]** till huvudområdet.
1. I POI-filterfönstret anger du det exakta namnet på den POI som du vill ha som mål.

   >[!TIP]
   >
   >Du kan göra ytterligare val för att bestämma tidsperioden sedan användarens tidigare besök i denna POI.

   ![&quot;Push messaging 2 in ACS&quot;](/help/assets/ACS_push2.png)

1. Klicka på **[!UICONTROL Confirm]**.
1. Kör räkningen igen längst upp för att se hur er målgruppsstorlek ändras.

   Om du inte ser din räkningsuppdatering kan du ha angett ett POI-namn som inga enheter har aktiverat en post för. Att ha webbkroken Slack blir värdefullt i den här situationen, eftersom du kan se en lista över POI-poster från olika testenheter.

1. Du kan dra ut ytterligare POI-platsfilter för att inkludera flera POI i meddelandet.
1. Klicka på **[!UICONTROL Next]** för att skapa push-meddelandet för leverans.

   ![&quot;Skicka meddelande 3 i ACS&quot;](/help/assets/ACS_push3.png)

Med Platstjänst tillsammans med Adobe Campaign Standard får du ett kraftfullt verktyg för att segmentera och rikta meddelanden till användare baserat på geofence-poster och utgångar. Denna integrering hjälper er att bygga mer personaliserade och sammanhangsbaserade användningsfall.
