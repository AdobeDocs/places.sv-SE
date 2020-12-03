---
title: Ta bort ett bibliotek
description: Ta bort ett bibliotek med hjälp av Plats REST API:er.
translation-type: tm+mt
source-git-commit: 8a84fe2dc5a0efe94ce3121e589524e3c7a80c5e
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
>Ersätt variabler som `<lIBRARYID>`, `<API KEY>`, `<TOKEN>`och `<ORGID>`med faktiska värden.

