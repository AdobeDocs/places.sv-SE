---
title: Rapport om platsdata på arbetsytan i Analytics
description: I det här avsnittet finns information om hur du rapporterar platsdata i arbetsytan för Analytics.
exl-id: 45ca3c80-71b7-41de-9b00-645504061935
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 6%

---

# Rapport om platsdata på arbetsytan i Analytics {#places-in-workspace}

Det här dokumentet visar ett exempel på hur du rapporterar platsdata på arbetsytan i Analytics. Varje steg kommer att innehålla en sammanfattning på hög nivå med information från referenser till andra dokumentationssidor.

## Förutsättningar

Det här dokumentet förutsätter följande:

1. Tillägget Platser implementeras i ditt program.

   Mer information om hur du implementerar tillägget Platser finns i [Placerar tillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

1. Adobe Analytics-användaren är administratör och har tillgång till bearbetningsregler.

   Mer information om bearbetningsregler finns i [Översikt över bearbetningsregler](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html).

1. I Launch-egenskapen har dataelement skapats för platstjänstvariablerna som du vill använda.

   Mer information om dataelement i Launch finns i [Definiera ett dataelement](/help/use-places-launch-workflow/define-data-elements.md).


## 1. Skapa en startregel

Skapa en regel som gör att SDK skickar data till Analytics när enheten anger en POI. Att skapa den här typen av regel beskrivs på [Skicka POI-post och avsluta data till Analytics](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md) sida.

I det här exemplet har regelns åtgärd följande värden definierade för Analytics-begäran:

* **[!UICONTROL Action]** är ett värde på **[!UICONTROL Places Entry]**.

* Kontextens datanyckel **[!UICONTROL poi.name]** är inställt på värdet för dataelementet **[!UICONTROL {%%POI Name%%}]**.

![&quot;ange en åtgärd&quot;](/help/assets/pt-setAction.png)

## 2. Skapa analysvariabler

För att mappa kontextdata (skickas i steg 1) måste variabler först skapas för Analytics-rapportsviten. Mer information om hur du skapar variabler i Analytics finns i [Konverteringsvariabler (eVars)](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-conversion-variables-evar.html).

I det här exemplet har en konverteringsvariabel, **[!UICONTROL Evar2]**, har skapats och namngetts **[!UICONTROL Places POI Name]**. Ytterligare variabler måste skapas för varje platsvariabel som du vill visa i rapporter.

![&quot;skapa en analysvariabel&quot;](/help/assets/aa-evar.png)

## 3. Skapa bearbetningsregler

Det här steget behövs för att mappa kontextdata (steg 1) till analysvariabler (steg 2). Mer information om hur du skapar bearbetningsregler finns i [Översikt över bearbetningsregler](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html).

I det här exemplet har en bearbetningsregel skapats för att mappa kontextdatavärdet **[!UICONTROL poi.name]** till **[!UICONTROL Places POI Name (eVar2)]**. Ytterligare bearbetningsregler måste skapas för varje platsvariabel som skapas.

![&quot;skapa en bearbetningsregel&quot;](/help/assets/aa-processing-rule.png)

## 4. Generera en rapport i Workspace

I det här steget visas en grundläggande rapport på arbetsytan för analyser för att visa de data som samlats in i steg 1-3. Mer information om hur du använder arbetsytan i Analytics finns i [Översikt över arbetsytan i Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/analysis-workspace-features.html).

I det här exemplet har rapporten följande inställningar:

* Mått - **[!UICONTROL Occurrences]**

* Dimension - **[!UICONTROL Action Name]**

   * Nedbruten som Dimension - **[!UICONTROL Places POI Name]**

![&quot;skapa en rapport på arbetsytan&quot;](/help/assets/aa-workspace.png)
