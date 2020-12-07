---
ms.openlocfilehash: f98548a1332417d92b126a2cb7499fea5306b34f
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584644"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="166ab-101">En este ejercicio, ampliará la aplicación del ejercicio anterior para admitir la autenticación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="166ab-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="166ab-102">Esto es necesario para obtener el token de acceso de OAuth necesario para llamar a la API de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="166ab-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph API.</span></span>

1. <span data-ttu-id="166ab-103">Open **./wwwroot/appsettings.js**.</span><span class="sxs-lookup"><span data-stu-id="166ab-103">Open **./wwwroot/appsettings.json**.</span></span> <span data-ttu-id="166ab-104">Agregue una `GraphScopes` propiedad y actualice los `Authority` `ClientId` valores y para que se correspondan con lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="166ab-104">Add a `GraphScopes` property and update the `Authority` and `ClientId` values to match the following.</span></span>

    :::code language="json" source="../demo/GraphTutorial/wwwroot/appsettings.example.json" highlight="3-4,7":::

    <span data-ttu-id="166ab-105">Reemplace `YOUR_APP_ID_HERE` por el identificador de la aplicación del registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="166ab-105">Replace `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="166ab-106">Si usa un control de código fuente como GIT, ahora sería un buen momento para excluir la **appsettings.jsen** el archivo del control de código fuente para evitar la pérdida inadvertida del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="166ab-106">If you're using source control such as git, now would be a good time to exclude the **appsettings.json** file from source control to avoid inadvertently leaking your app ID.</span></span>

    <span data-ttu-id="166ab-107">Revise los ámbitos incluidos en el `GraphScopes` valor.</span><span class="sxs-lookup"><span data-stu-id="166ab-107">Review the scopes included in the `GraphScopes` value.</span></span>

    - <span data-ttu-id="166ab-108">**User. Read** permite a la aplicación obtener el perfil y la foto del usuario.</span><span class="sxs-lookup"><span data-stu-id="166ab-108">**User.Read** allows the application to get the user's profile and photo.</span></span>
    - <span data-ttu-id="166ab-109">**MailboxSettings. Read** permite a la aplicación obtener la configuración del buzón de correo, que incluye la zona horaria preferida del usuario.</span><span class="sxs-lookup"><span data-stu-id="166ab-109">**MailboxSettings.Read** allows the application to get mailbox settings, which includes the user's preferred time zone.</span></span>
    - <span data-ttu-id="166ab-110">**Calendars. ReadWrite** permite que la aplicación Lea y escriba en el calendario del usuario.</span><span class="sxs-lookup"><span data-stu-id="166ab-110">**Calendars.ReadWrite** allows the application to read and write to the user's calendar.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="166ab-111">Implementar el inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="166ab-111">Implement sign-in</span></span>

<span data-ttu-id="166ab-112">En este momento, la plantilla de proyecto .NET Core ha agregado el código para habilitar el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="166ab-112">At this point the .NET Core project template has added the code to enable sign in.</span></span> <span data-ttu-id="166ab-113">Sin embargo, en esta sección, agregará código adicional para mejorar la experiencia agregando información de Microsoft Graph a la identidad del usuario.</span><span class="sxs-lookup"><span data-stu-id="166ab-113">However, in this section you'll add additional code to improve the experience by adding information from Microsoft Graph to the user's identity.</span></span>

1. <span data-ttu-id="166ab-114">Abra **./pages/Authentication.Razor** y reemplace su contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="166ab-114">Open **./Pages/Authentication.razor** and replace its contents with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/Authentication.razor" id="AuthenticationSnippet":::

    <span data-ttu-id="166ab-115">Esto reemplaza el mensaje de error predeterminado cuando se produce un error en el inicio de sesión para mostrar cualquier mensaje de error devuelto por el proceso de autenticación.</span><span class="sxs-lookup"><span data-stu-id="166ab-115">This replaces the default error message when login fails to display any error message returned by the authentication process.</span></span>

1. <span data-ttu-id="166ab-116">Cree un nuevo directorio en la raíz del proyecto denominado **Graph**.</span><span class="sxs-lookup"><span data-stu-id="166ab-116">Create a new directory in the root of the project named **Graph**.</span></span>

1. <span data-ttu-id="166ab-117">Cree un archivo nuevo en el directorio **./Graph** denominado **GraphUserAccountFactory.CS** y agregue el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="166ab-117">Create a new file in the **./Graph** directory named **GraphUserAccountFactory.cs** and add the following code.</span></span>

    ```csharp
    using System.Security.Claims;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Components.WebAssembly.Authentication;
    using Microsoft.AspNetCore.Components.WebAssembly.Authentication.Internal;
    using Microsoft.Extensions.Logging;
    using Microsoft.Graph;

    namespace GraphTutorial.Graph
    {
        // Extends the AccountClaimsPrincipalFactory that builds
        // a user identity from the identity token.
        // This class adds additional claims to the user's ClaimPrincipal
        // that hold values from Microsoft Graph
        public class GraphUserAccountFactory
            : AccountClaimsPrincipalFactory<RemoteUserAccount>
        {
            private readonly IAccessTokenProviderAccessor accessor;
            private readonly ILogger<GraphUserAccountFactory> logger;

            public GraphUserAccountFactory(IAccessTokenProviderAccessor accessor,
                ILogger<GraphUserAccountFactory> logger)
            : base(accessor)
            {
                this.accessor = accessor;
                this.logger = logger;
            }

            public async override ValueTask<ClaimsPrincipal> CreateUserAsync(
                RemoteUserAccount account,
                RemoteAuthenticationUserOptions options)
            {
                // Create the base user
                var initialUser = await base.CreateUserAsync(account, options);

                // If authenticated, we can call Microsoft Graph
                if (initialUser.Identity.IsAuthenticated)
                {
                    try
                    {
                        // Add additional info from Graph to the identity
                        await AddGraphInfoToClaims(accessor, initialUser);
                    }
                    catch (AccessTokenNotAvailableException exception)
                    {
                        logger.LogError($"Graph API access token failure: {exception.Message}");
                    }
                    catch (ServiceException exception)
                    {
                        logger.LogError($"Graph API error: {exception.Message}");
                        logger.LogError($"Response body: {exception.RawResponseBody}");
                    }
                }

                return initialUser;
            }

            private async Task AddGraphInfoToClaims(
                IAccessTokenProviderAccessor accessor,
                ClaimsPrincipal claimsPrincipal)
            {
                // TEMPORARY: Get the token and log it
                var result = await accessor.TokenProvider.RequestAccessToken();

                if (result.TryGetToken(out var token))
                {
                    logger.LogInformation($"Access token: {token.Value}");
                }
            }
        }
    }
    ```

    <span data-ttu-id="166ab-118">Esta clase amplía la clase **AccountClaimsPrincipalFactory** y reemplaza el `CreateUserAsync` método.</span><span class="sxs-lookup"><span data-stu-id="166ab-118">This class extends the **AccountClaimsPrincipalFactory** class and overrides the `CreateUserAsync` method.</span></span> <span data-ttu-id="166ab-119">Por ahora, este método solo registra el token de acceso para fines de depuración.</span><span class="sxs-lookup"><span data-stu-id="166ab-119">For now, this method only logs the access token for debugging purposes.</span></span> <span data-ttu-id="166ab-120">Implementará las llamadas de Microsoft Graph más adelante en este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="166ab-120">You'll implement the Microsoft Graph calls later in this exercise.</span></span>

1. <span data-ttu-id="166ab-121">Abra **./Program.CS** y agregue las siguientes `using` instrucciones en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="166ab-121">Open **./Program.cs** and add the following `using` statements at the top of the file.</span></span>

    ```csharp
    using Microsoft.AspNetCore.Components.WebAssembly.Authentication;
    using GraphTutorial.Graph;
    ```

1. <span data-ttu-id="166ab-122">Dentro `Main` de, reemplace la `builder.Services.AddMsalAuthentication` llamada existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="166ab-122">Inside `Main`, replace the existing `builder.Services.AddMsalAuthentication` call with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Program.cs" id="AddMsalAuthSnippet":::

    <span data-ttu-id="166ab-123">Considere lo que hace este código.</span><span class="sxs-lookup"><span data-stu-id="166ab-123">Consider what this code does.</span></span>

    - <span data-ttu-id="166ab-124">Carga el valor de `GraphScopes` desde **appsettings.js** y agrega cada ámbito a los ámbitos predeterminados que usa el proveedor de MSAL.</span><span class="sxs-lookup"><span data-stu-id="166ab-124">It loads the value of `GraphScopes` from **appsettings.json** and adds each scope to the default scopes used by the MSAL provider.</span></span>
    - <span data-ttu-id="166ab-125">Reemplaza a la fábrica de cuentas existente con la clase **GraphUserAccountFactory** .</span><span class="sxs-lookup"><span data-stu-id="166ab-125">It replaces the existing account factory with the **GraphUserAccountFactory** class.</span></span>

1. <span data-ttu-id="166ab-126">Guarde los cambios y reinicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="166ab-126">Save your changes and restart the app.</span></span> <span data-ttu-id="166ab-127">Use el vínculo **iniciar sesión** para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="166ab-127">Use the **Log in** link to log in.</span></span> <span data-ttu-id="166ab-128">Revise y acepte los permisos solicitados.</span><span class="sxs-lookup"><span data-stu-id="166ab-128">Review and accept the requested permissions.</span></span>

1. <span data-ttu-id="166ab-129">La aplicación se actualiza con un mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="166ab-129">The app refreshes with a welcome message.</span></span> <span data-ttu-id="166ab-130">Obtenga acceso a las herramientas de desarrollo del explorador y revise la pestaña de la **consola** . La aplicación registra el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="166ab-130">Access your browser's developer tools and review the **Console** tab. The app logs the access token.</span></span>

    ![Captura de pantalla de la ventana herramientas de desarrollo del explorador que muestra el token de acceso](images/access-token.png)

## <a name="get-user-details"></a><span data-ttu-id="166ab-132">Obtener detalles del usuario</span><span class="sxs-lookup"><span data-stu-id="166ab-132">Get user details</span></span>

<span data-ttu-id="166ab-133">Una vez que el usuario haya iniciado sesión, podrá obtener su información de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="166ab-133">Once the user is logged in, you can get their information from Microsoft Graph.</span></span> <span data-ttu-id="166ab-134">En esta sección, usará información de Microsoft Graph para agregar notificaciones adicionales al **ClaimsPrincipal** del usuario.</span><span class="sxs-lookup"><span data-stu-id="166ab-134">In this section you'll use information from Microsoft Graph to add additional claims to the user's **ClaimsPrincipal**.</span></span>

1. <span data-ttu-id="166ab-135">Cree un archivo nuevo en el directorio **./Graph** denominado **GraphClaimsPrincipalExtensions.CS** y agregue el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="166ab-135">Create a new file in the **./Graph** directory named **GraphClaimsPrincipalExtensions.cs** and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphClaimsPrincipalExtensions.cs" id="GraphClaimsExtensionsSnippet":::

    <span data-ttu-id="166ab-136">Este código implementa métodos de extensión para la clase **ClaimsPrincipal** que permiten obtener y establecer notificaciones con valores de objetos de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="166ab-136">This code implements extension methods for the **ClaimsPrincipal** class that allow you to get and set claims with values from Microsoft Graph objects.</span></span>

1. <span data-ttu-id="166ab-137">Cree un archivo nuevo en el directorio **./Graph** denominado **BlazorAuthProvider.CS** y agregue el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="166ab-137">Create a new file in the **./Graph** directory named **BlazorAuthProvider.cs** and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/BlazorAuthProvider.cs" id="BlazorAuthProviderSnippet":::

    <span data-ttu-id="166ab-138">Este código implementa un proveedor de autenticación para el SDK de Microsoft Graph que usa el **IAccessTokenProviderAccessor** proporcionado por el paquete **Microsoft. AspNetCore. Components. webassembly. Authentication** para obtener los tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="166ab-138">This code implements an authentication provider for the Microsoft Graph SDK that uses the **IAccessTokenProviderAccessor** provided by the **Microsoft.AspNetCore.Components.WebAssembly.Authentication** package to get access tokens.</span></span>

1. <span data-ttu-id="166ab-139">Cree un archivo nuevo en el directorio **./Graph** denominado **GraphClientFactory.CS** y agregue el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="166ab-139">Create a new file in the **./Graph** directory named **GraphClientFactory.cs** and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphClientFactory.cs" id="GraphClientFactorySnippet":::

    <span data-ttu-id="166ab-140">Esta clase crea un **GraphServiceClient** configurado con **BlazorAuthProvider**.</span><span class="sxs-lookup"><span data-stu-id="166ab-140">This class creates a **GraphServiceClient** configured with the **BlazorAuthProvider**.</span></span>

1. <span data-ttu-id="166ab-141">Abra **./Program.CS** y cambie la **BaseAddress** del nuevo **HttpClient** a `"https://graph.microsoft.com"` .</span><span class="sxs-lookup"><span data-stu-id="166ab-141">Open **./Program.cs** and change the **BaseAddress** of the new **HttpClient** to `"https://graph.microsoft.com"`.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Program.cs" id="HttpClientSnippet":::

1. <span data-ttu-id="166ab-142">Agregue el siguiente código antes de la `await builder.Build().RunAsync();` línea.</span><span class="sxs-lookup"><span data-stu-id="166ab-142">Add the following code before the `await builder.Build().RunAsync();` line.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Program.cs" id="AddGraphClientFactorySnippet":::

    <span data-ttu-id="166ab-143">Esto agrega la **GraphClientFactory** como servicio con ámbito que podemos hacer disponible a través de la inserción de dependencias.</span><span class="sxs-lookup"><span data-stu-id="166ab-143">This adds the **GraphClientFactory** as a scoped service that we can make available via dependency injection.</span></span>

1. <span data-ttu-id="166ab-144">Abra **./Graph/GraphUserAccountFactory.CS** y agregue la siguiente propiedad a la clase.</span><span class="sxs-lookup"><span data-stu-id="166ab-144">Open **./Graph/GraphUserAccountFactory.cs** and add the following property to the class.</span></span>

    ```csharp
    private readonly GraphClientFactory clientFactory;
    ```

1. <span data-ttu-id="166ab-145">Actualice el constructor para que tome un parámetro **GraphClientFactory** y asígnelo a la `clientFactory` propiedad.</span><span class="sxs-lookup"><span data-stu-id="166ab-145">Update the constructor to take a **GraphClientFactory** parameter and assign it to the `clientFactory` property.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphUserAccountFactory.cs" id="ConstructorSnippet" highlight="2,7":::

1. <span data-ttu-id="166ab-146">Reemplace la función `AddGraphInfoToClaims` existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="166ab-146">Replace the existing `AddGraphInfoToClaims` function with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphUserAccountFactory.cs" id="AddGraphInfoToClaimsSnippet":::

    <span data-ttu-id="166ab-147">Considere lo que hace este código.</span><span class="sxs-lookup"><span data-stu-id="166ab-147">Consider what this code does.</span></span>

    - <span data-ttu-id="166ab-148">[Obtiene el perfil del usuario](https://docs.microsoft.com/graph/api/user-get).</span><span class="sxs-lookup"><span data-stu-id="166ab-148">It [gets the user's profile](https://docs.microsoft.com/graph/api/user-get).</span></span>
        - <span data-ttu-id="166ab-149">Se usa `Select` para limitar las propiedades que se devuelven.</span><span class="sxs-lookup"><span data-stu-id="166ab-149">It uses `Select` to limit which properties are returned.</span></span>
    - <span data-ttu-id="166ab-150">[Obtiene la foto del usuario](https://docs.microsoft.com/graph/api/profilephoto-get).</span><span class="sxs-lookup"><span data-stu-id="166ab-150">It [gets the user's photo](https://docs.microsoft.com/graph/api/profilephoto-get).</span></span>
        - <span data-ttu-id="166ab-151">Solicita específicamente la versión en píxeles 48x48 de la foto del usuario.</span><span class="sxs-lookup"><span data-stu-id="166ab-151">It requests specifically the 48x48 pixel version of the user's photo.</span></span>
    - <span data-ttu-id="166ab-152">Agrega la información a **ClaimsPrincipal**.</span><span class="sxs-lookup"><span data-stu-id="166ab-152">It adds the information to the **ClaimsPrincipal**.</span></span>

1. <span data-ttu-id="166ab-153">Abra **./Shared/LoginDisplay.Razor** y realice los siguientes cambios.</span><span class="sxs-lookup"><span data-stu-id="166ab-153">Open **./Shared/LoginDisplay.razor** and make the following changes.</span></span>

    - <span data-ttu-id="166ab-154">Reemplazar `/img/no-profile-photo.png` por `@(context.User.GetUserGraphPhoto() ?? "/img/no-profile-photo.png")` .</span><span class="sxs-lookup"><span data-stu-id="166ab-154">Replace `/img/no-profile-photo.png` with `@(context.User.GetUserGraphPhoto() ?? "/img/no-profile-photo.png")`.</span></span>
    - <span data-ttu-id="166ab-155">Reemplazar `placeholder@contoso.com` por `@context.User.GetUserGraphEmail()` .</span><span class="sxs-lookup"><span data-stu-id="166ab-155">Replace `placeholder@contoso.com` with `@context.User.GetUserGraphEmail()`.</span></span>

    ```razor
    ...
    <img src="@(context.User.GetUserGraphPhoto() ?? "/img/no-profile-photo.png")"
         class="nav-profile-photo rounded-circle align-self-center mr-2">

    ...

    <p class="dropdown-item-text text-muted mb-0">@context.User.GetUserGraphEmail()</p>
    ...
    ```

1. <span data-ttu-id="166ab-156">Guarde todos los cambios y reinicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="166ab-156">Save all of your changes and restart the app.</span></span> <span data-ttu-id="166ab-157">Inicie sesión en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="166ab-157">Log into the app.</span></span> <span data-ttu-id="166ab-158">La aplicación se actualiza para mostrar la foto del usuario en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="166ab-158">The app updates to show the user's photo in the top menu.</span></span> <span data-ttu-id="166ab-159">Al seleccionar la foto del usuario se abre un menú desplegable con el nombre del usuario, la dirección de correo electrónico y un botón **Cerrar sesión** .</span><span class="sxs-lookup"><span data-stu-id="166ab-159">Selecting the user's photo opens a drop-down menu with the user's name, email address, and a **Log out** button.</span></span>

    ![Una captura de pantalla de la aplicación con la foto del usuario mostrada](images/user-photo.png)

    ![Captura de pantalla del menú desplegable](images/user-info.png)
