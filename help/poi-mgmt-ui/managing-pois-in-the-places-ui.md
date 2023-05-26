---
title: Hantera befintliga POI
description: I användargränssnittet för platstjänster kan du redigera, ta bort eller filtrera befintliga POI.
exl-id: a4cf28ae-1e3c-4724-bca3-ac1d0cd6da09
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 6%

---

# Hantera befintliga POI {#managing-existing-pois}

POI och bibliotek skapas och hanteras i platsdatabasen med hjälp av användargränssnittet Platser.

## Redigera en POI

1. Logga in på platser med din Adobe ID.
1. Logga in på Platstjänst med din Adobe ID.
1. Klicka på ikonen längst upp till höger som ser ut som en punktlista.
1. Leta reda på den POI som du vill redigera.
1. Klicka på **[!UICONTROL ...]** och välj **[!UICONTROL View Details]**.
1. Uppdatera informationen och klicka på **[!UICONTROL Save]**.

## Ta bort en POI

1. Logga in på platser med din Adobe ID.
1. Logga in på Platstjänst med din Adobe ID.
1. Klicka på ikonen längst upp till höger som ser ut som en punktlista.
1. Leta reda på den POI som du vill ta bort.
1. Klicka på **[!UICONTROL ...]** och välj **[!UICONTROL Delete]**.

## Filtrera POI efter ort, delstat, land eller metadata

![filtrera en POI](/help/assets/filter_poi.png)

1. Logga in på användargränssnittet för Platstjänst med din Adobe ID.
1. Klicka på filterikonen längst upp till höger.
1. Du kan filtrera POI på något av följande sätt:

   * Per bibliotek:

      a. Välj ett bibliotek.

   * Efter egenskap:

      a. I listrutan Egenskaper väljer du **[!UICONTROL Country]**, **[!UICONTROL State]**, eller **[!UICONTROL City]**.

      b. Ange ett värde på nästa rad.

      Du kan till exempel välja **[!UICONTROL State]** och text **[!UICONTROL California]**.

   * Med metadata:

      a. Ange en nyckel och ett värde.

## Definiera en geofence-POI

Geofence är en typ av POI och definieras i databasen baserat på följande nycklar:

| Tangenter | Beskrivning | Obligatoriskt? |
| :--- | :--- | :--- |
| ID | Unik identifierare som tilldelats varje POI | Ja |
| Namn | Eget namn för POI. | Ja |
| Bibliotek | Varje POI måste tilldelas ett bibliotek för organisationen. | Ja |
| Radie | Radien för din POI i meter. | Ja |
| Ikon | Hjälpa till med visualiseringar av POI. | Ja (tilldelad standard) |
| Färg | Hjälpa till med visualiseringar av POI. | Ja (tilldelad standard) |
| Kategori | Tilldela ett gemensamt ramverk med kategorier som är gemensamma för alla POI i alla bibliotek. | Nej |
| Adress | Gatuadress. | Nej |
| Ort | Postens stad. | Nej |
| Stat/region | Postens delstat eller region. | Nej |
| Land | POI-land. | Nej |
| Latitud | Latitudkoordinat för POI-centrum. | Ja |
| Longitud | Longituskoordinat för POI-centrum. | Ja |
| Metadata | Anpassade nyckel- och värdepar som kan tilldelas POI:er. Dessa metadata effektiviserar framtida arbetsflöden genom att göra det möjligt att gruppera POI i bibliotek för var och en att använda regler och filter i arbetsflöden längre fram i kedjan, till exempel skicka ett push-meddelande när någon skriver ett POI med Type = Competitor. | Nej |
