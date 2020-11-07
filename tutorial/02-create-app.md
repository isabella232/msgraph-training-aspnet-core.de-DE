---
ms.openlocfilehash: 308938efbedc4618c7b0ca3ea6b2eebc0582da10
ms.sourcegitcommit: 9d0d10a9e8e5a1d80382d89bc412df287bee03f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822484"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="24787-101">Erstellen Sie zunächst eine ASP.net Core-Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="24787-101">Start by creating an ASP.NET Core web app.</span></span>

1. <span data-ttu-id="24787-102">Öffnen Sie die Befehlszeilenschnittstelle (CLI) in einem Verzeichnis, in dem Sie das Projekt erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="24787-102">Open your command-line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="24787-103">Führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="24787-103">Run the following command.</span></span>

    ```Shell
    dotnet new mvc -o GraphTutorial
    ```

1. <span data-ttu-id="24787-104">Nachdem das Projekt erstellt wurde, stellen Sie sicher, dass es funktioniert, indem Sie das aktuelle Verzeichnis in das **GraphTutorial** -Verzeichnis ändern und den folgenden Befehl in ihrer CLI ausführen.</span><span class="sxs-lookup"><span data-stu-id="24787-104">Once the project is created, verify that it works by changing the current directory to the **GraphTutorial** directory and running the following command in your CLI.</span></span>

    ```Shell
    dotnet run
    ```

1. <span data-ttu-id="24787-105">Öffnen Sie den Browser, und navigieren Sie zu `https://localhost:5001` .</span><span class="sxs-lookup"><span data-stu-id="24787-105">Open your browser and browse to `https://localhost:5001`.</span></span> <span data-ttu-id="24787-106">Wenn alles funktioniert, sollte eine standardmäßige ASP.net-Kern Seite angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="24787-106">If everything is working, you should see a default ASP.NET Core page.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24787-107">Wenn Sie eine Warnung erhalten, dass das Zertifikat für **localhost** nicht vertrauenswürdig ist, können Sie die .net-Kern-CLI verwenden, um das Entwicklungszertifikat zu installieren und ihm zu vertrauen.</span><span class="sxs-lookup"><span data-stu-id="24787-107">If you receive a warning that the certificate for **localhost** is un-trusted you can use the .NET Core CLI to install and trust the development certificate.</span></span> <span data-ttu-id="24787-108">Anweisungen zu bestimmten Betriebssystemen finden Sie unter [Erzwingen von HTTPS in ASP.net Core](/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1) .</span><span class="sxs-lookup"><span data-stu-id="24787-108">See [Enforce HTTPS in ASP.NET Core](/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1) for instructions for specific operating systems.</span></span>

## <a name="add-nuget-packages"></a><span data-ttu-id="24787-109">Hinzufügen von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="24787-109">Add NuGet packages</span></span>

<span data-ttu-id="24787-110">Bevor Sie fortfahren, installieren Sie einige zusätzliche NuGet-Pakete, die Sie später verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="24787-110">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="24787-111">[Microsoft. Identity. Internet](https://www.nuget.org/packages/Microsoft.Identity.Web/) zum Anfordern und Verwalten von Zugriffstoken.</span><span class="sxs-lookup"><span data-stu-id="24787-111">[Microsoft.Identity.Web](https://www.nuget.org/packages/Microsoft.Identity.Web/) for requesting and managing access tokens.</span></span>
- <span data-ttu-id="24787-112">[Microsoft. Identity. Internet. Microsoft Graph](https://www.nuget.org/packages/Microsoft.Identity.Web.MicrosoftGraph/) zum Hinzufügen des Microsoft Graph-SDK über Dependency Injection.</span><span class="sxs-lookup"><span data-stu-id="24787-112">[Microsoft.Identity.Web.MicrosoftGraph](https://www.nuget.org/packages/Microsoft.Identity.Web.MicrosoftGraph/) for adding the Microsoft Graph SDK via dependency injection.</span></span>
- <span data-ttu-id="24787-113">[Microsoft. Identity. Internet. UI](https://www.nuget.org/packages/Microsoft.Identity.Web.UI/) für die Benutzeroberfläche für die Anmeldung und Abmeldung.</span><span class="sxs-lookup"><span data-stu-id="24787-113">[Microsoft.Identity.Web.UI](https://www.nuget.org/packages/Microsoft.Identity.Web.UI/) for sign-in and sign-out UI.</span></span>
- <span data-ttu-id="24787-114">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) zum Aufrufen von Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="24787-114">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) for making calls to Microsoft Graph.</span></span>
- <span data-ttu-id="24787-115">[TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) zur plattformübergreifenden Verarbeitung von Zeitzonenbezeichnern.</span><span class="sxs-lookup"><span data-stu-id="24787-115">[TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) for handling time zoned identifiers cross-platform.</span></span>

1. <span data-ttu-id="24787-116">Führen Sie die folgenden Befehle in der CLI aus, um die Abhängigkeiten zu installieren.</span><span class="sxs-lookup"><span data-stu-id="24787-116">Run the following commands in your CLI to install the dependencies.</span></span>

    ```Shell
    dotnet add package Microsoft.Identity.Web --version 1.1.0
    dotnet add package Microsoft.Identity.MicrosoftGraph --version 1.1.0
    dotnet add package Microsoft.Identity.Web.UI --version 1.1.0
    dotnet add package Microsoft.Graph --version 3.18.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a><span data-ttu-id="24787-117">Entwerfen der App</span><span class="sxs-lookup"><span data-stu-id="24787-117">Design the app</span></span>

<span data-ttu-id="24787-118">In diesem Abschnitt wird die grundlegende UI-Struktur der Anwendung erstellt.</span><span class="sxs-lookup"><span data-stu-id="24787-118">In this section you will create the basic UI structure of the application.</span></span>

### <a name="implement-alert-extension-methods"></a><span data-ttu-id="24787-119">Implementieren von Warnungs Erweiterungsmethoden</span><span class="sxs-lookup"><span data-stu-id="24787-119">Implement alert extension methods</span></span>

<span data-ttu-id="24787-120">In diesem Abschnitt erstellen Sie Erweiterungsmethoden für den `IActionResult` Typ, der von Controller Ansichten zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="24787-120">In this section you will create extension methods for the `IActionResult` type returned by controller views.</span></span> <span data-ttu-id="24787-121">Mit dieser Erweiterung können temporäre Fehler oder Erfolgsmeldungen an die Ansicht übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="24787-121">This extension will enable passing temporary error or success messages to the view.</span></span>

> [!TIP]
> <span data-ttu-id="24787-122">Sie können einen beliebigen Text-Editor verwenden, um die Quelldateien für dieses Lernprogramm zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="24787-122">You can use any text editor to edit the source files for this tutorial.</span></span> <span data-ttu-id="24787-123">[Visual Studio Code](https://code.visualstudio.com/) stellt jedoch zusätzliche Features bereit, beispielsweise Debuggen und IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="24787-123">However, [Visual Studio Code](https://code.visualstudio.com/) provides additional features, such as debugging and Intellisense.</span></span>

1. <span data-ttu-id="24787-124">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Alerts**.</span><span class="sxs-lookup"><span data-stu-id="24787-124">Create a new directory in the **GraphTutorial** directory named **Alerts**.</span></span>

1. <span data-ttu-id="24787-125">Erstellen Sie eine neue Datei mit dem Namen **WithAlertResult.cs** im Verzeichnis **./Alerts** , und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="24787-125">Create a new file named **WithAlertResult.cs** in the **./Alerts** directory and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Alerts/WithAlertResult.cs" id="WithAlertResultSnippet":::

1. <span data-ttu-id="24787-126">Erstellen Sie eine neue Datei mit dem Namen **AlertExtensions.cs** im Verzeichnis **./Alerts** , und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="24787-126">Create a new file named **AlertExtensions.cs** in the **./Alerts** directory and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Alerts/AlertExtensions.cs" id="AlertExtensionsSnippet":::

### <a name="implement-user-data-extension-methods"></a><span data-ttu-id="24787-127">Implementieren von Benutzerdaten Erweiterungsmethoden</span><span class="sxs-lookup"><span data-stu-id="24787-127">Implement user data extension methods</span></span>

<span data-ttu-id="24787-128">In diesem Abschnitt erstellen Sie Erweiterungsmethoden für das `ClaimsPrincipal` Objekt, das von der Microsoft Identity-Plattform generiert wird.</span><span class="sxs-lookup"><span data-stu-id="24787-128">In this section you will create extension methods for the `ClaimsPrincipal` object generated by the Microsoft Identity platform.</span></span> <span data-ttu-id="24787-129">Auf diese Weise können Sie die vorhandene Benutzeridentität mit Daten aus Microsoft Graph erweitern.</span><span class="sxs-lookup"><span data-stu-id="24787-129">This will allow you to extend the existing user identity with data from Microsoft Graph.</span></span>

> [!NOTE]
> <span data-ttu-id="24787-130">Dieser Code ist nur ein Platzhalter für jetzt, Sie werden ihn in einem späteren Abschnitt fertig stellen.</span><span class="sxs-lookup"><span data-stu-id="24787-130">This code is just a placeholder for now, you will complete it in a later section.</span></span>

1. <span data-ttu-id="24787-131">Erstellen Sie ein neues Verzeichnis im **GraphTutorial** -Verzeichnis mit dem Namen **Graph**.</span><span class="sxs-lookup"><span data-stu-id="24787-131">Create a new directory in the **GraphTutorial** directory named **Graph**.</span></span>

1. <span data-ttu-id="24787-132">Erstellen Sie eine neue Datei mit dem Namen **GraphClaimsPrincipalExtensions.cs** , und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="24787-132">Create a new file named **GraphClaimsPrincipalExtensions.cs** and add the following code.</span></span>

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

### <a name="create-views"></a><span data-ttu-id="24787-133">Erstellen von Ansichten</span><span class="sxs-lookup"><span data-stu-id="24787-133">Create views</span></span>

<span data-ttu-id="24787-134">In diesem Abschnitt werden die Razor-Ansichten für die Anwendung implementiert.</span><span class="sxs-lookup"><span data-stu-id="24787-134">In this section you will implement the Razor views for the application.</span></span>

1. <span data-ttu-id="24787-135">Fügen Sie eine neue Datei mit dem Namen " **_LoginPartial. cshtml** " im Verzeichnis **./views/Shared** hinzu, und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="24787-135">Add a new file named **_LoginPartial.cshtml** in the **./Views/Shared** directory and add the following code.</span></span>

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Shared/_LoginPartial.cshtml" id="LoginPartialSnippet":::

1. <span data-ttu-id="24787-136">Fügen Sie eine neue Datei mit dem Namen " **_AlertPartial. cshtml** " im Verzeichnis **./views/Shared** hinzu, und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="24787-136">Add a new file named **_AlertPartial.cshtml** in the **./Views/Shared** directory and add the following code.</span></span>

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Shared/_AlertPartial.cshtml" id="AlertPartialSnippet":::

1. <span data-ttu-id="24787-137">Öffnen Sie die Datei **./Views/Shared/_Layout. cshtml** , und ersetzen Sie den gesamten Inhalt durch den folgenden Code, um das globale Layout der App zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="24787-137">Open the **./Views/Shared/_Layout.cshtml** file, and replace its entire contents with the following code to update the global layout of the app.</span></span>

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Shared/_Layout.cshtml" id="LayoutSnippet":::

1. <span data-ttu-id="24787-138">Öffnen Sie **/wwwroot/CSS/Site.CSS** , und fügen Sie den folgenden Code am Ende der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="24787-138">Open **./wwwroot/css/site.css** and add the following code at the bottom of the file.</span></span>

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/site.css" id="CssSnippet":::

1. <span data-ttu-id="24787-139">Öffnen Sie die Datei **./views/Home/Index.cshtml** , und ersetzen Sie den Inhalt durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="24787-139">Open the **./Views/Home/index.cshtml** file and replace its contents with the following.</span></span>

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Home/Index.cshtml" id="HomeIndexSnippet":::

1. <span data-ttu-id="24787-140">Erstellen Sie ein neues Verzeichnis im **./wwwroot** -Verzeichnis mit dem Namen **IMG**.</span><span class="sxs-lookup"><span data-stu-id="24787-140">Create a new directory in the **./wwwroot** directory named **img**.</span></span> <span data-ttu-id="24787-141">Fügen Sie in diesem Verzeichnis eine Bilddatei Ihrer Wahl namens **no-profile-photo.png** hinzu.</span><span class="sxs-lookup"><span data-stu-id="24787-141">Add an image file of your choosing named **no-profile-photo.png** in this directory.</span></span> <span data-ttu-id="24787-142">Dieses Bild wird als Foto des Benutzers verwendet, wenn der Benutzer in Microsoft Graph kein Foto hat.</span><span class="sxs-lookup"><span data-stu-id="24787-142">This image will be used as the user's photo when the user has no photo in Microsoft Graph.</span></span>

    > [!TIP]
    > <span data-ttu-id="24787-143">Sie können das in diesen Screenshots verwendete Bild von [GitHub](https://github.com/microsoftgraph/msgraph-training-aspnet-core/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png)herunterladen.</span><span class="sxs-lookup"><span data-stu-id="24787-143">You can download the image used in these screenshots from [GitHub](https://github.com/microsoftgraph/msgraph-training-aspnet-core/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).</span></span>

1. <span data-ttu-id="24787-144">Speichern Sie alle Änderungen, und starten Sie den Server neu ( `dotnet run` ).</span><span class="sxs-lookup"><span data-stu-id="24787-144">Save all of your changes and restart the server (`dotnet run`).</span></span> <span data-ttu-id="24787-145">Nun sollte die APP sehr unterschiedlich aussehen.</span><span class="sxs-lookup"><span data-stu-id="24787-145">Now, the app should look very different.</span></span>

    ![Screenshot der neu gestalteten Homepage](./images/create-app-01.png)
