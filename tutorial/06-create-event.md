---
ms.openlocfilehash: f70714a0bc2588fc67d63096b4ab746380bb8e2c
ms.sourcegitcommit: 9d0d10a9e8e5a1d80382d89bc412df287bee03f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822330"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="8f4b2-101">In diesem Abschnitt können Sie die Möglichkeit zum Erstellen von Ereignissen im Kalender des Benutzers hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8f4b2-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-model"></a><span data-ttu-id="8f4b2-102">Modell erstellen</span><span class="sxs-lookup"><span data-stu-id="8f4b2-102">Create model</span></span>

1. <span data-ttu-id="8f4b2-103">Erstellen Sie eine neue Datei mit dem Namen **NewEvent.cs** im Verzeichnis **./Models** , und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="8f4b2-103">Create a new file named **NewEvent.cs** in the **./Models** directory and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Models/NewEvent.cs" id="NewEventSnippet":::

## <a name="create-view"></a><span data-ttu-id="8f4b2-104">Ansicht erstellen</span><span class="sxs-lookup"><span data-stu-id="8f4b2-104">Create view</span></span>

1. <span data-ttu-id="8f4b2-105">Erstellen Sie eine neue Datei namens " **New. cshtml** " im Verzeichnis "He **./views/Calendar** ", und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="8f4b2-105">Create a new file named **New.cshtml** in he **./Views/Calendar** directory and add the following code.</span></span>

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Calendar/New.cshtml" id="NewFormSnippet":::

## <a name="add-controller-actions"></a><span data-ttu-id="8f4b2-106">Hinzufügen von controlleraktionen</span><span class="sxs-lookup"><span data-stu-id="8f4b2-106">Add controller actions</span></span>

1. <span data-ttu-id="8f4b2-107">Öffnen Sie **/Controllers/CalendarController.cs** , und fügen Sie der Klasse die folgende Aktion hinzu `CalendarController` , um das neue Ereignis Formular zu rendern.</span><span class="sxs-lookup"><span data-stu-id="8f4b2-107">Open **./Controllers/CalendarController.cs** and add the following action to the `CalendarController` class to render the new event form.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Controllers/CalendarController.cs" id="CalendarNewGetSnippet":::

1. <span data-ttu-id="8f4b2-108">Fügen Sie der Klasse die folgende Aktion hinzu, `CalendarController` um das neue Ereignis aus dem Formular zu erhalten, wenn der Benutzer auf **Speichern** klickt und Microsoft Graph verwendet, um das Ereignis dem Kalender des Benutzers hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="8f4b2-108">Add the following action to the `CalendarController` class to receive the new event from the form when the user clicks **Save** and use Microsoft Graph to add the event to the user's calendar.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Controllers/CalendarController.cs" id="CalendarNewPostSnippet":::

1. <span data-ttu-id="8f4b2-109">Starten Sie die App, melden Sie sich an, und klicken Sie auf den Link **Kalender**.</span><span class="sxs-lookup"><span data-stu-id="8f4b2-109">Start the app, sign in, and click the **Calendar** link.</span></span> <span data-ttu-id="8f4b2-110">Klicken Sie auf die Schaltfläche **Neues Ereignis** , füllen Sie das Formular aus, und klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="8f4b2-110">Click the **New event** button, fill in the form, and click **Save**.</span></span>

    ![Screenshot des neuen Ereignis Formulars](./images/create-event-01.png)
