---
title: Adobe Developer Project - översikt
description: Information om hur du skapar ett Adobe Developer API-projekt.
exl-id: d7d31938-6c0e-40f8-a9d3-30af96043119
source-git-commit: 3d477c6133b74a7e6380d0db1af5125aaa844035
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Placerar API-åtkomstöversikt och krav {#developer-prereqs}

Den här informationen visar hur du skapar ett projekt i Adobe Developer Console och genererar en åtkomsttoken som ska användas i platsens API-begäranden.

## Krav för användaråtkomst

Kontrollera med din organisations systemadministratör att följande åtgärder har slutförts:

* Du har lagts till i organisationen.
* Du har lagts till i en profil inom Adobe Experience Platform.

  Mer information finns i *Lägga till en användare eller en utvecklare i platstjänsten och Experience Platform Launch-profiler* i [Få åtkomst till platstjänsten](/help/places-gain-access.md).

### REST API-begäranden

Varje begäran till platstjänstens REST API kräver följande:

* Ett organisations-ID
* En API-nyckel (kallas även klient-ID)
* Klienthemlighet
* En innehavartoken

Ett projekt med [Adobe Developer-konsolen](https://developer.adobe.com/console) innehåller dessa objekt.

* Information om hur du skapar ett projekt för platstjänstens API finns i avsnittet *Skapa ett platstjänstprojekt* nedan.

>[!IMPORTANT]
>
>Om du inte kan logga in på [Adobe Developer-konsolen](https://developer.adobe.com/console), eller om Platstjänst inte är ett alternativ på *sidan Skapa integreringar*, se *Organisationskrav* i [Översikt över API:t för webbtjänster](/help/web-service-api/places-web-services.md).

## Skapa ett API-projekt för platstjänster

Så här skapar du ett projekt för platstjänstens API:

1. Logga in på [Adobe Developer webbplats](https://developer.adobe.com) med din Adobe ID.
2. Klicka på **[!UICONTROL Console]** i det övre högra hörnet på sidan.
3. Om du har tilldelats till mer än en Adobe-organisation väljer du rätt organisation i listrutan i sidans övre högra hörn.
4. Klicka på knappen **[!UICONTROL Create new project]**.
5. Klicka på knappen **[!UICONTROL Add API]** i sektionen Kom igång med ditt nya projekt.
6. Om du vill välja plats-API:t rullar du nedåt på sidan till platskortet och klickar på kryssrutan i kortets övre högra hörn.
7. Klicka på knappen **[!UICONTROL Next]**.
8. Välj alternativet OAuth Server-till-server (om det finns ett alternativ).
9. Namnge autentiseringsuppgifterna och klicka på **[!UICONTROL Next]**.
10. Välj en profil (alla bör fungera om det finns fler än en).
11. Klicka på **[!UICONTROL Save and configure API]**.
12. Klicka på länken **[!UICONTROL OAuth Server-to-Server]** under AUTENTISERINGSUPPGIFTER i den vänstra panelen
13. Den här sidan innehåller följande:
   * Ett sätt att generera en åtkomsttoken som ska användas i platstjänstens REST API-begäranden.
   * Visa ett bol-kommando som exempel på hur du kan skapa en åtkomsttoken från din egen kod.
   * Visa klient-ID (kallas även API-nyckel)
   * Visa klienthemligheten
   * Visa organisations-ID
   * Alla krävs i förfrågningarna till platstjänstens REST API.
14. Du kan byta namn på projektet till något mer beskrivande genom att klicka på projektnamnet i sökvägen längst upp till vänster i fönstret
15. Klicka sedan på knappen **[!UICONTROL Edit project]** längst upp till höger på sidan.

>[!IMPORTANT]
>
>Åtkomsttoken för Adobe är giltiga **endast** i 24 timmar, så spara CURL-exempelkommandot (steg 5). Om åtkomsttoken inte längre är giltig måste du generera om token.
