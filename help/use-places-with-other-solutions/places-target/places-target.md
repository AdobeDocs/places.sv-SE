---
title: Adobe Target
description: I det här avsnittet finns information om hur du använder tjänsten Platser med Adobe Target.
exl-id: 6ee91fca-ea48-4de2-8dcf-87981813c678
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 7%

---

# Använd Platstjänst med Adobe Target {#places-target}

Det här dokumentet förutsätter att du har implementerat tillägget Platser i ditt program. Om du behöver hjälp med att implementera tillägget Platser finns mer information i [Placerar tillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

När platstillägget har skickats in händelser för poster och avslut kan du använda regler i Launch för att bifoga dina platstjänstdata till dina Adobe Target SDK-händelser. När du har valt önskad egenskap i Launch kan du skapa den här typen av regel genom att utföra följande uppgifter:

## 1. Skapa en regel

1. På **[!UICONTROL Rules]** flik, klicka **[!UICONTROL Create New Rule]**.

   Kom ihåg följande information:

   * Om du inte har några regler för den här egenskapen är knappen i mitten av skärmen.
   * Om egenskapen har regler visas knappen längst upp till höger på skärmen.

## 2. Välj en händelse

1. Ge regeln ett beskrivande namn så att den blir lätt igenkännbar i regellistan.

   I det här exemplet har regeln namnet **[!UICONTROL Attach Places Service Data to Target Content Requested]**.

1. Under **[!UICONTROL Events]** avsnitt, klicka **[!UICONTROL Add]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Adobe Target]**.
1. I listrutan **[!UICONTROL Event Type]** väljer du **[!UICONTROL Content Requested]**.
1. Klicka på **[!UICONTROL Keep Changes]**.

![lägg till en händelse](/help/assets/ad-setEvent_target.png)

## 3. Lägg till villkor

>[!IMPORTANT]
>
>Slutför det här steget om du vill lägga till villkor i regeln. Annars går du till *Definiera åtgärden* nedan.

I följande exempel skapas ett villkor som gör att regeln bara aktiveras för användare som har startat programmet fem eller fler gånger.

1. Under **[!UICONTROL Conditions]** avsnitt, klicka **[!UICONTROL Add]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Mobile Core]**.
1. I listrutan **[!UICONTROL Condition Type]** väljer du **[!UICONTROL Launches]**.
1. Ändra listrutans- och nummerkontrollerna i den högra rutan så att villkoret läses **[!UICONTROL User has launched the app greater than or equal to 5 times]**.
1. Klicka på **[!UICONTROL Keep Changes]**.

![lägg till ett villkor](/help/assets/ad-setCondition_target.png)

## 4. Definiera åtgärden

1. Under **[!UICONTROL Actions]** avsnitt, klicka **[!UICONTROL Add]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Mobile Core]**.
1. I listrutan **[!UICONTROL Action Type]** väljer du **[!UICONTROL Attach Data]**.
1. I den högra rutan, i **[!UICONTROL JSON Payload]** anger du de data som ska läggas till i den här händelsen.
1. Klicka på **[!UICONTROL Keep Changes]**.

I den högra rutan kan du lägga till en JSON-nyttolast på frihand som lägger till data i en SDK-händelse innan tilläggen som lyssnar efter den här händelsen hör den.

I följande exempel `poiCity` och `poiName` värden läggs till i **[!UICONTROL mboxparameters]** för varje begäran som behandlas i Target-händelsen. Värdena för de nya nycklarna bestäms dynamiskt av SDK när den här händelsen utförs.

>[!TIP]
>
>Den här JSON-nyttolasten använder en specialnotering för `request` -objekt. I den ursprungliga händelsen `request` är en array med anonyma objekt. När data bifogas till alla objekt i en array med Bifoga data, `[*]` notation på en nyckel som är känd för att innehålla en array gör att nyttolasten tillämpas på alla objekt i den arrayen.
>
>Beteckningen `request[*]` kan läsas upp högt som _för varje objekt i `request` array_.

![definiera åtgärden](/help/assets/ad-setAction-target.png)

## 5. Spara regeln och återskapa din egenskap

När du är klar med konfigurationen kontrollerar du att regeln ser ut så här:

![slutförd regel](/help/assets/ad-ruleComplete-target.png)

1. Klicka på **[!UICONTROL Save]**
1. Återskapa Launch-egenskapen och distribuera den till rätt miljö.
