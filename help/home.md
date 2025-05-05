---
title: Places Service
description: Platstjänsten är ett viktigt sammanhang när det gäller att förstå mobilanvändarnas engagemang. Genom att använda det här sammanhanget kan utvecklare av mobilappar förbättra appdesignen och göra den till en mer personaliserad och engagerande upplevelse.
exl-id: 7369176f-c072-437a-9ee3-b463c5ff1d12
source-git-commit: e78e3c5ee6623d6cdf2a33c0582667a70283fdc6
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 7%

---

# Places Service {#home}

Plats är en viktig kontext för att förstå och interagera med mobilanvändare. Genom att använda det här sammanhanget kan utvecklare av mobilappar förbättra appdesignen och göra den till en mer personaliserad och engagerande upplevelse.

Platstjänsten, som tidigare kallades Adobe Experience Platform Location Service, är en geolokaliseringstjänst som gör det möjligt för mobilappar med platsmedvetenhet att förstå platskontexten genom att använda avancerade och lättanvända SDK-gränssnitt tillsammans med en flexibel databas med intressepunkter.

Med Platstjänst kan du uppnå följande:

* Skapa och hantera en databas med POI som kan utnyttjas med andra Adobe Experience Cloud-lösningar.
* Koppla anpassade metadata till POI:n för att göra dem mer omfattande och meningsfulla genom att ange ytterligare attribut.
* Visualisera POI på en karta för att enkelt förstå det spatiala sammanhanget och lägga till/redigera metadataattribut.
* Konfigurera SDK i Adobe Experience Platform Launch för att definiera dina platsutlösta regler och metadatabaserade villkor.
* Minska koden som du behöver skriva för att övervaka en enhets plats och använd tillägget Platser för att automatiskt aktivera platsspecifika regler.

Detta gör att du kan vidta åtgärder från platssignaler i realtid, när och var det gäller. Rätt sammanhang ger en mer berikande mobilupplevelse.

Här är några sätt att använda platser:

* Skicka ett meddelande i realtid när någon anger ett POI, *&quot;Hej...Välkommen till stadion.&quot;*
* Analysera fottrafiken i era egna butiker jämfört med konkurrentbutikerna.
* Segmentera en målgrupp baserat på offlinebeteende genom att använda målgruppsprofiler med positionskontext.
* Rikta en användare med en butiksupplevelse när det är relevant.

## Placerar tjänstkomponenter

Platstjänsten omfattar följande komponenter:

* **Webbtjänst**

  Du kan skapa och hantera POI med hjälp av Places REST API:er. Mer information om REST API:er finns i [Hantera bibliotek](/help/web-service-api/api-usage/manage-libraries/manage-libraries.md) och [Hantera POI:er](/help/web-service-api/api-usage/manage-pois/manage-pois.md).

* **Gränssnitt för POI-hantering**

  Visualisera POI på en karta för att förstå det spatiala sammanhanget och för att lägga till/redigera POI och deras anpassade metadata.

* **Platstillägg**

  Det mobila API-gränssnittet för flera plattformar för att integrera platskontexten i era mobilappar. Mer information om SDK:er finns i [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

* **Startregler**

  De geointelligenta startreglerna som gör att du kan aktivera åtgärder med start- och avslutningshändelser. Reglerna gör det även möjligt att använda geo-attribut i villkor för att personalisera upplevelsen.

## Terminologi

Här är några vanliga termer som används i den här dokumentationen:

* En **intressepunkt (POI)** är en geoplats som är av intresse för din organisation.

  Du kan definiera POI med attribut som namn, radie, adress, kategori och metadatataggar.

* En **geofence** är en typ av POI.

  Denna POI-typ är en virtuell geografisk gräns som definieras av latitud- och longitudkoordinater.

* En **fyr** är en typ av POI.

  Den här POI-typen är en fysisk enhet som representerar en plats genom att skicka en blå tand med låg effekt. Stöd för beacons kommer i en kommande version.

* Ett **bibliotek** är en samling intressepunkter, som grupperas för att enkelt koppla regler till en uppsättning i stället för till en intressepunkt.

* Ett **tillägg** är det Experience Platform Launch-tillägg som krävs för att integrera platsens SDK i dina mobilappar.

  Det tillägg som används tillsammans med andra SDK:er för mobiler för att lägga till platskontext i era upplevelser.

* En **organisation** är den Adobe-enhet som identifierar ditt företag i Adobe Experience Cloud.

  Vanligtvis är en organisation ditt företagsnamn. Ett företag kan dock ha flera organisationer. Organisationsadministratören kan konfigurera grupper och användare och konfigurera funktioner för enkel inloggning.

* **orgID** är det ID som representerar din organisation i Adobe Experience Platform.

  Mer information finns i [Söka efter ditt orgID](https://forums.adobe.com/thread/2339895).

* Tjänsten **Experience Cloud ID** tillhandahåller ett universellt, beständigt ID som identifierar dina besökare i alla lösningar i Experience Cloud.

  Mer information finns i [Översikt](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=sv-SE).

