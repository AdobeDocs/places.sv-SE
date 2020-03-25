---
title: Adobe Target
description: I det här avsnittet finns information om hur du använder Platstjänst med Adobe Target.
translation-type: tm+mt
source-git-commit: d33e4e2d798c7048bdd275cdf6c0aabf3434f789

---


# Använd platstjänst med Adobe Target {#places-target}

Det här dokumentet förutsätter att du har implementerat tillägget Platser i ditt program. Om du behöver hjälp med att implementera tillägget Platser, se [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

När platstillägget har skickats in händelser för poster och avslut kan du använda regler i Launch för att bifoga dina platstjänstdata till dina Adobe Target SDK-händelser. När du har valt önskad egenskap i Launch kan du skapa den här typen av regel genom att utföra följande uppgifter:

## 1. Skapa en regel

1. On the **[!UICONTROL Rules]** tab, click **[!UICONTROL Create New Rule]**.

   Kom ihåg följande information:

   * Om du inte har några regler för den här egenskapen är knappen i mitten av skärmen.
   * Om egenskapen har regler visas knappen längst upp till höger på skärmen.

## 2. Välj en händelse

1. Ge regeln ett beskrivande namn så att den blir lätt igenkännbar i regellistan.

   I det här exemplet får regeln namnet **[!UICONTROL Attach Places Service Data to Target Content Requested]**.

1. Klicka på under **[!UICONTROL Events]** avsnittet **[!UICONTROL Add]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Adobe Target]**.
1. I listrutan **[!UICONTROL Event Type]** väljer du **[!UICONTROL Content Requested]**.
1. Klicka på **[!UICONTROL Keep Changes]**.

![lägg till en händelse](/help/assets/ad-setEvent_target.png)

## 3. Lägg till villkor

>[!IMPORTANT]
>
>Slutför det här steget om du vill lägga till villkor i regeln. I annat fall går du till *Definiera åtgärden* nedan.

I följande exempel skapas ett villkor som gör att regeln bara aktiveras för användare som har startat programmet fem eller fler gånger.

1. Klicka på under **[!UICONTROL Conditions]** avsnittet **[!UICONTROL Add]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Mobile Core]**.
1. I listrutan **[!UICONTROL Condition Type]** väljer du **[!UICONTROL Launches]**.
1. I den högra rutan ändrar du listrutans- och nummerkontrollerna så att villkoret läses **[!UICONTROL User has launched the app greater than or equal to 5 times]**.
1. Klicka på **[!UICONTROL Keep Changes]**.

![lägg till ett villkor](/help/assets/ad-setCondition_target.png)

## 4. Definiera åtgärden

1. Klicka på under **[!UICONTROL Actions]** avsnittet **[!UICONTROL Add]**.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Mobile Core]**.
1. I listrutan **[!UICONTROL Action Type]** väljer du **[!UICONTROL Attach Data]**.
1. Skriv de data som ska läggas till i den här händelsen i **[!UICONTROL JSON Payload]** fältet till höger.
1. Klicka på **[!UICONTROL Keep Changes]**.

I den högra rutan kan du lägga till en JSON-nyttolast på frihand som lägger till data i en SDK-händelse innan tilläggen som lyssnar efter den här händelsen hör den.

I följande exempel läggs `poiCity` och `poiName` värden till i **[!UICONTROL mboxparameters]** för varje begäran som bearbetas i Target-händelsen. Värdena för de nya nycklarna bestäms dynamiskt av SDK när den här händelsen utförs.

>[!TIP]
>
>Den här JSON-nyttolasten använder en specialnotation för `request` objektet. I den ursprungliga händelsen `request` är en array med anonyma objekt. När du kopplar data till alla objekt i en array med hjälp av Bifoga data, tillämpas nyttolasten på alla objekt i arrayen om en nyckel som är känd som `[*]` innehåller en array.
>
>Kommentaren för `request[*]` kan läsas upp högt som _för varje objekt i`request`arrayen_.

![definiera åtgärden](/help/assets/ad-setAction-target.png)

## 5. Spara regeln och återskapa din egenskap

När du är klar med konfigurationen kontrollerar du att regeln ser ut så här:

![slutförd regel](/help/assets/ad-ruleComplete-target.png)

1. Klicka på **[!UICONTROL Save]**
1. Återskapa Launch-egenskapen och distribuera den till rätt miljö.
