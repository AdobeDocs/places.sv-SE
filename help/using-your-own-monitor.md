---
title: Använda din egen skärm
description: Du kan också använda dina övervakningstjänster och integrera med Platstjänst genom att använda API:erna för Platstjänsttillägg.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b

---


# Använda din egen skärm {#using-your-monitor}

Du kan också använda dina övervakningstjänster och integrera med Platstjänst genom att använda API:erna för Platstillägg.

## Registrerar geofence

Om du bestämmer dig för att använda dina övervakningstjänster registrerar du geofences of the POIs runt din aktuella plats genom att utföra följande steg:

### iOS

I iOS utför du följande steg:

1. Skicka platsuppdateringarna som hämtades från Core location-tjänsterna för iOS till Platser-tillägget.

1. Använd API:t för `getNearbyPointsOfInterest` Platser-tillägg för att hämta arrayen med objekt runt den aktuella `ACPPlacesPoi` platsen.

   ```objective-c
   - (void) locationManager: (CLLocationManager*) manager didUpdateLocations: (NSArray<CLLocation*>*) locations {
       [ACPPlaces getNearbyPointsOfInterest:currentLocation limit:10 callback: ^ (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi) {
           [self startMonitoringGeoFences:nearbyPoi];
       }];
   }
   ```

1. Extrahera informationen från de hämtade `ACPPlacesPOI` objekten och börja övervaka dessa POI.

   ```objective-c
   - (void) startMonitoringGeoFences: (NSArray*) newGeoFences {
       // verify if the device supports monitoring geofences
       // check for location permission
   
       for (ACPPlacesPoi * currentRegion in newGeoFences) {
           // make the circular region
           CLLocationCoordinate2D center = CLLocationCoordinate2DMake(currentRegion.latitude, currentRegion.longitude);
           CLCircularRegion* currentCLRegion = [[CLCircularRegion alloc] initWithCenter:center
                                                                                 radius:currentRegion.radius
                                                                             identifier:currentRegion.identifier];
           currentCLRegion.notifyOnExit = YES;
           currentCLRegion.notifyOnEntry = YES;
   
           // start monitoring the new region
           [_locationManager startMonitoringForRegion:currentCLRegion];
       }
   }
   ```

### Android

1. Skicka platsuppdateringar som hämtats från Google Play-tjänsterna eller Android-platstjänsterna till platstillägget.

1. Använd API:t för `getNearbyPointsOfInterest` Platser-tillägg för att få en lista över `PlacesPoi` objekt runt den aktuella platsen.

   ```java
   LocationCallback callback = new LocationCallback() {
       @Override
       public void onLocationResult(LocationResult locationResult) {
           super.onLocationResult(locationResult);
   
           Places.getNearbyPointsOfInterest(currentLocation, 10, new AdobeCallback<List<PlacesPOI>>() {
               @Override
               public void call(List<PlacesPOI> pois) {
                   starMonitoringGeofence(pois);
               }
           });
       }
   };
   ```

1. Extrahera data från de hämtade `PlacesPOI` objekten och börja övervaka dessa POI.

   ```java
   private void startMonitoringFences(final List<PlacesPOI> nearByPOIs) {
       // check for location permission
       for (PlacesPOI poi : nearByPOIs) {
           final Geofence fence = new Geofence.Builder()
               .setRequestId(poi.getIdentifier())
               .setCircularRegion(poi.getLatitude(), poi.getLongitude(), poi.getRadius())
               .setExpirationDuration(Geofence.NEVER_EXPIRE)
               .setTransitionTypes(Geofence.GEOFENCE_TRANSITION_ENTER |
                                   Geofence.GEOFENCE_TRANSITION_EXIT)
               .build();
           geofences.add(fence);
       }
   
       GeofencingRequest.Builder builder = new GeofencingRequest.Builder();
       builder.setInitialTrigger(GeofencingRequest.INITIAL_TRIGGER_ENTER);
       builder.addGeofences(geofences);
       builder.build();
       geofencingClient.addGeofences(builder.build(), geoFencePendingIntent)
   }
   ```


Anrop av API:t leder till ett nätverksanrop som hämtar platsen runt den aktuella platsen. `getNearbyPointsOfInterest`

>[!IMPORTANT]
>
>Du bör anropa API:t sparsamt eller endast när det finns en betydande platsändring av användaren.

## Publicera geofence-händelser

### iOS

I iOS anropar du `processGeofenceEvent` Places-API:t i `CLLocationManager` delegaten. Detta API meddelar dig om användaren har angivit eller avslutat en viss region.

```objective-c
- (void) locationManager:(CLLocationManager *)manager didEnterRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
}

- (void) locationManager:(CLLocationManager *)manager didExitRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeExit];
}
```

### Android

I Android anropar du `processGeofence` metoden tillsammans med lämplig övergångshändelse i Geofence-sändningsmottagaren. Du kanske vill strukturera listan över geofences som tagits emot för att förhindra dubblettposter/-utträden.

```java
void onGeofenceReceived(final Intent intent) {
    // do appropriate validation steps for the intent
    ...

    // get GeofencingEvent from intent
    GeofencingEvent geoEvent = GeofencingEvent.fromIntent(intent);

    // get the transition type (entry or exit)
    int transitionType = geoEvent.getGeofenceTransition();

    // validate your geoEvent and get the necessary Geofences from the list
    List<Geofence> myGeofences = geoEvent.getTriggeringGeofences();

    // process region events for your geofences
    for (Geofence geofence : myGeofences) {
        Places.processGeofence(geofence, transitionType);
    }
}
```
