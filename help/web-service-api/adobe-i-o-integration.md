---
title: Adobe I/O integreringsöversikt
description: Information om hur du skapar en integrering med Adobe I/O.
exl-id: d7d31938-6c0e-40f8-a9d3-30af96043119
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 6%

---

# Översikt över integrationen och krav {#integration-prereqs}

Den här informationen visar hur du skapar en integrering mellan Adobe I/O och en Platstjänst.

## Krav för användaråtkomst

Kontrollera med din organisations systemadministratör att följande åtgärder har slutförts:

* Platser för bastjänst visas i organisationens Admin Console.
* Du har lagts till i organisationen.
* Du har lagts till som användare i Platser Core Service i din organisation.

   Mer information finns i *Lägg till en användare eller en utvecklare i platstjänsten och Experience Platform Launch-profilerna* in [Få åtkomst till platstjänsten](/help/places-gain-access.md).

* Du har lagts till som utvecklare i Platser Core Service i din organisation.

   Mer information om hur du lägger till utvecklare finns i *Lägg till en användare eller en utvecklare i platstjänsten och Experience Platform Launch-profilerna* in [Få åtkomst till platstjänsten](/help/places-gain-access.md).

   Mer information om utvecklarrollen finns i [Hantera utvecklare](https://helpx.adobe.com/se/enterprise/using/manage-developers.html).

### REST API-begäranden

Varje begäran till platstjänstens REST API kräver följande:

* Ett organisations-ID
* En API-nyckel
* En innehavartoken

En integrering med Adobe I/O innehåller dessa objekt och ett sätt att begära bearer-token med hjälp av en JSON Web Token (JWT).

* Mer information om JWT finns i [Introduktion till JSON Web Tokens](https://jwt.io/introduction/).
* Information om hur du skapar en integrering för Platstjänst finns i *Skapa en platsintegrering* nedan.
* Mer information om API-nyckelintegrering, generering av JWT och certifikat för offentlig nyckel finns i [Autentiseringsöversikt för Adobe I/O](https://www.adobe.io/apis/cloudplatform/console/authentication/gettingstarted.html).

>[!IMPORTANT]
>
>Om du inte kan logga in på Adobe I/O-konsolen eller om Platstjänst inte är ett alternativ på *Skapa integreringssida*, se *Organisationskrav* in [API-översikt för webbtjänster](/help/web-service-api/places-web-services.md).

## Skapa en platsintegrering

Om du vill skapa en platsintegrering utför du följande uppgifter:

### Generera ett nyckelpar för offentlig och privat nyckel

Om du vill skapa en integrering med platstjänster behöver du ett offentligt och ett privat nyckelpar. Dessa par kan köpas eller så kan du generera egna självsignerade nycklar.

Så här skapar du egna självsignerade nycklar:

1. I ett terminalfönster kopierar och klistrar du in följande rader och trycker på **[!UICONTROL Enter]** efter inklistring av varje rad:

   ```text
      mkdir keys
      cd keys
      openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout places_integration_test_private.key -out    places_integration_test_public.crt
   ```

   >[!IMPORTANT]
   >
   >Vi rekommenderar att du namnger nycklarna så att de blir enkla att referera till och sparar dem i en mapp. Om du skapar flera integreringar kan du enkelt identifiera och hantera vilka nycklar som hör till vilken integrering.

1. Skriv den information som krävs av OpenSSL:

   ```text
   Country Name (2 letter code:  // Example: US
   State or Province Name (full name):  // Example: California
   Locality Name (eg, city):  // Example: San Jose
   Organization Name (eg, company):  // Example: Places
   Organizational Unit Name (eg, section):  // Example: Engineering
   Common Name (eg, fully qualified host name):  // Example: places.com
   Email Address:  // Example:  poi@places.com
   ```

   Mer information om OpenSSL finns i [OpenSSL](https://www.openssl.org/).

   >[!IMPORTANT]
   >
   >Informationen du anger inkluderas i nycklarna.

1. Navigera till katalogen där `.key` och `.crt` filer finns.

   I MacOS går du till exempel till **[!UICONTROL Macintosh HD]** > **[!UICONTROL users]** > **[!UICONTROL (your user name)]** > **[!UICONTROL Keys]**.

I följande videofilm får du hjälp med att generera nyckelparet:

![integreringsvideo](/help/assets/places_integration_video.gif)

### Skapa en platsintegrering i Adobe I/O-konsolen

Så här skapar du en platstjänstintegration:

1. Gå till [https://console.adobe.io](https://console.adobe.io) och logga in med din Adobe ID.
1. I **Snabbstart** avsnitt, klicka på **Skapa integrering**.
1. Markera **[!UICONTROL Access an API]** och klicka på **[!UICONTROL Continue]**.

   **[!UICONTROL Access an API]** är standardplats.

1. Om du har tillgång till mer än en Experience Cloud-organisation väljer du organisationen i listrutan högst upp till höger.
1. Under **[!UICONTROL Experience Cloud]** väljer du **[!UICONTROL Places Service]** som den Adobe-tjänst som du vill integrera med och klickar sedan på **[!UICONTROL Continue]**.
1. Markera **[!UICONTROL New integration]** och klicka på **[!UICONTROL Continue]**.
1. Ange ett namn och en beskrivning på skärmen Skapa en ny integration.
1. Dra och släpp `xxxx_public.crt` filen som du skapade ovan, till **[!UICONTROL Public keys certificates]** släppzon.
1. Välj en produktprofil.

   Kontakta systemadministratören om du är osäker på vilken profil du ska välja.
1. Klicka på längst ned på sidan **[!UICONTROL Create integration]**.
1. Efter några sekunder i *Integrationen har skapats* kontrollerar du att följande meddelande visas:

   `Your integration has been created.`

1. Integrationsinformationssidan visas med integreringens namn högst upp.

   The **[!UICONTROL Overview]** -fliken visas som standard och API-nyckeln, ditt organisations-ID, det tekniska konto-ID:t och annan information om dina integreringar visas.

### Registrera organisations-ID och API-nyckeln

1. På sidan med integreringsinformation klickar du på **[!UICONTROL Services]** och bekräfta att **[!UICONTROL Places Service]** visas under **[!UICONTROL Configured Services]**.
1. På **[!UICONTROL Overview]** Leta reda på och spela in API-nyckeln (klient-ID) och organisations-ID:t.

   Dessa ID:n behövs för varje platstjänstens REST API-begäran.

![](/help/assets/places_orgid_api-key.png)

### Generera en JWT-token

På sidan med integreringsinformation klickar du på **[!UICONTROL JWT]** så att du kan testa integrationen genom att generera en JWT och ange utbytes-URL:en.

Så här skapar du en JWT-token:

1. Öppna `private.key` filen som du skapade ovan.
1. På fliken **[!UICONTROL JWT]** kopierar du innehållet i nyckeln och klistrar in det i fältet **[!UICONTROL Paste private key]**.
1. Klicka på **[!UICONTROL Generate JWT]**.
1. I avsnittet **[!UICONTROL Sample CURL command]** klickar du på **[!UICONTROL Copy]** och klistrar in innehållet i kommandotolken eller terminalfönstret.
1. Kör kommandot genom att trycka på **[!UICONTROL Enter]** på tangentbordet.
1. Leta reda på `"token_type": "bearer"` och `"access_token"` värde.

   Värdet för innehavaråtkomsttoken är det som du kommer att använda i dina platstjänstens API-begäranden.

>[!IMPORTANT]
>
>Åtkomsttoken för Adobe är giltiga **endast** i 24 timmar, så spara CURL-exempelkommandot (steg 5). Om åtkomsttoken inte längre är giltig måste du generera om token.
