---
ms.openlocfilehash: 723f1d08b9d1085d47d0d5fac71da5371badc3d0
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584637"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="d2ef1-101">En esta sección, agregará la capacidad de crear eventos en el calendario del usuario.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-101">In this section you will add the ability to create events on the user's calendar.</span></span>

1. <span data-ttu-id="d2ef1-102">Cree un archivo nuevo en el directorio **./páginas** denominado **NewEvent. Razor** y agregue el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-102">Create a new file in the **./Pages** directory named **NewEvent.razor** and add the following code.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventFormSnippet":::

    <span data-ttu-id="d2ef1-103">De este modo, se agrega un formulario a la página para que el usuario pueda escribir valores para el nuevo evento.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-103">This adds a form to the page so the user can enter values for the new event.</span></span>

1. <span data-ttu-id="d2ef1-104">Agregue el siguiente código al final del archivo.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-104">Add the following code to the end of the file.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventCodeSnippet":::

    <span data-ttu-id="d2ef1-105">Considere lo que hace este código.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-105">Consider what this code does.</span></span>

    - <span data-ttu-id="d2ef1-106">En `OnInitializedAsync` ella obtiene la zona horaria del usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-106">In `OnInitializedAsync` it gets the authenticated user's time zone.</span></span>
    - <span data-ttu-id="d2ef1-107">En `CreateEvent` él se inicializa un nuevo objeto **Event** con los valores del formulario.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-107">In `CreateEvent` it initializes a new **Event** object using the values from the form.</span></span>
    - <span data-ttu-id="d2ef1-108">Usa el SDK de Graph para agregar el evento al calendario del usuario.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-108">It uses the Graph SDK to add the event to the user's calendar.</span></span>

1. <span data-ttu-id="d2ef1-109">Guarde todos los cambios y reinicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-109">Save all of your changes and restart the app.</span></span> <span data-ttu-id="d2ef1-110">En la página **calendario** , seleccione **nuevo evento**.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-110">On the **Calendar** page, select **New event**.</span></span> <span data-ttu-id="d2ef1-111">Rellene el formulario y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="d2ef1-111">Fill in the form and choose **Create**.</span></span>

    ![Captura de pantalla del nuevo formulario de eventos](images/create-event.png)
