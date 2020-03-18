---
title: Meddelanden i appen
description: I det här avsnittet visas hur du använder tjänsten Platser med meddelanden i appen.
translation-type: tm+mt
source-git-commit: 0ca2162f113fba6bfbd54443109068b1a506762b

---


# Meddelanden i appen {#places-push-messaging}

Följande information visar hur du konfigurerar meddelanden i appen som ska utlösas från Platstjänst-händelser.

>[!IMPORTANT]
>
>Meddelandena måste vara på en Analytics-träff.

## Meddelande i appen

Med Mobiltjänster kan ni använda platsdata som skickas till Analytics som utlösande händelser och/eller villkor för ett meddelande i appen. Om meddelanden i appen utlöses från SDK och inte behöver vänta på att data ska bearbetas av Analytics, kan meddelandena visas i realtid så snart utlösaren inträffar.

### Lokala meddelanden

Här är en lista över tillgängliga meddelandetyper i appen:

* Helskärm
* Varning
* Lokala meddelanden

Dessa typer är meddelanden i appen eftersom de aktiveras av SDK:n. Lokala meddelanden ser ut och känns som push-meddelanden eftersom de visas när programmet är i bakgrunden. Dessa meddelanden skickar även meddelanden i realtid när användare anger eller avslutar dina POI-dokument när programmet är i bakgrunden. Mer information finns i [Platsmonitortillägg](/help/places-ext-aep-sdks/places-monitor-extension/places-monitor-extension.md).

### Förutsättningar

Innan du börjar förstår du hur du skickar och skapar ett meddelande i appen i Mobiltjänster och hur utlösarna fungerar. Mer information finns i [Skapa ett meddelande i appen.](https://docs.adobe.com/content/help/en/mobile-services/using/messaging-ug/inapp-messages/t-in-app-message.html)

## Regler i Experience Platform Launch

Ni kan skapa regler för Experience Platform Launch som skickar de data som ni vill kunna använda som en del av era utlösarregler för meddelanden i appen till Analytics. Du kan använda data från Places-tilläggen i Experience Platform Launch-reglerna som antingen händelser och/eller villkor beroende på ditt användningsfall.

* Använda platsdata som utlösande händelse.

   Du kan till exempel skicka data till Analytics när en användare anger en POI.

* Använda platsdata som villkor för en utlösande händelse.

   Om du till exempel har skapat en anpassad metadatatagg i Platstjänst för vädret i olika POI:er kan du använda dessa metadata som parameter för regelvillkoret. Du kan använda det här villkoret med en POI-posthändelse som beskrivs ovan, men du kan även använda villkoret som kontext för alla händelser.

När regeln har konfigurerats med rätt händelse- och villkorsparametrar slutför du regelkonfigurationen genom att konfigurera åtgärden för att skicka data till Analytics.

## Skapa en åtgärd

Så här skapar du en åtgärd:

1. Markera **[!UICONTROL Adobe Analytics]** tillägget.
1. I listrutan **[!UICONTROL Action type]** väljer du **[!UICONTROL Track.]**
1. Skriv ett namn för åtgärden.
1. I den högra rutan i **[!UICONTROL Context Data]** väljer du nyckelvärdepar för att ange de kontextdata som ska skickas till Analytics.

Du kan till exempel välja `poiname` som tangent och `{%%Last Entered POI Name}` som värde.

>[!TIP]
>
>Analysbearbetningsregler kan anges för att hämta kontextdata. Mer information finns i [Bearbetningsregler](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-processing-rules.html). I exemplet i *Skapa en åtgärd* skickar åtgärden `poiname` som kontext för att beskriva POI-händelsen som skickas till Analytics.

![skapa ett funktionsmakro](/help/assets/configure-action.png)

Här är ett exempel på den fullständiga regeln:

![slutförd regel](/help/assets/create-a-rule.png)

## Skapa ett meddelande i appen i Mobiltjänster

Som en del av dina utlösarparametrar kan du skapa målgruppen för meddelandet med data från platstjänsten på något av följande sätt:

* Använda platsspecifika åtgärder som en inmatning eller en avslutning.
* Använda POI-metadata som skickas som kontextdata för att begränsa målgruppen.

   Det här alternativet kan användas med en platsspecifik åtgärd, till exempel en post, eller som kontext till en annan händelse, till exempel en start eller ett knappklick.

   Här är ett exempel på hur du konfigurerar ett meddelande i appen för att välkomna användare som anger ett POI som har **[!UICONTROL Adobe]** i namnet:

   ![trigger parameters](/help/assets/trigger-parameters.png)

* Parametrar i platstjänstens rubriker på sidan *Utlösare och traits* i Mobiltjänster fungerar inte med data från platstjänsten.

   De här parametrarna gäller endast för den gamla platstjänstdatabasen som skapades i Mobile Services.