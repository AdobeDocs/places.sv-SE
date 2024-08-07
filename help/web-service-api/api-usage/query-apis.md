---
title: Översikt
description: Förstå och använda API:er för frågor.
exl-id: cc61a49c-1cf2-407f-b81a-3d38fcb622cc
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Fråga API:er

En GET-metod som gör att du kan fråga de POI:er som är närmast anroparen.

## Begäran

```text
GET https://query.places.adobe.com/placesedgequery
```

Med följande indata returnerar tjänsten en lista över de POI:er som är närmast anroparen:

* Uppringarens position (latitud, longitud).
* ID:n för de POI-bibliotek som ska inkluderas i sökningen.
* Det maximala antalet POI som ska returneras.  Standardvärdet är 100.

  Avståndet mellan anroparen och POI definieras som avståndet från anroparen till kanten på POI:s geofence. I svaret markeras POI som innehåller anroparen som anroparen.

Argument anges som följande frågeparametrar:

* (**Obligatorisk**) `latitude`

  Anroparens latitud, som måste vara mellan -85 och 85.
* (**Obligatorisk**) `longitude`

  Uppringarens longitud, som måste vara mellan -180 och 180.

* (**Valfritt**) `limit`

  Det maximala antalet POI som ska returneras.

* (**Obligatorisk**) `library`

  ID för det bibliotek som ska frågas. Om du vill fråga flera bibliotek måste du ta med flera kopior av biblioteksparametern i frågan.

Här följer ett exempel på det returnerade JSON-formatet:

```markup
{
    "places": {
        "userWithin": [
            {
                "p": [
                    "poi id",
                    "poi name",
                    "poi center's latitude",
                    "poi center's longitude",
                    poiRadius,
                    rank
                ],
                "x": {
                    "country": "US",
                    "city": "Fremont",
                    "street": "Vineyard Heights",
                    "Color": "Blue",
                    "state": "CA",
                    <other POI metadata>
                }
            }
        ],
        "pois": [
            {
                "p": [
                    "poi id",
                    "poi name",
                    "poi center's latitude",
                    "poi center's longitude",
                    poiRadius,
                    rank
                ],
                "x": {
                    "country": "US",
                    "city": "Milpitas",
                    "street": null,
                    "state": "CA"
                }
            },
            {
                "p": [
                    "poi id",
                    "poi name",
                    "poi center's latitude",
                    "poi center's longitude",
                    poiRadius,
                    rank
                ],
                "x": {
                    "country": "US",
                    "city": "Fremont",
                    "street": null,
                    "state": "CA"
                }
            }
        ]
    }
}
```

POI under `places.pois` sorteras efter avstånd från anroparen till kanten av POI:n. POI under `places.userWithin` innehåller anroparen och dessa POI sorteras efter rangordning och sedan genom att radien ökas.

## Exempel på samtal

Här är ett exempel på samtalet:

```text
GET https://query.places.adobe.com/placesedgequery?latitude=<userLatitude>&longitude=<userLongitude>&library=<libID1>&library=<libID2>&limit=20
```
