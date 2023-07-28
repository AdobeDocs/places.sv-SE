---
title: Skapa en regel för egenskapen Platstjänst
description: Platserna SDK håller reda på den aktuella platsen, övervakar konfigurerade POI:er runt den aktuella platsen och spårar post- och avslutshändelser för dessa POI:er.
exl-id: dd5aa7ac-55f9-44dc-8632-e483ef3b91a0
source-git-commit: d5c216aebd99ffef01c37c17c62576835b52438b
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 11%

---

# Skapa regler för inträde och utträde {#create-entry-exit-rules}

Med platstillägget och en regionövervakningslösning som är installerad i ditt mobilprogram kan du skapa regler i Adobe Experience Platform Launch som aktiveras eller villkoras av platsdata, inklusive platsinmatnings- och avslutshändelser.

## Regler

Du kan konfigurera en regel som består av en händelse, ett villkor och en åtgärd. Varje regel består av följande:

* En eller flera händelser
* (Valfritt) villkor
* En eller flera åtgärder

### Platstjänsthändelser

Platstjänsten erbjuder följande händelser som du kan köra en regel för:

* **Ange POI**, som utlöses av Places SDK när kunden anger den POI som du konfigurerade.
* **Avsluta POI**, som aktiveras av Places SDK när kunden lämnar den POI som du konfigurerade.

### Villkor för platsservice

Villkoren definierar de kriterier som data som är associerade med händelsen, eller det delade tillståndet för ett tillägg i den instansen, måste uppfylla för att åtgärden ska kunna utföras. Du kan till exempel ställa in ett villkor för att utlösa en åtgärd för ett inträde på en kafé endast i San Francisco.

Platser-SDK behåller följande lägen:

* Aktuell POI, som avser den POI där kunden befinner sig.
* Senaste publicerade POI, som avser den senaste POI som kunden lämnade.
* Senaste POI, som avser den senaste POI som kunden angett.

Varje POI innehåller följande dataelement:

* ID
* Namn
* Latitud/longitud
* Radie
* Metadata som ort, land, delstat, kategori

### Instruktioner

Åtgärder definierar vad programmet ska göra som svar på att villkoret för regeln är uppfyllt för den utlösta händelsen. När kunden till exempel anger sin POI kan du konfigurera ett välkomstmeddelande som ska visas på deras mobila enhet.

## Skapa en regel: ett exempel

>[!CAUTION]
>
>I det här exemplet antas att du har skapat ett bibliotek med alla kaféer i USA. Mer information om hur du skapar POI och bibliotek finns i [Skapa en POI](/help/poi-mgmt-ui/create-a-poi-ui.md) och *Skapa ett bibliotek* in [Hantera flera bibliotek](https://experienceleague.adobe.com/docs/places/using/poi-mgmt-ui/manage-libraries-in-the-places-ui.html).

Följande procedur är ett exempel på hur du skapar en regel som skickar tillbaka ett inlägg till Slack när du går in i en kaffebutik i San Francisco.

Händelsen, villkoret och åtgärden definieras på följande sätt:

* **Händelse**: Platshändelse.
* **Villkor**: Stad för **aktuell intressepunkt** är San Francisco
* **Åtgärd**: Skicka ett återanslående till Slack av namnet på den kaffebutik som kunden angav.

### Förutsättning

Innan du skapar en regel måste du skapa ett dataelement i Adobe Experience Platform Launch. Dataelementen fyller automatiskt i den nödvändiga informationen om din POI i postback-meddelandet.

Så här skapar du ett dataelement i Experience Platform Launch:

1. Klicka på **Dataelement** -fliken.
1. Klicka **Lägg till dataelement**.
1. Skriv ett namn, till exempel **Aktuellt namn på kaffebutik**.
1. I **Tillägg** nedrullningsbar lista, välja **Platser - Beta**.
1. I **Dataelement**, markera **Ort**.
1. I den högra rutan väljer du **Aktuell POI**.
1. Klicka **Spara**.

### Skapa en regel i Experience Platform Launch för Platstjänst

![skapa en regel](/help/assets/placesrule.png)

1. Klicka på fliken **[!UICONTROL Rules]** i Experience Platform Launch.
1. Klicka på **[!UICONTROL Add Rule]**.
1. Skriv ett namn för regeln, till exempel **[!UICONTROL Track entry for coffee shop in SF]**.

### Skapa en händelse

1. Klicka på i avsnittet Händelser **[!UICONTROL + Add]**. Händelser avgör när du vill att regeln ska utlösas.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places – Beta]**.
1. I listrutan **[!UICONTROL Event Type]** väljer du **[!UICONTROL Enter POI]**.
1. I **[!UICONTROL Name]** anger du ett namn på händelsen, till exempel **[!UICONTROL Entering a coffee shop]**.
1. Klicka på **[!UICONTROL Keep Changes]**.

### Skapa ett villkor

1. Klicka på i avsnittet Villkor **[!UICONTROL +Add]**. Villkoren avgör vilka kriterier som måste uppfyllas för att åtgärden ska vidtas.
1. I **[!UICONTROL Logic Type]** väljer du Normal, vilket innebär att åtgärder kan köras om villkoret är uppfyllt.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places – Beta]**.
1. I **[!UICONTROL Condition Type]** väljer du **[!UICONTROL City]**.
1. Skriv ett villkorsnamn, till exempel **[!UICONTROL Coffee shop in SF]**.
1. I höger ruta klickar du på **[!UICONTROL Current POI]** och i listrutan väljer du **[!UICONTROL San Francisco]** som en av dina städer.
1. Klicka på **[!UICONTROL Keep Changes]**.

### Skapa en åtgärd

1. I **[!UICONTROL Actions]** avsnitt, klicka **[!UICONTROL + Add]**.
1. I **[!UICONTROL Extension]** nedrullningsbar lista, lämna standardlistan **[!UICONTROL Mobile Core]** markerat alternativ.
1. Välj en åtgärdstyp, till exempel **[!UICONTROL Send Postback]**.

   a. In **[!UICONTROL URL]** skriver du URL-adressen för återanslående för Slack, till exempel `https://hooks.slack.com/services/`.

   b. Välj **[!UICONTROL Add Post Body]** kryssruta.

   c. In **[!UICONTROL Post Body]**, lägger till texten i posten, till exempel: `{ "text": "A customer has entered" }`

   c. Skriv en innehållstyp, till exempel **[!UICONTROL application/json]**.

   d. Välj ett timeout-värde, till exempel **[!UICONTROL 5]**.

1. Klicka på **[!UICONTROL Keep Changes]**.

### Publicera regeln

1. Om du vill aktivera regeln måste du publicera den. Mer information om hur du publicerar din regel i Experience Platform Launch finns i [Publicering](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html).

### Tänk bortom poster och utträden

Det är otroligt kraftfullt att använda platsdata som villkor för att aktivera regler i Experience Platform Launch när du använder platsdata. Du kan till exempel ha en händelseutlösare för en Mobile Core Track-åtgärd klar att utlösas baserat på en särskild trackAction-anropshändelse i din app. Baserat på den här händelsen kan du placera ytterligare platsvillkor för händelsen innan en åtgärd utförs. Öppna t.ex. en undersökning i appen när ett inköp `trackAction` inträffar, men **endast** om användarens aktuella plats innehåller specifika metadata för platstjänsten.

![skapa ett villkor](/help/assets/places-condition.png)
