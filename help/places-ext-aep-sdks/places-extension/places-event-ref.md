---
title: Händelsereferens för platser
description: En lista över händelser som hanteras av tillägget Platser.
feature: Mobile SDK
exl-id: 98210ef4-5ff1-4792-b97b-2845ce02e78a
source-git-commit: f521d5e3b0b69977877d88382ce41fcb7d1c54b9
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 7%

---

# Händelsereferens för platser {#places-event-reference}

Här är en lista över de händelser som hanteras av tillägget Platser.

## GetCurrentPointsOfInterest

**Händelseinformation**

| Typ | Källa | Namn | Parade |
| :--- | :--- | :--- | :--- |
| PLATSER | REQUEST_CONTENT | `requestgetuserwithinplaces` | True |

**Händelsebeskrivning**

Den här händelsen är en begäran om att hämta de POI:er som enheten finns i.

**Definition av datanyttolast**

n/a

## GetNearbyPointsOfInterest

**Händelseinformation**

| Typ | Källa | Namn | Parade |
| :--- | :--- | :--- | :--- |
| PLATSER | REQUEST_CONTENT | `requestgetnearbyplaces` | True |

**Händelsebeskrivning**

Den här händelsen är en begäran om att få närliggande POI genom att ta hänsyn till den aktuella enhetsplatsen och de konfigurerade platsbiblioteken.

**Definition av datanyttolast**

| Nyckel | Värdetyp | Obligatoriskt | Standardvärde | Beskrivning |
| :--- | :--- | :--- | :--- | :--- |
| latitud | double | sant | n/a | Innehåller latitudvärdet för mitten av sökningen efter närliggande POI. |
| longitud | double | sant | n/a | Innehåller longitudvärdet för mitten av sökningen efter närliggande POI. |
| radie | heltal | falskt | n/a | Radie, i meter, används vid sökning efter närliggande POI. |
| count | heltal | falskt | 10 | Maximalt antal POI som ska returneras i den resulterande svarshändelsen. |

## ProcessRegionEvent

**Händelseinformation**

| Typ | Källa | Namn | Parade |
| :--- | :--- | :--- | :--- |
| PLATSER | REQUEST_CONTENT | `requestprocessregionevent` | Falskt |

**Händelsebeskrivning**

Den här händelsen gör att Platser-tillägget bearbetar en geofence-post eller en exit-händelse.

**Definition av datanyttolast**

| Nyckel | Värdetyp | Obligatoriskt | Beskrivning |
| :--- | :--- | :--- | :--- |
| regionid | string | sant | ID för regionen som genererar händelsen. |
| regionEventType | int | sant | Typ av regionhändelse som genereras. 1 för inträde och 2 för utförsel. |

## Händelser som skickas av tillägget Platser

Den här informationen pågår för närvarande.
