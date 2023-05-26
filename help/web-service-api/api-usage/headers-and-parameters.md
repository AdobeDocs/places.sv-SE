---
title: Sidhuvuden och parametrar
description: Sidhuvuden och parametrar som är tillgängliga i platstjänstens REST-API:er.
exl-id: 3c7e76de-f0ff-4966-a3ec-7f64d819c140
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# Sidhuvuden och parametrar {#headers-and-parameters}

Här är information om de rubriker och parametrar som är tillgängliga i Platstjänst REST API:

## Rubriker som stöds

| Sidhuvud | Beskrivning | Metod | Exempel |
| :--- | :--- | :--- | :--- |
| `Authorization` | Din innehavartoken | Alla |  |
| `x-api-key` | Din API-nyckel | Alla | `19776964b4cde49e08d8f62e5824f777b` |
| `x-gw-ims-org-id` | Ditt företags-ID | Alla | `18FB61145BAC2FFB0A494777@AdobeOrg` |
| `Content-Type` | Format för innehåll som skickas eller tas emot | PUT, POST | `application/json` |
| `Accept-Language` | Språk som används för felmeddelanden | Valfritt | `en-US` |

## Biblioteksparametrar

| Parameter | Beskrivning | Typ | Gräns | Begäran eller svar | Exempel |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | ID för bibliotek | tilldelad | n/a | Svar | `"id": "b2488788-2d2a-462b-b1a2-305272777dda"` |
| `name` | Bibliotekets namn | string | 256 tecken | båda, krävs på begäran | `"name": "Amazing Places"` |
| `orgID` | Experience cloud orgID för organisationen | tilldelad | n/a | Svar | `"orgID": "777F20F55BACA09E0A495D8F@AdobeOrg"` |
| `poiCount` | Antal POI i biblioteket | heltal | Högst 150 000 | Svar | `"poiCount": 25149` |
| `metadataDescriptors` | Antal för varje unikt nyckelvärdepar för POI-metadata | blandad | n/a | Svar |  |
| `poiCountInCities` | Antal för varje unikt POI-stadsvärde | blandad | n/a | Svar |  |

## POI-parametrar

| Parameter | Beskrivning | Typ | Gräns | Begäran eller svar | Exempel |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Poi data | Matris med POI-detaljer | n/a | båda |  |
| `id` | ID för POI | tilldelad | n/a | svar | `"id": "1455462b-7f9c-4220-9f42-5bbce777a0d1"` |
| `name` | POI-namn | string | 512 tecken | båda, valfria\* | `"name": "My Favorite Place"` |
| `description` | Beskrivning av POI | string | 512 tecken | båda, valfria\* | `"description": "This is a very good place."` |
| `location` | Array med POI-typ och koordinater | array (mixad) | n/a | båda | `"location": {"type": "Point", "coordinates": [-122.201007, 37.604713]` |
| `type` | Typ av POI | string | endast &quot;Point&quot; stöds för närvarande | båda, krävs på begäran | `"type": "Point"` |
| `coordinates` | Longitud och latitud för POI | array (float) | longitud: -180 till 180, latitud -85 till 85 | båda, krävs på begäran | `"coordinates": [-122.201007, 37.604713]` |
| `radius` | Storlek på cirkulär geofence runt POI | float | 10-2 000 meter | båda, krävs på begäran | `"radius": 100` |
| `country` | Land för POI | string | 32 tecken | båda, tillval* | `"country": "United States"` |
| `state` | Delstat för POI | string | 32 tecken | båda, tillval* | `"state": "California"` |
| `city` | Postens ort | string | 32 tecken | båda, tillval* | `"city": "San Jose"` |
| `street` | Gatuadress för POI | string | 256 tecken | båda, tillval* | `"street": "122 Woz Way"` |
| `category` | Kategori för POI | string | 100 tecken | båda, tillval* | `"category": "cafe"` |
| `icon` | Ikon för POI | string | 50 tecken | båda, tillval* | `"icon": "star"` |
| `color` | Färg för POI | string | 8 tecken | båda, tillval* | `"color": "blue"` |
| `metadata` | Array med nyckel/värde-par för POI | array(string) | nyckel: 256 tecken, värde: 256 tecken, maximalt 10 par | båda, tillval* | `"metadata": {"region": "Equator"}` |
| `lib_id` | ID för det bibliotek som POI finns i | n/a | n/a | båda, krävs | `"lib_id": "ac7a0b25-c6c2-43ba-bbc6-2b1777b80fe9"` |

* Om parametervärdet inte inkluderas ställs värdet in på `empty` i databasen. Om det befintliga nyckel/värde-paret inte inkluderas, tas nyckel/värde-paret bort för den POI-informationen i databasen.
