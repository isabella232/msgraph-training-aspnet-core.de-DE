---
ms.openlocfilehash: f70714a0bc2588fc67d63096b4ab746380bb8e2c
ms.sourcegitcommit: 9d0d10a9e8e5a1d80382d89bc412df287bee03f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822330"
---
<!-- markdownlint-disable MD002 MD041 -->

In diesem Abschnitt können Sie die Möglichkeit zum Erstellen von Ereignissen im Kalender des Benutzers hinzufügen.

## <a name="create-model"></a>Modell erstellen

1. Erstellen Sie eine neue Datei mit dem Namen **NewEvent.cs** im Verzeichnis **./Models** , und fügen Sie den folgenden Code hinzu.

    :::code language="csharp" source="../demo/GraphTutorial/Models/NewEvent.cs" id="NewEventSnippet":::

## <a name="create-view"></a>Ansicht erstellen

1. Erstellen Sie eine neue Datei namens " **New. cshtml** " im Verzeichnis "He **./views/Calendar** ", und fügen Sie den folgenden Code hinzu.

    :::code language="cshtml" source="../demo/GraphTutorial/Views/Calendar/New.cshtml" id="NewFormSnippet":::

## <a name="add-controller-actions"></a>Hinzufügen von controlleraktionen

1. Öffnen Sie **/Controllers/CalendarController.cs** , und fügen Sie der Klasse die folgende Aktion hinzu `CalendarController` , um das neue Ereignis Formular zu rendern.

    :::code language="csharp" source="../demo/GraphTutorial/Controllers/CalendarController.cs" id="CalendarNewGetSnippet":::

1. Fügen Sie der Klasse die folgende Aktion hinzu, `CalendarController` um das neue Ereignis aus dem Formular zu erhalten, wenn der Benutzer auf **Speichern** klickt und Microsoft Graph verwendet, um das Ereignis dem Kalender des Benutzers hinzuzufügen.

    :::code language="csharp" source="../demo/GraphTutorial/Controllers/CalendarController.cs" id="CalendarNewPostSnippet":::

1. Starten Sie die App, melden Sie sich an, und klicken Sie auf den Link **Kalender**. Klicken Sie auf die Schaltfläche **Neues Ereignis** , füllen Sie das Formular aus, und klicken Sie auf **Speichern**.

    ![Screenshot des neuen Ereignis Formulars](./images/create-event-01.png)
