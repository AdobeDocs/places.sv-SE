---
title: Lägg till platskontext i Analytics-begäranden
description: I det här avsnittet finns information om hur du lägger till platskontext i Analytics-begäranden.
exl-id: bee7b6e3-a75b-4a07-b6e2-f93ce33aa042
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 7%

---

# Lägg till platskontext i Analytics-begäranden {#run-reports-aa-locserv-data}

>[!IMPORTANT]
>
>Det här dokumentet förutsätter att du har implementerat Platstjänst i ditt program. Mer information om hur du implementerar tjänsten Platser finns i [Placerar tillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

När platstjänsten har skickat in- och avslutshändelserna kan du skapa regler i Experience Platform Launch och bifoga dina platstjänstdata till alla Adobe Analytics-händelser. Om du vill skapa den här typen av regel väljer du egenskapen i Launch och utför följande steg:

## 1. Skapa en regel

1. På **[!UICONTROL Rules]** flik, klicka **[!UICONTROL Create New Rule]**.

   Kom ihåg följande information:
   * Om du inte har några regler för den här egenskapen kan du **[!UICONTROL Create New Rule]** -knappen visas mitt på skärmen.
   * Om din egenskap har regler **[!UICONTROL Create New Rule]** knappen visas längst upp till höger på skärmen.

## 2. Välj en händelse

1. Ge regeln ett beskrivande namn så att den blir lätt igenkännbar i regellistan.

   I det här exemplet har regeln namnet **[!UICONTROL Attach Places Service Data to Analytics Track Action Events]**.

1. Under **[!UICONTROL Events]** avsnitt, klicka **[!UICONTROL Add]**.

1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Mobile Core]**.

1. I listrutan **[!UICONTROL Event Type]** väljer du **[!UICONTROL Track Action]**.

Nu kan du bestämma vilka utlösare du vill ta med för den här regeln. I det här exemplet baseras utlösaren på alla `TrackAction` samtal. När du har konfigurerat händelsen klickar du på **[!UICONTROL Keep Changes]**.

![&quot;create an event&quot;](/help/assets/ad-setEvent_use-analytics-data.png)


## 3. Lägg till villkor

>[!IMPORTANT]
>
>Slutför den här proceduren om du vill lägga till villkor i regeln. Annars går du till *Definiera åtgärden* nedan.

I det här exemplet skapas ett villkor som gör att regeln bara aktiveras för AT&amp;T-kunder.

1. Under **[!UICONTROL Conditions]** avsnitt, klicka **[!UICONTROL Add]**.

1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Mobile Core]**.

1. I listrutan **[!UICONTROL Condition Type]** väljer du **[!UICONTROL Carrier Name]**.

1. I fönstret till höger väljer du **[!UICONTROL AT&T]** kryssrutan.

1. Klicka på **[!UICONTROL Keep Changes]**.

![&quot;skapa ett villkor&quot;](/help/assets/ad-setCondition_use-analytics-data.png)

## 4. Definiera åtgärden

1. Under **[!UICONTROL Actions]** avsnitt, klicka **[!UICONTROL Add]**.

1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Mobile Core]**.

1. I listrutan **[!UICONTROL Action Type]** väljer du **[!UICONTROL Attach Data]**.

1. I den högra rutan, i **[!UICONTROL JSON Payload]** anger du de data som ska läggas till i den här händelsen.

1. Klicka på **[!UICONTROL Keep Changes]**.

I den högra rutan kan du lägga till en JSON-nyttolast på fri hand som lägger till data i en SDK-händelse innan ett tillägg som lyssnar efter den här händelsen kan höra händelsen. I det här exemplet läggs vissa kontextdata till i den här händelsen innan Analytics-tillägget bearbetar den. De tillagda kontextdata kommer nu att ingå i den utgående Analytics-träffen.

I följande exempel `poi.city` och `poi.name` värden läggs till i kontextdata för Analytics-händelsen. Värdena för de nya nycklarna bestäms dynamiskt av SDK när den här händelsen bearbetas.

![&quot;skapa en åtgärd&quot;](/help/assets/ad-setAction_use-analytics-data.png)

## 5. Spara regeln och återskapa din egenskap

När du är klar med konfigurationen kontrollerar du att regeln ser ut så här:

![&quot;regeln är färdig.&quot;](/help/assets/ad-ruleComplete_use-analytics-data.png)

1. Klicka på **[!UICONTROL Save]**

1. Återskapa Launch-egenskapen och distribuera den till rätt miljö.
