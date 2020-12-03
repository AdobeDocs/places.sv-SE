---
title: Ta bort flera POI
description: Använd batch-API:erna för att ta bort flera POI:er.
translation-type: tm+mt
source-git-commit: 5a0705f02c8ecd540506b628371aec45107df7b2
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---



# Ta bort flera POI {#delete-multiple-pois}

En metod som gör att du kan ta bort flera POI-POSTER.

## Begäran

```text
POST https://api-places.adobe.io/places/placesapi/v1/pois/batchDelete
```

## Sidhuvuden

```text
-H' Content-Type: application/json'  -H 'Authorization: Bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## Brödtext

```text
{  "ids": [    "<POIID>",    "<POIID>",    .    .    .    "<POIID>",    "<POIID>"  ]}
```

## Exempelsvar

```text
If successful a Status of "204 No Content" is returned.
```

## CURL, kommando

Använd följande CURL-kommando för att testa detta API:

```text
curl -X POST 'https://api-places.adobe.io/places/placesapi/v1/pois/batchDelete' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' --data-binary "@<PATHTOBATCHDELETEJSONFILE>" -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>Ersätt `<API KEY>`, `<TOKEN>`, `<ORGID>`och `<PATHTOBATCHDELETEJSONFILE>` med verkliga värden.

## JSON-exempelfil

Här följer ett exempel på JSON-fil för `batchDelete` API:

```text
{​"ids":["31a49d5c-c6ad-46ae-b88d-a6912a8a6b2f","6a78a729-7973-4373-9199-36da18cc5b8c","74eaa3da-2464-4298-9b6d-5376fa7ea00f"]​}
```
