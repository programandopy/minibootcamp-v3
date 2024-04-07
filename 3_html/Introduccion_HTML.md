---
title: Introducción a HTML
has_children: false
nav_order: 4
has_toc: true
---

# Proyecto "Portfolio Web" - Parte 1: Introducción a HTML
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

# Introducción:

HTML, o HyperText Markup Language, es el "esqueleto" de la web. Si CSS 'viste' tu HTML y JavaScript le da vida, el cuerpo de tu aplicación web es tu HTML. La sintaxis de HTML incluso refleja esa idea, ya que incluye etiquetas "head" (cabeza), "body" (cuerpo) y "footer" (pie).

En esta lección y las siguientes vamos a construir un portfolio web acorde a los requerimientos explicados en la [sección anterior](/3_html/Portfolio).

Usaremos HTML para diseñar el 'esqueleto' y todo el contenido del portfolio.

### Actividad - Creación del proyecto

{: .no_toc }

En tu computadora, crea una carpeta llamada 'portfolio'.

Una vez creada, abri el Visual Studio Code, y abri la carpeta que creaste. Dentro de ella, crea un archivo llamado 'index.html'. Podés hacer esto en Visual Studio Code después de crear tu carpeta del proyecto abriendo una nueva ventana de VS Code, haciendo clic en 'abrir carpeta' y navegando a tu nueva carpeta. Hacé clic en el botón pequeño 'archivo' en el panel del Explorador y creá el nuevo archivo

<!-- Insertar Gif para abrir la carpeta -->
<!-- Insertar Gif para crear archivo -->

> El archivo index.html indica a un navegador que es el archivo predeterminado en una carpeta; las URL como `https://anysite.com/test` se pueden construir usando una estructura de carpetas que incluya una carpeta llamada `test` con `index.html` dentro; `Index.html` no tiene que aparecer en una URL.

---

# Las etiquetas DocType y html

La primera línea de un archivo HTML es su doctype. Es un poco sorprendente que necesite tener esta línea en la parte superior del archivo, pero le dice a los navegadores más antiguos que el navegador necesita representar la página en un modo estándar, siguiendo la especificación html actual.

> Consejo: en VS Code, puedes colocar el cursor sobre una etiqueta y obtener información sobre su uso en las guías de referencia de MDN.

La segunda línea debe ser la etiqueta de apertura de la etiqueta `<html>`, seguida ahora por su etiqueta de cierre. Estas etiquetas son los elementos raíz de su interfaz.

### Actividad - `<!DOCTYPE html>`

{: .no_toc }

Agregá estas líneas en la parte superior de tu archivo `index.html`:

```HTML
<!DOCTYPE html>
<html></html>
```

{: .important }
Es importante que cuando hagamos una pagina web, tengamos en cuenta que no sabemos que navegador utiliza el usuario, utilizamos la etiqueta `<!DOCTYPE html>` para que incluso los usuarios con los navegadores mas viejos puedan ver nuestra web, y de la misma manera tendremos que tener en cuenta otras consideraciones de compatibilidad en adelante.

---

# El 'encabezado' del documento

El área 'encabezado' del documento HTML incluye información crucial sobre tu página web, también conocida como [metadatos](https://developer.mozilla.org/es/docs/Web/HTML/Element/meta){:target="\_blank"}. En nuestro caso, solo le vamos a poner un titulo a nuestra pagina web

### Actividad - `<title>`

{: .no_toc }

Agregá un bloque de 'encabezado' a tu documento entre las etiquetas de apertura y cierre `<html>`.

```html
<head>
  <title>Mi portafolio personal</title>
</head>
```

{: .concept }
El encabezado debe incluir la información que necesita el navegador para saber como interpretar el código HTML.

Guarda estos cambios y abri la pagina web en el navegador.

✅ ¿Donde se puede ver el el titulo que pusimos?

---

# El `cuerpo` del documento

En HTML, agregamos etiquetas al archivo .html para crear elementos de una página web. Cada etiqueta generalmente tiene una etiqueta de apertura y cierre, como esta: `<p>hola</p>` para indicar un párrafo.

Todo este contenido va a en el `cuerpo` del documento HTML, para lo que se usa la etiqueta `<body>`.

### Actividad - El primer titulo (`<h1>`)

<!-- {: .no_toc } -->

Lo primero que vamos a hacer es construir el formulario que vamos a usar para la calculadora.

Agrega a tu HTML el cuerpo del documento y empecemos cargando el primer elemento de nuestra web, nuestro nombre!.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mi portafolio personal</title>
  </head>
  <body>
    <h1>Mi nombre</h1>
  </body>
</html>
```

{: .concept }
Las etiquetas que encapsulan algún contenido le dicen al navegador de que tipo de contenido se trata. La etiqueta `h1` dice que su contenido es un titulo, y de la misma manera hay etiquetas para todo tipo de contenido, texto normal, botones, etc.

La mayoría de las etiquetas encapsulan contenido mediante etiquetas de apertura y etiquetas de cierre, de esta manera: `<apertura> contenido encapsulado </cierre>`

Agreguemos algo mas de información, ahora que tenemos el nombre nos falta indicar a que nos dedicamos, agrega otro encabezado mas pequeño debajo de tu nombre, que diga "Web Developer". Tenes que usar una etiqueta `h2` asi: `<h2>Web Developer</h2>`

✅ ¿Cual es la diferencia entre `<h1>` y `<h2>`?

## División del documento en secciones

Como podemos ver con lo que hicimos hasta ahora, HTML nos permite etiquetar el contenido de nuestra página web para que el navegador y otros programas sepan cómo interpretarlo.

Así como tenemos etiquetas que indican que un texto particular es un encabezado (`<h1>`), también necesitamos organizar nuestra página en diferentes secciones, o grupos de elementos.

Para hacer esto podemos utilizar una variedad de elementos, como `<div>`, `<header>`, `<main>`, `<section>` y otros.

{: .concept }
La etiqueta `<header>` en HTML se utiliza para definir la sección de encabezado de una página web. Esta sección suele contener información introductoria o de navegación importante para el sitio web.

En nuestro caso, nos interesa tener nuestro nombre y profesión como encabezado.

### Actividad - Encabezado.

Encapsula los dos encabezados que agregaste anteriormente con las etiquetas de apertura y cierre `<header>`.

El código HTML debería quedar asi:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mi portafolio personal</title>
  </head>
  <body>
    <header>
      <h1>Mi nombre</h1>
      <h2>Mi profesión</h2>
    </header>
  </body>
</html>
```

{: .concept }
Es importante entender cómo los encabezados `<h1>` y `<h2>` está “dentro” de un elemento `<header>`, ya que está entre sus etiquetas de apertura y cierre, así como el `<header>` esta “dentro” del elemento `<body>`

---

{: .concept }
La etiqueta `<main>` se utiliza para definir el contenido principal de una página web. Debe contener el contenido central y relevante de la página, excluyendo elementos como encabezados, pie de página, barras laterales, etc.

### Actividad - `<main>` y `<footer>`

Ahora vamos a agregar un elemento `<main>` debajo del encabezado, acá vamos a ir colocando todo el contenido principal del portfolio.

Además vamos a necesitar un `<footer>` o pie de página. Por lo general, el pie de página contiene información de contacto, enlaces a secciones importantes del sitio, derechos de autor, enlaces de navegación secundarios y otros elementos similares.

```html
<body>
  <header>
    <h1>Mi nombre</h1>
    <h2>Mi profesión</h2>
  </header>
  <main></main>
  <footer>
    <p>Copyright &copy; 2024</p>
  </footer>
</body>
```

Por ahora, solo vamos a agregar información de copyright en el pie de pagina.

✅ ¿Qué hace el código &copy;que pusimos en el footer? Abri la página que estás construyendo en el navegador y busca el resultado.

{: .concept }
La etiqueta <p> en HTML se utiliza para definir un párrafo de texto. Esta etiqueta se utiliza para delimitar un bloque de texto que forma un párrafo coherente en una página web.

{: .note }
No es obligatorio que nuestra página web tenga header, main y footer. Puede tener los tres, podemos tener solo header, o podemos obviar el footer. Son herramientas que nos ayudan a organizar el contenido como nosotros queramos.

---

Ahora que tenemos la estructura de la página, podemos ir agregando las secciones que el portfolio debe tener:

- Acerca de mi.
- Habilidades.
- Experiencia.
- Lista de proyectos.
- Información de contacto.

### Actividad - Acerca de mí

Trata de seguir los siguientes pasos sin mirar el código completo:

1. Vamos a agregar una sección “dentro” del elemento <main>, utilizando la etiqueta <sección>.
2. Dentro de esta nueva sección vamos a agregar un encabezado <h2> que diga “Acerca de mi”.
3. Finalmente agregamos un párrafo breve describiendo algo sobre nosotros.

El código del elemento <main> te debería haber quedado así:

```html
<main>
  <section>
    <h2>Acerca de mí</h2>
    <p>
      Como desarrollador web junior, fusiono mi pasión por el diseño y la
      programación para crear experiencias web excepcionales. Me esfuerzo por
      cada línea de código y cada detalle de diseño para asegurarme de que mis
      sitios web sean visualmente atractivos, funcionales y accesibles para
      todos. Estoy comprometido a seguir aprendiendo y mejorando continuamente
      mientras busco oportunidades desafiantes que amplíen mi experiencia en el
      desarrollo web.
    </p>
  </section>
</main>
```

{: .important }
Proba el código que escribiste mirando como está quedando la página en el navegador. Siempre que agregamos algo nuevo tenemos que probarlo antes de seguir, por si hay algo que arreglar.

---

### Actividad - Habilidades

Con esto tenemos la primera sección del portfolio. Ahora seguimos con la segunda sección, agregando otro elemento `<section>` y vamos a utilizar la etiqueta `<ul>` (de un-ordered list) y `<li>` (de list item) para hacer una lista con viñetas para listar las habilidades (que vamos a obtener cuando terminemos el curso!).

1. Primero agregamos una nueva sección (`<section>`) debajo de la sección anterior, esto es, debajo de la etiqueta de cierre (`</section>`).
2. Dentro de esta nueva sección vamos a agregar el siguiente código:

```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
  <li>Git</li>
  <li>Metodologías ágiles</li>
</ul>
```

El contenido encapsulado en las etiquetas `<li>` es un ítem con una viñeta, y todos los ítems deben estar encapsulados en un elemento `<ul>`, para que el navegador sepa dónde empieza y dónde termina una lista, esto es importante especialmente cuando la lista es ordenada, por ejemplo con números.

✅ Proba que pasa si usas `<ol>` en lugar de `<ul>` para hacer la lista.

En este punto la sección <main> debería estar quedando asi:

```html
<main>
  <section>
    <h2>Acerca de mí</h2>
    <p>
      Como desarrollador web junior, fusiono mi pasión por el diseño y la
      programación para crear experiencias web excepcionales. Me esfuerzo por
      cada línea de código y cada detalle de diseño para asegurarme de que mis
      sitios web sean visualmente atractivos, funcionales y accesibles para
      todos. Estoy comprometido a seguir aprendiendo y mejorando continuamente
      mientras busco oportunidades desafiantes que amplíen mi experiencia en el
      desarrollo web.
    </p>
  </section>
  <section>
    <h2>Habilidades</h2>
    <ul>
      <li>HTML</li>
      <li>CSS</li>
      <li>JavaScript</li>
      <li>Git</li>
      <li>Metodologías ágiles</li>
    </ul>
  </section>
</main>
```

{: .important }
Fíjate como ahora en el contenido principal del portfolio (`<main>`) tenemos dos secciones (`<section>`), “Acerca de mi” y “Habilidades”.

---

## Anidado de elementos

En la siguiente sección vamos a listar nuestra experiencia previa. Para hacer esto podemos utilizar nuevamente una lista no ordenada (`<ul>`). Pero lo que buscamos conseguir es algo como esto:

- Empresa X (2022 - presente)
  > - Logro 1
  > - Logro 2
- Empresa Y (2020-2022)
  > - Logro 1
  > - Logro 2

El anidado se refiere a como en este ejemplo tenemos una lista dentro de otra. En el primer nivel listamos las empresas, y en el segundo nivel listamos los logros.

Esto se puede replicar en HTML simplemente poniendo un elemento dentro de otro, que es algo que ya venimos haciendo, por ejemplo, al colocar secciones dentro de `<main>`.

### Actividad - Experiencia

✅ Fijate que pasa si agregas este código:

```html
<ul>
  <li>
    Empresa X
    <ul>
      <li>Logro</li>
    </ul>
  </li>
</ul>
```

En este ejemplo tenemos una lista con un ítem, y dentro de ese ítem tenemos otra lista con otro ítem, logrando así los dos niveles que necesitamos.

Construí la sección de “Experiencia” utilizando este concepto.

El código completo de la sección debería quedarte mas o menos de esta forma:

{: .important }
Recomendamos que evites copiar y pegar este código que es más largo. Lo mejor es ir agregando un elemento a la vez. Empezá agregando el encabezado, luego el primer nivel de la lista con las empresas, y finalmente el segundo nivel con las responsabilidades o logros.

```html
<section>
  <h2>Experiencia</h2>
  <ul>
    <li>
      <b>Empresa X</b> (2022-presente)
      <ul>
        <li>Desarrollador web junior</li>
        <li>
          Responsable del desarrollo y mantenimiento de la página web de la
          empresa
        </li>
      </ul>
    </li>
    <li>
      <strong>Empresa Y</strong> (2020-2022)
      <ul>
        <li>Diseñador web</li>
        <li>
          Responsable del diseño y maquetación de la página web de la empresa
        </li>
      </ul>
    </li>
  </ul>
</section>
```

{: .important }
Asegurate de que cada etiqueta de apertura tenga una etiqueta de cierre correspondiente. Si hay 6 etiquetas de apertura `<li>`, tienen que haber 6 etiquetas de cierre `</li>`

{: .concept }
Las etiquetas `<b>` y `<strong>` se usan para poner un texto en negritas.

✅ ¿Cuál es la diferencia entre las etiquetas `<b>` y `<strong>`? ¡Busca en Google!

## Atributos

En HTML podemos utilizar un “elemento ancla” para crear un enlace a una dirección web, como este [enlace](https://developer.mozilla.org/es/docs/Web/HTML/Element/a), que te lleva a la página web de la documentación del elemento.

✅ Hace click en la palabra "enlace" en el párrafo anterior.

Vemos como en el ejemplo de la documentación tenemos por un lado un texto que estamos mostrando, la palabra “enlace” en este caso, y por otro lado tenemos la dirección web.

Para usar un elemento ancla de esa forma utilizamos la etiqueta `<a>`.

Digamos que quiero que al hacer click sobre la palabra **“Foro”**, el navegador abra la página web de **Stack Overflow**, el foro más popular para buscar ayuda con temas de programación.

Para lograr esto puedo encapsular la palabra con las etiquetas de apertura y cierre `<a>` `</a>`, asi: `<a>Foro</a>`. Pero me falta una forma de indicarle al navegador que este elemento es un ancla al enlace `https://stackoverflow.com/`.

Para darle al navegador esta información adicional, podemos utilizar atributos.

Ya mencionamos que las etiquetas tienen una apertura y un cierre, pero ademas de eso pueden tener **atributos**, que nos permiten agregar información adicional que el navegador sabe interpretar.

{: .concept }
Todos los elementos HTML pueden tener atributos que proveen información adicional sobre los elementos.
Los atributos siempre van en la etiqueta de apertura y tienen un nombre y un valor, que se escriben así: **nombre="valor"** ("valor" siempre entre comillas)

En este caso, el nombre del atributo que tenemos que usar es **href**, y el valor es el enlace al que queremos ir.

Los atributos siempre se ponen dentro de la etiqueta de apertura, y pueden haber tantos atributos como se necesiten para lograr lo que queremos hacer.

✅ Proba de agregar `<a href="https://stackoverflow.com/">Foro</a>` a tu HTML para probar que pasa.

### Actividad - Proyectos (`<a>`)

<!-- {: .no_toc } -->

Contruí la sección de "Proyectos" del portfolio.

Para hacer esto tenes que usar una lista no ordenada nuevamente (`<ul>`), donde cada item `<li>` sea un proyecto. Para cada item ademas, queremos tener un titulo o nombre del proyecto, y un párrafo (`<p>`) para agregar una descripción, y como siempre, tiene que estar todo dentro de su propia sección `<section>`.

Ademas, queremos que al hacer click en el nombre de cualquier proyecto el navegador abra una pagina web que contenga una demo. Para hacer esto tenemos que usar un elemento de anclaje (`<a>`) y su atributo **href**.

Todavía no tenes proyectos reales, asi que por ahora podes poner Proyecto 1, Proyecto 2, etc, con links a cualquier pagina web.

Trata de hacer esto sin mirar el código completo! Una vez que termines, la sección completa debería quedar asi:

```html
<section>
  <h2>Proyectos</h2>
  <ul>
    <li>
      <a href="https://www.nytimes.com/games/wordle/index.html"
        >Clon de Wordle</a
      >
      <p>Descripción del proyecto 1</p>
    </li>
    <li>
      <a href="https://www.nytimes.com/games/wordle/index.html">Proyecto 2</a>
      <p>Descripción del proyecto 2</p>
    </li>
  </ul>
</section>
```

---

Ahora solo nos falta la sección de contactos. Tradicionalmente, cuando hacemos una página web pondríamos una sección de contactos en el pie de página, en el `<footer>`, pero este es un caso diferente, porque al tratarse de un portfolio, la sección de contactos es parte del contenido principal, el objetivo final de la página es que alguien nos contacte, y como tal, debe estar dentro del `<main>` como otro `<section>`.

### Actividad - Contacto

Crea una nueva sección para los contactos. Necesitamos "listar" un correo electrónico, teléfono, y redes sociales.

```html
<section>
  <h2>Contacto</h2>
  <ul>
    <li>Email: ejemplo@correo.com</li>
    <li>Teléfono: 123-456-7890</li>
    <li>
      Redes Sociales:
      <ul>
        <li>
          <a href="https://www.facebook.com/tucuenta">Facebook</a>
        </li>
        <li>
          <a href="https://twitter.com/tucuenta">Twitter</a>
        </li>
        <li>
          <a href="https://www.linkedin.com/in/tucuenta">LinkedIn</a>
        </li>
        <!-- Agrega más redes sociales si lo deseas -->
      </ul>
    </li>
  </ul>
</section>
```

# Navegación

Con esto tenemos el portfolio casi terminado, pero podemos agregar una cosa mas para mejorar la "experiencia de usuario" de nuestro sitio.

Podemos agregar un menu, para que en el caso en el que el portfolio sea muy largo, podamos navegar rápidamente a la sección que nos interesa.

Para hacer esto vamos a tener que darle un nombre a cada sección.

### Actividad - Menú

Busca todas las etiquetas de apertura `<section>`, y a cada una ponele el atributo **"id"** con un nombre único.

{: .concept }
En HTML, un ID es un nombre único que usamos para identificar un elemento. Este nombre no se puede repetir. La sintaxis es esta: `id="nombre_propio"`

Las secciones deberían quedarte asi:

```html
<section id="acerca-de-mi">...</section>
<section id="habilidades">...</section>
<section id="experiencia">...</section>
<section id="proyectos">...</section>
<section id="contacto">...</section>
```

A continuación, vamos a utilizar el elemento `<nav>` para crear un menu, y dentro ponemos enlaces a todas las secciones con una lista ordenada:

```html
<nav>
  <ul>
    <a href="#acerca-de-mi">Acerca de mí</a>
    <a href="#habilidades">Habilidades</a>
    <a href="#experiencia">Experiencia</a>
    <a href="#proyectos">Proyectos</a>
    <a href="#contacto">Contacto</a>
  </ul>
</nav>
```

Lo normal es poner este menu dentro del elemento `<header>`, para que quede mas ordenado todo.

# Checkpoint

Al llegar hasta aca el contenido del portfolio ya esta terminado, y tenes los conocimientos básicos de HTML que necesitas para seguir avanzando por tu cuenta!

El documento HTML debería quedarte asi si estas siguiendo el tutorial:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mi portafolio personal</title>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <a href="#acerca-de-mi">Acerca de mí</a>
          <a href="#habilidades">Habilidades</a>
          <a href="#experiencia">Experiencia</a>
          <a href="#proyectos">Proyectos</a>
          <a href="#contacto">Contacto</a>
        </ul>
      </nav>
      <h1>Mi nombre</h1>
      <h2>Mi profesión</h2>
    </header>
    <main>
      <section id="acerca-de-mi">
        <h2>Acerca de mí</h2>
        <p>
          Como desarrollador web junior, fusiono mi pasión por el diseño y la
          programación para crear experiencias web excepcionales. Me esfuerzo
          por cada línea de código y cada detalle de diseño para asegurarme de
          que mis sitios web sean visualmente atractivos, funcionales y
          accesibles para todos. Estoy comprometido a seguir aprendiendo y
          mejorando continuamente mientras busco oportunidades desafiantes que
          amplíen mi experiencia en el desarrollo web.
        </p>
      </section>
      <section id="habilidades">
        <h2>Habilidades</h2>
        <ul>
          <li>HTML</li>
          <li>CSS</li>
          <li>JavaScript</li>
          <li>Git</li>
          <li>Metodologías ágiles</li>
        </ul>
      </section>
      <section id="experiencia">
        <h2>Experiencia</h2>
        <ul>
          <li>
            <b>Empresa X</b> (2022-presente)
            <ul>
              <li>Desarrollador web junior</li>
              <li>
                Responsable del desarrollo y mantenimiento de la página web de
                la empresa
              </li>
            </ul>
          </li>
          <li>
            <strong>Empresa Y</strong> (2020-2022)
            <ul>
              <li>Diseñador web</li>
              <li>
                Responsable del diseño y maquetación de la página web de la
                empresa
              </li>
            </ul>
          </li>
        </ul>
      </section>
      <section id="proyectos">
        <h2>Proyectos</h2>
        <ul>
          <li>
            <a href="https://www.nytimes.com/games/wordle/index.html"
              >Clon de Wordle</a
            >
            <p>Descripción del proyecto 1</p>
          </li>
          <li>
            <a href="https://www.nytimes.com/games/wordle/index.html"
              >Proyecto 2</a
            >
            <p>Descripción del proyecto 2</p>
          </li>
        </ul>
      </section>
      <section id="contacto">
        <h2>Contacto</h2>
        <ul>
          <li>Email: ejemplo@correo.com</li>
          <li>Teléfono: 123-456-7890</li>
          <li>
            Redes Sociales:
            <ul>
              <li>
                <a href="https://www.facebook.com/tucuenta">Facebook</a>
              </li>
              <li>
                <a href="https://twitter.com/tucuenta">Twitter</a>
              </li>
              <li>
                <a href="https://www.linkedin.com/in/tucuenta">LinkedIn</a>
              </li>
              <!-- Agrega más redes sociales si lo deseas -->
            </ul>
          </li>
        </ul>
      </section>
    </main>
    <footer>
      <p>Copyright &copy; 2024</p>
    </footer>
  </body>
</html>
```

# Marcado semántico

En general, es preferible usar ‘semántica’ significativa al escribir HTML. Qué significa eso? Significa que tenemos que utilizar las etiquetas HTML de la forma en que fueron diseñadas. Por ejemplo, el título principal en una página debería usar siempre una etiqueta `<h1>`.

El uso de marcado semántico, como que los encabezados sean `<h1>` y las listas no ordenadas se representen como `<ul>`, ayuda a los lectores de pantalla a navegar por una página. En general, los botones deben escribirse como `<button>` y las listas deben ser `<li>`. Si bien es posible usar elementos `<span>` de estilo especial con controladores de clic para simular botones, es mejor para los usuarios con capacidades diferentes usar tecnologías para determinar en qué parte de una página reside un botón e interactuar con él. Por esta razón, intenta utilizar el marcado semántico tanto como sea posible.
