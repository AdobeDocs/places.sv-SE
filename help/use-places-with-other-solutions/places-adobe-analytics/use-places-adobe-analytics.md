---
title: Skicka POI-post och avsluta data till Analytics
description: I det här avsnittet finns information om hur du skickar POI-post och avslutar data till Analytics.
exl-id: 69e96261-4902-47dd-a930-a8f3d19c179c
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 8%

---

# Skicka POI-post och avsluta data till Analytics {#places-data-analytics}


>[!IMPORTANT]
>
>I det här avsnittet förutsätts att du har implementerat Platstjänst i ditt program. Mer information om hur du implementerar Platstjänst finns i [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

När platstjänsten har skickat in- och avslutshändelserna kan du skapa regler i Experience Platform Launch för att skicka platstjänstdata till Adobe Analytics. Om du vill skapa den här typen av regel väljer du egenskapen i Launch och utför följande steg:

## 1. Skapa en regel

1. Klicka på **[!UICONTROL Create New Rule]** på fliken **[!UICONTROL Rules]**.

   Kom ihåg följande information:

   * Om du inte har några befintliga regler för den här egenskapen kommer knappen **[!UICONTROL Create New Rule]** att vara mitt på skärmen.
   * Om egenskapen har regler visas knappen **[!UICONTROL Create New Rule]** längst upp till höger på skärmen.

## 2. Välj en händelse

1. Skriv ett beskrivande namn för regeln.

   På det här sättet kan regeln lätt kännas igen i din lista över regler. I det här exemplet heter regeln **[!UICONTROL Send Data to Analytics]**.

1. Klicka på **[!UICONTROL Add]** i avsnittet **[!UICONTROL Events]**.

1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places Service]**.

1. I listrutan **[!UICONTROL Event Type]** väljer du **[!UICONTROL Enter POI]**.

1. Klicka på **[!UICONTROL Keep Changes]**.

   ![&quot;välj en händelse&quot;](/help/assets/pt-selectEvent.png)


## 3. Lägg till villkor

>[!IMPORTANT]
>
>Slutför det här steget om du vill lägga till villkor i regeln. Annars går du till *Definiera åtgärden* nedan.

I det här exemplet skapas ett villkor som gör att regeln bara utlöses när den aktuella POI:ns namn är lika med **[!UICONTROL My POI]**.

1. Klicka på **[!UICONTROL Add]** under avsnittet **[!UICONTROL Conditions]**.

1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places Service]**.

1. I listrutan **[!UICONTROL Condition Type]** väljer du **[!UICONTROL Name]**.

1. Skriv **[!UICONTROL My POI]** i textfältet i den högra rutan.

1. Klicka på **[!UICONTROL Keep Changes]**.

   ![ anger ett villkor ](/help/assets/pt-setCondition.png)


## 4. Definiera åtgärden

1. Klicka på **[!UICONTROL Add]** under avsnittet **[!UICONTROL Actions]**.

1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Adobe Analytics]**.

1. I listrutan **[!UICONTROL Action Type]** väljer du **[!UICONTROL Track]**.

1. Lägg till åtgärden eller läget som du vill skicka till Analytics (Analyser) i den högra rutan.

   Du kan också välja att lägga till ytterligare kontextdata i den här begäran. Kom ihåg att du kan använda dataelement för att hämta data dynamiskt från SDK:n.

1. Klicka på **[!UICONTROL Keep Changes]**.

   I följande exempel skickas ett `TrackAction`-anrop till Analytics med ytterligare kontextdata på `poi.name` som är lika med namnet på den POI som utlöste den här starthändelsen:

   ![&quot;ange en åtgärd&quot;](/help/assets/pt-setAction.png)

## 5. Spara regeln och återskapa din egenskap

När du är klar med konfigurationen kontrollerar du att regeln ser ut så här:

![&quot;regel har skapats&quot;](/help/assets/pt-ruleComplete.png)

1. Klicka på **[!UICONTROL Save]**

1. Återskapa Launch-egenskapen och distribuera den till rätt miljö.
