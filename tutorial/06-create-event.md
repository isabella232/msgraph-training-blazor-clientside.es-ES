---
ms.openlocfilehash: 723f1d08b9d1085d47d0d5fac71da5371badc3d0
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584637"
---
<!-- markdownlint-disable MD002 MD041 -->

En esta sección, agregará la capacidad de crear eventos en el calendario del usuario.

1. Cree un archivo nuevo en el directorio **./páginas** denominado **NewEvent. Razor** y agregue el siguiente código.

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventFormSnippet":::

    De este modo, se agrega un formulario a la página para que el usuario pueda escribir valores para el nuevo evento.

1. Agregue el siguiente código al final del archivo.

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventCodeSnippet":::

    Considere lo que hace este código.

    - En `OnInitializedAsync` ella obtiene la zona horaria del usuario autenticado.
    - En `CreateEvent` él se inicializa un nuevo objeto **Event** con los valores del formulario.
    - Usa el SDK de Graph para agregar el evento al calendario del usuario.

1. Guarde todos los cambios y reinicie la aplicación. En la página **calendario** , seleccione **nuevo evento**. Rellene el formulario y elija **crear**.

    ![Captura de pantalla del nuevo formulario de eventos](images/create-event.png)
