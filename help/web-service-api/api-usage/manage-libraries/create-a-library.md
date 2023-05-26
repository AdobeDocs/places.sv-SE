---
title: Skapa ett bibliotek
description: Skapa ett bibliotek med hjälp av Plats REST API.
exl-id: 155cc6e6-9254-4389-bb02-e526d15908f4
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '48'
ht-degree: 0%

---

# Skapa ett bibliotek {#create-a-library}

En biblioteksmetod som du kan använda för att skapa ett POST.

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
