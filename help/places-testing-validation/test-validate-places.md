---
title: Testa och validera platstjänst
description: I det här avsnittet finns information om hur du kan testa och validera platstjänsten.
exl-id: 8dad6619-566b-4aea-b29c-a89192a66441
source-git-commit: 2b5c53887c9ed0f2a672c377121a39537ee58f01
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 1%

---

# Recommendations för att testa Platstjänst {#test-validate-loc-svc}

Många kunder och organisationer kommer att definiera POI över hela världen, så det är viktigt att ha ett sätt att simulera och testa hur Platstjänsten interagerar med ditt program. Den här informationen hjälper dig att förstå hur du testar och validerar de platsserviceposter och utgångar som utlöses korrekt utifrån definierade POI:er och användarens aktuella plats.

Eftersom miljövariabler kan vara en faktor för platssignal och precision rekommenderar vi att du först fastställer baslinjeresultat genom att arbeta lokalt med utvecklingsverktyg och simulerade platsposter. Målet är att validera att alla platshändelser fungerar som de ska. När platshändelserna har validerats på rätt sätt kan lösningsintegreringar (till exempel Analytics, Target och Campaign) testas. För att du ska kunna testa dina aktiviteter bör du konfigurera Slack Webhooks med en återanslående och läsa in GPX-filer i din enskilda utvecklingsmiljö.

>[!IMPORTANT]
>
>I den här planen förutsätts att POI har skapats i [användargränssnittet för platstjänsten](https://places.adobe.com) och att de senaste versionerna av platstillägget är installerade och korrekt konfigurerade. Vid aktiv regionövervakning förutsätter det också att en lösning för regionövervakning implementeras. Mer information finns i [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md), [CoreLocation-dokumentation](https://developer.apple.com/documentation/corelocation/monitoring_the_user_s_proximity_to_geographic_regions) för iOS eller [Android platsdokumentation](https://developer.android.com/training/location/geofencing).

| Steg | Beskrivning | Förväntat resultat |
|--- |--- |--- |
| 1 | Bekräfta att rätt manifestnycklar har angetts för att Android ska kunna bevilja åtkomst till spårplatsen. | Bekräftat |
| 1a | Bekräfta platsuppdateringar har konfigurerats i iOS. Se även till att du har rätt plist-nycklar i iOS för att begära användarbehörighet för att spåra platsen. | Bekräftat |
| 2 | Bekräfta vilket övervakningsläge som har angetts för iOS. I det kontinuerliga läget får du större precision och beständighet men också större batteritid. | Betydande ändringar eller kontinuerlig |
| 3 | Om du använder mer än ett POI-bibliotek måste du kontrollera att rätt bibliotek har valts i tillägget Platser för Experience Platform Launch. | Bekräftat |
| 4 | Bekräfta att de senaste versionerna av Mobile Core- och Places-tilläggen har paketerats med appen via Gradle eller CocoaPods. | Bekräftat - mer information om de senaste uppdateringarna finns i [versionsinformationen.](/help/release-notes.md) |
| 5 | Bekräfta att rätt miljöer är konfigurerade för testning. ID:t för startmiljön ska överensstämma med utvecklingsmiljön för Launch. | Bekräftat |
| 6 | Skapa GPX-filer för varje POI som du vill testa. GPX-filer kan användas i lokal utvecklingsmiljö för att simulera en platspost. Mer information om hur du skapar och använder GPX-filer finns i följande: <br>[GPX-filer för iOS-simulatorn [stängd]](https://stackoverflow.com/questions/17292783/gpx-files-for-ios-simulator)<br>[https://mapstogpx.com/mobiledev.php](https://mapstogpx.com/mobiledev.php)<br>[LOCATION TESTING IN MOBILE APPS](https://qacumtester.wordpress.com/2014/02/27/location-testing-in-mobile-apps/) | GPX-filer skapas och läses in i programprojektet. |
| 7 | Utan att göra något annat bör du kunna starta programmet från Android Studio eller XCode och se lämplig varning för att begära åtkomst till spårningsplatsen. Klicka på behörigheten *Tillåt alltid*.<br><br>Vi rekommenderar att du använder en riktig enhet som är ansluten till datorn i stället för att använda enhetssimulatorn. | Platsförfrågan ska visas när programmet läses in via IDE |
| 8 | När platsbehörigheten har godkänts. Platser-SDK hämtar enhetens aktuella plats och regionövervakningskoden ska börja övervaka de 20 närmaste POI:erna från den aktuella platsen | Se loggexemplet under tabellen. |
| 9 | Om du växlar mellan olika platser i XCode eller Android studio bör du skapa ingångshändelser för specifika POI. nedanstående loggar förväntas vid inträde i en POI. | Se loggexemplet under tabellen. |
| 10 | När regionsövervakaren hittar närliggande POI:er bör du testa genom att skicka positionspingar ut. I Launch skapar du en ny regel som använder Platser-tillägget för att utlösa baserat på en geo-fence-post. Skapa sedan en ny åtgärd genom att använda Mobile Core för att skicka en återanslående. Genom att skapa en webbkrok-app för Slack kan du se platsposter och utgångar. Mer information om hur du skapar en webbkrok-app för Slack finns i [Skicka meddelanden med inkommande webbhooks.](https://api.slack.com/messaging/webhooks) |  |
| 10a | I Launch ska du lägga till dataelement för Platser-tillägget, inklusive följande: <br>Aktuellt POI-namn<br>Aktuellt POI-sista<br>Aktuellt POI-långt<br>Senaste angivna namn<br>Senaste inmatade<br>Senaste inmatade långa<br>Senaste avslutade namn<br>Senaste avslutad lång<br>Tidsstämpel<br> |  |
| 10b | Skapa en ny regel med händelsen Händelse = Platser → Ange POI |  |
| 10c | Skapa en åtgärd = Mobile Core → Postback |  |
| 10d | Använd webkroks-URL:en för ditt Slack-program, till exempel https://hooks.slack.com/services/TKN5FKS68/BNFP7SVD..... |  |
| 10e | Posten liknar: `{text: User is in POI -  {%%Last Entered POI Name%%} in {%%Last Entered POI City%%} additional information: Radius:{%%Last Entered POI Radius%%} Timestamp: {%%timestamp%%}}`. <br>Kontrollera att du använder de specifika dataelement som du har skapat här. |  |
| 10f | Kontrollera att du har publicerat alla nya dataelement och regeländringar i Launch. (Du bör välja ett fungerande enhetsbibliotek i det övre högra hörnet av startgränssnittet.) |  |
| 11 | Starta och testa programmet igen genom att växla mellan GPX-platserna i utvecklingsmiljön. | Nu bör du se Slack-meddelanden som visar poster för varje POI när du väljer olika platser i utvecklingsmiljön. |
|  | **SNABBSAMMANFATTNINGSPUNKT**<br> All den här testningen kan utföras lokalt utan att du behöver gå till en specifik POI-plats. Valideringstestning säkerställer att programmet är korrekt konfigurerat och har fått rätt behörigheter för platsen. <br><br>Den här valideringen ger dig även förtroende för att definierade POI:er fungerar korrekt med implementeringen av regionövervakning.  Efter det här steget kommer vi att börja testa meddelanden i Campaign för att se om rätt meddelanden visas baserat på POI-poster och utträden. |  |
|  | **Testar Adobe Campaign Standard In-App Messaging med Platstjänst.** |  |
| 12 | Konfigurera ett nytt meddelande i appen (type = broadcast) på huvudpanelen för Campaign |  |
| 12a | I utlösare väljer du **Platshändelsetyp - Post som utlösare**. |  |
| 12b | Välj **[!UICONTROL Places Custom metadata]** som ett extra filter - använd POI-typ = Senaste angivna POI.<br>Vi använder **[!UICONTROL Last Entered]** som POI-typ eftersom **[!UICONTROL Last Entered]** i de flesta fall är samma som **[!UICONTROL Current POI]**. <br><br>**[!UICONTROL Current POI]**&#x200B;ska bara användas i instanser där det finns överlappande POI-geofences. I det här fallet måste dessa POI:er RANKED, och sedan visar **[!UICONTROL Current POI]**&#x200B;den högst rankade POI:n av de 2 eller 3 geostängsel som en användare för närvarande befinner sig i. |  |
| 12c | Välj en anpassad metadatanyckel som hjälper dig att begränsa vilka POI som ska ta emot ett meddelande. |  |
| 12d | För frekvens och varaktighet bör du bara hålla till en eller två dagar, så om du inte är nöjd med villkoret kan du förfalla utlösaren på en kortare tid. |  |
| 12e | För Alltid/En eller Till klickning väljer du *ALLTID* så att du kan testa över flera platser. | Ett meddelande i appen visas ALLTID när du simulerar en platsändring som uppfyller metadatavillkoret. |
| 12f | För visningen väljer du ett annat alternativ än Lokalt meddelande. Det gör det enklare att se när du testar med appen i förgrunden.) |  |
| 12g | Förbered/bekräfta och distribuera meddelandet i appen. |  |
| 13 | Om du vill vara säker på att nya kampanjregler hämtas i utvecklingsmiljön avslutar du programmet och startar det igen. | Glöm inte att programmen måste startas helt igen för att den nya Campaign-regelfilen ska kunna hämtas till enheten. |
| 14 | I utvecklingsprogrammet byter du plats med hjälp av de GPX-filer som skapats tidigare. | Du bör se meddelandet i appen visas baserat på tidigare villkor som angetts. |
| 15 | Vid nästa test kopierar vi i stort sett samma steg som tidigare, men den här gången testar vi LOCAL NOTIFICATION. | Det förväntade resultatet är att lokala meddelanden visas varje gång som matchningsvillkoren uppfylls. |
| 16 | Konfigurera ett nytt In-App-Message (type = broadcast). |  |
| 16a | I utlösare väljer du **[!UICONTROL Places event type]** - **[!UICONTROL Entry as the trigger]**. |  |
| 16b | Välj Anpassade metadata för platser som ett extra filter - använd **[!UICONTROL POI type]** = **[!UICONTROL Last Entered POI]**. |  |
| 16c | Välj en anpassad metadatanyckel som hjälper dig att begränsa vilka POI som ska ta emot ett meddelande. |  |
| 16d | För frekvens och varaktighet bör du bara hålla en eller två dagar, så om du inte är nöjd med villkoret kan du förfalla utlösaren på en kortare tid. |  |
| 16e | För Alltid/En eller Tills klickfrekvens, **[!UICONTROL ALWAYS]**. |  |
| 16f | Välj **[!UICONTROL Local Notification]** som visningstyp. |  |
| 16g | Förbered/bekräfta och distribuera meddelandet i appen. |  |
| 17 | Anslut enheten i utvecklingsmiljön och tryck på **[!UICONTROL Play]** på bygget. När du har etablerat att platsen fungerar lägger du programmet i bakgrunden och fortsätter växla mellan platser i Xcode eller Android Studio. Du bör fortfarande se utlästa konsoler som indikerar platsändringen, och du bör också se lokala meddelanden som visas beroende på vilka villkor som har angetts i utlösaren. (En fördröjning på 1-2 sekunder kan förekomma.) | Det förväntade resultatet är att lokala meddelanden visas varje gång de matchande villkoren uppfylls. |
|  | **SAMMANFATTNINGSPUNKT** <br>I det här skedet bör POI-poster visas i vår lokala miljö. Vi bör också se meddelanden från Campaign baserat på POI-arbetet. Om fel uppstår kontrollerar du om ett Slack-meddelande inte har skickats. Om det inte finns något Slack-meddelande bör du kontrollera programkonsolen eftersom en ny platspost kanske inte har spelats in. Om resultaten blir lyckade kan vi vara ganska säkra på att programmet fungerar korrekt och att Platstjänst och Kampanjmeddelandetjänsten också fungerar korrekt. |  |
|  | **TESTNING PÅ PLATS** <br>Inte mycket bör ändras vid platstestning. Genom att hålla återföringen aktiv kan du lättare förstå om enheten får en start och en avslutning för platsen. |  |
| 18 | Utför tester med enheter som börjar med Wi-Fi och mobiltelefoner inaktiverade och aktivera sedan en gång i POI-regionen. | Om ett fel uppstår bör du tänka på om du får ett geo-fence-bidrag och ett meddelande i Slack. Vad är tidsstämpeln på Slack-meddelandet? |
| 19 | Utför testet med endast mobildata aktiverat och med Wi-Fi inaktiverat. |  |
| 20 | Utför tester med både mobil och wifi aktiverat. |  |
|  | **SAMMANFATTNINGSPUNKT** <br>Testning på plats bör överensstämma med utvecklingstestningen. Tänk på att det finns vissa miljöfaktorer som kan komma att spela in när du fastställer en användarplats, till exempel hur lång tid som tillbringats i en POI-geostängsel, tillgången på cellsignal och styrkan hos närliggande Wi-Fi-åtkomstpunkter. |  |

## Loggexempel

**Steg 8:** iOS- och Android-loggar förväntades under en platsuppdatering

**iOS**

```
[AdobeExperienceSDK DEBUG <Places>]: Requesting 20 nearby POIs for device location (<lat>, <longitude>)
[AdobeExperienceSDK DEBUG <Places>]: Response from Places Query Service contained <n> nearby POIs   
```

**Android**

```
PlacesExtension - Dispatching nearby places event with n POIs   
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
