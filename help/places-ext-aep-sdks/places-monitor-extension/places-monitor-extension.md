---
title: Platsövervakartillägg
description: Tillägget Platsövervakare hanterar interaktionen med operativsystemet för att registrera och övervaka de POI som är närmast användaren.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Platsövervakartillägg {#places-monitor-extension}

Tillägget Platsövervakare hanterar interaktionen med operativsystemet för att registrera och övervaka de POI som är närmast användaren. Det här tillägget hämtar de POI:er som behöver registreras från tillägget Platser och skickar meddelanden om in- och utträde till tillägget Platser. Dessa meddelanden kommer att vara tillgängliga i Experience Platform Launch regler som händelser.

Tillägget Monitor är valfritt eftersom vissa kunder kanske redan övervakar områden med operativsystemet. Om så är fallet måste du lägga till API:erna för platstillägg så att du kan ta emot de närmaste POI:erna från platstjänstdatabasen och även skicka in in- och avslutshändelserna så att rätt åtgärder kan vidtas.
