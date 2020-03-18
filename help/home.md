---
title: Platstjänst
description: 'Platstjänsten är ett viktigt sammanhang när det gäller att förstå mobilanvändarnas engagemang. Genom att använda det här sammanhanget kan utvecklare av mobilappar förbättra appdesignen och göra den till en mer personaliserad och engagerande upplevelse. '
translation-type: tm+mt
source-git-commit: 05b4d29aa7925f7a43e70c644e3cb88045cbe446

---


# Platstjänst {#home}

![&quot;Platstjänst&quot;](/help/assets/places-service-header.png)

Plats är en viktig kontext för att förstå och engagera mobilanvändare. Genom att använda det här sammanhanget kan utvecklare av mobilappar förbättra appdesignen och göra den till en mer personaliserad och engagerande upplevelse.

Platstjänsten, som tidigare kallades Adobe Experience Platform Location Service, är en geolokaliseringstjänst som gör det möjligt för mobilappar med platsmedvetenhet att förstå platskontexten genom att använda avancerade och lättanvända SDK-gränssnitt tillsammans med en flexibel databas med intressepunkter (POI).

Med Platstjänst kan du uppnå följande:

* Skapa och hantera en databas med POI som kan utnyttjas med andra Adobe Experience Cloud-lösningar.
* Koppla anpassade metadata till POI:n för att göra dem mer omfattande och meningsfulla genom att ange ytterligare attribut.
* Visualisera POI på en karta för att enkelt förstå det spatiala sammanhanget och lägga till/redigera metadataattribut.
* Konfigurera SDK i Adobe Experience Platform Launch för att definiera era platsutlösta regler och metadatabaserade villkor.
* Minska koden som du behöver skriva för att övervaka en enhets plats och använd tillägget Platser för att automatiskt aktivera platsspecifika regler.

Detta gör att du kan vidta åtgärder från platssignaler i realtid, när och var det gäller. Rätt sammanhang ger en mer berikande mobilupplevelse.

Här är några sätt att använda platser:

* Skicka ett meddelande i realtid när någon går in i en POI, *&quot;Hej...Välkommen till stadion.&quot;*
* Analysera fottrafiken i era egna butiker jämfört med konkurrentbutikerna.
* Segmentera en målgrupp baserat på offlinebeteende genom att använda målgruppsprofiler med positionskontext.
* Rikta en användare med en butiksupplevelse när det är relevant.

## Placerar tjänstkomponenter

Platstjänsten omfattar följande komponenter:

* **Webbtjänst**

   Du kan skapa och hantera POI med hjälp av Places REST API:er. Mer information om REST API:er finns i [Hantera bibliotek](/help/web-service-api/api-usage/manage-libraries/manage-libraries.md) och [Hantera POI](/help/web-service-api/api-usage/manage-pois/manage-pois.md).

* **Gränssnitt för POI-hantering**

   Visualisera POI på en karta för att förstå det spatiala sammanhanget och för att lägga till/redigera POI och deras anpassade metadata.

* **Tillägget Platser**

   Det mobila API-gränssnittet för flera plattformar för att integrera platskontexten i era mobilappar. Mer information om SDK:er finns i [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

* **Starta regler**

   De geointelligenta startreglerna som gör att du kan aktivera åtgärder med start- och avslutningshändelser. Reglerna gör det även möjligt att använda geo-attribut i villkor för att personalisera upplevelsen.

* **Platsövervakartillägg**

   Den mobila SDK som kan bäddas in i din mobilapp för att automatiskt övervaka din användares platsändringar och aktivera Platsregler. Mer information finns i [Platsövervakartillägg](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md).

## Terminologi

Här är några vanliga termer som används i den här dokumentationen:

* En **intressepunkt (POI)** är en geografisk plats som är av intresse för din organisation.

   Du kan definiera POI med attribut som namn, radie, adress, kategori och metadatataggar.

* En **geofence** är en typ av POI.

   Denna POI-typ är en virtuell geografisk gräns som definieras av latitud- och longitudkoordinater.

* En **fyr** är en typ av POI.

   Den här POI-typen är en fysisk enhet som representerar en plats genom att skicka en blå tand med låg effekt. Stöd för beacons kommer i en kommande version.

* Ett **bibliotek** är en samling intressepunkter, som grupperas för att enkelt koppla regler till en uppsättning i stället för till en intressepunkt.

* Ett **tillägg** är det Experience Platform Launch-tillägg som krävs för att integrera Platser SDK i dina mobilappar.

   Det tillägg som används tillsammans med andra SDK:er för mobiler för att lägga till platskontext i era upplevelser.

* En **organisation** är den Adobe-enhet som identifierar ditt företag i Adobe Experience Cloud.

   Vanligtvis är en organisation ditt företagsnamn. Ett företag kan dock ha mer än en organisation. Organisationsadministratören kan konfigurera grupper och användare och konfigurera funktioner för enkel inloggning.

* **orgID** är det ID som representerar din organisation i Adobe Experience Platform.

   Mer information finns i [Söka efter ditt orgID](https://forums.adobe.com/thread/2339895).

* Med **Experience Cloud ID** -tjänsten får ni ett universellt, beständigt ID som identifierar era besökare i alla lösningar i Experience Cloud.

   Mer information finns i [Översikt](https://docs.adobe.com/content/help/en/id-service/using/intro/overview.html).
