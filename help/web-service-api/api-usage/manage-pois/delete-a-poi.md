---
title: Ta bort en POI
description: Ta bort en POI med hjälp av Places REST API:er.
translation-type: tm+mt
source-git-commit: 8a84fe2dc5a0efe94ce3121e589524e3c7a80c5e

---


# Ta bort en POI {#delete-a-poi}

En DELETE-metod som gör att du kan ta bort en POI.

## Begäran

```text
DELETE https://api-places.adobe.io/places/placesapi/v1/pois/<POIID>
```

## Sidhuvuden

```text
-H' Content-Type: application/json'  
-H 'Authorization: Bearer <TOKEN>'  
-H 'x-api-key: <API KEY>'  
-H 'x-gw-ims-org-id: <ORGID>'  
-H 'Accept-Language: en-US'
```

## Exempelsvar

```text
If successful a Status of "204 No Content" is returned.
```

## CURL, kommando

Använd följande CURL-kommando för att testa API:t:

```text
curl -X DELETE 'https://api-places.adobe.io/places/placesapi/v1/pois/<POIID>' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>Ersätt `<POIID>`, `<API KEY>`, `<TOKEN>`och `<ORGID>` med faktiska värden.

