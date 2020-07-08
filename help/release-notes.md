---
title: Versionsinformation
description: Versionsinformation för Platstjänst.
translation-type: tm+mt
source-git-commit: 3f986697179eb9c0af1d9b54daf67793a99b8491
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 2%

---


# Versionsinformation {#release-notes}

## 8 juli 2020

* **Bildtillägg för Platser och Platser**

   * Tillägg för Platser och Platsövervakare har lagts till för [React Native-program](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#react-native)
   * Tillägg för Platser och Platsövervakare har lagts till för [Cordova-program](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#cordova)
   * Mer information finns i: [Använda platstillägg](https://docs.adobe.com/content/help/en/places/using/places-ext-aep-sdks/places-extension/places-extension.html)


## 12 maj 2020

* **Places Service**

   * Importera POI-filer gruppvis från en CSV-fil med knappen Importera POI-filer
   * Markera flera POI och redigera eller lägg till metadatavärden gruppvis

## 6 maj 2020

* **PlacesMonitor 2.2.1**

   * **Android**

      * Förbättrad loggning

## 5 maj 2020


* **PlacesMonitor 2.1.3**

   * **iOS**

      * Förbättrad loggning

## 20 februari 2020

* **ACPlaces 1.3.1 (iOS)**

   * Platstillägget rapporterar nu versionsinformation till händelsehubben i Core SDK.
   * Information om enhetens POI-medlemskap har nu en standardtid för direktuppspelning på en timme från den tidpunkt då den samlas in. Mer information finns i [Ändra platser för medlemskap med tidsbegränsad publicering](places-ext-aep-sdks/places-extension/places-extension.md#places-ttl)


* **Platser 1.4.1 (Android)**

   * Platstillägget rapporterar nu versionsinformation till händelsehubben i Core SDK.
   * Information om enhetens POI-medlemskap har nu en standardtid för direktuppspelning på en timme från den tidpunkt då den samlas in. Mer information finns i [Ändra platser för medlemskap med tidsbegränsad publicering](places-ext-aep-sdks/places-extension/places-extension.md#places-ttl)

## 27 januari 2020

* **PlacesMonitor 2.2.0**

   * **Android**

      * Anropa det nya Places-API:t för att samla in auktoriseringsstatus när appen startas och när auktoriseringen ändras medan appen körs.
      * Added setRequestLocationPermission API and deprecated setLocationPermission API.

## 9 januari 2020

* **Platser 1.4.0**

   * **Android**

      * En ny API har lagts till `setAuthorizationStatus`för att ange enhetsauktoriseringsstatus för Platstjänster. Värdet lagras och används i läget Platser delade.

## 4 december 2019

* **PlacesMonitor 2.1.2**

   * **iOS**

      * Anropa Places API för att samla in CLAuthorizationStatus från enheten när den ändras.

## 3 december 2019

* **ACPlaces 1.3.0**

   * **iOS**

      * En ny API har lagts till `setAuthorizationStatus`för att ange enhetsauktoriseringsstatus för Platstjänster. Värdet lagras och används i läget Platser delade.

## 25 november 2019

* **PlacesMonitor 2.1.1**

   * **iOS**

      * Fasta importsatser för Cocopods-projekt som använder flera pod-projekt.

## 22 november 2019

* **PlacesMonitor 2.1.1**

   * **Android**

      * Skärmen känner nu igen starten för en Android-enhet och registrerar vid behov geofences igen med operativsystemet baserat på enhetens aktuella plats.
      * Korrigerade ett tävlingsvillkor som ibland orsakade att post-/avslutshändelser ignorerades.

## 9 oktober 2019

* **PlacesMonitor 2.1.0**

   * **iOS**

      * En ny API har lagts till `setRequestAuthorizationLevel`för att ange vilken typ av platsauktoriseringsbegäran som användaren ska tillfrågas om.
   * **Android**

      * En ny API har lagts till `setLocationPermission`för att ange vilken typ av platsbehörighetsbegäran som användaren ska tillfrågas om.
      * Platsövervakaren har nu stöd för Android 10.



## 8 aug 2019

Följande uppdateringar gjordes i den här versionen:

### Gränssnittsuppdateringar

Här är en lista över uppdateringar av användargränssnittet för platser:

#### Nya funktioner

* En ny listvy har lagts till som visar POI utan kartan.
* Alternativ för POI-filtrering har lagts till för stad, stat, land och metadata.
* Det första biblioteket i en organisation skapas automatiskt.
* POI-sortering har lagts till i listvyn.

#### Gränssnittsuppdateringar

* Listan och informationspanelen flyttades till höger om användargränssnittet.
* En ny sökpanel har lagts till högst upp i användargränssnittet.
* Om det bara finns ett bibliotek väljs det här biblioteket automatiskt när du skapar en POI.
* Bibliotekshantering har flyttats till ett popup-fönster.
* Ett POI-värde har lagts till bredvid filtren.

## 6 aug 2019

Följande uppdateringar gjordes i den här versionen:

### Monitor Launch Extension 2.0.0

* Android- och iOS-installationsinstruktionerna för Places Monitor 2.0 har uppdaterats.

## 31 juli 2019

Följande uppdateringar gjordes i den här versionen:

### Platsbildskärm 2.0.0

* Övervakningsstatusen behålls nu mellan starterna.
* Hanteringen av återanropet, som är ett resultat av en platsbehörighetsbegäran, kräver inte längre att du utökar PlacesActivity.
* Ändrade ett befintligt API så att utvecklare kan rensa alla platsdata från enheten:

   Gammalt API: `public static void stop();`

   Nytt API: `public static void stop (final boolean clearData);`

* API:t har uppdaterats för att hantera felscenarier mer effektivt. `getNearbyPointsOfInterest`

## 25 juli 2019

Följande uppdateringar gjordes i den här versionen:

### ACPlacesMonitor 2.0.0

* Om du vill ta bort alla platsdata från enheten

   i ACPlacesMonitor ersatte ett befintligt API `+ (void) stop;` med`+ (void) stop: (BOOL) clearData;`.

* API:t för ACPlaces `getNearbyPointsOfInterest` har uppdaterats för att hantera felscenarier mer effektivt.

## 22 juli 2019

Följande uppdateringar gjordes i den här versionen:

### Android Platser 1.3.0

* Ett nytt API har lagts till som tar bort alla platsrelaterade data från delat läge, minne i appen och delade inställningar.
* Ett problem där det delade tillståndet inte uppdaterades när programmet startades har åtgärdats.
* Korrigerade ett fel där `getNearbyPointsOfInterest` återanropet returnerade felkod `SERVER_RESPONSE_ERROR instead of CONNECTIVITY_ERROR` på Internet.
* `getNearbyPointsOfInterest` API (utan errorCallback) anropas med en tom poi-lista om det uppstår fel när närliggande intressepunkter hämtas. `successCallback`

## 19 juli 2019

Följande uppdateringar gjordes i den här versionen:

**iOS Platser 1.2.0**

Ett nytt API har lagts till som rensar bort alla platsrelaterade data från delat läge, minne i appen och `NSUserDefaults`.

## 25 juni 2019

Följande uppdateringar gjordes i den här versionen:

**iOS Places Monitor 1.0.2**

* Bättre livskvalitet, bland annat bättre koddokumentation och loggning.

## 17 juni 2019

Följande uppdateringar gjordes i den här versionen:

**iOS Platser 1.1.0**

* En ny API har lagts till för att returnera en felkod när det uppstår ett fel när närliggande platser hämtas.
* När sekretessstatus ändras till avanmälan kommer alla platsrelaterade data nu att rensas från enheten.
* Korrigerade ett problem som, efter en första start, ibland orsakade att Platshändelser gick förlorade på grund av felaktiga nätverksförhållanden.
* Ett problem har korrigerats där tokenersättning via regelmotorn ibland refererar till fel POI när POI-anmälningshändelser bearbetas i snabb följd.

## 30 maj 2019

**Android Places Monitor 1.0.1**

* Korrigerade ett problem som förhindrade en starthändelse för POI när Platsövervakning startades.

## 28 maj 2019

Följande problem i användargränssnittet för platser har korrigerats:

* Uppdaterade Solution Switcher i Platser för att passa in i resten av Experience Cloud.
* Korrigerade ett problem där rankningen sparades i instanser där inga rangändringar gjordes.
* Ökade den minsta tillåtna radien i användargränssnittet till 10 meter.
* Ett problem har korrigerats där radiefältet återställdes till 20 meter om du tar bort alla nummer i fältet.

## 17 maj 2019

Följande uppdateringar gjordes i den här versionen:

**Android Platser 1.2.0**

* En ny API har lagts till för att bearbeta en enskild Geofence.
* Felkorrigering för att förhindra flera på varandra följande starthändelser.

**Android Places Monitor 1.0.0**

Första versionen av Places Monitor för Android.

Platsövervakaren hanterar plats-API:erna på operativsystemnivå och kommunicerar direkt med platstillägget. Med båda tilläggen installerade kan kunderna ha körklar regionövervakning i sina program.
Klicka här om du vill ha mer information om Platsövervakaren.


## 2 maj 2019

**Android Platser 1.1.0**

* Introducerade ett nytt API för getNearByPlaces, som har ett errorCallback och anropas med en errorCode som anger orsaken till felet.
* Platstillägget placerar nu händelserna i kö tills en konfiguration har hämtats.
* Stöd för miljömedvetna konfigurationer har lagts till.
* Felkorrigering: korrigerade nycklarna för regionens in-/avslutshändelser
* Lagring av den senast kända platsen respekterar nu användarens sekretessstatus


## 9 apr 2019

Följande uppdateringar gjordes i den här versionen:

**iOS Places Monitor 1.0.1**

* Tillagd full testtäckning.
* CI-integrering (CircleCI)
* Integrering av kodtäckning (codecov)

## 25 mars 2019

iOS Places Monitor 1.0.0

Första versionen av Platsövervakaren för iOS.

Platsövervakaren hanterar plats-API:erna på operativsystemnivå och kommunicerar direkt med platstillägget. Med båda tilläggen installerade kan kunderna ha körklar regionövervakning i sina program. Mer information om Platsövervakaren finns i [Platsövervakartillägg](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md).

## 28 februari 2019

### Betaversion

Det här är den första versionen av Places Service, en uppsättning verktyg som gör att kunderna kan berika sina användarupplevelser med platsdata i verkligheten. I den första versionen är vårt främsta användningsexempel att göra det möjligt för mobilappar att hämta anpassade platsdata och agera utifrån dessa data via Adobe Experience Platform Launch.

### Viktiga funktioner

Här är de viktigaste funktionerna i den här versionen:

#### Användargränssnitt för platstjänst

Vi har släppt ett hanteringsgränssnitt där du kan visa och hantera dina intressepunkter. Du kan också ordna dina POI-filer i bibliotek. Förutom standardmetadata som stad, delstat och kategori stöder vi även möjligheten att lägga till anpassade metadata i dina POI-filer.

* Om du vill se användargränssnittet går du till [https://places.adobe.com](https://places.adobe.com).
* Information om hur du kommer igång med användargränssnittet finns i [Komma igång](/help/getting-started.md).

#### Platstillägg

Med hjälp av platstillägget kan du lägga till dina platsservicebibliotek i din mobilapp och agera utifrån deras POI. Med hjälp av regelbyggaren i Experience Platform Launch kan du utlösa åtgärder som ska utlösas när användare går in i och avslutar POI.

I tillägget Platser:

* Du kan välja vilka POI-bibliotek som ska ingå i appen.
* Regelhändelser som utlöses vid POI-inträde eller -utträde.
* Skapa dataelement som pekar på användarens aktuella POI.

For more information about the Places extension, see [Places extension](/help/places-ext-aep-sdks/places-extension/places-extension.md).

#### Placerar API:er

Du kan använda Places-API:erna för att göra följande:

* Tillåt utvecklare att fylla i och uppdatera sin lista över POI.
* Bygg ett eget användargränssnitt eller integrera med en befintlig POI-databas.
* Använd Places-API:ts batchslutpunkter för att göra en bulkimport av POI:er.

   Du kan använda det medföljande Python-verktyget för att slutföra bulkimporten.

Mer information om Places-API:er finns i [Webbtjänste-API](/help/web-service-api/places-web-services.md).

### Kommer snart

#### Analytics-integrering

Analytics-tillägget uppdateras för att automatiskt lägga till platssammanhangsdata från din Places-tjänstdatabas till alla utgående Analytics-samtal när en användare befinner sig i en POI (passiva samtal). Uppdateringen tillåter även att regler skapas för att starta Analytics-spåranrop direkt vid POI-inträde eller -utträde (aktiva anrop).
