---
title: Push-meddelanden med Platstjänst
description: I det här avsnittet finns information om hur du använder platstjänsten med push-meddelanden i Campaign Standarden.
exl-id: 4b50f552-deb8-49cd-9221-fbbf33aaa5f9
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 4%

---

# Push-meddelanden med platstjänst {#push-notifications}

I det här avsnittet får du lära dig hur du använder historisk geolokaliseringsinformation för att rikta push-meddelanden som levereras via Adobe Campaign Standard.

## Förutsättningar

Utför följande uppgifter innan du börjar:

* har en mobilapp konfigurerad med Adobe Experience Platform Mobile SDK, som [Adobe Campaign Standard-tillägg](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard).

* Integrera [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) i appen.
* Lägg till [Adobe Campaign Standard Extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) till din mobilappskonfiguration.

* [Skapa en POI](/help/poi-mgmt-ui/create-a-poi-ui.md) i POI-hanteringsgränssnittet för platstjänster.

* Aktivera och installera [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).


## Skapa dataelement i Experience Platform Launch

Efter verifiering av att Platstillägget och en regionövervakningslösning ([Dokumentation för CoreLocation](https://developer.apple.com/documentation/corelocation/monitoring_the_user_s_proximity_to_geographic_regions) för iOS, eller [Android-platsdokumentation](https://developer.android.com/training/location/geofencing)) fungerar korrekt i ditt program och du måste skapa dataelement i Experience Platform Launch. Med dataelement kan du läsa den information som tillhandahölls av tilläggen som kom via händelsehubben Mobile SDK och agera som ett alias för att hämta data från klientprogrammet. Om du vill hämta data från platstilläggen och skicka informationen om platstjänster till Campaign måste du skapa några dataelement.

Så här skapar du ett dataelement:

1. Klicka på **[!UICONTROL Data Elements]** och klicka **[!UICONTROL Add Data Element]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places Service]**.
1. I listrutan **[!UICONTROL Data Element Type]** väljer du **[!UICONTROL Name]**.
1. I den högra rutan kan du välja **[!UICONTROL Current POI]** som hämtar namnet på den POI där användaren befinner sig.

   **[!UICONTROL Last Entered]** hämtar namnet på den POI som användaren senast angav, och **[!UICONTROL Last Exited]** innehåller namnet på det POI som användaren senast lämnade. I det här exemplet har vi valt **[!UICONTROL Last Entered]** och skrev ett namn för dataelementet, till exempel **[!UICONTROL Last Entered POI Name]** och klickat **[!UICONTROL Save]**.

   ![&quot;Push messaging in Campaign Standard&quot;](/help/assets/ACS_Push1.png)

1. Upprepa stegen 1-4 ovan och skapa dataelement för *Senaste angivna POI-latitud*, *Senaste angivna POI-longitud* och *Senaste angivna POI-radie*.

Förutom dataelementen för Platstjänst måste du skapa dataelement för Mobile Core för *Program-ID* och *Experience Cloud ID*.

## Skapa en regel för att skicka platsdata till Adobe Campaign Standard

Med regler i Experience Platform Launch kan du skapa komplexa arbetsflöden med flera lösningar som baseras på händelseutlösare. Med hjälp av regler kan du skapa nya regler eller ändra befintliga regler och distribuera uppdateringarna dynamiskt till dina mobilprogram. I följande exempel aktiveras regeln när en användare anger en geofenad POI. När regeln har utlösts skickas en uppdatering till Campaign Standarden för att spela in en post till en viss POI för en viss användare baserat på Experience Cloud-ID:t.

1. I din mobila Experience Platform Launch-egendom på **[!UICONTROL Rules]** flik, klicka **[!UICONTROL Add Rule]**.
1. Under **[!UICONTROL Events]** avsnitt, klicka **[!UICONTROL +]** och markera **[!UICONTROL Places Service]** som tillägget.
1. Välj **[!UICONTROL Enter POI]** för **[!UICONTROL Event Type]**.
1. Namnge regeln, till exempel **Användaren angav POI**.
1. Klicka på **[!UICONTROL Keep Changes]**.
1. Lämna **[!UICONTROL Conditions]** -avsnittet är tomt.

   I det här avsnittet kan du filtrera eller placera begränsningar för när den här regeln ska utlösas.

1. Under **[!UICONTROL Actions]** avsnitt, klicka **[!UICONTROL +]**.
1. I **[!UICONTROL Extension]** nedrullningsbar lista, välja **[!UICONTROL Mobile Core]** och i **[!UICONTROL Action Type]** nedrullningsbar lista, välja **[!UICONTROL Send Postback]**.
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
>* Kom ihåg att publicera de senaste ändringarna av appen för att kontrollera att regeln och alla dataelement är distribuerade som en del av konfigurationen. När du har publicerat ska du starta mobilprogrammet igen för att få de senaste konfigurationsuppdateringarna.


## Använd platsdata för att rikta Campaign-meddelanden

Nu när vi har platsdata i Campaign kan vi använda POI som målgruppsverktyg.

1. Klicka på **[!UICONTROL Create Push Notification]**.
1. Välj **[!UICONTROL Send push to Campaign profiles]**.
1. Klicka **[!UICONTROL Next]** och ange allmän information.
1. På skärmen Audience klickar du på **[!UICONTROL Count]** för att bestämma hur många användare push-meddelandet ska skickas.

   >[!TIP]
   >
   >I det här exemplet är antalet 3 eftersom det finns tre installerade enheter som programmet testas på.

1. Expandera **[!UICONTROL Profile]** och dra **[!UICONTROL POI location]** filtrera till huvudområdet.
1. I POI-filterfönstret anger du det exakta namnet på den POI som du vill ha som mål.

   >[!TIP]
   >
   >Du kan göra ytterligare val för att bestämma tidsperioden sedan användarens tidigare besök i det här POI:t.

   ![&quot;Push messaging 2 in ACS&quot;](/help/assets/ACS_push2.png)

1. Klicka på **[!UICONTROL Confirm]**.
1. Kör räkningen igen längst upp för att se hur er målgruppsstorlek ändras.

   Om du inte ser din räkningsuppdatering kan du ha angett ett POI-namn som inga enheter har aktiverat en post för. Att ha webbkroken Slack blir värdefullt i den här situationen, eftersom du kan se en lista över POI-poster från olika testenheter.

1. Du kan dra ut ytterligare POI-platsfilter för att inkludera flera POI i meddelandet.
1. Klicka på **[!UICONTROL Next]** för att skapa push-meddelandet för leverans.

   ![&quot;Push messaging 3 in ACS&quot;](/help/assets/ACS_push3.png)

Med Platstjänst tillsammans med Adobe Campaign Standard får du ett kraftfullt verktyg för att segmentera och rikta meddelanden till användare baserat på geofence-poster och utgångar. Denna integrering hjälper er att bygga mer personaliserade och sammanhangsbaserade användningsfall.
