---
title: Skapa ett bibliotek
description: Skapa ett bibliotek med hjälp av Plats REST API.
translation-type: tm+mt
source-git-commit: 8a84fe2dc5a0efe94ce3121e589524e3c7a80c5e

---


# Skapa ett bibliotek {#create-a-library}

En POST-metod som gör att du kan skapa ett bibliotek.

## Begäran

```text
POST https://api-places.adobe.io/places/placesapi/v1/libraries
```

## Sidhuvuden

```text
-H' Content-Type: application/json'  -H 'Authorization: Bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## Brödtext

```text
{"name": "<LIBRARY_NAME>"}
```

## Exempelsvar

```text
{       "id": "449f08f3-eff5-4658-9329-2d9687af777e",       "name": "Facinating places",      "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",       "poiCount": 0  }
```

## CURL, kommando

Använd följande CURL-kommando för att testa detta API:

```text
curl -X POST 'https://api-places.adobe.io/places/placesapi/v1/libraries' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' -d '{"name":"New Library Name"}' -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>Ersätt variabler som `<API KEY>`, `<TOKEN>`och `<ORGID>` med faktiska värden.

