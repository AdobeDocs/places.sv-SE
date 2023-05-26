---
title: Push-meddelanden
description: I det här avsnittet visas hur du använder platstjänsten med push-meddelanden.
exl-id: c094fe9c-6148-45ba-850a-f4c520d3362c
source-git-commit: 4ab15ded930b31e4e06920af31f37fdfe45df8eb
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---

# Push-meddelanden

Med Mobiltjänster kan du skicka push-meddelanden till Adobe Analytics-segment. I Platstjänst kan du segmentera målgruppen för ditt push-meddelande genom att använda deras historiska interaktioner med dina POI. Du kan till exempel skicka ett meddelande till användare som har varit i någon av dina butiker de senaste 30 dagarna.

Kontrollera att du har utfört följande uppgifter innan du börjar:

* Platstjänstdata har bearbetats av Adobe Analytics.

   Det innebär att din mobilapp har skickat platsdata till en rapportsserie och att data är tillgängliga för segmentering.

* Push-meddelandekanalen i Mobile Services har konfigurerats.

   Mer information finns i [Skapa ett push-meddelande](https://docs.adobe.com/content/help/en/mobile-services/using/manage-app-settings-ug/configuring-app/prerequisites-push-messaging.html).

* Lär dig hur du skickar ett push-meddelande till ett Analytics-segment i Mobiltjänster.

   Mer information finns i [Skapa ett push-meddelande](https://docs.adobe.com/content/help/en/mobile-services/using/messaging-ug/push-messages/t-create-push-message.html).

## Skicka ett meddelande

På **[!UICONTROL Audience]** -fliken i *Skapa push-meddelande* kan du skapa målgruppen för det här meddelandet på något av följande sätt:

* I **[!UICONTROL Analytics Segments]** väljer du ett tidigare skapat Adobe Analytics-segment.

* I **[!UICONTROL Custom Segment]** kan du skapa en målgrupp med hjälp av tillgängliga anpassade segmentparametrar.

![konfigurera ett push-meddelande](/help/assets/push-set-up.png)
