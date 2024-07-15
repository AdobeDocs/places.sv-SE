---
title: Använda metadata med POI
description: I det här avsnittet finns information och strategier om hur du använder metadata med POI.
exl-id: e669e560-a999-43ff-aeb4-06e6308b0d5c
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Strategier för att använda metadata med POI {#using-metadata-pois}

När du skapar en ny POI i Platstjänst är de enda nödvändiga elementen Namn, Radie, Latitude och Longitud. Mer information om hur du skapar en POI finns i [Skapa en POI](/help/poi-mgmt-ui/create-a-poi-ui.md). Om du bara anger den minsta informationen kommer du dock att sakna möjligheten att skapa ytterligare värde.

POI-metadata kan användas på flera olika sätt. Ur POI-hanteringsperspektiv kan det vara lättare att söka efter eller filtrera en lista med potentiellt tusentals POI. Om du skapar metadata för nyckelattribut som är kopplade till en POI kan det ge ett värde i arbetsflöden längre fram i kedjan. En hotellkedja som skapar POI för varje fastighet kanske vill inkludera metadata som om hotellegendomen har en pool eller inte, en restaurang och bar eller om de har en gymnastik. Dessa metadata kan inkluderas som kontextdata i analyser och kan även användas för riktade erbjudanden eller meddelanden.

## Placerar metadata för tjänsten i Launch

I Experience Platform Launch kan du skapa dataelement för varje metadatafält för Platstjänster som är viktigt för spårning och meddelanden.

![dataelement för gymmet](/help/assets/gymfacility.png)

Du kan sedan skapa en åtgärd med Analytics-tillägget för att skapa en ny träff som innehåller alla metadata du vill ha som kontextdata.

![åtgärd för gymmet](/help/assets/Analytics-gym.png)

## Meddelanden i appen i Adobe Campaign

Metadata kan användas som ett filter för lokala meddelanden och meddelanden i appen som definieras i Adobe Campaign Standard. Genom att använda metadata som ett filter kan du skapa ett mer relevant meddelande som är sammanhangsberoende till den faktiska platsen.

![filtrera lokala meddelanden och meddelanden i programmet i ACS](/help/assets/ACS_gym_metadata.png)
