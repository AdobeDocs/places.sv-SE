---
title: Få åtkomst till platstjänsten
description: I det här avsnittet finns information om hur du lägger till en användare i Platstjänst och Experience Platform Launch så att användaren kan komma åt Platstjänst.
exl-id: f388945e-cf26-4694-9697-9fe564ae4b69
source-git-commit: c9058e9b70c2ef97151078f43913963471730bd2
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# Få åtkomst till platstjänsten {#adding-user-launch-places}

Platstjänsten är nu tillgänglig i användargränssnittet för datainsamling. Du kommer åt Datainsamling via snabbmenyn på [Adobe Experience Cloud home](https://experience.adobe.com).

![snabbåtkomstmeny](/help/assets/quickaccess.png)

Du kan även komma åt Datainsamling via Adobe Experience Platform-menyn:

![Experience Platform-menyn](/help/assets/solutionaccessmenu.png)

Om ditt användar-ID har åtkomst visas ikonen Platstjänst i den vänstra panelen under Datahantering i datainsamling enligt nedan:

![Vänster panel för datainsamling](/help/assets/places_in_data_collection.png)

Om du inte ser platstjänsten på den här platsen kontaktar du en administratör i din organisation för att lägga till ditt användar-ID i Adobe Experience Platform på Admin Console.

## Lägga till en användare för åtkomst till Platstjänst och Upplev Adobe Experience Platform Data Collection

Platser ingår nu i Adobe Experience Platform. Om du vill tillåta användare att få åtkomst till [platstjänsten](https://experience.adobe.com/#/data-collection/places) måste de läggas till i Adobe Experience Platform i Admin Console som användare. Om du vill ge användare åtkomst till Experience Platform Data Collection med de behörigheter som krävs för att konfigurera mobila egenskaper och använda platser med Adobe Experience Platform SDK, måste de även läggas till i Adobe Experience Platform Data Collection i Admin Console och få följande behörigheter för Adobe Experience Platform Data Collection:

* Alla behörigheter under Egenskaper Rights:
   * Godkänn
   * Utveckla
   * Redigera egenskap
   * Hantera miljöer
   * Hantera tillägg
   * Publish
* Hantera egenskapsbehörighet under Företagsrättigheter

Om det är första gången du lägger till en användare utför du följande steg för att lägga till användare i Adobe Experience Platform Data Collection och Adobe Experience Platform. Om du har lagt till användare tidigare kan flera profiler visas, så se till att du väljer rätt profil.

>[!IMPORTANT]
>
>Endast organisationsadministratörer kan komma åt Admin Console och lägga till användare.

### 1. Verifiera att Adobe Experience Platform och Adobe Experience Platform Data Collection har etablerats

1. Logga in på din Experience Cloud-organisation, [Adobe Experience Cloud home](https://experience.adobe.com).
1. Klicka på Experience Cloud-skalväljaren längst upp till höger för att visa en listruta.

   ![gränssnittsväljare](/help/assets/places_shell_switcher1.png)

1. Klicka på **[!UICONTROL Admin Console]** längst ned i listan. (En länk till **[!UICONTROL Admin Console]** finns också i snabbåtkomstavsnittet).

   Om du inte ser **[!UICONTROL Admin Console]** i listan är du ingen administratör. Du måste kontakta din organisationsadministratör för att slutföra den här proceduren.

1. Om du har åtkomst till flera organisationer i Admin Console ska du kontrollera att rätt organisation är markerad i sidans övre högra hörn.

   Det här är den organisation som du ska lägga till dina användare i. Om rätt organisation inte har valts klickar du på organisationen och väljer rätt organisation i listrutan.

   >[!IMPORTANT]
   >
   >Om önskad organisation inte finns med i listrutan betyder det att du inte har administratörsåtkomst till den organisationen.

1. Klicka på fliken Produkter i Admin Console och kontrollera att korten för **[!UICONTROL Adobe Experience Platform Data Collection]** och **[!UICONTROL Adobe Experience Platform]** visas.

   ![](/help/assets/places_provisioned1.png)

   Dessa två produkter tillhandahålls automatiskt till alla organisationer, så de bör vara närvarande.


### 2. Lägg till användare för de här produkterna

#### Lägg till användare för att ge åtkomst till användargränssnittet för platstjänster

1. Klicka på kortet **[!UICONTROL Adobe Experience Platform]** på fliken Produkter.
2. En användare kan läggas till i vilken profil som helst inom **[!UICONTROL Adobe Experience Platform]** för att få åtkomst till platser. Inga specifika behörigheter behöver anges.
3. Välj en profil (om det finns fler än en) och klicka på den för att öppna den.
4. Klicka på den blå knappen **Lägg till användare**, fyll i användaren med användarens AdobeID och namn och klicka sedan på Spara för att slutföra tillägget.

#### Lägg till användare i datainsamling

1. Klicka på kortet **[!UICONTROL Adobe Experience Platform Data Collection]** på fliken Produkter.
2. Som standard har en profil med namnet **Standarddatainsamling all åtkomst** skapats. Om du lägger till en användare i den här profilen ser du till att de har rätt behörighet att arbeta med platstjänsten och datainsamlingen. Om du väljer en annan profil måste du se till att de behörigheter som nämns ovan ingår.
3. Välj en profil (om det finns fler än en) och klicka på den för att öppna den.
4. Klicka på den blå knappen **Lägg till användare**, fyll i användaren med användarens AdobeID och namn och klicka sedan på Spara för att slutföra tillägget.

#### Lägg till en användare som utvecklare för Platstjänst.

För användare som också behöver tillgång till platstjänstens REST API måste du lägga till dem som en utvecklare.
1. Klicka på kortet **[!UICONTROL Adobe Experience Platform]** på fliken Produkter.
2. Om användaren redan har lagts till på **[!UICONTROL Adobe Experience Platform]**-kortet via instruktionerna ovan väljer du samma profil som användes tidigare och klickar på den.
3. Klicka på fliken **Utvecklare** i profilen
4. Klicka på den blå knappen **Lägg till utvecklare**, fyll i användaren med användarens AdobeID och namn och klicka sedan på Spara för att slutföra tillägget.

När ovanstående steg har slutförts får användaren ett e-postmeddelande som meddelar dem att de har åtkomst till **[!UICONTROL Adobe Experience Platform]** och **[!UICONTROL Adobe Experience Platform Data Collection]**. De kan sedan logga in på [Adobe Experience Cloud](https://experience.adobe.com) för den här organisationen och få åtkomst till platstjänsten och datainsamlingen. Om du också slutför stegen **[!UICONTROL Add a developer]** kan användaren även logga in på [Adobe Developer Console](https://developer.adobe.com/console/home) för att skapa ett projekt som ger åtkomst till platstjänstens REST API.
