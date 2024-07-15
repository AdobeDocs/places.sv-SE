---
title: Rapport om platsdata i Analytics Workspace
description: I det här avsnittet finns information om hur du rapporterar platsdata i Analytics Workspace.
exl-id: 45ca3c80-71b7-41de-9b00-645504061935
source-git-commit: d5c216aebd99ffef01c37c17c62576835b52438b
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Rapport om platsdata i Analytics Workspace {#places-in-workspace}

Det här dokumentet visar ett exempel på hur du rapporterar platsdata i Analytics Workspace. Varje steg kommer att innehålla en sammanfattning på hög nivå med information från referenser till andra dokumentationssidor.

## Förhandskrav

Det här dokumentet förutsätter följande:

1. Tillägget Platser implementeras i ditt program.

   Mer information om hur du implementerar Platstillägg finns i [Platstillägg](/help/places-ext-aep-sdks/places-extension/places-extension.md).

1. Adobe Analytics-användaren är administratör och har tillgång till bearbetningsregler.

   Mer information om hur du bearbetar regler finns i [Översikt över bearbetningsregler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.html).

1. I Launch-egenskapen har dataelement skapats för platstjänstvariablerna som du vill använda.

   Mer information om dataelement i Launch finns i [Definiera ett dataelement](/help/use-places-launch-workflow/define-data-elements.md).


## 1. Skapa en startregel

Skapa en regel som gör att SDK skickar data till Analytics när enheten anger en POI. Att skapa den här typen av regel beskrivs på sidan [Skicka POI-post och avsluta data till Analytics](/help/use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md).

I det här exemplet har regelns åtgärd följande värden definierade för Analytics-begäran:

* **[!UICONTROL Action]** anges med värdet **[!UICONTROL Places Entry]**.

* Kontextdatanyckeln **[!UICONTROL poi.name]** är inställd på värdet för dataelementet **[!UICONTROL {%%POI Name%%}]**.

![&quot;ange en åtgärd&quot;](/help/assets/pt-setAction.png)

## 2. Skapa analysvariabler

För att mappa kontextdata (skickas i steg 1) måste variabler först skapas för Analytics-rapportsviten. Mer information om hur du skapar variabler i Analytics finns i [Konverteringsvariabler (eVars)](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html).

I det här exemplet har en konverteringsvariabel, **[!UICONTROL Evar2]**, skapats och fått namnet **[!UICONTROL Places POI Name]**. Ytterligare variabler måste skapas för varje platsvariabel som du vill visa i rapporter.

![&quot;skapa en analysvariabel&quot;](/help/assets/aa-evar.png)

## 3. Skapa bearbetningsregler

Det här steget behövs för att mappa kontextdata (steg 1) till analysvariabler (steg 2). Mer information om hur du skapar bearbetningsregler finns i [Översikt över bearbetningsregler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.html).

I det här exemplet har en bearbetningsregel skapats för att mappa kontextdatavärdet **[!UICONTROL poi.name]** till **[!UICONTROL Places POI Name (eVar2)]**. Ytterligare bearbetningsregler måste skapas för varje platsvariabel som skapas.

![&quot;skapa en bearbetningsregel&quot;](/help/assets/aa-processing-rule.png)

## 4. Generera en rapport i Workspace

I det här steget visas en grundläggande rapport i Analytics Workspace för att visa de data som samlats in i steg 1-3. Mer information om hur du använder Analytics Workspace finns i [Analytics Workspace - översikt](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html).

I det här exemplet har rapporten följande inställningar:

* Mått - **[!UICONTROL Occurrences]**

* Dimension - **[!UICONTROL Action Name]**

   * Nedbruten av Dimensionen - **[!UICONTROL Places POI Name]**

![&quot;skapa en rapport på arbetsytan&quot;](/help/assets/aa-workspace.png)
