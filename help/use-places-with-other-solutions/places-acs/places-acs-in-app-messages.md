---
title: Meddelanden i appen med Platstjänst
description: Det här avsnittet innehåller information om hur du använder push-meddelanden i Campaign Standard med meddelanden i appen i Campaign Standard.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b

---


# Meddelanden i appen med Platstjänst {#in-app-messages-loc-service}

Den här informationen hjälper dig att förstå hur du kan använda platsinformation för att skicka meddelanden i appen eller lokala meddelanden.

## Förutsättningar

Utför följande uppgifter innan du börjar:

* Ha en mobilapplikation konfigurerad med Adobe Experience Platform Mobile SDK, inklusive [Adobe Campaign Standard-tillägget](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard).

* Integrera [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) i appen.
* Lägg till [Adobe Campaign Standard Extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) i din mobilappskonfiguration.

* [Skapa en POI](/help/poi-mgmt-ui/create-a-poi-ui.md) i POI-hanteringsgränssnittet för platstjänster.

* Installera och konfigurera [platstillägget](/help/places-ext-aep-sdks/places-extension/places-extension.md) och [platsövervakartilläggen](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md) i ditt mobilprogram.

## Skicka ett meddelande i appen baserat på en geo-fence-post eller ett avslut

1. Klicka på i Adobe Campaign Standard-instansen **[!UICONTROL Create In-App message]**.
1. För meddelandetypen väljer du **[!UICONTROL Target all users of a Mobile application]**.
1. Klicka **[!UICONTROL Next]** och skriv den allmänna informationen.
1. I den vänstra rutan kontrollerar du att du kan använda olika utlösare som är relaterade till Platstjänster.

   * Du kan välja att visa meddelandet i appen om användaren har angivit en POI-geostängsel.
   * Du kan också använda metadata som är definierade i användargränssnittet för Platstjänster för att filtrera publiken.
   I exemplet nedan kan du utlösa ett meddelande i appen som bara visas för användare som anger en av semesterresurserna som deltar i ett gratisprogram och du vill skicka en kupong till dessa användare när de kommer.

   ![&quot;Platsmetadata för meddelanden i appen&quot;](/help/assets/last-entered-vacation.png)

1. Click the **[!UICONTROL Next]** to finish creating the In-app message for delivery.

   ![&quot;create an event&quot;](/help/assets/prepare-ACS.png)

   Om du vill testa leveransen av meddelanden i appen startar du programmet i Xcode- eller Android-studion och använder platssimulatorn för att välja en POI som uppfyller meddelandevillkoren.

   ![&quot;Dragkupong&quot;](/help/assets/drink-coupon-on-app.png)

Med hjälp av Platstjänster med Adobe Campaign Standard får ni ett kraftfullt verktyg för att segmentera och rikta ert budskap till användarna baserat på geofence-poster och utgångar. Tack vare den här integreringen kan ni skapa mer personaliserade och sammanhangsbaserade användningsfall.

>[!VIDEO](https://www.youtube.com/watch?v=ikiTTQw9c-o)