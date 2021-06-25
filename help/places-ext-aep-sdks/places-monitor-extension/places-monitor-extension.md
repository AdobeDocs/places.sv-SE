---
title: Platsövervakartillägg
description: Tillägget Platsövervakare hanterar interaktionen med operativsystemet för att registrera och övervaka de POI som är närmast användaren.
exl-id: 254b33a0-79c4-4d51-8835-16e60f5c055e
source-git-commit: 8dcd777acf5d578b748afae9aa609c2349ea94a9
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Platsövervakartillägg {#places-monitor-extension}

Tillägget Platsövervakare hanterar interaktionen med operativsystemet för att registrera och övervaka de POI som är närmast användaren. Det här tillägget hämtar de POI:er som behöver registreras från tillägget Platser och skickar meddelanden om in- och utträde till tillägget Platser. Dessa meddelanden kommer att vara tillgängliga i Experience Platform Launch regler som händelser.

Tillägget Monitor är valfritt eftersom vissa kunder kanske redan övervakar områden med operativsystemet. Om så är fallet måste du lägga till API:erna för platstillägg så att du kan ta emot de närmaste POI:erna från platstjänstdatabasen och även skicka in in- och avslutshändelserna så att rätt åtgärder kan vidtas.

## Borttagning av platsövervakare

Den 31 augusti 2021 kommer Places Monitor-tillägget för Adobe Experience Platform Mobile SDK att tas bort. Tillägget Platsövervakaren får inga ytterligare uppdateringar eller support efter den 31 augusti.

Kunder som för närvarande använder tillägget Platsövervakare kan fortsätta att använda det här tillägget, under förutsättning att inga ytterligare uppdateringar eller support är tillgängliga via Adobe.

Borttagningen av tillägget Platsövervakare har ingen negativ eller negativ inverkan på Platstjänsttillägget, som även fortsättningsvis stöds med förbättringar och uppdateringar.

Kunder som vill gå över från Places Monitor-tillägget till sin egen övervakningslösning bör läsa dokumentationen för: [Använd Platstjänst med din egen övervakningslösning](https://experienceleague.adobe.com/docs/places/using/using-your-own-monitor.html?lang=en). I det här dokumentet förklaras hur du interagerar med platstjänsten genom att implementera [bastjänsterna](https://developer.apple.com/documentation/corelocation) på iOS eller [platstjänster](https://developers.google.com/android/reference/com/google/android/gms/location/package-summary) från Google Play.
