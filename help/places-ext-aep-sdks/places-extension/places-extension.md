---
title: Tillägget Platser
description: Med tillägget Platser kan du agera utifrån platsen för dina användare.
translation-type: tm+mt
source-git-commit: a7dddb78e1e00a0bde01ea668334932759a9dae8
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 3%

---


# Tillägget Platser {#places-extension}

Med tillägget Platser kan du agera utifrån platsen för dina användare. Det här tillägget är gränssnittet till API:erna för platstjänster för frågetjänster. Genom att avlyssna händelser som innehåller GPS-koordinater och händelser för geofence-regioner skickar det här tillägget nya händelser som bearbetas av regelmotorn. Tillägget Platser hämtar och levererar även en lista över närmaste POI för appdata som hämtas från API:erna. De regioner som returneras av API:erna lagras i cache och beständighet, vilket tillåter begränsad offlinebearbetning.

## Installera tillägget Platser i Adobe Experience Platform Launch

1. Klicka på fliken **[!UICONTROL Extensions]** i Experience Platform Launch.
1. Leta upp **[!UICONTROL Catalog]** tillägget på **[!UICONTROL Places]** fliken och klicka på **[!UICONTROL Install]**.
1. Markera de platsbibliotek som du vill använda i den här egenskapen. Det här är de bibliotek som kommer att vara tillgängliga i din app.
1. Klicka på **[!UICONTROL Save]**.

   När du klickar **[!UICONTROL Save]** söker Experience Platform SDK efter POI i de bibliotek som du har valt. POI-data inkluderas inte i hämtningen av biblioteket när du skapar appen, men en platsbaserad delmängd av POI hämtas till slutanvändarens enhet under körningen och baseras på användarens GPS-koordinater.

1. Slutför publiceringsprocessen för att uppdatera SDK-konfigurationen.

   Mer information om publicering i Experience Platform Launch finns i [Publicera](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html).

### Konfigurera tillägget Platser {#configure-places-extension}

![](//help/assets/places-extension.png)

## Lägg till tillägget Platser i din app {#add-places-to-app}

Du kan lägga till tillägget Platser i dina Android- och iOS-appar. Stegen för att lägga till platser i iOS- eller Android-program visas nedan. Platstillägg är också tillgängliga för följande plattformar nedan. Om du vill lägga till platser i programmet när du utvecklar med någon av de här plattformarna läser du följande länkar:

**[Cordova Places Plugin](https://github.com/adobe/cordova-acpplaces/blob/master/README.md)**

**[Plugin-programmet React Native Places](https://github.com/adobe/react-native-acpplaces/blob/master/README.md)**

**[Plugin-programmet Flutter Places](https://github.com/adobe/flutter-acpplaces_monitor)**

**[Plugin-programmet Xamarin Places](https://github.com/adobe/xamarin-acpcore)**


### Android

Så här lägger du till tillägget Platser i ditt program med Java:

1. Lägg till tillägget Platser i ditt projekt med programmets övertoningsfil.

   ```java
   implementation 'com.adobe.marketing.mobile:places:1.+'
   implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
   ```

1. Importera tillägget Platser i programmets huvudaktivitet.

   ```java
   import com.adobe.marketing.mobile.Places;
   ```


### iOS

Så här lägger du till platstillägg i appen med Mål-C eller Skift:

1. Lägg till platserna och [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) -biblioteken i ditt projekt. Du måste lägga till följande punkter `Podfile`:

   ```objective-c
   pod 'ACPPlaces', '~> 1.0'
   pod 'ACPCore', '~> 2.0'    # minimum Core version for Places is 2.0.3
   ```

   Om du inte använder Cocopods kan du även inkludera Mobile Core och Places-biblioteken manuellt från vår [releasesida](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/) på Github.

1. Uppdatera dina Cocopods:

   ```objective-c
   pod update
   ```

1. Öppna Xcode, och i klassen AppDelegate importerar du rubrikerna Core och Places:

   **Mål-C**

   ```objective-c
   #import "ACPCore.h"
   #import "ACPPlaces.h"
   ```

   **Swift**

   ```swift
   import ACPCore
   import ACPPlaces
   ```

### Registrera tillägget Platser med Mobile Core {#register-places-mobile-core}

Du måste registrera Platser-tillägget med Mobile Core i Android och iOS.

#### Android

Registrera platstilläggen i appens `OnCreate` metod:

```java
public class PlacesTestApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);

        try {
            Places.registerExtension();
            MobileCore.start(null);
        } catch (Exception e) {
            Log.e("PlacesTestApp", e.getMessage());
        }
    }
}
```

#### iOS

Registrera tillägget Platser med dina andra SDK-registreringsanrop i appens `application:didFinishLaunchingWithOptions:` metod:

**Mål-C**

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // make other sdk registration calls
    [ACPPlaces registerExtension];    
    return YES;
}
```

**Swift**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // make other sdk registration calls
    ACPPlaces.registerExtension();
    return true;
}
```

### Ändra plats för medlemskap från tid till publicering {#places-ttl}

Platsdata kan snabbt bli inaktuella, särskilt om enheten inte tar emot bakgrundsuppdateringar.

Styr tiden för live-visning för platsmedlemskapsdata på enheten genom att ange `places.membershipttl` konfigurationsinställningen. Värdet som skickas representerar antalet sekunder som platsläget förblir giltigt för enheten.

#### Android

Inuti återanropet för att `MobileCore.start()` uppdatera konfigurationen med nödvändiga ändringar innan anrop görs `lifecycleStart`:

```java
public class PlacesTestApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);

        try {
            Places.registerExtension();
            MobileCore.start(new AdobeCallback() {
                @Override
                public void call(Object o) {
                    // switch to your App ID from Launch
                    MobileCore.configureWithAppID("my-app-id");

                    final Map<String, Object> config = new HashMap<>();
                    config.put("places.membershipttl", 30);
                    MobileCore.updateConfiguration(config);

                    MobileCore.lifecycleStart(null);
                }
            });
        } catch (Exception e) {
            Log.e("PlacesTestApp", e.getMessage());
        }
    }
}
```

#### iOS

På den första raden i callback-funktionen för `ACPCore`&#39;s `start:` method anropar du `updateConfiguration:`

**Mål-C**

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // make other sdk registration calls

    const UIApplicationState appState = application.applicationState;
    [ACPCore start:^{
        [ACPCore updateConfiguration:@{@"places.membershipttl":@(30)}];

        if (appState != UIApplicationStateBackground) {
            [ACPCore lifecycleStart:nil];            
        }
    }];

    return YES;
}
```

**Swift**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // make other sdk registration calls

    let appState = application.applicationState;            
    ACPCore.start {
        ACPCore.updateConfiguration(["places.membershipttl" : 30])

        if appState != .background {
            ACPCore.lifecycleStart(nil)
        }    
    }

    return true;
}
```

## Konfigurationsnycklar

Om du vill uppdatera SDK-konfigurationen programmatiskt vid körning använder du följande information för att ändra platsens tilläggskonfigurationsvärden. Mer information finns i [Configuration API Reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| Nyckel | Obligatoriskt | Beskrivning |
| :--- | :--- | :--- |
| `places.libraries` | Ja | Platstilläggsbiblioteken för mobilappen. Den anger biblioteks-ID och namnet på biblioteket som mobilappen stöder. |
| `places.endpoint` | Ja | Standardslutpunkten för platstjänster, som används för att hämta information om bibliotek och POI. |
| `places.membershipttl` | Nej | Standardvärdet är 3 600 (sekunder i en timme). Anger hur länge, i sekunder, information om platshållarmedlemskap för enheten ska vara giltig. |
