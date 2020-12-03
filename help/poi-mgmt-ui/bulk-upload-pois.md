---
title: Massöverföring av POI
description: I det här avsnittet finns information om hur du överför dina POI-filer satsvis.
translation-type: tm+mt
source-git-commit: 462df20bb351795dc72009cc18d390cb45e262a8
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# Massöverföring av POI {#bulk-upload-pois}

Knappen **Importera POI** i platstjänsten kan användas för att massöverföra nya POI:er med hjälp av en CSV-fil. En exempelmall för kalkylblad finns för att visa vilka datakolumner som krävs och hur du lägger till valfria anpassade metadata.

![Skärm för massimport](/help/assets/Bulk-import.png)

I den här videon visas processen för massimport och massredigering:

<!--I changed this embed to a link to pass validation. We should not link to youtube videos, so please upload this to MCP-->

[Platser för massimport och redigering av POI](https://www.youtube.com/watch?v=75qVtirsXhg)

## Python API-skript

En uppsättning Python-skript har skapats för att förenkla batchimporten av POI från en CSV-fil till en POI-databas med hjälp av webbtjänstens API:er. Dessa skript kan laddas ned från den här öppna [Git-rapporten](https://github.com/adobe/places-scripts).

Innan du kör dessa skript läser du *Krav för användaråtkomst* i [Integreringsöversikt och -krav](/help/web-service-api/adobe-i-o-integration.md)för att få åtkomst till webbtjänstens API:er.

Här är lite information om skripten:

>[!TIP]
>
>Den här informationen ingår också i en Viktigt-fil i [Git-rapporten](https://github.com/adobe/places-scripts).

## CSV-fil

Ett exempel på en CSV-fil `places_sample.csv`är en del av det här paketet och innehåller de sidhuvuden som krävs och en rad med exempeldata. Dessa rubriker är små och motsvarar reserverade metadatanycklar som används i platsdatabasen. Kolumner som du lägger till i CSV-filen läggs till i POI-databasen i ett separat metadataavsnitt för varje POI som nyckel/värde-par, och rubrikvärdet används som nyckel.

Här är en lista över kolumnerna och de värden som du behöver använda:

* `lib_id`

   Ett giltigt biblioteks-ID som hämtas från POI-databasen.

* `type`

   Point är för närvarande det enda giltiga värdet.

* `longitude`

   Ett värde mellan -180 och 180.

* `latitude`

   Ett värde mellan -85 och 85.

* `radius`

   Ett värde mellan 10 och 20 000.

### Kolumnvärden

Värdena för följande kolumner används i användargränssnittet för platstjänster:

* färg, som används som färg på det stift som representerar platsen för POI på kartan för användargränssnitt för Platstjänst.
   * Giltiga värden är &quot;&quot;, #3E76D0, #AA99E8, #DC2ABA, #FC685B, #FC962E, #F6C436, #BECE5D, #61B56B, #3DC8DE och &quot;&quot;.
   * Om värdet lämnas tomt används blått som standardfärg i användargränssnittet för Platstjänster.

      Värdena motsvarar blått (#3E76D0), lila (#AA99E8), fuschia (#DC2ABA), orange (#FC685B), ljusorange (#FC962E), gult (#F6C436), ljusgrönt (#BECE5D), grönt (#61B 56B) och ljusblå (#3DC8DE).

* -ikonen, som används som ikon på det stift som representerar platsen för POI på kartan för användargränssnitt för Platstjänst.

   * Giltiga värden är &quot;&quot;, shop, hotelbed, car, airplane, train, ship, stadium, amusementpark, anchor, beaker, bell, bid, book, box, portfölj, browse, brush, building, calculator, camera, clock, education, flashlight, follow, game, hon, hon, present, hammer, home, key, launch, lightbulb, mailbox, money, pin, pin, Promote, ribbon, shoppingCart, star, target, teapot, thumbDown, thumbUp, trap, trophy, wrench.

      Ikonvärdena visas i den ordning som de visas på följande bild:

      ![ikoner i användargränssnittet](/help/assets/UI_icons.png)

   * Om värdet lämnas tomt används stjärnan som standardikon.

* Kolumner som inte nämns kan lämnas tomma.

## Köra skriptet

1. Hämta filer från [Git-rapporten](https://github.com/adobe/places-scripts) till din lokala katalog.
1. Öppna `config.py` filen i en textredigerare och utför följande uppgifter:

   a. Redigera följande variabelvärden som strängar:

   * `csv_file_path`

      Detta är sökvägen till din `.csv` fil.

   * `access_code`

      Det här är din åtkomstkod som hämtats från anropet till Adobe IMS. Mer information om hur du hämtar den här åtkomstkoden finns i *Krav för användaråtkomst* i [Integreringsöversikt och -villkor](/help/web-service-api/adobe-i-o-integration.md).

   * `org_id`

      Det Experience Cloud orgID som POI ska importeras till. Mer information om hur du hämtar organisation-ID:t finns i *Krav för användaråtkomst* i [Integreringsöversikt och villkor](/help/web-service-api/adobe-i-o-integration.md).

   * `api_key`

      Det här är den REST-API-nyckel du fått från Adobe I/O Plataces-integreringen. Mer information om hur du hämtar API-nyckeln finns i *Krav för användaråtkomst* i [Integreringsöversikt och villkor](/help/web-service-api/adobe-i-o-integration.md).
   b. Spara ändringarna.

1. Navigera till `…/places-scripts/import/` katalogen i ett terminalfönster.
1. Skriv `python ./places_import.py` och tryck på **[!UICONTROL enter]** (**[!UICONTROL return]**).


## CSV-kontroller före import

Skriptet slutför först följande kontroller av CSV-filen:

* Om en `.csv` fil har angetts.
* Anger om filsökvägen är giltig.
* Anger om reserverade metadatarubriker inkluderas.

   De reserverade metadatarubrikerna är lib_id, name, description, type, longitude, latitude, radius, country, state, city, street, category, icon och color.

   >[!TIP]
   >
   >Alla rubriker är små och kan listas i vilken ordning som helst.

* Verifierar värdena för kolumnerna som anges i CSV-filavsnittet.

Om fel hittas skrivs skriptet ut och avbryts. Om inga fel hittas försöker skriptet importera POI:er i grupper om 1 000. Om batchen har importerats rapporterar skriptet statuskoden 200. Om batchen inte kan importeras rapporteras fel.

## Enhetstester

Enhetstester finns i `tests.py` filen, ska köras före varje pull-begäran och ska alla utföras. Ytterligare tester bör läggas till med ny kod. Om du vill köra testerna navigerar du till `…/places-scripts/import/` katalogen och anger `python ./places_import.py` i terminalen.
