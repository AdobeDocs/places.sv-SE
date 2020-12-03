---
title: API-referens för platser
description: Information om API-referenserna i Platser.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 31%

---


# API-referens för platser {#places-api-reference}

Här är information om API-referenserna i tillägget Platser:

## Bearbeta en regionhändelse

När en enhet korsar en av dina apps fördefinierade gränser för platstjänster, skickas regionen och händelsetypen till SDK för bearbetning.

### ProcessGeofence (Android)

Bearbeta en `Geofence` områdeshändelse för den angivna `transitionType`.

Skicka `transitionType` från `GeofencingEvent.getGeofenceTransition()`. För närvarande `Geofence.GEOFENCE_TRANSITION_ENTER` och `Geofence.GEOFENCE_TRANSITION_EXIT` stöds.

**Syntax**

Här är syntaxen för den här metoden:

```java
public static void processGeofence(final Geofence geofence, final int transitionType);
```

**Exempel**

Anropa den här metoden i `IntentService` som är registrerad för att ta emot Android-geofence-händelser.

Här följer ett kodexempel för den här metoden:

```java
public class GeofenceTransitionsIntentService extends IntentService {

    public GeofenceTransitionsIntentService() {
        super("GeofenceTransitionsIntentService");
    }

    protected void onHandleIntent(Intent intent) {
        GeofencingEvent geofencingEvent = GeofencingEvent.fromIntent(intent);

        List<Geofence> geofences = geofencingEvent.getTriggeringGeofences();

        if (geofences.size() > 0) {
          // Call the Places API to process information
          Places.processGeofence(geofences.get(0), geofencingEvent.getGeofenceTransition());
        }
    }
}
```

### ProcessRegionEvent (iOS)

Den här metoden ska anropas i `CLLocationManager` delegaten, som anger om användaren har angett eller avslutat en viss region.

**Syntax**

Här är syntaxen för den här metoden:

```objectivec
+ (void) processRegionEvent: (nonnull CLRegion*) region forRegionEventType: (ACPRegionEventType) eventType;
```

**Exempel**

Här är kodexemplet för den här metoden:


```objectivec
- (void) locationManager:(CLLocationManager *)manager didEnterRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
}

- (void) locationManager:(CLLocationManager *)manager didExitRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeExit];
}
```

### ProcessGeofencingEvent (Android)

Bearbeta allt `Geofences` i `GeofencingEvent` en och samma gång.

**Syntax**

```java
public static void processGeofenceEvent(final GeofencingEvent geofencingEvent);
```

**Exempel**

Anropa den här metoden i `IntentService` som är registrerad för att ta emot Android-geofence-händelser

```java
public class GeofenceTransitionsIntentService extends IntentService {

    public GeofenceTransitionsIntentService() {
        super("GeofenceTransitionsIntentService");
    }

    protected void onHandleIntent(Intent intent) {
        GeofencingEvent geofencingEvent = GeofencingEvent.fromIntent(intent);
        // Call the Places API to process information
        Places.processGeofenceEvent(geofencingEvent);
    }
}
```

## Hämta närliggande intressepunkter

Returnerar en ordnad lista med närliggande POI:er i ett återanrop. En överlagrad version av den här metoden returnerar en felkod om något gick fel med det resulterande nätverksanropet.

### GetNearbyPointsOfInterest (Android)

Här är syntaxen för den här metoden:

**Syntax**

```java
public static void getNearbyPointsOfInterest(final Location location, final int limit,
                                             final AdobeCallback<List<PlacesPOI>> callback);

public static void getNearbyPointsOfInterest(final Location location, final int limit,
                                             final AdobeCallback<List<PlacesPOI>> callback,
                                             final AdobeCallback<PlacesRequestError> errorCallback);
```

**Exempel**

Här är kodexemplet för den här metoden:

```java
// getNearbyPointsOfInterest without an error callback
Places.getNearbyPointsOfInterest(currentLocation, 10, new AdobeCallback<List<PlacesPOI>>() {
    @Override
    public void call(List<PlacesPOI> pois) {
        // do required processing with the returned nearbyPoi array
        startMonitoringPois(pois);
    }
});

// getNearbyPointsOfInterest with an error callback
Places.getNearbyPointsOfInterest(currentLocation, 10,
    new AdobeCallback<List<PlacesPOI>>() {
        @Override
        public void call(List<PlacesPOI> pois) {
            // do required processing with the returned nearbyPoi array
            startMonitoringPois(pois);
        }
    }, new AdobeCallback<PlacesRequestError>() {
        @Override
        public void call(PlacesRequestError placesRequestError) {
            // look for the placesRequestError and handle the error accordingly
            handleError(placesRequestError);
        }
    }
);
```

### GetNearbyPointsOfInterest (iOS)

**Syntax**

```objectivec
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi)) callback;

+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi)) callback
                     errorCallback: (nullable void (^) (ACPPlacesRequestError result)) errorCallback;
```

**Exempel**

```objectivec
// getNearbyPointsOfInterest without an error callback
[ACPPlaces getNearbyPointsOfInterest:location
                               limit:10     
                            callback:^(NSArray<ACPPlacesPoi*>* nearbyPoi) {
    // do required processing with the returned nearbyPoi array
    [self startMonitoringPois:nearbyPOI];
}];

// getNearbyPointsOfInterest with an error callback
[ACPPlaces getNearbyPointsOfInterest:location limit:10
    callback:^(NSArray<ACPPlacesPoi *> * _Nullable nearbyPoi) {
        // do required processing with the returned nearbyPoi array
        [self startMonitoringPois:nearbyPOI];
    } errorCallback:^(ACPPlacesRequestError result) {
        // look for the error and handle accordingly
        [self handleError:result];
    }
];
```

## Hämta aktuella intressanta enhetspunkter

Begär en lista över POI:er där enheten för närvarande är känd och returnerar dem i ett återanrop.

### GetCurrentPointsOfInterest (Android)

Här är syntaxen för den här metoden:

**Syntax**

```java
public static void getCurrentPointsOfInterest(final AdobeCallback<List<PlacesPOI>> callback);
```

**Exempel**

Här är kodexemplet för den här metoden:

```java
Places.getCurrentPointsOfInterest(new AdobeCallback<List<PlacesPOI>>() {
    @Override
    public void call(List<PlacesPOI> pois) {
        // use the obtained POIs that the device is within
        processUserWithinPois(pois);        
    }
});
```

### GetCurrentPointsOfInterest (iOS)

**Syntax**

Här är syntaxen för den här metoden:

```objectivec
+ (void) getCurrentPointsOfInterest: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable userWithinPoi)) callback;
```

**Exempel**

Här är kodexemplet för den här metoden:

```objectivec
[ACPPlaces getCurrentPointsOfInterest:^(NSArray<ACPPlacesPoi*>* userWithinPoi) {
    // do required processing with the returned userWithinPoi array
    [self processUserWithinPois:userWithinPoi];
}];
```


## Hämta enhetens plats

Begär platsen för enheten, som tidigare kallats, av tillägget Platser.

>[!TIP]
>
>Tillägget Platser känner bara till platser som det har fått via anrop till `GetNearbyPointsOfInterest`.


### GetLastKnownLocation (Android)

**Syntax**

Här är syntaxen för den här metoden:

```java
public static void getLastKnownLocation(final AdobeCallback<Location> callback);
```

**Exempel**

Här är kodexemplet för den här metoden:

```java
Places.getLastKnownLocation(new AdobeCallback<Location>() {
    @Override
    public void call(Location lastLocation) {
        // do something with the last known location
        processLastKnownLocation(lastLocation);        
    }
});
```

### GetLastKnownLocation (iOS)

**Syntax**

Här är syntaxen för den här metoden:

```objectivec
+ (void) getLastKnownLocation: (nullable void (^) (CLLocation* _Nullable lastLocation)) callback;
```

**Exempel**

Här är kodexemplet för den här metoden:

```objectivec
[ACPPlaces getLastKnownLocation:^(CLLocation* lastLocation) {
    // do something with the last known location
    [self processLastKnownLocation:lastLocation];
}];
```

## Rensa data på klientsidan


### Rensa (Android)

Tar bort klientdata för tillägget Platser i det delade läget, den lokala lagringen och i minnet.

**Syntax**

Här är syntaxen för den här metoden:

```java
public static void clear();
```

**Exempel**

Här är kodexemplet för den här metoden:

```java
Places.clear();
```

### clear (iOS)

Tar bort klientdata för tillägget Platser i delat läge, lokalt lagringsutrymme och i minnet.

**Syntax**

Här är syntaxen för den här metoden:

```objectivec
+ (void) clear;
```

**Exempel**

Här är kodexemplet för den här metoden:

```objectivec
[ACPPlaces clear];
```

## Ange auktoriseringsstatus för plats

### setAuthorizationStatus (Android)

*Tillgänglig från och med Plats v1.4.0*

Anger auktoriseringsstatus i tillägget Platser.

Den angivna statusen lagras i läget Platser delad och är endast avsedd som referens.
Anrop till den här metoden påverkar inte enhetens faktiska platsauktoriseringsstatus.

**Syntax**

Här är syntaxen för den här metoden:

```java
public static void setAuthorizationStatus(final PlacesAuthorizationStatus status);
```

**Exempel**

Här är kodexemplet för den här metoden:

```java
Places.setAuthorizationStatus(PlacesAuthorizationStatus.ALWAYS);
```

### setAuthorizationStatus (iOS)

*Tillgänglig från och med ACPlaces v1.3.0*

Anger auktoriseringsstatus i tillägget Platser.

Den angivna statusen lagras i läget Platser delad och är endast avsedd som referens.
Anrop till den här metoden påverkar inte enhetens faktiska platsauktoriseringsstatus.

När enhetens auktoriseringsstatus ändras `locationManager:didChangeAuthorizationStatus:` anropas metoden `CLLocationManagerDelegate` . I den här metoden bör du skicka det nya `CLAuthorizationStatus` värdet till ACPlaces- `setAuthorizationStatus:` API:t.

**Syntax**

Här är syntaxen för den här metoden:

```objectivec
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```

**Exempel**

Här är kodexemplet för den här metoden:

```objectivec
- (void) locationManager: (CLLocationManager*) manager didChangeAuthorizationStatus: (CLAuthorizationStatus) status {    
    [ACPPlaces setAuthorizationStatus:status];
}
```
