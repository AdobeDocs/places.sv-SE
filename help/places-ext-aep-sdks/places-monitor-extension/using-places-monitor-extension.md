---
title: Använda tillägget Platsövervakare
description: Information om hur du installerar, konfigurerar och använder tillägget Platsövervakare.
translation-type: tm+mt
source-git-commit: ac1d410a676557064d5390f8392f402541754478

---


# Använda tillägget Platsövervakare {#using-places-monitor-extension}

Utför följande uppgifter om du vill använda tillägget Platsövervakare:

## Installera Places Monitor-tillägget i Experience Platform Launch

1. Klicka på fliken **[!UICONTROL Extensions]** i Experience Platform Launch.
1. Leta upp **[!UICONTROL Catalog]** tillägget på **[!UICONTROL Places Monitor]** fliken och klicka på **Installera**.
1. Klicka på **[!UICONTROL Save]**.
1. Uppdatera SDK-konfigurationen genom att följa publiceringsprocessen.

### Konfigurera tillägget Platsövervakare {#configure-places-monitor-extension}

Det finns inga konfigurationsåtgärder för tillägget Platsövervakare.

![konfigurera ‌ Platsövervakaren](/help/assets/configure_places_monitor.png)

## Lägg till tillägget Platsövervakare i din app {#add-monitor-extension-to-app}

Du måste lägga till tillägget Platsövervakare i Android- eller iOS-appen.

### Android

I Android utför du följande steg:

#### Java

1. Lägg till Places Monitor-tillägget och Places-tillägget i ditt projekt med programmets övertoningsfil.

1. Inkludera även de senaste Google Location-tjänsterna i övertoningsfilen.

   ```java
   implementation 'com.adobe.marketing.mobile:places:1.+'
   implementation 'com.adobe.marketing.mobile:places-monitor:1.+'
   implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
   implementation 'com.google.android.gms:play-services-location:16.0.0'
   ```

1. Importera tillägget Platsövervakare i programmets huvudaktivitet.

   ```java
   import com.adobe.marketing.mobile.PlacesMonitor;
   ```

### iOS

I iOS utför du följande steg:

1. Lägg till biblioteket i ditt projekt via dina Cocopods `Podfile` genom att lägga till `pod 'ACPPlacesMonitor'`.
1. Importera bibliotek för Platser och Platsövervakare:

#### Mål-C

```objectivec
#import "ACPCore.h"
#import "ACPPlaces.h"
#import "ACPPlacesMonitor.h"
```

#### Swift

```swift
import ACPCore
import ACPPlaces
import ACPPlacesMonitor
```


## Registrera och starta Platsövervakaren {#register-start-places-monitor}

Du måste registrera och starta Platsövervakaren i Android eller iOS.

## Android

I Android utför du följande steg:

### Java

Registrera Places Monitor-tilläggen i appens `OnCreate` metod:

```java
public class MobileApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.ConfigureWithAppId("yourAppId");
        try {
            PlacesMonitor.registerExtension(); //Register PlacesMonitor with Mobile Core
            Places.registerExtension(); //Register Places with Mobile Core
            MobileCore.start(null);
            PlacesMonitor.start();//Start monitoring the geo-fences
        } catch (Exception e) {
            //Log the exception
        }
    }
}
```

>[!IMPORTANT]
>
>Platsövervakning beror på Platstillägg. När du installerar tillägget Platsövervakare manuellt måste du också lägga till biblioteket `places.aar` i projektet.

## iOS

I iOS-appen`application:didFinishLaunchingWithOptions`registrerar du dig `PlacesMonitor` och placerar med Mobile Core:

### Mål-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions {
    [ACPCore configureWithAppId:@"yourAppId"];
    [ACPPlaces registerExtension];
    [ACPPlacesMonitor registerExtension];
    [ACPCore start:^{            
        // do other initialization required for the SDK
        [ACPPlacesMonitor start];
    }];

    return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    ACPCore.configure(withAppId: "yourAppId")
    ACPPlaces.registerExtension()       
    ACPPlacesMonitor.registerExtension()
    ACPCore.start({
        // do other initialization required for the SDK
        ACPPlacesMonitor.start()
    })

    // Override point for customization after application launch.        
    return true
}
```

>[!IMPORTANT]
>
>Platsövervakning beror på Platstillägg. When manually installing the Places Monitor extension, ensure that you also add the `libACPPlaces_iOS.a` library to your project.


## Lägg till behörigheter i manifestet

### Android

**Java**

För alla versioner av Android anger du att din app behöver platsbehörighet genom att lägga till ett `<uses-permission>` element i appmanifestet som underordnat det översta `<manifest>` elementet. För Android-program som har API Level 29 och senare, och som vill tillåta programmet att få åtkomst till platsen i bakgrunden, inkluderar du behörigheten ACCESS_BACKGROUND_LOCATION.

```java
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.adobe.placesapp">
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    // Only for Android apps targeting API level 29 and above
  <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
  <application>        
    ...    
  </application>
</manifest>
```


## Aktivera platsuppdateringar i bakgrunden {#enable-location-updates-background}

iOS stöder leverans av platshändelser till appar som är inaktiverade eller inte längre körs. Om du vill få platsuppdateringar i bakgrunden för Platsövervakartillägget konfigurerar du funktionen för platsuppdateringar för appen i `Xcode.background-location-updates`.

![med hjälp av Platsövervakaren](/help/assets/using-the-places-monitor_1.png)

## Konfigurera plist-nycklarna

Följande nycklar måste inkluderas i appens `Info.plist` fil:

* `NSLocationWhenInUseUsageDescription` - texten ska beskriva varför appen begär åtkomst till användarens platsinformation när den körs i förgrunden.
* `NSLocationAlwaysAndWhenInUseUsageDescription` - texten ska alltid beskriva varför appen begär åtkomst till användarens platsinformation.

>[!TIP]
>
>Om din app har stöd för iOS 10 och tidigare, `NSLocationAlwaysUsageDescription` krävs även nyckeln.

![](/help/assets/using-the-places-monitor_2.png)
