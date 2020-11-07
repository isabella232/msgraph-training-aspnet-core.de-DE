---
ms.openlocfilehash: 30398bafbf47aaa374a200dd1834c9f2003e967f
ms.sourcegitcommit: 9d0d10a9e8e5a1d80382d89bc412df287bee03f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822444"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="d47e0-101">Vorgehensweise Ausführen des abgeschlossenen Projekts</span><span class="sxs-lookup"><span data-stu-id="d47e0-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d47e0-102">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="d47e0-102">Prerequisites</span></span>

<span data-ttu-id="d47e0-103">Um das abgeschlossene Projekt in diesem Ordner auszuführen, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="d47e0-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="d47e0-104">Das [.net Core SDK](https://dotnet.microsoft.com/download) , das auf Ihrem Entwicklungscomputer installiert ist.</span><span class="sxs-lookup"><span data-stu-id="d47e0-104">The [.NET Core SDK](https://dotnet.microsoft.com/download) installed on your development machine.</span></span> <span data-ttu-id="d47e0-105">( **Hinweis:** dieses Lernprogramm wurde mit .net Core SDK Version 3.1.201 geschrieben.</span><span class="sxs-lookup"><span data-stu-id="d47e0-105">( **Note:** This tutorial was written with .NET Core SDK version 3.1.201.</span></span> <span data-ttu-id="d47e0-106">Die Schritte in diesem Leitfaden funktionieren möglicherweise mit anderen Versionen, aber das wurde nicht getestet.)</span><span class="sxs-lookup"><span data-stu-id="d47e0-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="d47e0-107">Entweder ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits-oder Schulkonto.</span><span class="sxs-lookup"><span data-stu-id="d47e0-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="d47e0-108">Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="d47e0-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="d47e0-109">Sie können [sich für ein neues persönliches Microsoft-Konto registrieren](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="d47e0-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="d47e0-110">Sie können sich [für das Office 365 Entwicklerprogramm registrieren](https://developer.microsoft.com/office/dev-program) , um ein kostenloses Office 365-Abonnement zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="d47e0-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="d47e0-111">Registrieren einer Webanwendung im Azure-Active Directory Admin Center</span><span class="sxs-lookup"><span data-stu-id="d47e0-111">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="d47e0-112">Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d47e0-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="d47e0-113">Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.</span><span class="sxs-lookup"><span data-stu-id="d47e0-113">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="d47e0-114">Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="d47e0-114">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="d47e0-115">Screenshot der APP-Registrierungen</span><span class="sxs-lookup"><span data-stu-id="d47e0-115">A screenshot of the App registrations</span></span> ](../tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="d47e0-116">Wählen Sie **Neue Registrierung** aus.</span><span class="sxs-lookup"><span data-stu-id="d47e0-116">Select **New registration**.</span></span> <span data-ttu-id="d47e0-117">Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.</span><span class="sxs-lookup"><span data-stu-id="d47e0-117">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="d47e0-118">Legen Sie **Name** auf `ASP.NET Core Graph Tutorial` fest.</span><span class="sxs-lookup"><span data-stu-id="d47e0-118">Set **Name** to `ASP.NET Core Graph Tutorial`.</span></span>
    - <span data-ttu-id="d47e0-119">Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.</span><span class="sxs-lookup"><span data-stu-id="d47e0-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="d47e0-120">Legen Sie unter **Umleitungs-URI** die erste Dropdownoption auf `Web` fest, und legen Sie den Wert auf `https://localhost:5001/` fest.</span><span class="sxs-lookup"><span data-stu-id="d47e0-120">Under **Redirect URI** , set the first drop-down to `Web` and set the value to `https://localhost:5001/`.</span></span>

    ![Screenshot der Seite "Anwendung registrieren"](../tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="d47e0-122">Wählen Sie **Registrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="d47e0-122">Select **Register**.</span></span> <span data-ttu-id="d47e0-123">Kopieren Sie auf der Seite **ASP.net Core Graph Tutorial** den Wert der **Anwendungs-ID (Client)** , und speichern Sie ihn, und Sie benötigen ihn im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="d47e0-123">On the **ASP.NET Core Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](../tutorial/images/aad-application-id.png)

1. <span data-ttu-id="d47e0-125">Wählen Sie unter **Verwalten** die Option **Authentifizierung** aus.</span><span class="sxs-lookup"><span data-stu-id="d47e0-125">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="d47e0-126">Fügen Sie unter **Umleitungs-URIs** einen URI mit dem Wert hinzu `https://localhost:5001/signin-oidc` .</span><span class="sxs-lookup"><span data-stu-id="d47e0-126">Under **Redirect URIs** add a URI with the value `https://localhost:5001/signin-oidc`.</span></span>

1. <span data-ttu-id="d47e0-127">Legen Sie die **Abmelde-URL** auf fest `https://localhost:5001/signout-oidc` .</span><span class="sxs-lookup"><span data-stu-id="d47e0-127">Set the **Logout URL** to `https://localhost:5001/signout-oidc`.</span></span>

1. <span data-ttu-id="d47e0-128">Suchen Sie den Abschnitt **Implizite Gewährung** , und aktivieren Sie **ID-Token**.</span><span class="sxs-lookup"><span data-stu-id="d47e0-128">Locate the **Implicit grant** section and enable **ID tokens**.</span></span> <span data-ttu-id="d47e0-129">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="d47e0-129">Select **Save**.</span></span>

    ![Screenshot der Einstellungen für die Webplattform im Azure-Portal](../tutorial/images/aad-web-platform.png)

1. <span data-ttu-id="d47e0-131">Wählen Sie unter **Verwalten** die Option **Zertifikate und Geheime Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="d47e0-131">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="d47e0-132">Wählen Sie die Schaltfläche **Neuen geheimen Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="d47e0-132">Select the **New client secret** button.</span></span> <span data-ttu-id="d47e0-133">Geben Sie einen Wert in **Beschreibung** ein, wählen Sie eine der Optionen für **Gilt bis** aus, und wählen Sie dann **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="d47e0-133">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

    ![Screenshot des Dialogfelds "Geheimen Clientschlüssel hinzufügen"](../tutorial/images/aad-new-client-secret.png)

1. <span data-ttu-id="d47e0-135">Kopieren Sie den Wert des geheimen Clientschlüssels, bevor Sie diese Seite verlassen.</span><span class="sxs-lookup"><span data-stu-id="d47e0-135">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="d47e0-136">Sie benötigen ihn im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="d47e0-136">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d47e0-137">Dieser geheime Clientschlüssel wird nicht noch einmal angezeigt, stellen Sie daher sicher, dass Sie ihn jetzt kopieren.</span><span class="sxs-lookup"><span data-stu-id="d47e0-137">This client secret is never shown again, so make sure you copy it now.</span></span>

    ![Screenshot des neu hinzugefügten Clientschlüssels](../tutorial/images/aad-copy-client-secret.png)

## <a name="configure-the-sample"></a><span data-ttu-id="d47e0-139">Konfigurieren des Beispiels</span><span class="sxs-lookup"><span data-stu-id="d47e0-139">Configure the sample</span></span>

1. <span data-ttu-id="d47e0-140">Öffnen Sie die Befehlszeilenschnittstelle in dem Verzeichnis, in dem sich **GraphTutorial. csproj** befindet, und führen Sie die folgenden Befehle aus, indem `YOUR_APP_ID` Sie die Anwendungs-ID aus dem Azure-Portal und den `YOUR_APP_SECRET` geheimen Anwendungsschlüssel ersetzen.</span><span class="sxs-lookup"><span data-stu-id="d47e0-140">Open your command line interface (CLI) in the directory where **GraphTutorial.csproj** is located, and run the following commands, substituting `YOUR_APP_ID` with your application ID from the Azure portal, and `YOUR_APP_SECRET` with your application secret.</span></span>

    ```Shell
    dotnet user-secrets init
    dotnet user-secrets set "AzureAd:ClientId" "YOUR_APP_ID"
    dotnet user-secrets set "AzureAd:ClientSecret" "YOUR_APP_SECRET"
    ```

## <a name="run-the-sample"></a><span data-ttu-id="d47e0-141">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="d47e0-141">Run the sample</span></span>

<span data-ttu-id="d47e0-142">Führen Sie in der CLI den folgenden Befehl aus, um die Anwendung zu starten.</span><span class="sxs-lookup"><span data-stu-id="d47e0-142">In your CLI, run the following command to start the application.</span></span>

```Shell
dotnet run
```
