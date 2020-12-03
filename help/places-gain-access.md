---
title: 'Få åtkomst till platstjänsten '
description: I det här avsnittet finns information om hur du lägger till en användare i Platstjänst och Experience Platform Launch så att användaren kan komma åt Platstjänst.
translation-type: tm+mt
source-git-commit: 26538602a73e806a4822705c7a3aa44d76351030
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 8%

---

# Få åtkomst till platstjänsten {#adding-user-launch-places}

Du kommer åt Platstjänsten via snabbmenyn på [Adobe Experience Cloud home](https://experience.adobe.com).
Om ditt användar-ID har åtkomst visas ikonen Platstjänst enligt nedan:

![snabbmeny](/help/assets/quickaccess.png)

Du kan även få åtkomst till platstjänsten från Adobe Experience Platform-menyn:

![Experience Platform-menyn](/help/assets/solutionaccessmenu.png)

Om du inte ser Platstjänst på någon av dessa menyer kontaktar du en administratör i din organisation för att lägga till ditt användar-ID i Platsens bastjänst i Admin Console.

## Lägga till en användare i Platstjänst och Experience Platform Launch

För att användare ska kunna få tillgång till användargränssnittet [i](https://launch.adobe.com)Experience Platform Launch måste de läggas till som användare i bastjänsten för platser i Admin Console. För att användare ska kunna få tillgång till Experience Platform Launch, konfigurera mobila egenskaper och använda platser med Adobe Experience Platform SDK måste de läggas till Experience Platform Launch i Admin Console och få följande behörigheter för Experience Platform Launch:

* Alla egenskapsrättigheter:
   * Utveckla
   * Godkänn
   * Publicera
   * Hantera tillägg
   * Hantera miljöer
* Hantera egenskapsbehörighet under Företagsrättigheter

Om det här är första gången du lägger till en användare utför du följande steg för att lägga till användare i tjänsten Experience Platform Launch och Platser. Om du har lagt till användare tidigare kan flera profiler visas, så se till att du väljer rätt profil.

>[!IMPORTANT]
>
>Endast organisationsadministratörer kan komma åt Admin Console och lägga till användare.

### 1. Kontrollera att Platstjänst och Experience Platform Launch har etablerats

1. Logga in på din Experience Cloud-organisation.
1. Klicka på Experience Cloud-skalväljaren längst upp till höger.

   ![skalväxlare](/help/assets/places_shell_switcher1.png)

1. Under **[!UICONTROL Platform]**, klicka **[!UICONTROL Administration]**.

   Om du inte ser **Administration** i listan är du ingen administratör. Du måste kontakta din företagsadministratör för att slutföra den här proceduren.

1. Klicka på **[!UICONTROL Admin Console]** kortet på sidan Administration i Experience Cloud **[!UICONTROL Take me there]**.

1. Om du har åtkomst till flera organisationer i Admin Console ska du kontrollera att rätt organisation är markerad i sidans övre högra hörn.

   Det här är den organisation som du ska lägga till dina användare i. Om du inte har valt rätt organisation klickar du på organisationen och väljer organisation i listrutan.

   >[!IMPORTANT]
   >
   >Om du inte har tillgång till en organisation betyder det att du inte har administratörsåtkomst till den organisationen.

1. Kontrollera att korten för **[!UICONTROL Adobe Experience Platform Launch]** och **[!UICONTROL Places Core Services]** visas.

   ![](/help/assets/places_provisioned1.png)

   Om de visas har Platstjänst och Experience Platform Launch etablerats för din organisation. Om de inte visas måste de etableras för din organisation.


### 2. Konfigurera profilen och lägg till behörigheter

1. Konfigurera en Experience Platform Launch-profil, som tillåter användare som har lagts till i profilen att använda Experience Platform Launch och dess mobila egenskaper med Experience Platform SDK.

   a. Klicka på i menyraden **[!UICONTROL Product]**.

   b. Klicka på i den vänstra rutan i produktlistan **[!UICONTROL Adobe Experience Platform Launch]**.

   * Profilen/profilerna för Experience Platform Launch visas till höger.
   * Experience Platform Launch har en standardprofil som heter *Launch - (organisationsnamn)* .

      Om du tidigare har lagt till användare i Experience Platform Launch kan du se flera profiler.

1. Välj rätt profil:

   a. Klicka på namnet på standardprofilen.

   b. Klicka på **[!UICONTROL Permissions]** fliken.

   c. Klicka på **[!UICONTROL Edit]** bredvid **[!UICONTROL Property Rights]**.

   d. Klicka på i den vänstra rutan **[!UICONTROL + Add all]**.

   I det här steget flyttas alla tillgängliga behörigheter till den inkluderade behörighetslistan.

   e. Klicka **[!UICONTROL Company Rights]**.

   f. Klicka på i den vänstra rutan **[!UICONTROL + Manage Properties]**.

   g. Klicka **[!UICONTROL Save]**.

>[!IMPORTANT]
>
>Det finns en standardprofil för Platstjänst, men du behöver inte lägga till några behörigheter.

Du har lagt till behörigheter till profilen som du skapade.

### 3. Lägg till en användare eller en utvecklare i platstjänsten och Experience Platform Launch-profilerna

Du kan lägga till en användare och/eller en utvecklare i platstjänsten och Experience Platform Launch-profilerna.

### Lägg till en användare

Så här lägger du till en användare i platstjänsten och Experience Platform Launch-profilerna:

1. Lägg till en användare i profilen Experience Platform Launch.

   a. Klicka på i menyraden **[!UICONTROL Overview]**.

   b. On the **[!UICONTROL Adobe Experience Platform Launch]** card, verify the following:

   * Två punkter visas längst ned på kortet.
   * Punkten till vänster är svart.

      Om punkten till höger är svart kan du bara lägga till utvecklare. Om du vill lägga till en användare klickar du på punkten till vänster.
   c. Klicka **[!UICONTROL + Add Users]**.

   d. Ange användarens Adobe ID.

   e. Gör något av följande:

   * Om du lägger till en ny användare klickar du på **[!UICONTROL New user]** och anger användarens för- och efternamn.
   * Om du lägger till en befintlig användare klickar du på användarens namn som visas.

   f. Välj den profil du redigerade tidigare i listrutan **[!UICONTROL Please select a profile for this product]** .

   g. Klicka **[!UICONTROL Save]**.

1. Lägg till en användare i **[!UICONTROL Places Core Services]**.

   >[!TIP]
   >
   >För närvarande har alla användare av platstjänster samma behörigheter, så du behöver inte redigera behörigheterna.

   a. On the **[!UICONTROL Places Core Services]** card, verify the following:

   * Två punkter visas längst ned på kortet.
   * Punkten till vänster är svart.

   b. Klicka **[!UICONTROL + Assign Users]**.

   c. Ange användarens Adobe ID.

   d. Gör något av följande:

   * Om du lägger till en ny användare klickar du på **[!UICONTROL New user]** och anger användarens för- och efternamn.
   * Om du lägger till en befintlig användare klickar du på användarens namn som visas.

   e. Välj profilen Platser i den **[!UICONTROL Please select a profile for this product]** nedrullningsbara listan.

   f. Klicka **[!UICONTROL Save]**.

### Lägg till en utvecklare

För användare som också behöver tillgång till webbtjänstens API måste du lägga till dem som utvecklare.

Så här lägger du till en utvecklare:

1. Kontrollera följande på **[!UICONTROL Places Core Services]**-kortet:

   * Två punkter visas längst ned på kortet.
   * Klicka på punkten till höger så att den **[!UICONTROL Assign Developers]** visas längst ned på kortet.

1. Klicka på **[!UICONTROL + Assign Developers]**.

1. Ange användarens Adobe ID.

1. Gör något av följande:

   * Om du lägger till en ny användare klickar du på **[!UICONTROL New user]** och anger användarens för- och efternamn.
   * Om du lägger till en befintlig användare klickar du på användarens namn som visas.

1. Välj profilen Platstjänst i **[!UICONTROL Please select a profile for this product]** listrutan.

1. Klicka på **Spara**.

Användarna får ett e-postmeddelande som talar om för dem att de har tillgång till Experience Platform Launch. They can can log in to the [Experience Platform Launch](https://launch.adobe.com) or the [Places Service](https://places.adobe.com) UIs for this organization. Om du slutför steg 4 i proceduren **Lägg till en utvecklare** kan användaren även logga in på [Adobe I/O-konsolen](https://console.adobe.io) för att skapa en Places-integrering och använda Places REST API.
