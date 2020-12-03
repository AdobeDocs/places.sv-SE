---
title: Hantera bibliotek i användargränssnittet för platstjänster
description: Hantera dina bibliotek med hjälp av användargränssnittet för platstjänster.
translation-type: tm+mt
source-git-commit: 5a21e734c0ef56c815389a9f08b445bedaae557a
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 23%

---


# Hantera bibliotek {#manage-libraries-places-ui}

Ett bibliotek är en samling POI. Du kan ha upp till 150 000 POI i ett bibliotek och det kan finnas upp till 100 bibliotek per Experience Cloud-organisation.

Det finns olika sätt att ordna dina POI:er i bibliotek beroende på vad som är mest användbart för din organisation. Vissa kunder kanske föredrar att skapa ett separat bibliotek för varje mobilapp, medan andra kunder kanske använder bibliotek för att gruppera specifika typer av POI-filer som kaffebutiker, parker, hotell osv. Ett stort underhållningsföretag kan till exempel ha ett bibliotek som omfattar deras utomhuslokaler i ett bibliotek och deras butiker i ett annat bibliotek. En stadsregering kan ha ett bibliotek som omfattar alla byggnaderna i staden och ett annat bibliotek som omfattar alla parker i staden.

Bibliotek definieras av följande:

| Tangenter: | Beskrivning: |
| :--- | :--- |
| ID | en unik identifierare som tilldelas biblioteket när det skapas |
| Namn | ett eget namn som tilldelats ett bibliotek |
| Rankning | Dessa rankningar kan ignoreras om det inte finns några överlappande geofence i din organisation. Om det finns överlappande intressepunkter bör du placera alla geostaket i separata bibliotek, så att de kan viktas i förhållande till varandra. En användare kan bara finnas i ett geostaket åt gången. <br><br>Den högsta rankningen av de geostaket en användare är i avgör hans eller hennes aktuella geostaket-medlemskap. Om det finns geofence som har samma biblioteksrankning är den minsta geofence användarens aktuella geofence. <br><br>SDK:t känner också av *senast angivna* och *senast lämnade* intressepunkter, så du har fullständig kontroll över hur du vill att reglerna ska utlösas baserat på användarnas interaktion med intressepunkterna. |

## Skapa ett bibliotek

1. Logga in på platser med din Adobe ID.
1. Klicka på **[!UICONTROL ...]** > **[!UICONTROL Manage Libraries]** längst upp till höger.
1. Klicka på **[!UICONTROL New]**.
1. Skriv namnet.
1. Klicka på **[!UICONTROL Confirm]**.

## Ändra rangordningen för ett bibliotek i användargränssnittet för platser

1. Logga in på Platser med din Adobe ID.
1. Klicka på **[!UICONTROL ...]** > **[!UICONTROL Manage Libraries]** längst upp till höger.
1. Klicka på ikonen till vänster om biblioteksnamnet och dra biblioteket till den nya ordningen.

## Byta namn på ett bibliotek

1. Logga in på Platser med din Adobe ID.
1. Klicka på **[!UICONTROL ...]** > **[!UICONTROL Manage Libraries]** längst upp till höger.
1. Leta reda på det bibliotek som du vill ta bort.
1. Klicka på **[!UICONTROL ...]** och välj **[!UICONTROL Rename]**.
1. Uppdatera namnet och klicka på **[!UICONTROL Save]**.

## Ta bort ett bibliotek

1. Logga in på Platser med din Adobe ID.
1. Klicka på **[!UICONTROL ...]** > **[!UICONTROL Manage Libraries]** längst upp till höger.
1. Leta reda på det bibliotek som du vill ta bort.
1. Klicka på **[!UICONTROL ...]** och välj **[!UICONTROL Delete]**.

