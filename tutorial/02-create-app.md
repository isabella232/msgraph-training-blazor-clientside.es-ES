---
ms.openlocfilehash: 744df064e4fdc1bbf7821ae43a7b7878148902e9
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584682"
---
<!-- markdownlint-disable MD002 MD041 -->

Empiece por crear una aplicación de webassembler increíblemente brillante.

1. Abra la interfaz de línea de comandos (CLI) en un directorio donde desee crear el proyecto. Ejecute el comando siguiente.

    ```Shell
    dotnet new blazorwasm --auth SingleOrg -o GraphTutorial
    ```

    El `--auth SingleOrg` parámetro hace que el proyecto generado incluya la configuración para la autenticación con la plataforma de identidad de Microsoft.

1. Una vez creado el proyecto, compruebe que funciona cambiando el directorio actual al directorio **GraphTutorial** y ejecutando el siguiente comando en la CLI.

    ```Shell
    dotnet watch run
    ```

1. Abra el explorador y vaya a `https://localhost:5001` . Si todo funciona, debería ver un "Hola a todos". Mensaje.

> [!IMPORTANT]
> Si recibe una advertencia de que el certificado para **localhost** no es de confianza, puede usar .net Core CLI para instalar y confiar en el certificado de desarrollo. Consulte [forzar HTTPS en ASP.net Core](/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1) para obtener instrucciones sobre sistemas operativos específicos.

## <a name="add-nuget-packages"></a>Agregar paquetes NuGet

Antes de continuar, instale algunos paquetes NuGet adicionales que usará más adelante.

- [Microsoft. Graph](https://www.nuget.org/packages/Microsoft.Graph/) para realizar llamadas a Microsoft Graph.
- [TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) para traducir los identificadores de zona horaria de Windows a identificadores de IANA.

1. Ejecute los siguientes comandos en su CLI para instalar las dependencias.

    ```Shell
    dotnet add package Microsoft.Graph --version 3.18.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a>Diseñar la aplicación

En esta sección, creará la estructura básica de la interfaz de usuario de la aplicación.

1. Quita las páginas de ejemplo generadas por la plantilla. Elimine los siguientes archivos.

    - **./Pages/Counter.razor**
    - **./Pages/FetchData.razor**
    - **./Shared/SurveyPrompt.razor**
    - **./wwwroot/Sample-Data/weather.jsen**

1. Abra **./wwwroot/index.html** y agregue el siguiente código justo **antes** de la `</body>` etiqueta de cierre.

    :::code language="html" source="../demo/GraphTutorial/wwwroot/index.html" id="BootStrapJSSnippet":::

    Esto agrega los archivos JavaScript de [bootstrap](https://getbootstrap.com/docs/4.5/getting-started/introduction/) .

1. Abra el **./wwwroot/CSS/app.CSS** y agregue el siguiente código.

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/app.css" id="CssSnippet":::

1. Abra **./Shared/NavMenu.Razor** y reemplace su contenido por lo siguiente.

    :::code language="razor" source="../demo/GraphTutorial/Shared/NavMenu.razor" id="NavMenuSnippet":::

1. Abra **./pages/index.Razor** y reemplace su contenido por lo siguiente.

    :::code language="razor" source="../demo/GraphTutorial/Pages/Index.razor" id="IndexSnippet":::

1. Abra **./Shared/LoginDisplay.Razor** y reemplace su contenido por lo siguiente.

    ```razor
    @using Microsoft.AspNetCore.Components.Authorization
    @using Microsoft.AspNetCore.Components.WebAssembly.Authentication

    @inject NavigationManager Navigation
    @inject SignOutSessionStateManager SignOutManager

    <AuthorizeView>
        <Authorized>
            <a class="text-decoration-none" data-toggle="dropdown" href="#" role="button">
                <img src="/img/no-profile-photo.png" class="nav-profile-photo rounded-circle align-self-center mr-2">
            </a>
            <div class="dropdown-menu dropdown-menu-right">
                <h5 class="dropdown-item-text mb-0">@context.User.Identity.Name</h5>
                <p class="dropdown-item-text text-muted mb-0">placeholder@contoso.com</p>
                <div class="dropdown-divider"></div>
                <button class="dropdown-item" @onclick="BeginLogout">Log out</button>
            </div>
        </Authorized>
        <NotAuthorized>
            <a href="authentication/login">Log in</a>
        </NotAuthorized>
    </AuthorizeView>

    @code{
        private async Task BeginLogout(MouseEventArgs args)
        {
            await SignOutManager.SetSignOutState();
            Navigation.NavigateTo("authentication/logout");
        }
    }
    ```

1. Cree un nuevo directorio en el directorio **./wwwroot** denominado **IMG**. Agregue un archivo de imagen de su elección con nombre **no-profile-photo.png** en este directorio. Esta imagen se utilizará como foto del usuario cuando el usuario no tenga foto en Microsoft Graph.

    > [!TIP]
    > Puede descargar la imagen usada en estas capturas de pantallas desde [GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).

1. Guarde todos los cambios y actualice la página.

    ![Una captura de pantalla de la Página principal rediseñada](./images/create-app-01.png)
