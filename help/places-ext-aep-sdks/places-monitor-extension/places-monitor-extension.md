---
title: Platsövervakartillägg
description: Tillägget Platsövervakare hanterar interaktionen med operativsystemet för att registrera och övervaka de POI som är närmast användaren.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b

---


# Platsövervakartillägg {#places-monitor-extension}

Tillägget Platsövervakare hanterar interaktionen med operativsystemet för att registrera och övervaka de POI som är närmast användaren. Det här tillägget hämtar de POI:er som behöver registreras från tillägget Platser och skickar in meddelanden om att de ska skickas till tillägget Platser. Dessa meddelanden är tillgängliga som händelser i Experience Platform Launch-regler.

Tillägget Monitor är valfritt eftersom vissa kunder kanske redan övervakar områden med operativsystemet. Om så är fallet måste du lägga till API:erna för platstillägg så att du kan ta emot de närmaste POI:erna från platstjänstdatabasen och även skicka in in- och avslutshändelserna så att rätt åtgärder kan vidtas.
