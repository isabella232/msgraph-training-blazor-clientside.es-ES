---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584636"
---
<a name="open-iconic-v111"></a>[Abrir Icónication v 1.1.1](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconic-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collection"></a>Abrir icónica es el elemento del mismo nivel de código abierto de [icónica](http://useiconic.com). Es una colección de hipertexto de 223 iconos con una pequeña superficie &mdash; lista para usarse con bootstrap y base. [Ver la colección](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>¿Qué hay en icónica abierto?

* 223 iconos diseñados para ser legibles hasta 8 píxeles
* Archivos SVG súper ligeros: 61,8 para todo el conjunto 
* Sprite SVG &mdash; el reemplazo moderno para fuentes de icono
* Formatos webfont (EOT, OTF, SVG, TTF, WOFF), PNG y WebP
* Hojas de estilo de tipo webfont (incluidas versiones para bootstrap y base) en CSS, formatos menos, SCSS y Stylus
* Imágenes de trama de PNG y WebP en 8px, 16px, 24, 32, 48px y 64px.


## <a name="getting-started"></a>Introducción

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-icons-and-reference-sections"></a>Para obtener muestras de código y todo lo que necesita para empezar a abrir icónica, consulte nuestras secciones de [iconos](http://useiconic.com/open#icons) y [referencia](http://useiconic.com/open#reference) .

### <a name="general-usage"></a>Uso general

#### <a name="using-open-iconics-svgs"></a>Usar el SVG de iconos abiertos

Nos gusta SVG y pensamos que es la forma de Mostrar iconos en la Web. Dado que el icónica abierto es tan solo SVG Basic, le sugerimos que los muestre como lo haría con cualquier otra imagen (no olvide el `alt` atributo).

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>Usar el Sprite SVG de icónica abierto

Abrir icónica también se incluye en un Sprite SVG que permite mostrar todos los iconos del conjunto con una sola solicitud. Es como una fuente de icono, sin ser un pirata informático.

Agregar un icono desde un Sprite SVG es un poco diferente de lo que se usa, pero sigue siendo un trozo de tarta. *Sugerencia: para que los iconos tengan un estilo sencillo, le recomendamos que agregue una clase general a la* `<svg>` *y un nombre de clase único para cada icono diferente de la etiqueta* `<use>` *etiqueta.*  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

Los iconos de tamaño solo necesitan CSS básica. Todos los iconos tienen un formato cuadrado, por lo que solo hay que establecer la `<svg>` etiqueta con las mismas dimensiones de ancho y alto.

```
.icon {
  width: 16px;
  height: 16px;
}
```

Los iconos de color son incluso más fáciles. Todo lo que necesita hacer es establecer la `fill` regla en la `<use>` etiqueta.

```
.icon-account-login {
  fill: #f00;
}
```

Para obtener más información acerca de los sprites SVG, lea [la guía de Chris Coyier](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).

#### <a name="using-open-iconics-icon-font"></a>Usando el tipo de icono de iconos abiertos...


##### <a name="with-bootstrap"></a>... con bootstrap

Puede encontrar nuestras hojas de estilo bootstrap en `font/css/open-iconic-bootstrap.{css, less, scss, styl}`


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>... con base

Puede encontrar nuestras hojas de estilo de Foundation en `font/css/open-iconic-foundation.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>... por su cuenta

Puede encontrar nuestras hojas de estilo predeterminadas en `font/css/open-iconic.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>Licencia

### <a name="icons"></a>Iconos

Todo el código (incluido el marcado SVG) se encuentra bajo la [licencia de MIT](http://opensource.org/licenses/MIT).

### <a name="fonts"></a>Fonts

Todas las fuentes se encuentran bajo la [licencia de SIL](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).
