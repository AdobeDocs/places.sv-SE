---
title: API-referens för platsövervakare
description: En lista över API:er för Platsövervakaren.
translation-type: tm+mt
source-git-commit: 5a21e734c0ef56c815389a9f08b445bedaae557a

---


# API-referens för platsövervakare {#places-api-reference}

## Registrera Places Monitor-tillägg

Registrerar tillägget Platsövervakare med Core Event Hub.

### RegisterExtension (Android)

Här är syntaxen och exempelkoden för detta API:

#### Syntax

Här är syntaxen i Java:

```java
public static void registerExtension();
```

#### Exempel

Anropa den här metoden i den `onCreate` metod där du initierar resten av Experience Platform SDK.

```java
public class MobileApp extends Application {
  @Override
  public void onCreate(){
     super.onCreate();
     MobileCore.setApplication(this);
     try {
        PlacesMonitor.registerExtension();
     } catch (Exception e) {
       //Log the exception
       }
    }
 }
```

### RegisterExtension (iOS)

Här är syntaxen och exempelkoden för detta API:

#### Syntax

Här är syntaxen i mål C:

```objective-c
+ (void) registerExtension;
```

#### Exempel

Den här metoden ska anropas i metoden `didFinishLaunchingWithOptions` delegate för `AppDelegate`.

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [ACPCore configureWithAppId:@"launch-appID"];    
    [ACPPlaces registerExtension];    
    [ACPPlacesMonitor registerExtension];

    [ACPCore start:^{
        // do other initialization of the SDK
    }];

    return YES;
}
```

## Tilläggsversion

Returnerar den aktuella versionen av tillägget Platsövervakare

### ExtensionVersion (Android)

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```java
public static String extensionVersion();
```

#### Exempel

```java
String placesMonitorVersion = PlacesMonitor.extensionVersion();
```

### ExtensionVersion (iOS)

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```objective-c
+ (nonnull NSString*) extensionVersion;
```

#### Exempel

```objective-c
NSString *placesMonitorVersion = [ACPPlacesMonitor extensionVersion];
```

## Starta enhetsövervakning

Börja spåra enhetens plats och övervaka närliggande platser.

### Start (Android)

Om användaren inte har gett behörighet att använda enhetsplatsen uppmanas användaren att ange behörighet vid det första anropet till `start` API:t.

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```java
public static void start();
```

#### Exempel

```java
PlacesMonitor.start();
```

### Start (iOS)

>[!IMPORTANT]
>
>För att kunna börja övervaka måste platstjänsten ha nödvändig behörighet:
>
>* Om auktoriseringen för platstjänsten inte har angetts för programmet begär det första anropet till `start` API behörigheten att använda platstjänsten som konfigurerats för programmet.
>* Beroende på enhetens funktioner spårar Platsövervakaren användarens plats baserat på den aktuella inställningen `ACPPlacesMonitorMode`om behörighet har angetts. Bildskärmen använder som standard `ACPPlacesMonitorModeSignificantChanges`.


>[!CAUTION]
>
>Om ditt anrop om att starta övervakning görs innan SDK har slutfört initieringen kanske det ignoreras.

Du kan se till att SDK har slutfört initieringen genom att anropa `start` från det återanrop som finns till `ACPCore::start:`.

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```objectivec
+ (void) start;
```

#### Exempel

Startar Platsövervakaren när SDK initieras:

```objective-c
[ACPCore start:^{
    [ACPPlacesMonitor start];
}];
```

Starta Platsövervakaren senare i programkörningen:

```objective-c
[ACPPlacesMonitor start];
```

## Stoppa enhetsövervakning

Stoppar spårning av enhetens plats.

### Stoppa (Android)

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```java
public static void stop();
```

#### Exempel

```java
PlacesMonitor.stop();
```

### Stoppa (iOS)

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```objectivec
+ (void) stop;
```

#### Exempel

```objective-c
[ACPPlacesMonitor stop];
```

## Uppdatera plats

Använd detta API för att få en omedelbar uppdatering på enhetens plats. När du anropar denna API försöker enheten att fastställa platsen med den noggrannhetsnivå som du har angett. Den här processen uppdaterar även närliggande POI som övervakas av tillägget.

### UpdateLocation (Android)

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```java
public static void updateLocation();
```

#### Exempel

```java
PlacesMonitor.updateLocation();
```

### UpdateLocationNow (iOS)

#### Syntax

```objective-c
+ (void) updateLocationNow;
```

#### Exempel

```objective-c
[ACPPlacesMonitor updateLocationNow];
```

## Programplatsbehörighet

Du kan använda det här API:t för att ange vilken typ av platsbehörighet som användaren uppmanas att ange och har behörighet att använda för platstjänsten.

### SetLocationPermission (Android)

Detta API anger vilken typ av platsbehörighetsbegäran som användaren uppmanas att välja för.

>[!TIP]
>
>Detta API gäller endast för enheter som finns på Android 10 och senare.
>
>Om du vill ange att rätt autentiseringsfråga ska visas för användaren anropar du detta API före `PlacesMonitor.start()`. Om du anropar den här metoden, samtidigt som du aktivt övervakar, uppgraderas platsens behörighetsnivå till det begärda behörighetsvärdet. Om den begärda åtkomstnivån redan har angetts eller nekats av programanvändaren, eller om du försöker nedgradera behörigheten från `ALWAYS_ALLOW` till `WHILE_USING_APP`, har den här metoden ingen effekt.

Platsbehörigheten kan anges till ett av följande värden:

* `PlacesMonitorLocationPermission.WHILE_USING_APP`

   Det här värdet uppmanar användaren att bara få åtkomst till enhetsplatsen när programmet används. Ett program anses vara i bruk när användaren tittar på programmet på enhetens skärm, till exempel när en aktivitet körs i förgrunden.

   >[!TIP]
   >
   >Kontrollera att användarbehörigheten ACCESS_FINE_LOCATION är angiven i programmets manifestfil.

* `PlacesMonitorLocationPermission.ALWAYS_ALLOW`

   Det här värdet uppmanar användaren att komma åt enhetens plats även när programmet är bakgrundsbelagt.

   >[!TIP]
   >
   >Kontrollera att användarbehörigheterna ACCESS_BACKGROUND_LOCATION och ACCESS_FINE_LOCATION är angivna i programmets manifestfil.

   `PlacesMonitorLocationPermission.ALWAYS_ALLOW` är standardvärdet för platsbehörighet.

>[!IMPORTANT]
>
>Om appanvändaren beviljas `WHILE_USING_APP` behörigheten registreras inte geofences i operativsystemet. Det innebär att tillägget Platsövervakare inte kommer att utlösa in-/utträdeshändelser i områden som inträffar i bakgrunden.

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```java
public static void setLocationPermission(final PlacesMonitorLocationPermission placesMonitorLocationPermission)
```

#### Exempel

Så här begär du `WHILE_USING_APP` behörighet:

```java
// set the location permission
PlacesMonitor.setLocationPermission(PlacesMonitorLocationPermission.WHILE_USING_APP);
// start monitoring
PlacesMonitor.start()
```

Så här uppgraderar du till `ALWAYS_ALLOW` behörighet:

```java
// upgrade the permission level
PlacesMonitor.setLocationPermission(PlacesMonitorLocationPermission.ALWAYS_ALLOW);
```

### SetRequestAuthorizationLevel (iOS)

Detta API anger vilken typ av platsauktoriseringsbegäran som användaren uppmanas att göra.

Om du vill att rätt auktoriseringsprompt ska visas för användaren, ringer du `SetRequestAuthorizationLevel` innan du ringer `[ACPPlacesMonitor start]`. Om du vill ange att rätt autentiseringsfråga ska visas för användaren anropar du detta API före `[ACPPlacesMonitor start]`. Om du anropar den här metoden medan du aktivt övervakar, uppgraderas positionsauktoriseringsnivån till det begärda auktoriseringsvärdet. Om den begärda åtkomstnivån antingen redan tillhandahålls eller nekas av programanvändaren eller om det finns en nedgradering av behörigheten från `ACPPlacesRequestAuthorizationLevelAlways` till `ACPPlacesRequestAuthorizationLevelWhenInUse` auktorisering, har den här metoden ingen effekt.

Auktoriseringsnivån kan anges till ett av följande värden:

* `ACPPlacesRequestAuthorizationLevelWhenInUse`

   Begär användarens behörighet att använda platstjänsten när appen används. Användarprompten innehåller texten från nyckeln i filen Info.plist i programmet, och den nyckeln måste finnas när du anropar den här metoden. `NSLocationWhenInUseUsageDescription` Mer information finns i [Apples dokumentation om requestWhenInUseAuthorization](https://developer.apple.com/documentation/corelocation/cllocationmanager/1620562-requestwheninuseauthorization).

* `ACPPlacesRequestMonitorAuthorizationLevelAlways`

   Använd denna uppräkning för att begära Platstjänst även när appen finns i bakgrunden. Du måste ha knapparna `NSLocationAlwaysUsageDescription` och `NSLocationWhenInUseUsageDescription` i Info.plist för programmet. Dessa tangenter definierar den text som ska visas när användaren tillfrågas. Mer information finns i [Apples dokumentation om requestAlwaysAuthorization](https://developer.apple.com/documentation/corelocation/cllocationmanager/1620551-requestalwaysauthorization).

`ACPPlacesRequestAuthorizationLevelAlways` är standardvärdet för auktorisering av begäran.

>[!IMPORTANT]
>
>Programmet som godkände användningen av `ACPPlacesRequestAuthorizationLevelWhenInUse` behörigheten kommer inte att utlösa in-/utträdeshändelser i regioner som sker i bakgrunden.

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```objective-c
+ (void) setRequestAuthorizationLevel: (ACPPlacesRequestAuthorizationLevel) requestAuthorizationLevel;
```

#### Exempel

Så här begär du `ACPPlacesRequestAuthorizationLevelWhenInUse` behörighet:

```objective-c
// set the request authorization level
[ACPPlacesMonitor setRequestAuthorizationLevel: ACPPlacesRequestAuthorizationLevelWhenInUse];
// start monitoring
[ACPPlacesMonitor start];
```

Så här uppgraderar du till `ACPPlacesRequestAuthorizationLevelAlways` auktorisering:

```objective-c
// set the request authorization level
[ACPPlacesMonitor setRequestAuthorizationLevel: ACPPlacesRequestAuthorizationLevelAlways];
```

## Övervakningsläge (endast iOS)

Övervakning kan anges med något av följande värden:

* `ACPPlacesMonitorModeContinuous`

   Övervakningstillägget tar emot och bearbetar platser oftare. Denna övervakningsstrategi förbrukar mycket kraft men ger större precision. Mer information finns i [Apples dokumentation om kontinuerlig övervakning](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423750-startupdatinglocation).

* `ACPPlacesMonitorModeSignificantChanges`

   Övervakningstillägget tar endast emot och bearbetar platsuppdateringar efter att enheten har flyttat ett betydande avstånd från den tidigare bearbetade platsen. Denna övervakningsstrategi förbrukar mindre ström än den kontinuerliga övervakningsstrategin. Mer information finns i [Apples dokumentation om betydande övervakning](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423531-startmonitoringsignificantlocati)

### SetPlacesMonitorMode (iOS)

Här är syntaxen och exempelkoden för detta API:

#### Syntax

```objective-c
+ (void) setPlacesMonitorMode: (ACPPlacesMonitorMode) monitorMode;
```

#### Exempel

```objective-c
[ACPPlacesMonitor setPlacesMonitorMode:ACPPlacesMonitorModeSignificantChanges];
```
