---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584636"
---
<a name="open-iconic-v111"></a>[<span data-ttu-id="9ec70-101">Abrir Icónication v 1.1.1</span><span class="sxs-lookup"><span data-stu-id="9ec70-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconic-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collection"></a><span data-ttu-id="9ec70-102">Abrir icónica es el elemento del mismo nivel de código abierto de [icónica](http://useiconic.com).</span><span class="sxs-lookup"><span data-stu-id="9ec70-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="9ec70-103">Es una colección de hipertexto de 223 iconos con una pequeña superficie &mdash; lista para usarse con bootstrap y base.</span><span class="sxs-lookup"><span data-stu-id="9ec70-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="9ec70-104">Ver la colección</span><span class="sxs-lookup"><span data-stu-id="9ec70-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="9ec70-105">¿Qué hay en icónica abierto?</span><span class="sxs-lookup"><span data-stu-id="9ec70-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="9ec70-106">223 iconos diseñados para ser legibles hasta 8 píxeles</span><span class="sxs-lookup"><span data-stu-id="9ec70-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="9ec70-107">Archivos SVG súper ligeros: 61,8 para todo el conjunto</span><span class="sxs-lookup"><span data-stu-id="9ec70-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="9ec70-108">Sprite SVG &mdash; el reemplazo moderno para fuentes de icono</span><span class="sxs-lookup"><span data-stu-id="9ec70-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="9ec70-109">Formatos webfont (EOT, OTF, SVG, TTF, WOFF), PNG y WebP</span><span class="sxs-lookup"><span data-stu-id="9ec70-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="9ec70-110">Hojas de estilo de tipo webfont (incluidas versiones para bootstrap y base) en CSS, formatos menos, SCSS y Stylus</span><span class="sxs-lookup"><span data-stu-id="9ec70-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="9ec70-111">Imágenes de trama de PNG y WebP en 8px, 16px, 24, 32, 48px y 64px.</span><span class="sxs-lookup"><span data-stu-id="9ec70-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="9ec70-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="9ec70-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-icons-and-reference-sections"></a><span data-ttu-id="9ec70-113">Para obtener muestras de código y todo lo que necesita para empezar a abrir icónica, consulte nuestras secciones de [iconos](http://useiconic.com/open#icons) y [referencia](http://useiconic.com/open#reference) .</span><span class="sxs-lookup"><span data-stu-id="9ec70-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="9ec70-114">Uso general</span><span class="sxs-lookup"><span data-stu-id="9ec70-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="9ec70-115">Usar el SVG de iconos abiertos</span><span class="sxs-lookup"><span data-stu-id="9ec70-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="9ec70-116">Nos gusta SVG y pensamos que es la forma de Mostrar iconos en la Web.</span><span class="sxs-lookup"><span data-stu-id="9ec70-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="9ec70-117">Dado que el icónica abierto es tan solo SVG Basic, le sugerimos que los muestre como lo haría con cualquier otra imagen (no olvide el `alt` atributo).</span><span class="sxs-lookup"><span data-stu-id="9ec70-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="9ec70-118">Usar el Sprite SVG de icónica abierto</span><span class="sxs-lookup"><span data-stu-id="9ec70-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="9ec70-119">Abrir icónica también se incluye en un Sprite SVG que permite mostrar todos los iconos del conjunto con una sola solicitud.</span><span class="sxs-lookup"><span data-stu-id="9ec70-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="9ec70-120">Es como una fuente de icono, sin ser un pirata informático.</span><span class="sxs-lookup"><span data-stu-id="9ec70-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="9ec70-121">Agregar un icono desde un Sprite SVG es un poco diferente de lo que se usa, pero sigue siendo un trozo de tarta.</span><span class="sxs-lookup"><span data-stu-id="9ec70-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="9ec70-122">*Sugerencia: para que los iconos tengan un estilo sencillo, le recomendamos que agregue una clase general a la* `<svg>` *y un nombre de clase único para cada icono diferente de la etiqueta* `<use>` *etiqueta.*</span><span class="sxs-lookup"><span data-stu-id="9ec70-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="9ec70-123">Los iconos de tamaño solo necesitan CSS básica.</span><span class="sxs-lookup"><span data-stu-id="9ec70-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="9ec70-124">Todos los iconos tienen un formato cuadrado, por lo que solo hay que establecer la `<svg>` etiqueta con las mismas dimensiones de ancho y alto.</span><span class="sxs-lookup"><span data-stu-id="9ec70-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="9ec70-125">Los iconos de color son incluso más fáciles.</span><span class="sxs-lookup"><span data-stu-id="9ec70-125">Coloring icons is even easier.</span></span> <span data-ttu-id="9ec70-126">Todo lo que necesita hacer es establecer la `fill` regla en la `<use>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="9ec70-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="9ec70-127">Para obtener más información acerca de los sprites SVG, lea [la guía de Chris Coyier](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span><span class="sxs-lookup"><span data-stu-id="9ec70-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="9ec70-128">Usando el tipo de icono de iconos abiertos...</span><span class="sxs-lookup"><span data-stu-id="9ec70-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="9ec70-129">... con bootstrap</span><span class="sxs-lookup"><span data-stu-id="9ec70-129">…with Bootstrap</span></span>

<span data-ttu-id="9ec70-130">Puede encontrar nuestras hojas de estilo bootstrap en `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="9ec70-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="9ec70-131">... con base</span><span class="sxs-lookup"><span data-stu-id="9ec70-131">…with Foundation</span></span>

<span data-ttu-id="9ec70-132">Puede encontrar nuestras hojas de estilo de Foundation en `font/css/open-iconic-foundation.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="9ec70-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="9ec70-133">... por su cuenta</span><span class="sxs-lookup"><span data-stu-id="9ec70-133">…on its own</span></span>

<span data-ttu-id="9ec70-134">Puede encontrar nuestras hojas de estilo predeterminadas en `font/css/open-iconic.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="9ec70-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="9ec70-135">Licencia</span><span class="sxs-lookup"><span data-stu-id="9ec70-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="9ec70-136">Iconos</span><span class="sxs-lookup"><span data-stu-id="9ec70-136">Icons</span></span>

<span data-ttu-id="9ec70-137">Todo el código (incluido el marcado SVG) se encuentra bajo la [licencia de MIT](http://opensource.org/licenses/MIT).</span><span class="sxs-lookup"><span data-stu-id="9ec70-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="9ec70-138">Fonts</span><span class="sxs-lookup"><span data-stu-id="9ec70-138">Fonts</span></span>

<span data-ttu-id="9ec70-139">Todas las fuentes se encuentran bajo la [licencia de SIL](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span><span class="sxs-lookup"><span data-stu-id="9ec70-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>
