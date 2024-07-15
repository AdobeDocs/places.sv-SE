---
title: Ta bort ett bibliotek
description: Ta bort ett bibliotek med hjälp av Plats REST API:er.
exl-id: ad45ea38-9e12-43d7-b05f-17d3e40abaf5
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# Ta bort ett bibliotek {#delete-a-library}

En DELETE-metod som du kan använda för att ta bort ett bibliotek.

## Begäran

```text
DELETE https://api-places.adobe.io/places/placesapi/v1/libraries/<lIBRARYID>
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

Använd följande CURL-kommando för att testa detta API:

```text
curl -X DELETE 'https://api-places.adobe.io/places/placesapi/v1/libraries/<LIBRARYID>' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>'
```

>[!IMPORTANT]
>
>Ersätt variabler som `<lIBRARYID>`, `<API KEY>`, `<TOKEN>` och `<ORGID>` med faktiska värden.
