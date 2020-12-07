---
ms.openlocfilehash: 33bdb86a4a4af997c8ca522e23ec2f883fdeda88
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584693"
---
<!-- markdownlint-disable MD002 MD041 -->

En esta sección, incorporará Microsoft Graph a la aplicación para obtener una vista del calendario del usuario para la semana actual.

## <a name="get-a-calendar-view"></a>Obtener una vista de calendario

1. Cree un nuevo archivo en el directorio **./páginas** denominado **Calendar. Razor** y agregue el código siguiente.

    ```razor
    @page "/calendar"
    @using Microsoft.Graph
    @using TimeZoneConverter

    @inject GraphTutorial.Graph.GraphClientFactory clientFactory

    <AuthorizeView>
        <Authorized>
            <!-- Temporary JSON dump of events -->
            <code>@graphClient.HttpProvider.Serializer.SerializeObject(events)</code>
        </Authorized>
        <NotAuthorized>
            <RedirectToLogin />
        </NotAuthorized>
    </AuthorizeView>

    @code{
        [CascadingParameter]
        private Task<AuthenticationState> authenticationStateTask { get; set; }

        private GraphServiceClient graphClient;
        private IList<Event> events = new List<Event>();
        private string dateTimeFormat;
    }
    ```

1. Agregue el siguiente código dentro de la `@code{}` sección.

    :::code language="csharp" source="../demo/GraphTutorial/Pages/Calendar.razor" id="GetEventsSnippet":::

    Considere lo que hace este código.

    - Obtiene la zona horaria, el formato de fecha y el formato de hora del usuario actual de las notificaciones personalizadas agregadas al usuario.
    - Calcula el inicio y el final de la semana actual en la zona horaria preferida del usuario.
    - Obtiene una vista de calendario de Microsoft Graph para la semana actual.
        - Incluye el `Prefer: outlook.timezone` encabezado para que Microsoft Graph devuelva las `start` propiedades y `end` en la zona horaria especificada.
        - Usa `Top(50)` para solicitar hasta 50 eventos en la respuesta.
        - Usa `Select(u => new {})` para solicitar solo las propiedades que usa la aplicación.
        - Usa `OrderBy("start/dateTime")` para ordenar los resultados por hora de inicio.

1. Guarde todos los cambios y reinicie la aplicación. Elija el elemento de navegación **calendario** . La aplicación muestra una representación JSON de los eventos devueltos desde Microsoft Graph.

## <a name="display-the-results"></a>Mostrar los resultados

Ahora puede reemplazar el volcado de JSON con algo más fácil de uso.

1. Agregue la siguiente función dentro de la `@code{}` sección.

    :::code language="csharp" source="../demo/GraphTutorial/Pages/Calendar.razor" id="FormatDateSnippet":::

    Este código toma una cadena de fecha ISO 8601 y la convierte en el formato de fecha y hora preferido del usuario.

1. Reemplace el `<code>` elemento que hay en el `<Authorized>` elemento por lo siguiente.

    :::code language="razor" source="../demo/GraphTutorial/Pages/Calendar.razor" id="CalendarViewSnippet":::

    Se crea una tabla de los eventos devueltos por Microsoft Graph.

1. Guarde los cambios y reinicie la aplicación. Ahora la página de **calendario** representa una tabla de eventos.

    ![Una captura de pantalla de la aplicación que muestra una tabla de eventos](images/calendar-view.png)
