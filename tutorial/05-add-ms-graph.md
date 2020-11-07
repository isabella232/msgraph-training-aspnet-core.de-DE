---
ms.openlocfilehash: 17394dd6283464eabcbea1f60c48640412b55431
ms.sourcegitcommit: 9d0d10a9e8e5a1d80382d89bc412df287bee03f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822502"
---
<!-- markdownlint-disable MD002 MD041 -->

In diesem Abschnitt werden Sie Microsoft Graph in die Anwendung integrieren. Für diese Anwendung verwenden Sie die [Microsoft Graph-Clientbibliothek für .net](https://github.com/microsoftgraph/msgraph-sdk-dotnet) , um Anrufe an Microsoft Graph zu tätigen.

## <a name="get-calendar-events-from-outlook"></a>Abrufen von Kalenderereignissen von Outlook

Erstellen Sie zunächst einen neuen Controller für Kalenderansichten.

1. Fügen Sie im Verzeichnis **./Controllers** eine neue Datei mit dem Namen **CalendarController.cs** hinzu, und fügen Sie den folgenden Code hinzu.

    ```csharp
    using GraphTutorial.Models;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Logging;
    using Microsoft.Identity.Web;
    using Microsoft.Graph;
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    using TimeZoneConverter;

    namespace GraphTutorial.Controllers
    {
        public class CalendarController : Controller
        {
            private readonly GraphServiceClient _graphClient;
            private readonly ILogger<HomeController> _logger;

            public CalendarController(
                GraphServiceClient graphClient,
                ILogger<HomeController> logger)
            {
                _graphClient = graphClient;
                _logger = logger;
            }
        }
    }
    ```

1. Fügen Sie der Klasse die folgenden Funktionen hinzu `CalendarController` , um die Kalenderansicht des Benutzers abzurufen.

    :::code language="csharp" source="../demo/GraphTutorial/Controllers/CalendarController.cs" id="GetCalendarViewSnippet":::

    Überprüfen Sie, was der Code in `GetUserWeekCalendar` ausführt.

    - Es verwendet die Zeitzone des Benutzers, um UTC-Start-und-End-Datum/-Uhrzeitwerte für die Woche abzurufen.
    - Er fragt die [Kalenderansicht](/graph/api/calendar-list-calendarview?view=graph-rest-1.0) des Benutzers ab, um alle Ereignisse abzurufen, die zwischen den Start-und Enddatum/-Zeiten liegen. Das Verwenden einer Kalenderansicht anstelle von [Ereignislisten](/graph/api/user-list-events?view=graph-rest-1.0) erweitert wiederkehrende Ereignisse und gibt alle Vorkommen zurück, die im angegebenen Zeitfenster vorkommen.
    - Es verwendet die `Prefer: outlook.timezone` Kopfzeile, um Ergebnisse zurück in der Zeitzone des Benutzers abzurufen.
    - Es wird verwendet `Select` , um die Felder einzuschränken, die auf nur die von der APP verwendeten zurückkommen.
    - Sie verwendet `OrderBy` , um die Ergebnisse chronologisch zu sortieren.
    - Es verwendet ein `PageIterator` to- [Page durch die Events-Auflistung](/graph/sdks/paging). Dadurch wird der Fall behandelt, in dem der Benutzer über mehr Ereignisse in seinem Kalender verfügt als die angeforderte Seitengröße.

1. Fügen Sie die folgende Funktion zur `CalendarController` -Klasse hinzu, um eine temporäre Ansicht der zurückgegebenen Daten zu implementieren.

    ```csharp
    // Minimum permission scope needed for this view
    [AuthorizeForScopes(Scopes = new[] { "Calendars.Read" })]
    public async Task<IActionResult> Index()
    {
        try
        {
            var userTimeZone = TZConvert.GetTimeZoneInfo(
                User.GetUserGraphTimeZone());
            var startOfWeek = CalendarController.GetUtcStartOfWeekInTimeZone(
                DateTime.Today, userTimeZone);

            var events = await GetUserWeekCalendar(startOfWeek);

            // Return a JSON dump of events
            return new ContentResult {
                Content = _graphClient.HttpProvider.Serializer.SerializeObject(events),
                ContentType = "application/json"
            };
        }
        catch (ServiceException ex)
        {
            if (ex.InnerException is MicrosoftIdentityWebChallengeUserException)
            {
                throw ex;
            }

            return new ContentResult {
                Content = $"Error getting calendar view: {ex.Message}",
                ContentType = "text/plain"
            };
        }
    }
    ```

1. Starten Sie die App, melden Sie sich an, und klicken Sie auf den Link **Kalender** in der Navigationsleiste. Wenn alles funktioniert, sollte ein JSON-Abbild von Ereignissen im Kalender des Benutzers angezeigt werden.

## <a name="display-the-results"></a>Anzeigen der Ergebnisse

Jetzt können Sie eine Ansicht hinzufügen, um die Ergebnisse benutzerfreundlicher anzuzeigen.

### <a name="create-view-models"></a>Erstellen von ansichtsmodellen

1. Erstellen Sie eine neue Datei mit dem Namen **CalendarViewEvent.cs** im Verzeichnis **./Models** , und fügen Sie den folgenden Code hinzu.

    :::code language="csharp" source="../demo/GraphTutorial/Models/CalendarViewEvent.cs" id="CalendarViewEventSnippet":::

1. Erstellen Sie eine neue Datei mit dem Namen **DailyViewModel.cs** im Verzeichnis **./Models** , und fügen Sie den folgenden Code hinzu.

    :::code language="csharp" source="../demo/GraphTutorial/Models/DailyViewModel.cs" id="DailyViewModelSnippet":::

1. Erstellen Sie eine neue Datei mit dem Namen **CalendarViewModel.cs** im Verzeichnis **./Models** , und fügen Sie den folgenden Code hinzu.

    :::code language="csharp" source="../demo/GraphTutorial/Models/CalendarViewModel.cs" id="CalendarViewModelSnippet":::

### <a name="create-views"></a>Erstellen von Ansichten

1. Erstellen Sie ein neues Verzeichnis namens **Calendar** im Verzeichnis **./views** .

1. Erstellen Sie eine neue Datei mit dem Namen **_DailyEventsPartial. cshtml** im Verzeichnis **./views/Calendar** , und fügen Sie den folgenden Code hinzu.

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Calendar/_DailyEventsPartial.cshtml" id="DailyEventsPartialSnippet":::

1. Erstellen Sie eine neue Datei mit dem Namen **Index. cshtml** im Verzeichnis **./views/Calendar** , und fügen Sie den folgenden Code hinzu.

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Calendar/Index.cshtml" id="CalendarIndexSnippet":::

### <a name="update-calendar-controller"></a>Kalender Controller aktualisieren

1. Öffnen Sie **./Controllers/CalendarController.cs** , und ersetzen Sie die vorhandene `Index` Funktion durch Folgendes.

    :::code language="csharp" source="../demo/GraphTutorial/Controllers/CalendarController.cs" id="IndexSnippet":::

1. Starten Sie die App, melden Sie sich an, und klicken Sie auf den Link **Kalender**. Die App sollte nun eine Tabelle mit Ereignissen rendern.

    ![Ein Screenshot der Tabelle mit Ereignissen](./images/add-msgraph-01.png)
