---
title: Översikt
description: Förstå och använda API:er för frågor.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b

---



# Fråga API:er

En GET-metod som gör att du kan fråga de POI som är närmast anroparen.

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

* (**Obligatoriskt**) `latitude`

   Anroparens latitud, som måste vara mellan -85 och 85.
* (**Obligatoriskt**) `longitude`

   Uppringarens longitud, som måste vara mellan -180 och 180.

* (**Optional**) `limit`

   Det maximala antalet POI som ska returneras.

* (**Obligatoriskt**) `library`

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

POI under `places.pois` sorteras efter avståndet från anroparen till kanten av POI:n. POI under `places.userWithin` innehåller anroparen och dessa POI sorteras efter rangordning och sedan genom att radien ökas.

## Exempel på samtal

Här är ett exempel på samtalet:

```text
GET https://query.places.adobe.com/placesedgequery?latitude=<userLatitude>&longitude=<userLongitude>&library=<libID1>&library=<libID2>&limit=20
```
