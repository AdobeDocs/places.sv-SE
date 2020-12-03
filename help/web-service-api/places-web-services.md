---
title: 'Översikt över API för Web Services '
description: Platstjänsten är en uppsättning tjänster som gör det enklare för Adobe-kunder att hysa ut Adobe Experience Cloud- och Adobe Experience Platform-lösningar med platsdata och rätt upplevelse för rätt person vid rätt tidpunkt och på rätt plats.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---


# API-översikt för Web Services {#places-web-services-api}

Platstjänsten är en uppsättning tjänster som gör det enklare för Adobe-kunder att hysa ut Adobe Cloud Platform- och Adobe Experience Platform-lösningar med platsdata och rätt upplevelse för rätt person vid rätt tidpunkt och på rätt plats.

Med API:erna för webbtjänster kan du göra följande:

* Hantera geofle
* Mät platsen för användare även när appen finns i bakgrunden
* Använd data i realtid när det är viktigt

Det här avsnittet innehåller information om hur du använder REST API:er och POI-databasen, som innehåller organisationens POI-data.

## REST API:er 

Med hjälp av REST-API:t för platstjänster kan du programmässigt arbeta med organisationens POI. Med dessa API:er kan du skapa, uppdatera och ta bort dina bibliotek och POI:er i dessa bibliotek. Dessa API:er använder JSON-standarder (JavaScript Object Notation) för att formatera data som skickas och tas emot. En stor fördel med JSON är att det gör det enkelt för utvecklare och datorer att skriva, läsa och tolka API-frågor.

Innan du kan använda API:t för webbtjänster måste du kontrollera att följande krav är uppfyllda:

* Platstjänsten tillhandahålls i din organisation och du har lämplig åtkomst som användare.

   Mer information finns i *Krav för användaråtkomst* i [Integreringsöversikt och -krav](/help/web-service-api/adobe-i-o-integration.md).

* När Platstjänst har etablerats i din organisation och du har åtkomst skapar du en Adobe-integrering för Platstjänst.

   Mer information finns i *Skapa en platsintegrering* i [Integreringsöversikt och villkor](/help/web-service-api/adobe-i-o-integration.md).

Ytterligare information:

* Mer information om tillgängliga API:er och hur du använder dem finns i [Hantera bibliotek](/help/web-service-api/api-usage/manage-libraries/manage-libraries.md) och [Hantera POI](/help/web-service-api/api-usage/manage-pois/manage-pois.md).
* Mer information om rubriker och parametrar i dessa API:er finns i [Sidhuvuden och parametrar](/help/web-service-api/api-usage/headers-and-parameters.md).