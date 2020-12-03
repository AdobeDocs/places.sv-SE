---
title: Skapa en regel för platstjänstegenskapen
description: 'Platserna SDK håller reda på den aktuella platsen, övervakar konfigurerade POI:er runt den aktuella platsen och spårar post- och avslutshändelser för dessa POI:er. '
translation-type: tm+mt
source-git-commit: c22efc36f2eac6b20fc555d998c3988d8c31169e
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 11%

---


# Skapa regler för inträde och utträde {#create-entry-exit-rules}

Med Platser-tillägget och Places Monitor-tilläggen installerade i ditt mobilprogram kan du skapa regler i Adobe Experience Platform Launch som aktiveras eller villkoras av platsdata, inklusive platsinmatnings- och avslutshändelser.

## Regler

Du kan konfigurera en regel som består av en händelse, ett villkor och en åtgärd. Varje regel består av följande:

* En eller flera händelser
* (Valfritt) villkor
* En eller flera åtgärder

### Platstjänsthändelser

Platstjänsten erbjuder följande händelser som du kan köra en regel för:

* **Ange POI**, som aktiveras av Places SDK när kunden anger den POI som du har konfigurerat.
* **Avsluta POI**, som aktiveras av Places SDK när kunden lämnar den POI som du har konfigurerat.

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

### Åtgärder

Åtgärder definierar vad programmet ska göra som svar på att villkoret för regeln är uppfyllt för den utlösta händelsen. När kunden till exempel anger sin POI kan du konfigurera ett välkomstmeddelande som ska visas på deras mobila enhet.

## Skapa en regel: ett exempel

>[!CAUTION]
>
>I det här exemplet antas att du har skapat ett bibliotek med alla kaféer i USA. For more information about creating POIs and libraries, see [Create a POI](/help/poi-mgmt-ui/create-a-poi-ui.md) and *Create a Library* in [Manage multiple libraries](https://docs.adobe.com/content/help/en/places/using/poi-mgmt-ui/manage-libraries-in-the-places-ui.html).

Följande procedur är ett exempel på hur du skapar en regel som skickar tillbaka ett inlägg till Slack när du går in i en kaffebutik i San Francisco.

Händelsen, villkoret och åtgärden definieras på följande sätt:

* **Händelse**: Platsens starthändelse.
* **Villkor**: Stad för **aktuell intressepunkt** är San Francisco
* **Åtgärd**: Skicka ett återanslående till Slack på namnet på den kaffebutik som kunden angav.

### Förutsättning

Innan du skapar en regel måste du skapa ett dataelement i Adobe Experience Platform Launch. Dataelementen fyller automatiskt i den nödvändiga informationen om din POI i postback-meddelandet.

Så här skapar du ett dataelement i Experience Platform Launch:

1. Klicka på fliken **Dataelement** .
1. Klicka på **Lägg till dataelement**.
1. Skriv ett namn, till exempel **Aktuellt kaffebutiksnamn**.
1. I listrutan **Tillägg** väljer du **Platser - Beta**.
1. I **Dataelement** väljer du **Ort**.
1. Välj **Aktuell POI** i den högra rutan.
1. Klicka på **Spara**.

### Skapa en regel i Experience Platform Launch för Platstjänst

![skapa en regel](/help/assets/placesrule.png)

1. Klicka på fliken **[!UICONTROL Rules]** i Experience Platform Launch.
1. Klicka på **[!UICONTROL Add Rule]**.
1. Skriv till exempel ett namn på regeln **[!UICONTROL Track entry for coffee shop in SF]**.

### Skapa en händelse

1. Klicka på i händelseavsnittet **[!UICONTROL + Add]**. Händelser avgör när du vill att regeln ska utlösas.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places – Beta]**.
1. I listrutan **[!UICONTROL Event Type]** väljer du **[!UICONTROL Enter POI]**.
1. I **[!UICONTROL Name]** anger du ett namn på händelsen, till exempel **[!UICONTROL Entering a coffee shop]**.
1. Klicka på **[!UICONTROL Keep Changes]**.

### Skapa ett villkor

1. Klicka på under Villkor **[!UICONTROL +Add]**. Villkoren avgör vilka kriterier som måste uppfyllas för att åtgärden ska vidtas.
1. I **[!UICONTROL Logic Type]** väljer du Normal, vilket innebär att åtgärder kan köras om villkoret är uppfyllt.
1. I listrutan **[!UICONTROL Extension]** väljer du **[!UICONTROL Places – Beta]**.
1. I **[!UICONTROL Condition Type]** väljer du **[!UICONTROL City]**.
1. Skriv ett villkorsnamn, till exempel **[!UICONTROL Coffee shop in SF]**.
1. I höger ruta klickar du på **[!UICONTROL Current POI]** och i listrutan väljer du **[!UICONTROL San Francisco]** som en av dina städer.
1. Klicka på **[!UICONTROL Keep Changes]**.

### Skapa en åtgärd

1. In the **[!UICONTROL Actions]** section, click **[!UICONTROL + Add]**.
1. I den **[!UICONTROL Extension]** nedrullningsbara listan låter du standardalternativet **[!UICONTROL Mobile Core]** vara markerat.
1. Välj till exempel en åtgärdstyp **[!UICONTROL Send Postback]**.

   a. I **[!UICONTROL URL]** skriver du URL-adressen för återanslående för Slack, till exempel `https://hooks.slack.com/services/`.

   b. Markera kryssrutan om du vill skicka ett inlägg **[!UICONTROL Add Post Body]** .

   c. I **[!UICONTROL Post Body]** lägger du till texten i posten, till exempel: `{ "text": "A customer has entered" }`

   c. Skriv till exempel en innehållstyp **[!UICONTROL application/json]**.

   d. Välj till exempel ett timeout-värde **[!UICONTROL 5]**.

1. Klicka på **[!UICONTROL Keep Changes]**.

### Publicera regeln

1. Om du vill aktivera regeln måste du publicera den. Mer information om hur du publicerar regeln i Experience Platform Launch finns i [Publicera](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html).

### Tänk bortom poster och utträden

Det är otroligt kraftfullt att använda platsdata som villkor för att aktivera regler i Experience Platform Launch när du använder platsdata. Du kan till exempel ha en händelseutlösare för en Mobile Core Track-åtgärd klar att utlösas baserat på en särskild trackAction-anropshändelse i din app. Baserat på den här händelsen kan du placera ytterligare platsvillkor för händelsen innan en åtgärd utförs. Du kan till exempel öppna en undersökning i appen när en `trackAction` köphändelse inträffar, men **bara** om användarens aktuella plats innehåller specifika metadata för platstjänsten.

![skapa ett villkor](/help/assets/places-condition.png)