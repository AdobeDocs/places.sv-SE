---
title: Testa och validera platstjänst
description: I det här avsnittet finns information om hur du kan testa och validera platstjänsten.
translation-type: tm+mt
source-git-commit: 5a21e734c0ef56c815389a9f08b445bedaae557a

---


# Rekommendationer för att testa platstjänst {#test-validate-loc-svc}

Många kunder och organisationer kommer att definiera POI över hela världen, så det är viktigt att ha ett sätt att simulera och testa hur Platstjänsten interagerar med ditt program. Den här informationen hjälper dig att förstå hur du testar och validerar de platsserviceposter och utgångar som utlöses korrekt utifrån definierade POI:er och användarens aktuella plats.

Eftersom miljövariabler kan vara en faktor för platssignal och precision rekommenderar vi att du först fastställer baslinjeresultat genom att arbeta lokalt med utvecklingsverktyg och simulerade platsposter. Målet är att validera att alla platshändelser fungerar som de ska. När platshändelserna har validerats på rätt sätt kan lösningsintegreringar (till exempel Analytics, Target och Campaign) testas. För att underlätta testningen bör du konfigurera Slack Webhooks med återanslående och läsa in GPX-filer i din egen utvecklingsmiljö.

>[!IMPORTANT]
>
>I den här planen förutsätts att POI har skapats i användargränssnittet för [platstjänsten](https://places.adobe.com) och att de senaste versionerna av Places-tillägget och Platsövervakaren är installerade och korrekt konfigurerade. Mer information finns i [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md) och [Platsmonitortillägg](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md).

| Steg | Beskrivning | Förväntat resultat |
|--- |--- |--- |
| 1 | Bekräfta att rätt manifestnycklar har angetts för Android för att ge åtkomst till spårplatsen. Mer information finns i [Lägga till behörigheter i manifestet](https://docs.adobe.com/content/help/en/places/using/places-ext-aep-sdks/places-monitor-extension/using-places-monitor-extension.html#add-permissions-to-the-manifest). | Bekräftat |
| 1a | Bekräfta att platsuppdateringar har konfigurerats i iOS. Se även till att du har rätt plist-nycklar inställda i iOS för att begära användarbehörighet för att spåra platsen. Mer information finns i [Aktivera platsuppdateringar i bakgrunden.](https://docs.adobe.com/content/help/en/places/using/places-ext-aep-sdks/places-monitor-extension/using-places-monitor-extension.html#enable-location-updates-background) | Bekräftat |
| 2 | Bekräfta vilket övervakningsläge som är inställt för iOS. I det kontinuerliga läget får du större precision och beständighet men också större batteritid. Mer information finns i [Övervakningsläge (endast iOS).](https://docs.adobe.com/content/help/en/places/using/places-ext-aep-sdks/places-monitor-extension/places-monitor-api-reference.html#monitoring-mode-ios-only) | Betydande ändringar eller kontinuerlig |
| 3 | Om du använder mer än ett POI-bibliotek ska du kontrollera att rätt bibliotek har valts i platstillägget för Experience Platform Launch. | Bekräftat |
| 4 | Bekräfta att de senaste versionerna av tilläggen Mobile Core och Places/Places Monitor har paketerats med appen via Gradle eller CocoaPods. | Bekräftat - mer information om de senaste uppdateringarna finns i [versionsinformationen.](/help/release-notes.md) |
| 5 | Bekräfta att rätt miljöer är konfigurerade för testning. ID:t för startmiljön ska överensstämma med utvecklingsmiljön för Launch. | Bekräftat |
| 6 | Skapa GPX-filer för varje POI som du vill testa. GPX-filer kan användas i lokal utvecklingsmiljö för att simulera en platspost. Mer information om hur du skapar och använder GPX-filer finns i: <br>[GPX-filer för iOS-simulator [stängd]](https://stackoverflow.com/questions/17292783/gpx-files-for-ios-simulator)<br>[https://mapstogpx.com/mobiledev.](https://mapstogpx.com/mobiledev.php)<br>[phpLOCATION TESTING IN MOBILE APPS](https://qacumtester.wordpress.com/2014/02/27/location-testing-in-mobile-apps/) | GPX-filer skapas och läses in i programprojektet. |
| 7 | Utan att göra något annat bör du kunna starta programmet från Android Studio eller XCode och se lämplig varning för att begära åtkomst för spårningsplatsen. Klicka på *Tillåt* alltid behörighet.<br><br>Vi rekommenderar att du använder en riktig enhet som är ansluten till datorn i stället för att använda enhetssimulatorn. | Platsförfrågan ska visas när programmet läses in via IDE |
| 8 | När platsbehörigheten har godkänts. Platser-SDK hämtar enhetens aktuella plats och platsövervakartillägget börjar övervaka de 20 närmaste POI:erna från den aktuella platsen | Se loggexemplet under tabellen. |
| 9 | Om du växlar mellan olika platser i XCode- eller Android-studion bör du skapa ingångshändelser för specifika POI. nedanstående loggar förväntas vid inträde i en POI. | Se loggexemplet under tabellen. |
| 10 | När du ser att Platsövervakaren hittar närliggande POI bör du testa genom att skicka ut platspunkter. I Launch skapar du en ny regel som använder Platser-tillägget för att utlösa baserat på en geo-fence-post. Skapa sedan en ny åtgärd genom att använda Mobile Core för att skicka en återanslående. Genom att skapa en Slack Webkroks-app kan du se platsposter och utgångar. Mer information om hur du skapar en Slack Webkroch-app finns i [Skicka meddelanden med inkommande webbhooks.](https://api.slack.com/messaging/webhooks) |  |
| 10a | I Launch ska du se till att du har lagt till dataelement för Platser-tillägget som innehåller följande: <br>Aktuellt POI-<br>namnAktuellt POI<br>lastCurrent POI<br>longLast Entered<br>nameLast Entered<br>LastEntered<br>longLast Exited<br>nameLast Exited<br>lastLast Exited<br>longTimestamp |  |
| 10b | Skapa en ny regel med händelsen Händelse = Platser → Ange POI |  |
| 10c | Skapa en åtgärd = Mobile Core → Postback |  |
| 10d | Använd webkroks-URL:en för Slack-appen, till exempel https://hooks.slack.com/services/TKN5FKS68/BNFP7SVD..... |  |
| 10e | Posten skulle likna: `{text: User is in POI -  {%%Last Entered POI Name%%} in {%%Last Entered POI City%%} additional information: Radius:{%%Last Entered POI Radius%%} Timestamp: {%%timestamp%%}}`. <br>Se till att du använder de specifika dataelement som du skapade här. |  |
| 10f | Kontrollera att du har publicerat alla nya dataelement och regeländringar i Launch. (Du bör välja ett fungerande enhetsbibliotek i det övre högra hörnet av startgränssnittet.) |  |
| 11 | Starta och testa programmet igen genom att växla mellan GPX-platserna i utvecklingsmiljön. | Nu bör du se Slack-meddelanden som visar poster för varje POI när du väljer olika platser i utvecklingsmiljön. |
|  | **SNABBSAMMANFATTNING **<br>POINTAll denna testning kan utföras lokalt utan att man behöver gå till en specifik POI-plats. Valideringstestning säkerställer att programmet är korrekt konfigurerat och har fått rätt behörigheter för platsen.<br><br>Valideringen ger dig också förtroende för att definierade POI:er fungerar korrekt med tillägget Platsövervakare.  Efter det här steget kommer vi att börja testa meddelanden i Campaign för att se om rätt meddelanden visas baserat på POI-poster och utträden. |  |
|  | **Testar Adobe Campaign Standard In-App Messaging med Platstjänst.** |  |
| 12 | Konfigurera ett nytt meddelande i appen (type = broadcast) på huvudpanelen för Campaign |  |
| 12a | I utlösare väljer du **Platshändelsetyp - Post som utlösare**. |  |
| 12b | Välj **[UICONTROL Placerar anpassade metadata]** som ett extra filter - använd POI-typ = Senaste angivna POI.<br>Vi använder **[!UICONTROL Last Entered]** som POI-typ eftersom det i de flesta fall **[!UICONTROL Last Entered]** är samma som **[!UICONTROL Current POI]**. <br><br>**[!UICONTROL Current POI]** ska endast användas i fall där det finns överlappande POI-geofences. I det här fallet måste dessa POI:er vara RANKED, och sedan **[!UICONTROL Current POI]** visas den högst rankade POI:n av de 2 eller 3 geostängsel som en användare för närvarande befinner sig i. |  |
| 12c | Välj en anpassad metadatanyckel som hjälper dig att begränsa vilka POI som ska ta emot ett meddelande. |  |
| 12d | För frekvens och varaktighet bör du bara hålla till en eller två dagar, så om du inte är nöjd med villkoret kan du förfalla utlösaren på en kortare tid. |  |
| 12e | För Alltid/En eller Till klickning väljer du *ALLTID* så att du kan testa över flera platser. | Ett meddelande i appen visas ALLTID när du simulerar en platsändring som uppfyller metadatavillkoret. |
| 12f | För visningen väljer du ett annat alternativ än Lokalt meddelande. Det gör det enklare att se när du testar med appen i förgrunden.) |  |
| 12g | Förbered/bekräfta och distribuera meddelandet i appen. |  |
| 13 | För att säkerställa att nya kampanjregler hämtas i utvecklingsmiljön avslutar du programmet och startar det igen. | Glöm inte att programmen måste startas helt igen för att den nya Campaign-regelfilen ska kunna hämtas till enheten. |
| 14 | I utvecklingsprogrammet byter du plats med hjälp av de GPX-filer som skapats tidigare. | Du bör se meddelandet i appen visas baserat på tidigare villkor som angetts. |
| 15 | Vid nästa test kopierar vi i stort sett samma steg som tidigare, men den här gången testar vi LOCAL NOTIFICATION. | Det förväntade resultatet är att lokala meddelanden visas varje gång som matchningsvillkoren uppfylls. |
| 16 | Konfigurera ett nytt In-App-Message (type = broadcast). |  |
| 16a | I utlösare väljer du **[!UICONTROL Places event type]** - **[!UICONTROL Entry as the trigger]**. |  |
| 16b | Välj Placerar egna metadata som ett extra filter - använd **[!UICONTROL POI type]** = **[!UICONTROL Last Entered POI]**. |  |
| 16c | Välj en anpassad metadatanyckel som hjälper dig att begränsa vilka POI som ska ta emot ett meddelande. |  |
| 16d | För frekvens och varaktighet bör du bara hålla en eller två dagar, så om du inte är nöjd med villkoret kan du förfalla utlösaren på en kortare tid. |  |
| 16e | För Alltid/En eller Till klickfrekvens, **[!UICONTROL ALWAYS]**. |  |
| 16f | För visningstypen väljer du **[!UICONTROL Local Notification]**. |  |
| 16g | Förbered/bekräfta och distribuera meddelandet i appen. |  |
| 17 | Anslut enheten i utvecklingsmiljön och tryck **[!UICONTROL Play]** på bygget. När du har etablerat att platsen fungerar lägger du programmet i bakgrunden och fortsätter växla platser i Xcode eller Android Studio. Du bör fortfarande se utlästa konsoler som indikerar platsändringen, och du bör också se lokala meddelanden som visas beroende på vilka villkor som har angetts i utlösaren. (En fördröjning på 1-2 sekunder kan förekomma.) | Det förväntade resultatet är att lokala meddelanden visas varje gång de matchande villkoren uppfylls. |
|  | **SAMMANFATTNINGSPUNKT** <br>I det här skedet bör vi se POI-poster i vår lokala miljö. Vi bör också se meddelanden från Campaign baserat på POI-arbetet. Om det blir fel kontrollerar du om ett Slack-meddelande inte gick ut. Om det inte finns något Slack-meddelande bör du kontrollera programkonsolen eftersom en ny platspost kanske inte har spelats in. Om resultaten blir lyckade kan vi vara ganska säkra på att programmet fungerar korrekt och att Platstjänst och Kampanjmeddelandetjänsten också fungerar korrekt. |  |
|  | **TESTNING** PÅ PLATS <br>Inte mycket bör ändras vid testning på plats. Genom att hålla återföringen aktiv kan du lättare förstå om enheten får en start och en avslutning för platsen. |  |
| 18 | Utför tester med enheter som börjar med Wi-Fi och mobiltelefoner inaktiverade och aktivera sedan en gång i POI-regionen. | Om ett fel uppstår bör du notera om du får en geo-fence-post och ett meddelande i Slack. Vad är tidsstämpeln på Slack-meddelandet? |
| 19 | Utför testet med endast mobildata aktiverat och med Wi-Fi inaktiverat. |  |
| 20 | Utför tester med både mobil och wifi aktiverat. |  |
|  | **SAMMANFATTNINGSPUNKTEN** <br>Vid testning på plats bör vara i linje med utvecklingstestningen. Tänk på att det finns vissa miljöfaktorer som kan komma att spela in när du fastställer en användarplats, till exempel hur lång tid som tillbringats i en POI-geostängsel, tillgången på cellsignal och styrkan hos närliggande Wi-Fi-åtkomstpunkter. |  |

## Loggexempel

**Steg 8:** iOS- och Android-loggar förväntades under en platsuppdatering

**iOS**

```
[AdobeExperienceSDK DEBUG <com.adobe.placesMonitor>]: Authorization status changed: Always
[AdobeExperienceSDK DEBUG <Places>]: Requesting 20 nearby POIs for device location (<lat>, <longitude>)
[AdobeExperienceSDK DEBUG <Places>]: Response from Places Query Service contained <n> nearby POIs
[AdobeExperienceSDK DEBUG <com.adobe.placesMonitor>]: Received a new list of POIs from Places: (
<ACPPlacePoi: 0x600002b75a40> Name: <poi name>; ID:<poi id>; Center: (<lat>, <long>); Radius: <radius>
..
..)   
```

**Android**

```
PlacesMonitor - All location settings are satisfied to monitor location
PlacesMonitor - PlacesMonitorInternal : New location obtained: <latitude> <longitude> Attempting to get the near by pois
PlacesExtension - Dispatching nearby places event with n POIs
PlacesMonitor - Attempting to Monitor POI with id <poi id> name <poi name> latitude <lat> longitude <longitude>
PlacesMonitor - Attempting to Monitor POI with id <poi id> name <poi name> latitude <lat> longitude <longitude>
PlacesMonitor - Attempting to Monitor POI with id <poi id> name <poi name> latitude <lat> longitude <longitude>
...
...
PlacesMonitor - Successfully added n fences for monitoring
```

**Steg 9:** iOS- och Android-loggar förväntades under en händelse

**iOS**

```
[AdobeExperienceSDK TRACE <Places>]: Dispatching Places region entry event for place ID <poiId>
```

**Android**

```
PlacesExtension -  Dispatching Places Region Event for <poi name> with eventType entry
```
