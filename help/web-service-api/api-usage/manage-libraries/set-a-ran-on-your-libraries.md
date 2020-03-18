---
title: Ange en rankning i dina bibliotek
description: Ange en rankning för dina bibliotek med hjälp av Places REST API.
translation-type: tm+mt
source-git-commit: 8a84fe2dc5a0efe94ce3121e589524e3c7a80c5e

---


# Ange en rankning i dina bibliotek {#set-rank-on-libraries}

En PUT-metod som gör att du kan ange en rangordning för alla dina bibliotek.

## Begäran

`PUT https://api-places-dev.adobe.io/places/placesapi/v1/libraries/rank`

## Sidhuvuden

```-H Content-Type: application/json'
-H 'Authorization: Bearer <TOKEN>`  
-H 'x-api-key: <API KEY>'  
-H 'x-gw-ims-org-id: <ORGID>'  
-H 'Accept-Language: en-US'
```

## PUT-data

```
"library_rank_order": ["dfcc5270-1d6d-4bc9-9cd9-85ecd5ebc12b","ea45781f-26af-44b1-b4f8-43baf5f0fe28"]  
}
```

## Exempelsvar

```
{"library_rank_order" ["dfcc5270-1d6d-4bc9-9cd9-85ecd5ebc12b","ea45781f-26af-44b1-b4f8-43baf5f0fe28"]}
```

## CURL, kommando

```
curl -X PUT `'https://api-places.adobe.io/places/placesapi/v1/libraries/rank'` -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' -d '{"library_rank_order": ["dfcc5270-1d6d-4bc9-9cd9-85ecd5ebc12b","ea45781f-26af-44b1-b4f8-43baf5f0fe28"]}' -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>Ersätt variabler som `<API KEY>`, `<TOKEN>`och `<ORGID>` med faktiska värden.
