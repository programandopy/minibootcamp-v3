---
title: Introducción a CSS
has_children: false
nav_order: 5
---

# Proyecto "Portfolio Web": Introducción a CSS
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

# Introducción

{: .concept }
Las hojas de estilos en cascada (CSS) son un mecanismo simple para agregarle estilo (colores, espaciado, tipos de letra, etc.) a un Documento Web (otra forma de referirnos a un archivo html).

CSS, o Cascading Style Sheets, resuelve un problema importante del desarrollo web: cómo hacer que tu sitio web se vea bien.
La apariencia de una pagina web es muy importante, ya que en gran medida esto es lo que la hace útil y fácil de usar. CSS no se trata solo de hacer que tu aplicación se vea bien; también nos deja hacer animaciones y transformaciones que pueden permitir interacciones sofisticadas para tus aplicaciones.

Una organización conocida como _El grupo de trabajo CSS_ ayuda a mantener las especificaciones CSS actuales; podés seguir su trabajo en el [sitio del World Wide Web Consortium](https://www.w3.org/Style/CSS/members){:target="\_blank"}.

En esta lección, agregaremos estilos a nuestra página web y aprenderemos más sobre varios conceptos de CSS: la cascada, la herencia y el uso de selectores, posicionamiento y uso de CSS para estilizar una página.

## Requisito previo:
{: .no_toc }

{: .important }
Deberías tener el archivo HTML del proyecto terminado y listo para darle estilo, fijate en el apartado "Introducción a HTML".

# La cascada

Las hojas de estilo en cascada incorporan la idea de que los estilos 'se mueven en cascada' de manera que la aplicación de un estilo está guiada por su prioridad.

- Los estilos establecidos por el autor de un sitio web tienen prioridad sobre los establecidos por un navegador.
- Los estilos configurados 'en línea' tienen prioridad sobre los configurados en una hoja de estilo externa.

### Actividad:
{: .no_toc }

Para entender mejor esto, empecemos por cambiar algún estilo en nuestra página web. En este caso, queremos que el título sea de color rojo, y no negro como está ahora.

Para hacer esto, ubiquemos el _encabezado_ con contenido **Mi nombre** en nuestro archivo HTML:

```html
<h1>Mi nombre</h1>
```

Las etiquetas `<h1>` se muestran de color negro en el navegador. Para cambiar el color, podemos agregar un **Atributo** a la etiqueta. Los atributos nos permiten modificar la apariencia o el comportamiento de los elementos, y siempre se agregan en **la etiqueta de apertura**. Para cambiar el estilo (en este caso, solo el color), usamos el atributo `style`.

Modificá la linea donde se encuentra la etiqueta `<h1>`, para que quede así:

```html
<h1 style="color: red">Mi nombre</h1>
```

{: .concept }
Todos los elementos HTML pueden tener atributos que proveen información adicional sobre los elementos.
Los atributos siempre van en la etiqueta de apertura y tienen un nombre y un valor, que se escriben así: **nombre="valor"**

✅ Guardá los cambios en el HTML y fijate que pasa en la página web. Acordate de actualizar la página para ver los cambios!

Si hiciste todo bien, deberías haber notado que el color del encabezado cambió, y ahora es rojo. Lo que hacemos con el atributo `style`, es decirle al navegador que aplique el estilo indicado entre comillas, que está escrito en CSS.

De esta manera podemos seguir estilizando la página web cambiando colores y otras propiedades. Sin embargo, esto implica agregar atributos a todos los elementos del HTML, y esto resulta muy poco práctico y difícil de comprender cuando nuestro documento se hace más grande.

Para resolver este problema, usamos "Hojas de estilo externas". Se tratan de archivos en los que podemos escribir todos los estilos que queremos aplicar.

---

### Actividad:
{: .no_toc }

En Visual Studio, crea un archivo nuevo llamado `style.css` en la carpeta `portfolio`

![crear-archivo](images/Animation.gif)

El archivo `style.css`, será el lugar donde vamos a especificar todos los estilos de nuestra página.

Pero, ahora que tenemos un archivo externo donde vamos a escribir los estilos, como sabe el navegador que debe mirar ahí?

Tenemos que decirle al navegador que siempre mire el archivo que creamos para saber que estilos aplicar, esto se hace en el HTML, en la cabecera del archivo (en la sección `<head>`).

Ubicá la cabecera del HTML y agregá ahí esta línea:

```html
<link rel="stylesheet" href="./style.css" />
```

✅ No confundas `<head>` con `<header>`!

La **etiqueta** `<link />` define la relación entre el archivo HTML y otros archivos. Con el **atributo** `rel`, le decimos que el archivo que queremos vincular es una hoja de estilos, y el **atributo** `href` le dice al navegador donde encontrar el archivo.

{: .important }
En el atributo `href`, el nombre del archivo debe coincidir con el nombre que le dimos cuando lo creamos. Si mas adelante no ves cambios en los estilos, asegurate de que los nombres coincidan.

La cabecera del archivo HTML debería quedar así:

```html
<head>
  <title>Mi portafolio personal</title>
  <link rel="stylesheet" href="./style.css" />
</head>
```

Ahora que ya tenemos nuestra hoja de estilos externa creada y vinculada con el html, escribir nuestro primer estilo.

Agregá el siguiente código a tu archivo `style.css`:

```css
h1 {
  color: blue;
}
h2 {
  color: green;
}
```

✅ ¿Qué colores cambiaron tu aplicación web? ¿Por qué? (explicación mas abajo).

Si hiciste todo bien, no debería haber cambiado nada en el titulo con tu nombre.

Al escribir `h1{  }`, estamos diciendo que todos los estilos que escribamos entre las llaves `{}` se deben aplicar a todos los elementos `h1` en el HTML. En este caso, tenemos un elemento `h1`, pero le pusimos un estilo en línea para que sea rojo, directo en el HTML.

{: .concept }
`h1{  }` es un **SELECTOR** de etiquetas, porque selecciona todas las etiquetas `h1` del HTML para aplicarles los estilos correspondientes. Se puede usar para seleccionar cualquier etiqueta, por ejemplo: `div{  }`, o `h2{  }`. Es por esto que TODOS los elementos `<h2>` cambiaron de color.

Ahora el navegador ve en nuestra hoja de estilos que estamos pidiendo que el color del `<h1>` sea azul, así que el navegador tiene dos instrucciones contradictorias:

```css
/* EN EL CSS, DECIMOS QUE EL COLOR ES AZUL */
h1 {
  color: blue;
}
```

```html
<!-- EN EL HTML, DECIMOS QUE EL COLOR ES ROJO -->
<h1 style="color: red">Mi nombre</h1>
```

Como decide el navegador cual de los dos colores aplicar?

Lo hace siguiendo las reglas de la **cascada**, que dicen que siempre los estilos en linea tienen prioridad. Por eso el navegador sigue mostrando el color rojo, ignorando lo que escribimos en la hoja de estilos.

Si borramos el estilo en línea que aplicamos, el navegador tomará lo que encuentre en la hoja de estilos.

✅ Probá dejando esta línea del HTML como estaba originalmente:

```html
<h1>Mi nombre</h1>
```

Si guardas todos los cambios y actualizas la página, deberías ver que el elemento h1 ahora es azul.

---

# Herencia

Ahora que tenemos la hoja de estilos preparada y ya entendemos como y donde escribir CSS, empecemos a ajustar los estilos de nuestra página.

### Actividad:
{: .no_toc }

En primer lugar, queremos cambiar la fuente del texto, esto es el tipo de letra de todo el texto en nuestra página. Para lograrlo, agregá el siguiente código el archivo CSS:

```css
body {
  font-family: Arial, sans-serif;
}
```

Guardá los cambios y actualizá la página web para ver que pasó.

Deberías haber notado un cambio en el tipo de letra.

Logramos cambiar el tipo de letra utilizando la **propiedad** `font-family`.

Pero, anteriormente habíamos dicho que para cambiar el estilo de un elemento HTML, usábamos un selector de etiquetas para seleccionar las etiquetas que queríamos cambiar. Para cambiar una etiqueta `h1`, utilizamos el selector `h1 {  }`.

Entonces, por qué ahora utilizamos un selector `body {  }` para cambiar un elemento `h1`?

En HTML, decimos que los elementos pueden tener padres e hijos (antepasados y descendientes). Todos los elementos dentro de una etiqueta `body` son hijos de esa etiqueta.

De esta manera, si miramos nuestro HTML y vemos una estructura así:

```html
<body>
  <header>
    <h1>Mi nombre</h1>
    <h2>Mi profesión</h2>
  </header>
</body>
```

decimos que el elemento `h1` es un hijo del elemento `header` y nieto de `body`.

Lo que hicimos con el selector `body {  }` es definir un tipo de letra para el elemento `body`, y todos los estilos que sean aplicados a este elemento serán **heredados** a sus descendientes, en este caso, al elemento `h1` y también al `h2` y a todo el texto de la página.

Hacemos esto de manera a que todo el texto que incluyamos en la página web tenga este tipo de letra, sin tener que aplicar estilos a todos los elementos de texto que queramos cambiar.

{: .concept }
En HTML, los elementos heredan los estilos de todos sus antepasados.

✅ Podés probar agregando otros elementos de texto para verificar cómo funciona la herencia, y te desafiamos a que hagas que otras propiedades sean heredadas (podes probar con la propiedad `color` que ya utilizamos).

---

# Selectores CSS

En CSS, los selectores son patrones o una sintaxis específica que nos permiten _seleccionar_ los elementos que queremos estilizar.

Nos permiten aplicar estilos a elementos específicos. Hasta ahora, solo utilizamos los selectores de etiquetas.

## Selectores de Etiquetas

Hasta ahora, en el archivo `style.css` solo aplicamos estilos a dos elementos HTML: `<body>` y `<h1>`.

Los selectores de etiqueta o elementos nos permiten aplicar estilos a los elementos, buscando por sus etiquetas en el archivo HTML. Por ejemplo, cuando usamos el selector `h1 {  }`, estamos seleccionando **TODOS** los elementos de tipo `h1` en el HTML.

### Actividad:
{: .no_toc }

Vamos a utilizar un selector de elementos para agregarle algunos estilos al `<body>` que queremos que se hereden en todos los elementos.

Necesitamos cambiar el color de fondo, el tipo de letra y el color del texto para toda la pagina.

Asegurate de que tu archivo CSS quede de la siguiente manera (puede que tengas que reemplazar cosas las pruebas que vinimos haciendo):

```css
body {
  font-family: Arial, sans-serif;
  margin: 0;
  color: #3e363f;
  padding-top: 70px;
}
```

También podemos empezar a estilizar el menu:

```css
nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #fff;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}
```

Con este código, logramos que la barra de navegación quede fija y la parte superior de la pantalla y de damos algunos estilos.

✅ Proba en tu navegador moviéndote un poco por la pagina (scroll hacia abajo). Podes probar que pasa sacando algunas de las propiedades, especialmente **position**.

- `position: fixed;`: Esta propiedad establece la posición del elemento como fija con respecto a la ventana del navegador. Esto significa que la barra de navegación permanecerá en la misma posición en la pantalla, incluso si se desplaza hacia abajo en la página.
- `top: 0;`: Esta propiedad determina la distancia desde el borde superior de la ventana del navegador donde se ubicará la barra de navegación fija. Al establecerlo en 0, la barra de navegación se colocará en la parte superior de la ventana del navegador.
- `left: 0;`: Esta propiedad determina la distancia desde el borde izquierdo de la ventana del navegador.
- `width: 100%;`: Esta propiedad establece el ancho de la barra de navegación al 100% del ancho de la ventana del navegador.
- `background-color: #fff;`: Esta propiedad establece el color de fondo de la barra de navegación. En este caso, se establece en blanco
- `box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);`: Esta propiedad crea una sombra alrededor de la barra de navegación para darle profundidad visual.

✅ En el selector de `body` tenemos `padding-top: 70px;`, esto es para darle lugar a la barra de navegación. Proba que pasa si sacas esa linea.

---

Pareciera que con este tipo de selector podemos estilizar toda la página, pero el problema es que no podemos seleccionar un solo elemento específico, solo podemos seleccionar **todos** los `h1` o **todos** los `a`, y para continuar necesitamos aplicar estilos solo a un par de elementos de tipo `<a>`, pero no a los demás.

## Clases

Ahora que la barra de navegación esta mas prolija, nos queda ajustar un poco los estilos de los enlaces del menu. Como podemos ver en el HTML, estos enlaces son elementos de tipo `<a>`, asi que podríamos usar un selector de etiquetas de la siguiente manera: `a { ... }`. Pero esto afectaría a todos los elementos del mismo tipo, y como tenemos muchos en el documento, necesitamos una forma de estilizar solo algunos elementos de ese tipo.

Para resolver esto vamos a usar otro atributo: `class`.

### Actividad:
{: .no_toc }

Modifica el HTML para que quede asi la barra de navegación quede asi:

```html
<nav>
  <ul>
    <a class="menu-item" href="#acerca-de-mi">Acerca de mí</a>
    <a class="menu-item" href="#habilidades">Habilidades</a>
    <a class="menu-item" href="#experiencia">Experiencia</a>
    <a class="menu-item" href="#proyectos">Proyectos</a>
    <a class="menu-item" href="#contacto">Contacto</a>
  </ul>
</nav>
```

Para cambiar el estilo de los elementos `a` que tienen el atributo `class="menu-item"`, tenemos que utilizar un selector de clase.

{: .concept }
En HTML, una "clase" es un atributo que se puede agregar a elementos HTML para identificarlos y agruparlos en categorías específicas. Las clases se utilizan principalmente con fines de estilo y manipulación a través de CSS y JavaScript.

Utilizamos el selector de clase escribiendo `.` seguido del nombre que le dimos a la clase, en este caso "menu-item", el selector queda asi: `.menu-item {  }`. Todos los estilos en ese selector, serán aplicados a todos los elementos que tengan esa clase.

Agregamos esto al CSS:

```css
.menu-item {
  text-decoration: none;
  color: #333;
  padding: 10px;
  display: inline-block;
}
```

✅ Agrega estas propiedades una a una, para ir entendiendo como funcionan.

-`text-decoration: none;`: Esta propiedad elimina el subrayado predeterminado que suele aparecer en los enlaces (<a>). -`color: #333;`: Esta propiedad establece el color del texto de los elementos del menú. -`padding: 10px;`: Esta propiedad agrega un relleno de 10 píxeles alrededor de cada elemento del menú, solo con el fin de que las cosas se vean mas espaciadas. -`display: inline-block;`: Esta propiedad establece el tipo de visualización de los elementos del menú como "inline-block". Esto significa que los elementos del menú se colocarán uno al lado del otro en la misma línea horizontal, pero aún conservarán las propiedades de un bloque (como el ancho y el alto), lo que les permite tener un relleno y un espacio alrededor. Esto facilita la alineación horizontal de los elementos del menú y permite que se apliquen propiedades de bloque, como el padding, el margen y el ancho.

Para que se vea un poco mas interesante, vamos a agregar algunos estilos para que cada enlace cambie cuando se pasa el mouse por encima. Para esto escribimos el siguiente selector:

```css
.menu-item:hover {
  background-color: #ddd;
  transition: all 0.4s ease-in-out;
}
```

- `.menu-item:hover { ... }`: Esta parte del selector CSS (:hover) indica que estas reglas se aplicarán cuando el cursor del mouse esté sobre un elemento del menú
- `background-color: #ddd;`: Esta propiedad establece el color de fondo del elemento del menú cuando se pasa el cursor sobre él.
- `transition: all 0.4s ease-in-out;`: Esta propiedad implica que los estilos anteriores, que se van a aplicar cuando se pase el mouse por el elemento, se aplican con un efecto que dura 0.4 segundos. Jugá con ese valor para entender qué está pasando.

---

Con esto, ya tenemos terminada la barra de navegación. Nos falta estilizar un poco el encabezado, el pie de pagina y las secciones.

En este punto no hay nada nuevo, vamos a utilizar selectores de etiqueta para cambiar colores y bordes de estos elementos.

### Actividad:
{: .no_toc }

Primero vamos a ajustar los estilos del encabezado. Básicamente queremos cambiar el color de fondo y centrar el texto.

Como hay un solo elemento `<head>` podemos usar un selector de etiqueta con las siguientes propiedades:

```css
header {
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 20px;
  margin-bottom: 20px;
}
```

No tenemos propiedades nuevas en ese selector, pero podes ajustar los valores según tu preferencia.

Luego, queremos aplicar algunos estilos a todas las secciones. Como buscamos que se aplique lo mismo a todas, seguimos con el selector de etiquetas:

```css
section {
  padding: 20px;
  border: 1px solid #ddd;
  margin-bottom: 20px;
}
```

Con esto nuestro porfolio va tomando forma! solo nos faltan algunas cosas adicionales.

## Selectores de ID

Cuando en el HTML tenemos muchos elementos del mismo tipo (por ejemplo, muchos `section`) pero solo queremos modificar uno de ellos, podemos utilizar un selector de **ID**.

{: .concept }
En HTML, un ID es un nombre único que usamos para identificar un elemento. Este nombre no se puede repetir.

Si queremos aplicar un estilo a uno solo de los `section` que tenemos en nuestro HTML, necesitamos una forma de individualizarlo, darle un nombre único. Este nombre único es el **ID**.

Para darle un ID, utilizamos el [atributo](#1-la-cascada) `id`.

{: .concept }
Recordemos que anteriormente usamos los atributos `style` para asignar estilos y `class` para el otro tipo de selector. El atributo `id` hace otra cosa, pero tiene la misma sintaxis.

Para asignar un identificador a un elemento escribimos el atributo en la etiqueta de apertura, por ejemplo, en un `div`:

```html
<div id="nombre1"></div>
<div id="nombre2"></div>
<div id="nombre1"></div>
<!-- NO PERMITIDO, el id 'nombre1' ya existe -->
```

{: .concept }
En el ejemplo vemos como se utiliza el id para nombrar elementos, pero es importante recordar que **el id no puede repetirse**.

### Actividad:
{: .no_toc }

Nos interesa justificar el texto en la sección "Acerca de mi", para eso podemos usar la propiedad `text-align: justify;`, pero no la podemos poner en el selector de etiqueta que usamos anteriormente (`section { ... }`), porque solo queremos aplicar este estilo a una sección.

En el apartado de HTML ya les dimos un `id` a todas las secciones para que funcione la navegación, el id que nos interesa ahora es `id="acerca-de-mi"`.

Podemos utilizar este id para seleccionar ese elemento y darle estilos. Agregá el siguiente código en el CSS:

```css
#acerca-de-mi {
  text-align: justify;
}
```

Utilizamos el selector de id escribiendo `#` seguido del nombre que le dimos al elemento, en este caso: `#acerca-de-mi {  }`. Todos los estilos en ese selector, serán aplicados solo al `section` con ese ID.

Como vimos anteriormente, esta propiedad se asigna al elemento de tipo `section`, y se hereda a todos sus descendientes, que son un `h2` y un `p`.

---

## Combinando selectores

Ahora nos toca ajustar la sección de habilidades.

Para hacer eso tenemos que aplicar algunas propiedades a la lista (`<ul>`), y otras propiedades a los items de la lista (`<li>`).

No podemos usar selectores de etiquetas, porque no queremos afectar a los demás elementos de tipo `<ul>` o `<li>` que existan en el documento, solo queremos tocar los elementos de ese tipo que están dentro de la sección con `id="habilidades"`.

Para hacer esto podemos combinar el selector de ID con el selector de etiquetas.

### Actividad:
{: .no_toc }

Para combinar selectores simplemente tenemos que poner todos los selectores que queremos aplicar separados por espacios, asi:

```css
#habilidades ul {
  list-style: none;
  padding: 0;
}

#habilidades ul li {
  display: inline-block;
  padding: 5px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin-right: 10px;
}
```

Lo que estamos haciendo con el primer selector, es seleccionar todos los elementos `<ul>` que estén dentro del elemento con ID `habilidades`.

En el segundo bloque seleccionamos todos los elementos `<li>` que estén dentro de un elemento `<ul>`, que a su vez este dentro del elemento con ID `habilidades`.

Utilizamos los mismos mecanismos para modificar la forma en la que se ve la sección de "experiencia":

```css
#experiencia ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

#experiencia ul li {
  margin-bottom: 10px;
}
```

Y también nos queda hacer lo mismo para la sección de proyectos:

```css
#proyectos ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

#proyectos ul li a {
  text-decoration: none;
  color: #333;
}

#proyectos ul li a:hover {
  text-decoration: underline;
}
```

# Iconos

Solo nos falta darle algo de estilo a la sección de contactos. Para eso, podemos agregar los iconos de las redes sociales.

Ahora que entendemos como funciona una hoja de estilos externa (CSS), y como se vincula al HTML puede resultar mas fácil comprender que para usar una librería de iconos que existe en internet sin tener que descargar todas las imágenes, podemos utilizar una hoja de estilos que se encuentra en la internet.

Para usar el archivo CSS con el que venimos trabajando, agregamos la siguiente linea en la cabecera del HTML:

```html
<link rel="stylesheet" href="./style.css" />
```

El atributo `href` indica en que carpeta esta y como se llama el archivo CSS.

Para usar la librería de iconos de [Font Awesome](https://fontawesome.com/icons/categories/social), tenemos que agregar **OTRO** elemento `link` en la cabecera, de esta manera:

```html
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
/>
```

Esta vez el atributo `href` apunta al lugar de la internet donde se encuentra la hoja de estilos que queremos usar.

En esta hoja de estilos estan definidas muchas clases que se encargan de incluir un icono en el elemento en el que la utilizamos.

- Facebook: `class="fa fa-facebook"`
- Twitter: `class="fa fa-twitter"`
- LinkedIn: `class="fa fa-linkedin"`

Es importante notar que en todos los casos se estan asignando dos clases: `fa` y `fa-facebook` o la que corresponda. `fa-facebook` defini el icono que se va a mostrar, pero podemos usar la clase `fa` para cambiar la forma en la que se muestran todos estos iconos.

### Actividad:
{: .no_toc }

Ubicá en el HTML la lista donde se encuentran las redes sociales y agrega algunos ID y clases:

```html
<ul id="sociales">
  <li>
    <a href="https://www.facebook.com/tucuenta" class="fa fa-facebook"></a>
  </li>
  <li>
    <a href="https://twitter.com/tucuenta" class="fa fa-twitter"></a>
  </li>
  <li>
    <a href="https://www.linkedin.com/in/tucuenta" class="fa fa-linkedin"></a>
  </li>
  <!-- Agrega más redes sociales si lo deseas -->
</ul>
```

En este punto deberías poder ver los iconos si hiciste todo bien.

Si no ves los iconos retrocede un poco y fijate paso por paso en todas las cosas que agregaste.

Por ultimo, vamos agregar algunos estilos en el CSS:

```css
#sociales {
  list-style: none;
  padding: 0;
  margin-top: 10px;
}

#sociales li {
  list-style: none;
  display: inline-block;
  padding: 5px;
}

.fa {
  color: #333;
  text-decoration: none;
  margin-left: 0px;
}

footer {
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 10px;
}
```

---

Terminamos! La página web debería haberte quedado mas o menos como planteamos en la sección de requerimientos.

Ahora depende de vos seguir dándole una identidad.
