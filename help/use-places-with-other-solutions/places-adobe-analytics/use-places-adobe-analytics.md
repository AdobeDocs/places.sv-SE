---
title: Skicka POI-post och avsluta data till Analytics
description: I det här avsnittet finns information om hur du skickar POI-post och avslutar data till Analytics.
exl-id: 69e96261-4902-47dd-a930-a8f3d19c179c
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 8%

---

# Skicka POI-post och avsluta data till Analytics {#places-data-analytics}


>[!IMPORTANT]
>
>I det här avsnittet förutsätts att du har implementerat Platstjänst i ditt program. Mer information om hur du implementerar tjänsten Platser finns i [Placerar tillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

När platstjänsten har skickat in- och avslutshändelserna kan du skapa regler i Experience Platform Launch för att skicka platstjänstdata till Adobe Analytics. Om du vill skapa den här typen av regel väljer du egenskapen i Launch och utför följande steg:

## 1. Skapa en regel

1. På **[!UICONTROL Rules]** flik, klicka **[!UICONTROL Create New Rule]**.

   Kom ihåg följande information:

   * Om du inte har några regler för den här egenskapen kan du **[!UICONTROL Create New Rule]** -knappen visas mitt på skärmen.
   * Om din egenskap har regler **[!UICONTROL Create New Rule]** knappen visas längst upp till höger på skärmen.

## 2. Välj en händelse

1. Skriv ett beskrivande namn för regeln.

   På så sätt kan regeln lätt kännas igen i listan Regler. I det här exemplet har regeln namnet **[!UICONTROL Send Data to Analytics]**.

1. I **[!UICONTROL Events]** avsnitt, klicka **[!UICONTROL Add]**.

1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places Service]**.

1. I listrutan **[!UICONTROL Event Type]** väljer du **[!UICONTROL Enter POI]**.

1. Klicka på **[!UICONTROL Keep Changes]**.

   ![&quot;välj en händelse&quot;](/help/assets/pt-selectEvent.png)


## 3. Lägg till villkor

>[!IMPORTANT]
>
>Slutför det här steget om du vill lägga till villkor i regeln. Annars går du vidare till *Definiera åtgärden* nedan.

I det här exemplet skapas ett villkor som gör att regeln bara utlöses när den aktuella POI:ns namn är lika med **[!UICONTROL My POI]**.

1. Under **[!UICONTROL Conditions]** avsnitt, klicka **[!UICONTROL Add]**.

1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places Service]**.

1. I listrutan **[!UICONTROL Condition Type]** väljer du **[!UICONTROL Name]**.

1. I den högra rutan anger du **[!UICONTROL My POI]**.

1. Klicka på **[!UICONTROL Keep Changes]**.

   ![&quot;ange ett villkor&quot;](/help/assets/pt-setCondition.png)


## 4. Definiera åtgärden

1. Under **[!UICONTROL Actions]** avsnitt, klicka **[!UICONTROL Add]**.

1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Adobe Analytics]**.

1. I listrutan **[!UICONTROL Action Type]** väljer du **[!UICONTROL Track]**.

1. Lägg till åtgärden eller läget som du vill skicka till Analytics (Analyser) i den högra rutan.

   Du kan också välja att lägga till ytterligare kontextdata i den här begäran. Kom ihåg att du kan använda dataelement för att hämta data dynamiskt från SDK:n.

1. Klicka på **[!UICONTROL Keep Changes]**.

   I följande exempel är `TrackAction` anrop skickas till Analytics med ytterligare kontextdata för `poi.name` lika med namnet på det POI som utlöste den här starthändelsen:

   ![&quot;ange en åtgärd&quot;](/help/assets/pt-setAction.png)

## 5. Spara regeln och återskapa din egenskap

När du är klar med konfigurationen kontrollerar du att regeln ser ut så här:

![&quot;rule is created&quot;](/help/assets/pt-ruleComplete.png)

1. Klicka på **[!UICONTROL Save]**

1. Återskapa Launch-egenskapen och distribuera den till rätt miljö.
