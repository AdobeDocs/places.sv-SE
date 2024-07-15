---
title: Adobe Target
description: I det här avsnittet finns information om hur du använder tjänsten Platser med Adobe Target.
exl-id: 6ee91fca-ea48-4de2-8dcf-87981813c678
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 7%

---

# Använd Platstjänst med Adobe Target {#places-target}

Det här dokumentet förutsätter att du har implementerat tillägget Platser i ditt program. Om du behöver hjälp med att implementera Platser-tillägget läser du [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

När platstillägget har skickats in händelser för poster och avslut kan du använda regler i Launch för att bifoga dina platstjänstdata till dina Adobe Target SDK-händelser. När du har valt önskad egenskap i Launch kan du skapa den här typen av regel genom att utföra följande uppgifter:

## 1. Skapa en regel

1. Klicka på **[!UICONTROL Create New Rule]** på fliken **[!UICONTROL Rules]**.

   Kom ihåg följande information:

   * Om du inte har några regler för den här egenskapen är knappen i mitten av skärmen.
   * Om egenskapen har regler visas knappen längst upp till höger på skärmen.

## 2. Välj en händelse

1. Ge regeln ett beskrivande namn så att den blir lätt igenkännbar i regellistan.

   I det här exemplet heter regeln **[!UICONTROL Attach Places Service Data to Target Content Requested]**.

1. Klicka på **[!UICONTROL Add]** under avsnittet **[!UICONTROL Events]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Adobe Target]**.
1. I listrutan **[!UICONTROL Event Type]** väljer du **[!UICONTROL Content Requested]**.
1. Klicka på **[!UICONTROL Keep Changes]**.

![lägg till en händelse](/help/assets/ad-setEvent_target.png)

## 3. Lägg till villkor

>[!IMPORTANT]
>
>Slutför det här steget om du vill lägga till villkor i regeln. Annars går du till *Definiera åtgärden* nedan.

I följande exempel skapas ett villkor som gör att regeln bara aktiveras för användare som har startat programmet fem eller fler gånger.

1. Klicka på **[!UICONTROL Add]** under avsnittet **[!UICONTROL Conditions]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Mobile Core]**.
1. I listrutan **[!UICONTROL Condition Type]** väljer du **[!UICONTROL Launches]**.
1. I den högra rutan ändrar du listrutans- och nummerkontrollerna så att villkoret blir **[!UICONTROL User has launched the app greater than or equal to 5 times]**.
1. Klicka på **[!UICONTROL Keep Changes]**.

![lägg till ett villkor](/help/assets/ad-setCondition_target.png)

## 4. Definiera åtgärden

1. Klicka på **[!UICONTROL Add]** under avsnittet **[!UICONTROL Actions]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Mobile Core]**.
1. I listrutan **[!UICONTROL Action Type]** väljer du **[!UICONTROL Attach Data]**.
1. Skriv de data som ska läggas till i den här händelsen i fältet **[!UICONTROL JSON Payload]** i den högra rutan.
1. Klicka på **[!UICONTROL Keep Changes]**.

I den högra rutan kan du lägga till en JSON-nyttolast på frihand som lägger till data i en SDK-händelse innan tilläggen som lyssnar efter den här händelsen hör den.

I följande exempel läggs värdena `poiCity` och `poiName` till i **[!UICONTROL mboxparameters]** för varje begäran som bearbetas i Target-händelsen. Värdena för de nya nycklarna bestäms dynamiskt av SDK när den här händelsen utförs.

>[!TIP]
>
>Den här JSON-nyttolasten använder en specialnotation för objektet `request`. I den ursprungliga händelsen är `request` en array med anonyma objekt. När data bifogas till alla objekt i en array med hjälp av Bifoga data, tillämpas nyttolasten på alla objekt i arrayen med `[*]`-notation på en nyckel som är känd för att innehålla en array.
>
>Notation of `request[*]` kan läsas upp högt som _för varje objekt i `request`-arrayen_.

![definiera åtgärden](/help/assets/ad-setAction-target.png)

## 5. Spara regeln och återskapa din egenskap

När du är klar med konfigurationen kontrollerar du att regeln ser ut så här:

![slutförd regel](/help/assets/ad-ruleComplete-target.png)

1. Klicka på **[!UICONTROL Save]**
1. Återskapa Launch-egenskapen och distribuera den till rätt miljö.
