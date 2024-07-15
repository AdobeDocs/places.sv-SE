---
title: Uppdatera ett bibliotek
description: Uppdatera ett bibliotek med hjälp av Places REST API.
exl-id: 37ca2be2-39e1-4f8e-87c2-ef4cb366db0d
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '48'
ht-degree: 0%

---

# Uppdatera ett bibliotek {#update-a-library}

En PUT-metod som gör att du kan uppdatera ett bibliotek.

## Begäran

```text
PUT https://api-places.adobe.io/places/placesapi/v1/libraries/<lIBRARYID>
```

## Sidhuvuden

```text
-H' Content-Type: application/json'  -H 'Authorization: bearer <TOKEN>'  -H 'x-api-key: <API KEY>'  -H 'x-gw-ims-org-id: <ORGID>'  -H 'Accept-Language: en-US'
```

## Brödtext

```text
{"name": "<NEW_LIBRARY_NAME>"}
```

## Exempelsvar

```text
{       "id": "449f08f3-eff5-4658-9329-2d9687af777e",       "name": "Really facinating places",      "customerID": "777F20F55BACA09E0A495D8F@AdobeOrg",       "poiCount": 0  }
```

## CURL, kommando

Använd följande CURL-kommando för att testa detta API:

```text
curl -X PUT 'https://api-places.adobe.io/places/placesapi/v1/libraries/<LIBRARYID>' -H 'x-api-key: <API KEY>' -H 'Authorization: Bearer <TOKEN>' -H 'x-gw-ims-org-id: <ORGID>' -d '{"name":"Updated Library Name"}' -H "Content-Type: application/json"
```

>[!IMPORTANT]
>
>Ersätt variabler som `<lIBRARYID>`, `<API KEY>`, `<TOKEN>` och `<ORGID>` med faktiska värden.
