---
ms.openlocfilehash: debd685996df22a83110a14ca585cfafa4e08a0d
ms.sourcegitcommit: 9d0d10a9e8e5a1d80382d89bc412df287bee03f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822429"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="67ca2-101">In dieser Übung erstellen Sie mithilfe des Azure Active Directory Admin Center eine neue Azure AD-Webanwendungs Registrierung.</span><span class="sxs-lookup"><span data-stu-id="67ca2-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="67ca2-102">Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67ca2-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="67ca2-103">Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.</span><span class="sxs-lookup"><span data-stu-id="67ca2-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="67ca2-104">Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="67ca2-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="67ca2-105">Screenshot der APP-Registrierungen</span><span class="sxs-lookup"><span data-stu-id="67ca2-105">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="67ca2-106">Wählen Sie **Neue Registrierung** aus.</span><span class="sxs-lookup"><span data-stu-id="67ca2-106">Select **New registration**.</span></span> <span data-ttu-id="67ca2-107">Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.</span><span class="sxs-lookup"><span data-stu-id="67ca2-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="67ca2-108">Legen Sie **Name** auf `ASP.NET Core Graph Tutorial` fest.</span><span class="sxs-lookup"><span data-stu-id="67ca2-108">Set **Name** to `ASP.NET Core Graph Tutorial`.</span></span>
    - <span data-ttu-id="67ca2-109">Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.</span><span class="sxs-lookup"><span data-stu-id="67ca2-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="67ca2-110">Legen Sie unter **Umleitungs-URI** die erste Dropdownoption auf `Web` fest, und legen Sie den Wert auf `https://localhost:5001/` fest.</span><span class="sxs-lookup"><span data-stu-id="67ca2-110">Under **Redirect URI** , set the first drop-down to `Web` and set the value to `https://localhost:5001/`.</span></span>

    ![Screenshot der Seite "Anwendung registrieren"](./images/aad-register-an-app.png)

1. <span data-ttu-id="67ca2-112">Wählen Sie **Registrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="67ca2-112">Select **Register**.</span></span> <span data-ttu-id="67ca2-113">Kopieren Sie auf der Seite **ASP.net Core Graph Tutorial** den Wert der **Anwendungs-ID (Client)** , und speichern Sie ihn, und Sie benötigen ihn im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="67ca2-113">On the **ASP.NET Core Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](./images/aad-application-id.png)

1. <span data-ttu-id="67ca2-115">Wählen Sie unter **Verwalten** die Option **Authentifizierung** aus.</span><span class="sxs-lookup"><span data-stu-id="67ca2-115">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="67ca2-116">Fügen Sie unter **Umleitungs-URIs** einen URI mit dem Wert hinzu `https://localhost:5001/signin-oidc` .</span><span class="sxs-lookup"><span data-stu-id="67ca2-116">Under **Redirect URIs** add a URI with the value `https://localhost:5001/signin-oidc`.</span></span>

1. <span data-ttu-id="67ca2-117">Legen Sie die **Abmelde-URL** auf fest `https://localhost:5001/signout-oidc` .</span><span class="sxs-lookup"><span data-stu-id="67ca2-117">Set the **Logout URL** to `https://localhost:5001/signout-oidc`.</span></span>

1. <span data-ttu-id="67ca2-118">Suchen Sie den Abschnitt **Implizite Gewährung** , und aktivieren Sie **ID-Token**.</span><span class="sxs-lookup"><span data-stu-id="67ca2-118">Locate the **Implicit grant** section and enable **ID tokens**.</span></span> <span data-ttu-id="67ca2-119">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="67ca2-119">Select **Save**.</span></span>

    ![Screenshot der Einstellungen für die Webplattform im Azure-Portal](./images/aad-web-platform.png)

1. <span data-ttu-id="67ca2-121">Wählen Sie unter **Verwalten** die Option **Zertifikate und Geheime Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="67ca2-121">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="67ca2-122">Wählen Sie die Schaltfläche **Neuen geheimen Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="67ca2-122">Select the **New client secret** button.</span></span> <span data-ttu-id="67ca2-123">Geben Sie einen Wert in **Beschreibung** ein, wählen Sie eine der Optionen für **Gilt bis** aus, und wählen Sie dann **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="67ca2-123">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

    ![Screenshot des Dialogfelds "Geheimen Clientschlüssel hinzufügen"](./images/aad-new-client-secret.png)

1. <span data-ttu-id="67ca2-125">Kopieren Sie den Wert des geheimen Clientschlüssels, bevor Sie diese Seite verlassen.</span><span class="sxs-lookup"><span data-stu-id="67ca2-125">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="67ca2-126">Sie benötigen ihn im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="67ca2-126">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="67ca2-127">Dieser geheime Clientschlüssel wird nicht noch einmal angezeigt, stellen Sie daher sicher, dass Sie ihn jetzt kopieren.</span><span class="sxs-lookup"><span data-stu-id="67ca2-127">This client secret is never shown again, so make sure you copy it now.</span></span>

    ![Screenshot des neu hinzugefügten Clientschlüssels](./images/aad-copy-client-secret.png)
