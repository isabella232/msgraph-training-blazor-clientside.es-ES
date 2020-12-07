---
ms.openlocfilehash: 9029486df6b08042681c0a1a67b156cbbd0381a0
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584670"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="5638f-101">Cómo ejecutar el proyecto completado</span><span class="sxs-lookup"><span data-stu-id="5638f-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5638f-102">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5638f-102">Prerequisites</span></span>

<span data-ttu-id="5638f-103">Para ejecutar el proyecto completado en esta carpeta, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5638f-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="5638f-104">[.Net Core SDK](https://dotnet.microsoft.com/download) instalado en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="5638f-104">The [.NET Core SDK](https://dotnet.microsoft.com/download) installed on your development machine.</span></span> <span data-ttu-id="5638f-105">(**Nota:** este tutorial se ha escrito con .net Core SDK versión 3.1.402.</span><span class="sxs-lookup"><span data-stu-id="5638f-105">(**Note:** This tutorial was written with .NET Core SDK version 3.1.402.</span></span> <span data-ttu-id="5638f-106">Los pasos de esta guía pueden funcionar con otras versiones, pero no se han probado.</span><span class="sxs-lookup"><span data-stu-id="5638f-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="5638f-107">Una cuenta de Microsoft personal con un buzón de correo en Outlook.com o una cuenta profesional o educativa de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5638f-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="5638f-108">Si no tiene una cuenta de Microsoft, hay un par de opciones para obtener una cuenta gratuita:</span><span class="sxs-lookup"><span data-stu-id="5638f-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="5638f-109">Puede [registrarse para obtener una nueva cuenta Microsoft personal](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="5638f-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="5638f-110">Puede [registrarse para el programa de desarrolladores de office 365](https://developer.microsoft.com/office/dev-program) para obtener una suscripción gratuita a Office 365.</span><span class="sxs-lookup"><span data-stu-id="5638f-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="5638f-111">Registro de una aplicación web con el centro de administración de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5638f-111">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="5638f-112">Abra un explorador y vaya al [centro de administración de Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5638f-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="5638f-113">Inicie sesión con una **cuenta personal** (también conocida como: cuenta Microsoft) o una **cuenta profesional o educativa**.</span><span class="sxs-lookup"><span data-stu-id="5638f-113">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="5638f-114">Seleccione **Azure Active Directory** en el panel de navegación izquierdo y, a continuación, seleccione **Registros de aplicaciones** en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="5638f-114">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="5638f-115">Una captura de pantalla de los registros de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5638f-115">A screenshot of the App registrations</span></span> ](../tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="5638f-116">Seleccione **Nuevo registro**.</span><span class="sxs-lookup"><span data-stu-id="5638f-116">Select **New registration**.</span></span> <span data-ttu-id="5638f-117">En la página **Registrar una aplicación**, establezca los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="5638f-117">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="5638f-118">Establezca **Nombre** como `Blazor Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="5638f-118">Set **Name** to `Blazor Graph Tutorial`.</span></span>
    - <span data-ttu-id="5638f-119">Establezca **Tipos de cuenta admitidos** en **Cuentas en cualquier directorio de organización y cuentas personales de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="5638f-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="5638f-120">En **URI de redirección**, establezca la primera lista desplegable en `Web` y establezca el valor `https://localhost:5001/authentication/login-callback`.</span><span class="sxs-lookup"><span data-stu-id="5638f-120">Under **Redirect URI**, set the first drop-down to `Web` and set the value to `https://localhost:5001/authentication/login-callback`.</span></span>

    ![Captura de pantalla de la página registrar una aplicación](../tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="5638f-122">Seleccione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="5638f-122">Select **Register**.</span></span> <span data-ttu-id="5638f-123">En la página del **tutorial de gráfico increíblemente brillante** , copie el valor del identificador de la **aplicación (cliente)** y guárdelo, lo necesitará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="5638f-123">On the **Blazor Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Captura de pantalla del identificador de la aplicación del nuevo registro de la aplicación](../tutorial/images/aad-application-id.png)

1. <span data-ttu-id="5638f-125">Seleccione **Autenticación** en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="5638f-125">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="5638f-126">Busque la sección **concesión implícita** y habilite **tokens de acceso** y **tokens de identificador**.</span><span class="sxs-lookup"><span data-stu-id="5638f-126">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="5638f-127">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5638f-127">Select **Save**.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="5638f-128">Configuración del ejemplo</span><span class="sxs-lookup"><span data-stu-id="5638f-128">Configure the sample</span></span>

1. <span data-ttu-id="5638f-129">Cambie el nombre del **appsettings.example.js/GraphTutorial/wwwroot/en** el archivo en el que se **appsettings.js**.</span><span class="sxs-lookup"><span data-stu-id="5638f-129">Rename the **/GraphTutorial/wwwroot/appsettings.example.json** file to **appsettings.json**.</span></span>

1. <span data-ttu-id="5638f-130">Modifique **appsettings.js** y reemplace `YOUR_APP_ID_HERE` por el identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5638f-130">Edit **appsettings.json** and replace `YOUR_APP_ID_HERE` with your application ID.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="5638f-131">Ejecutar el ejemplo</span><span class="sxs-lookup"><span data-stu-id="5638f-131">Run the sample</span></span>

<span data-ttu-id="5638f-132">En la CLI, ejecute el siguiente comando para iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5638f-132">In your CLI, run the following command to start the application.</span></span>

```Shell
dotnet run
```
