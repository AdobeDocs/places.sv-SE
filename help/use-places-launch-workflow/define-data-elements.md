---
title: Definiera dataelement
description: I det här avsnittet finns information om hur du skapar, använder och publicerar dataelement i Experience Platform Launch för platser.
exl-id: 57e88a37-0b0b-4064-ab72-382a36a0d01d
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Definiera ett dataelement {#define-data-elements}

Följande information hjälper dig att förstå dataelement och hur du skapar och publicerar dem.

## Om dataelement

Dataelement är byggstenarna för programmets dataordlista och används för att samla in, organisera och leverera data över marknadsförings- och annonseringsteknologi.

Ett dataelement är en variabel där värdet kan mappas till ett besökar-ID, ett bärarnamn, ett Advertising-ID, ett push-ID och så vidare. I Experience Platform Launch kan du referera till det här värdet med hjälp av dess variabelnamn. Den här samlingen dataelement blir en ordlista med definierade data som du kan använda för att skapa regler (händelser, villkor och åtgärder), och den här ordlistan delas över Experience Platform Launch där den kan användas med valfritt tillägg i din egenskap.

Med tillägget Platser kan du referera till värden från följande mål:

* Aktuell POI, som avser den POI där kunden befinner sig.

  Om användaren finns i flera POI:er väljs den som tillhör biblioteket med högre rankning. Om flera POI tillhör det högsta rangordnade biblioteket väljs det med den minsta radien.
* Senaste exponerade POI, som refererar till den senaste POI som användaren lämnade.
* Senaste inmatade POI, som refererar till den senaste POI som användaren angav.

Varje POI innehåller följande datareferenser:

* **[!UICONTROL Category]**: kategori för POI
* **[!UICONTROL City]**: POI-postens stad
* **[!UICONTROL Country]**: POI-land
* **[!UICONTROL Latitude]**: POI-latitud
* **[!UICONTROL Longitude]**: POI-longitud
* **[!UICONTROL Metadata]**: anpassade metadata för POI
* **[!UICONTROL Name]**: POI-namnet
* **[!UICONTROL Radius]**: POI-radien
* **[!UICONTROL Region ID]**: ID för POI
* **[!UICONTROL Region/State]**: region, provins eller delstat i POI

### Skapa ett dataelement

1. Klicka på fliken **[!UICONTROL Data Elements]** på egenskapssidan för din app.

1. Klicka på **[!UICONTROL Create New Data Element]**.

1. I listan med installerade tillägg söker du efter **[!UICONTROL Places]**.

1. Välj en datareferens för det här dataelementet i listrutan **[!UICONTROL Data Element Type]**.

1. Välj ett POI-mål.

1. Om det här dataelementet är en anpassad metadatareferens väljer du en metadatanyckel.

1. Ange ett namn för dataelementet och klicka på **[!UICONTROL Save]**.

   ![Skapa dataelement](/help/assets/create-de-7-v3.png)


## Använda ett dataelement

När ett dataelement har skapats kan du, om det finns en dataelementväljare, använda dataelementet från valfri regelkomponent.

![Använd dataelementet](/help/assets/use-de-v2.png)

Om det inte finns någon dataelementväljare i regelkomponenten kan du använda dataelementet genom att kapsla in dataelementnamnet med **[!UICONTROL %%]**-tokens.
Om dataelementnamnet till exempel är **[!UICONTROL Last POI City]** kan du lägga till **[!UICONTROL LAST POI City]** i en textinmatning.


## Publish dataelement

Om dataelement används i någon av regelkomponenterna måste dessa dataelement också inkluderas i biblioteket och publiceras.
