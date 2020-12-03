---
title: Skaffa ett biblioteks rankning
description: Få ett biblioteks rankning med hjälp av Places REST API.
translation-type: tm+mt
source-git-commit: 8a84fe2dc5a0efe94ce3121e589524e3c7a80c5e
workflow-type: tm+mt
source-wordcount: '41'
ht-degree: 0%

---


# Skaffa ett biblioteks rankning {#get-library-rank}

En GET-metod som gör att du kan rangordna bibliotek.

## Begäran

`GET https://api-places.adobe.io/places/placesapi/v1/libraries/rank`

## Sidhuvuden

```
-H Content-Type: application/JSON  
-H 'Authorization: Bearer <TOKEN>'  
-H 'x-api-key: <API KEY>'  
-H 'x-gw-ims-org-id: <ORGID>'  
-H 'Accept-Language: en-US'
```

## Exempelsvar

```
{"library_rank_order":["ea45781f-26af-44b1-b4f8-43baf5f0fe28","dfcc5270-1d6d-4bc9-9cd9-85ecd5ebc12b"]}
```

## CURL, kommando

```
curl -X GET 'https://api-places.adobe.io/places/placesapi/v1/libraries/rank ' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>Ersätt variabler som `<API KEY>`, `<TOKEN>`och `<ORGID>` med faktiska värden.

