---
title: Frågor och svar
description: Det här avsnittet innehåller ytterligare information om några vanliga frågor och svar.
exl-id: cee9f447-5e50-4ed8-b37b-baecbc0e9b7b
source-git-commit: 010de286c25c1eeb989fb76e3c2adaa82ac9fd35
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# Frågor och svar

Här är information och vanliga frågor om Platstjänst.

## Migrera från trackLocation i v4 SDK

Om du migrerar från v4 SDK och letar efter en ersättning till `trackLocation` API, se ämnet [Använd platstjänst utan övervakning av aktiv region](use-places-without-active-monitoring.md).

## Storlek och tillförlitlighet

Observera alla geofences som används i regionövervakning från en mobilapp, oavsett om Adobe eller någon annan tjänst används. Operativsystemen rekommenderar att du tar hänsyn till vissa parametrar när du skapar geofences. För maximal tillförlitlighet bör geofences ha en radie på minst 100 meter. Det går bra att skapa mindre geofences, men start- och avslutshändelser kanske inte genereras eller kan genereras när användaren slutar flytta under en period.

Dessutom kan tillförlitligheten och tillförlitligheten minskas beroende på maskinvaruförhållanden som att wi-fi är avstängd eller inte är tillgängliga, och även utifrån enhetens placering i förhållande till hur GPS-signalerna hindras. Exempelvis kan bergsområden, stadsinställningar och inomhusområden minska positionens exakthet från operativsystemen iOS och Android.

## Hur utlöser en exit-händelse?

Den implementerade regionövervakaren ska begära en lista med närliggande POI:er. När en region har tagits emot ska den registreras i operativsystemet för varje POI. Operativsystemet ansvarar nu för att meddela SDK när enheten korsar en gräns (inträde eller utträde) för en av de övervakade regionerna. SDK utlöser endast en exit-händelse när operativsystemet meddelar SDK om att händelsen har inträffat. Huvudorsaken till detta meddelande är platsens tidskänslighet.

Om operativsystemet inte kan leverera en exit-händelse när enheten lämnar ett område är det säkrare för SDK att bara utelämna exit-händelsen. Om SDK tillverkar en avslutningshändelse utan att händelsen aktiveras av operativsystemet, finns det en risk för att exithändelsen kan bearbetas långt utanför den tidsperiod under vilken enheten befann sig nära POI.

## Antal POI

I Places-tjänstens gränssnitt för hantering av POI kan kunderna lägga till upp till 150 000 intressepunkter i ett visst bibliotek. Kunder kan definiera flera bibliotek för att segmentera POI-grupperingar om så önskas.

## Några anteckningar om platsändring och övervakning av aktiva regioner

Övervakningen av en geografisk region börjar omedelbart efter registreringen av auktoriserade appar. Men vänta dig inte att få en händelse direkt, eftersom bara gränsövergångar genererar en händelse. Om användarens plats redan finns i regionen vid registreringen genererar inte platshanteraren automatiskt en händelse. Appen måste i stället vänta på att användaren ska gå över regionsgränsen innan en händelse genereras och skickas till delegaten.

Var klok när du anger vilka områden som ska övervakas. Regionerna är en delad systemresurs och det totala antalet regioner som är tillgängliga i hela systemet är begränsat. Därför begränsas Core Location till 20 av antalet regioner som kan övervakas samtidigt av en enda app. För att kringgå denna gräns bör du överväga att endast registrera de regioner som finns i användarens omedelbara närhet.

[Mer information finns på Apple utvecklarwebbplats] (https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/LocationAwarenessPG/RegionMonitoring/RegionMonitoring.html#//apple_ref/doc/uid/TP40009497-CH9-SW11)
