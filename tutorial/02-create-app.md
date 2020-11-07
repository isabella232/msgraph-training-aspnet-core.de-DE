---
ms.openlocfilehash: 308938efbedc4618c7b0ca3ea6b2eebc0582da10
ms.sourcegitcommit: 9d0d10a9e8e5a1d80382d89bc412df287bee03f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822484"
---
<!-- markdownlint-disable MD002 MD041 -->

Erstellen Sie zunächst eine ASP.net Core-Webanwendung.

1. Öffnen Sie die Befehlszeilenschnittstelle (CLI) in einem Verzeichnis, in dem Sie das Projekt erstellen möchten. Führen Sie den folgenden Befehl aus.

    ```Shell
    dotnet new mvc -o GraphTutorial
    ```

1. Nachdem das Projekt erstellt wurde, stellen Sie sicher, dass es funktioniert, indem Sie das aktuelle Verzeichnis in das **GraphTutorial** -Verzeichnis ändern und den folgenden Befehl in ihrer CLI ausführen.

    ```Shell
    dotnet run
    ```

1. Öffnen Sie den Browser, und navigieren Sie zu `https://localhost:5001` . Wenn alles funktioniert, sollte eine standardmäßige ASP.net-Kern Seite angezeigt werden.

> [!IMPORTANT]
> Wenn Sie eine Warnung erhalten, dass das Zertifikat für **localhost** nicht vertrauenswürdig ist, können Sie die .net-Kern-CLI verwenden, um das Entwicklungszertifikat zu installieren und ihm zu vertrauen. Anweisungen zu bestimmten Betriebssystemen finden Sie unter [Erzwingen von HTTPS in ASP.net Core](/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1) .

## <a name="add-nuget-packages"></a>Hinzufügen von NuGet-Paketen

Bevor Sie fortfahren, installieren Sie einige zusätzliche NuGet-Pakete, die Sie später verwenden werden.

- [Microsoft. Identity. Internet](https://www.nuget.org/packages/Microsoft.Identity.Web/) zum Anfordern und Verwalten von Zugriffstoken.
- [Microsoft. Identity. Internet. Microsoft Graph](https://www.nuget.org/packages/Microsoft.Identity.Web.MicrosoftGraph/) zum Hinzufügen des Microsoft Graph-SDK über Dependency Injection.
- [Microsoft. Identity. Internet. UI](https://www.nuget.org/packages/Microsoft.Identity.Web.UI/) für die Benutzeroberfläche für die Anmeldung und Abmeldung.
- [Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) zum Aufrufen von Microsoft Graph
- [TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) zur plattformübergreifenden Verarbeitung von Zeitzonenbezeichnern.

1. Führen Sie die folgenden Befehle in der CLI aus, um die Abhängigkeiten zu installieren.

    ```Shell
    dotnet add package Microsoft.Identity.Web --version 1.1.0
    dotnet add package Microsoft.Identity.MicrosoftGraph --version 1.1.0
    dotnet add package Microsoft.Identity.Web.UI --version 1.1.0
    dotnet add package Microsoft.Graph --version 3.18.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a>Entwerfen der App

In diesem Abschnitt wird die grundlegende UI-Struktur der Anwendung erstellt.

### <a name="implement-alert-extension-methods"></a>Implementieren von Warnungs Erweiterungsmethoden

In diesem Abschnitt erstellen Sie Erweiterungsmethoden für den `IActionResult` Typ, der von Controller Ansichten zurückgegeben wird. Mit dieser Erweiterung können temporäre Fehler oder Erfolgsmeldungen an die Ansicht übergeben werden.

> [!TIP]
> Sie können einen beliebigen Text-Editor verwenden, um die Quelldateien für dieses Lernprogramm zu bearbeiten. [Visual Studio Code](https://code.visualstudio.com/) stellt jedoch zusätzliche Features bereit, beispielsweise Debuggen und IntelliSense.

1. Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Alerts**.

1. Erstellen Sie eine neue Datei mit dem Namen **WithAlertResult.cs** im Verzeichnis **./Alerts** , und fügen Sie den folgenden Code hinzu.

    :::code language="csharp" source="../demo/GraphTutorial/Alerts/WithAlertResult.cs" id="WithAlertResultSnippet":::

1. Erstellen Sie eine neue Datei mit dem Namen **AlertExtensions.cs** im Verzeichnis **./Alerts** , und fügen Sie den folgenden Code hinzu.

    :::code language="csharp" source="../demo/GraphTutorial/Alerts/AlertExtensions.cs" id="AlertExtensionsSnippet":::

### <a name="implement-user-data-extension-methods"></a>Implementieren von Benutzerdaten Erweiterungsmethoden

In diesem Abschnitt erstellen Sie Erweiterungsmethoden für das `ClaimsPrincipal` Objekt, das von der Microsoft Identity-Plattform generiert wird. Auf diese Weise können Sie die vorhandene Benutzeridentität mit Daten aus Microsoft Graph erweitern.

> [!NOTE]
> Dieser Code ist nur ein Platzhalter für jetzt, Sie werden ihn in einem späteren Abschnitt fertig stellen.

1. Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Graph**.

1. Erstellen Sie eine neue Datei mit dem Namen **GraphClaimsPrincipalExtensions.cs** , und fügen Sie den folgenden Code hinzu.

    ```csharp
    using System.Security.Claims;

    namespace GraphTutorial
    {
        public static class GraphClaimTypes {
            public const string DisplayName ="graph_name";
            public const string Email = "graph_email";
            public const string Photo = "graph_photo";
            public const string TimeZone = "graph_timezone";
            public const string DateTimeFormat = "graph_datetimeformat";
        }

        // Helper methods to access Graph user data stored in
        // the claims principal
        public static class GraphClaimsPrincipalExtensions
        {
            public static string GetUserGraphDisplayName(this ClaimsPrincipal claimsPrincipal)
            {
                return "Adele Vance";
            }

            public static string GetUserGraphEmail(this ClaimsPrincipal claimsPrincipal)
            {
                return "adelev@contoso.com";
            }

            public static string GetUserGraphPhoto(this ClaimsPrincipal claimsPrincipal)
            {
                return "/img/no-profile-photo.png";
            }
        }
    }
    ```

### <a name="create-views"></a>Erstellen von Ansichten

In diesem Abschnitt werden die Razor-Ansichten für die Anwendung implementiert.

1. Fügen Sie eine neue Datei mit dem Namen " **_LoginPartial. cshtml** " im Verzeichnis **./views/Shared** hinzu, und fügen Sie den folgenden Code hinzu.

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Shared/_LoginPartial.cshtml" id="LoginPartialSnippet":::

1. Fügen Sie eine neue Datei mit dem Namen " **_AlertPartial. cshtml** " im Verzeichnis **./views/Shared** hinzu, und fügen Sie den folgenden Code hinzu.

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Shared/_AlertPartial.cshtml" id="AlertPartialSnippet":::

1. Öffnen Sie die Datei **./Views/Shared/_Layout. cshtml** , und ersetzen Sie den gesamten Inhalt durch den folgenden Code, um das globale Layout der App zu aktualisieren.

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Shared/_Layout.cshtml" id="LayoutSnippet":::

1. Öffnen Sie **/wwwroot/CSS/Site.CSS** , und fügen Sie den folgenden Code am Ende der Datei hinzu.

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/site.css" id="CssSnippet":::

1. Öffnen Sie die Datei **./views/Home/Index.cshtml** , und ersetzen Sie den Inhalt durch Folgendes.

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Home/Index.cshtml" id="HomeIndexSnippet":::

1. Erstellen Sie ein neues Verzeichnis im **./wwwroot** -Verzeichnis mit dem Namen **IMG**. Fügen Sie in diesem Verzeichnis eine Bilddatei Ihrer Wahl namens **no-profile-photo.png** hinzu. Dieses Bild wird als Foto des Benutzers verwendet, wenn der Benutzer in Microsoft Graph kein Foto hat.

    > [!TIP]
    > Sie können das in diesen Screenshots verwendete Bild von [GitHub](https://github.com/microsoftgraph/msgraph-training-aspnet-core/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png)herunterladen.

1. Speichern Sie alle Änderungen, und starten Sie den Server neu ( `dotnet run` ). Nun sollte die APP sehr unterschiedlich aussehen.

    ![Screenshot der neu gestalteten Homepage](./images/create-app-01.png)
