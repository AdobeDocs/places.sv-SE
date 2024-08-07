---
title: API-referens för platser
description: Information om API-referenserna i Platser.
feature: Mobile SDK
exl-id: ce1a113c-dee0-49df-8d2f-789ccc1c8322
source-git-commit: f521d5e3b0b69977877d88382ce41fcb7d1c54b9
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 29%

---

# API-referens för platser {#places-api-reference}

Här är information om API-referenserna i tillägget Platser:

## Bearbeta en regionhändelse

När en enhet korsar en av dina apps fördefinierade gränser för platstjänster, skickas regionen och händelsetypen till SDK för bearbetning.

### ProcessGeofence (Android)

Bearbeta en `Geofence`-regionhändelse för angiven `transitionType`.

Skicka `transitionType` från `GeofencingEvent.getGeofenceTransition()`. För närvarande stöds `Geofence.GEOFENCE_TRANSITION_ENTER` och `Geofence.GEOFENCE_TRANSITION_EXIT`.

**Syntax**

Här är syntaxen för den här metoden:

```java
public static void processGeofence(final Geofence geofence, final int transitionType);
```

**Exempel**

Anropa den här metoden i din `IntentService` som är registrerad för att ta emot Android geofence-händelser.

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

Den här metoden ska anropas i `CLLocationManager`-delegaten, som anger om användaren har angett eller avslutat en viss region.

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

Bearbeta alla `Geofences` i `GeofencingEvent` samtidigt.

**Syntax**

```java
public static void processGeofenceEvent(final GeofencingEvent geofencingEvent);
```

**Exempel**

Anropa den här metoden i din `IntentService` som är registrerad för att ta emot Android geofence-händelser

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


## Hämta platsen för enheten

Begär platsen för enheten, som tidigare kallats, av tillägget Platser.

>[!TIP]
>
>Tillägget Platser känner bara till platser som har angetts till det via anrop till `GetNearbyPointsOfInterest`.


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

*Tillgängligt från och med Places v1.4.0*

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

När enhetens auktoriseringsstatus ändras anropas metoden `locationManager:didChangeAuthorizationStatus:` för `CLLocationManagerDelegate`. I den här metoden bör du skicka det nya `CLAuthorizationStatus`-värdet till ACPlaces `setAuthorizationStatus:` API.

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
