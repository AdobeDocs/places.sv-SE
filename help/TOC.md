---
audience: end-user
user-guide-title: Användarhandbok för tjänsten Places
user-guide-description: Tjänsten Places är en geopositioneringstjänst som gör det möjligt för mobila appar med platsmedvetenhet att förstå platskontexten.
feature: Places
source-git-commit: 9f2c6fee6e0d6d075b662cc0b6cbee49cf05ee55
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 14%

---


# Places Service {#using}

+ [Platstjänst - översikt](home.md)
+ [Versionsinformation](release-notes.md)
+ [Komma igång](getting-started.md)
+ [Få åtkomst till platstjänsten](places-gain-access.md)
+ Användargränssnitt för platstjänst {#poi-mgmt-ui}
   + [Översikt över användargränssnittet för Platstjänst](poi-mgmt-ui/poi-mgmt-ui-overview.md)
   + [Skapa en POI](poi-mgmt-ui/create-a-poi-ui.md)
   + [Hantera tidigare skapade POI](poi-mgmt-ui/managing-pois-in-the-places-ui.md)
   + [Strategier för att använda metadata med POI](poi-mgmt-ui/metadata-with-pois.md)
   + [Massöverföring av POI](poi-mgmt-ui/bulk-upload-pois.md)
   + [Hantera flera bibliotek](poi-mgmt-ui/manage-libraries-in-the-places-ui.md)
+ Webbtjänstens API {#web-service-api}
   + [API-översikt för webbtjänst](web-service-api/places-web-services.md)
   + [Krav för integrering](web-service-api/adobe-i-o-integration.md)
   + API-användning {#api-usage}
      + [API-användningsöversikt](web-service-api/api-usage/api-usage-overview.md)
      + [Huvuden och parametrar](web-service-api/api-usage/headers-and-parameters.md)
      + Hantera bibliotek {#manage-libraries}
         + [Hantera bibliotek - översikt](web-service-api/api-usage/manage-libraries/manage-libraries.md)
         + [Skapa ett bibliotek](web-service-api/api-usage/manage-libraries/create-a-library.md)
         + [Läsa ett bibliotek](web-service-api/api-usage/manage-libraries/read-a-library.md)
         + [Uppdatera ett bibliotek](web-service-api/api-usage/manage-libraries/update-a-library.md)
         + [Ta bort ett bibliotek](web-service-api/api-usage/manage-libraries/delete-a-library.md)
         + [Läs alla bibliotek i organisationen](web-service-api/api-usage/manage-libraries/read-all-libraries-in-your-organization.md)
         + [Ange en rankning i dina bibliotek](web-service-api/api-usage/manage-libraries/set-a-ran-on-your-libraries.md)
         + [Skaffa ett biblioteks rankning](web-service-api/api-usage/manage-libraries/get-a-librarys-rank.md)
      + Hantera intressepunkter {#manage-pois}
         + [Hantera POI-översikt](web-service-api/api-usage/manage-pois/manage-pois.md)
         + [Skapa en POI](web-service-api/api-usage/manage-pois/create-a-poi.md)
         + [Läsa ett POI](web-service-api/api-usage/manage-pois/read-a-poi.md)
         + [Uppdatera en POI](web-service-api/api-usage/manage-pois/update-a-poi.md)
         + [Ta bort en POI](web-service-api/api-usage/manage-pois/delete-a-poi.md)
         + [Läs alla POI:er i ett bibliotek](web-service-api/api-usage/manage-pois/read-all-pois-in-a-library.md)
         + [Läs alla POI:er i organisationen](web-service-api/api-usage/manage-pois/read-all-pois-in-your-organization.md)
         + Grupp-API:er {#batch-apis}
            + [Översikt över API:er för grupp](web-service-api/api-usage/manage-pois/batch-apis/batch-apis.md)
            + [Skapa flera POI](web-service-api/api-usage/manage-pois/batch-apis/create-multiple-pois.md)
            + [Uppdatera flera POI](web-service-api/api-usage/manage-pois/batch-apis/update-multiple-pois.md)
            + [Ta bort flera POI](web-service-api/api-usage/manage-pois/batch-apis/delete-multiple-pois.md)
      + [Fråga API:er](web-service-api/api-usage/query-apis.md)
+ Tillägg för mobil SDK {#places-ext-aep-sdks}
   + [Platstillägg](places-ext-aep-sdks/places-extension/places-extension.md)
+ [Använd Platstjänst med din egen övervakningslösning](using-your-own-monitor.md)
+ [Använd platstjänsten utan övervakning av aktiva regioner](use-places-without-active-monitoring.md)
+ Använd Platstjänst som en del av Experience Platform Launch-arbetsflödet {#use-places-launch-workflow}
   + [Använd Platstjänst som en del av Experience Platform Launch-arbetsflödet](use-places-launch-workflow/places-launch-workflow.md)
   + [Definiera dataelement](use-places-launch-workflow/define-data-elements.md)
   + [Skapa regler för inträde och utträde](use-places-launch-workflow/create-rule-places-property.md)
+ Använd Platstjänst med andra Adobe-lösningar {#use-places-with-other-solutions}
   + Adobe Analytics {#places-adobe-analytics}
      + [Använd Platstjänst med Adobe Analytics](use-places-with-other-solutions/places-adobe-analytics/use-places-analytics-overview.md)
      + [Skicka POI-post och avsluta data till Analytics](use-places-with-other-solutions/places-adobe-analytics/use-places-adobe-analytics.md)
      + [Lägg till platskontext i Analytics-begäranden](use-places-with-other-solutions/places-adobe-analytics/run-reports-aa-places-data.md)
      + [Rapport om platsdata i Analytics Workspace](use-places-with-other-solutions/places-adobe-analytics/places-in-workspace.md)
   + Adobe Mobile Services {#places-mobile-svcs-messaging}
      + [Adobe Mobile Services](use-places-with-other-solutions/places-mobile-svcs-for-messaging/use-places-mobie-svcs-messaging.md)
      + [Push-meddelanden](use-places-with-other-solutions/places-mobile-svcs-for-messaging/mobile-svcs-messaging-push.md)
      + [Meddelanden i appen](use-places-with-other-solutions/places-mobile-svcs-for-messaging/mobile-svcs-messaging-inapp.md)
   + Adobe Campaign Standard {#places-acs}
      + [Använd Platstjänst med Adobe Campaign Standard](use-places-with-other-solutions/places-acs/places-acs-overview.md)
      + [Push-meddelanden](use-places-with-other-solutions/places-acs/places-acs-push-notifications.md)
      + [Meddelanden i appen](use-places-with-other-solutions/places-acs/places-acs-in-app-messages.md)
   + Adobe Target {#places-target}
      + [Använd Platstjänst med Adobe Target](use-places-with-other-solutions/places-target/places-target.md)
+ Testning och validering {#places-testing-validation}
   + [Testa och validera platstjänst](places-testing-validation/test-validate-places.md)
+ [Vanliga frågor och svar](places-faqs.md)
