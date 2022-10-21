---
title: Introducción a CSS
has_children: false
nav_order: 5
---

# Proyecto de Diseño Parte 2: Introducción a CSS
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

{: .concept }
Las hojas de estilos en cascada (CSS) son un mecanismo simple para agregarle estilo (colores, espaciado, tipos de letra, etc.) a un Documento Web (otra forma de referirnos a un archivo html).

CSS, o Cascading Style Sheets, resuelve un problema importante del desarrollo web: cómo hacer que tu sitio web se vea bien. 
La apariencia de una pagina web es muy importante, ya que en gran medida esto es lo que la hace útil y fácil de usar. CSS no se trata solo de hacer que tu aplicación se vea bien; también nos deja hacer animaciones y transformaciones que pueden permitir interacciones sofisticadas para tus aplicaciones.

Una organización conocida como *El grupo de trabajo CSS* ayuda a mantener las especificaciones CSS actuales; podés seguir su trabajo en el [sitio del World Wide Web Consortium](https://www.w3.org/Style/CSS/members){:target="_blank"}.

En esta lección, agregaremos estilos a nuestra página web y aprenderemos más sobre varios conceptos de CSS: la cascada, la herencia y el uso de selectores, posicionamiento y uso de CSS para estilizar una página.

## Requisito previo:

{: .important }
Deberías tener el archivo HTML del proyecto terminado y listo para darle estilo, fijate en el apartado "Introducción a HTML".

# La cascada

Las hojas de estilo en cascada incorporan la idea de que los estilos 'se mueven en cascada' de manera que la aplicación de un estilo está guiada por su prioridad. 
* Los estilos establecidos por el autor de un sitio web tienen prioridad sobre los establecidos por un navegador. 
* Los estilos configurados 'en línea' tienen prioridad sobre los configurados en una hoja de estilo externa.

### Actividad:
{: .no_toc }

Para entender mejor esto, empecemos por cambiar algún estilo en nuestra página web. En este caso, queremos que el título sea de color rojo, y no negro como está ahora.

Para hacer esto, ubiquemos el *encabezado* con contenido **Hidratación Basal** en nuestro archivo HTML:

```html
<h1>Hidratación Basal</h1>
```

Las etiquetas `<h1>` se muestran de color negro en el navegador. Para cambiar el color, podemos agregar un **Atributo** a la etiqueta. Los atributos nos permiten modificar la apariencia o el comportamiento de los elementos, y siempre se agregan en **la etiqueta de apertura**. Para cambiar el estilo (en este caso, solo el color), usamos el atributo `style`.

Modificá la linea donde se encuentra la etiqueta `<h1>`, para que quede así:

```html
<h1 style="color: red">Hidratación Basal</h1>
```

{: .concept }
Todos los elementos HTML pueden tener atributos que proveen información adicional sobre los elementos.
Los atributos siempre van en la etiqueta de apertura y tienen un nombre y un valor, que se escriben así: **nombre="valor"**

✅ Guardá los cambios en el HTML y fijate que pasa en la página web. Acordate de actualizar la página para ver los cambios!

Si hiciste todo bien, deberias haber notado que el color del encabezado cambió, y ahora es rojo. Lo que hacemos con el atributo `style`, es decirle al navegador que aplique el estilo indicado entre comillas, que está escrito en CSS.

De esta manera podemos seguir estilizando la página web cambiando colores y otras propiedades. Sin embargo, esto implica agregar atributos a todos los elementos del HTML, y esto resulta muy poco práctico y difícil de comprender cuando nuestro documento se hace más grande.

Para resolver este problema, usamos "Hojas de estilo externas". Se tratan de archivos en los que podemos escribir todos los estilos que queremos aplicar.

---

### Actividad:
{: .no_toc }

En Visual Studio, crea un archivo nuevo llamado `style.css` en la carpeta `Layout`

![crear-archivo](images/Animation.gif)

El archivo `style.css`, será el lugar donde vamos a especificar todos los estilos de nuestra página.

Pero, ahora que tenemos un archivo externo donde vamos a escribir los estilos, como sabe el navegador que debe mirar ahí?

Tenemos que decirle al navegador que siempre mire el archivo que creamos para saber que estilos aplicar, esto se hace en el HTML, en la cabecera del archivo (en la sección `<head>`).

Ubicá la cabecera del HTML y agregá ahí esta línea:

```html
<link rel="stylesheet" href="./style.css" />
```

La **etiqueta** `<link />` define la relación entre el archivo HTML y otros archivos. Con el **atributo** `rel`, le decimos que el archivo que queremos vincular es una hoja de estilos, y el **atributo** `href` le dice al navegador donde encontrar el archivo.

{: .important }
En el atributo `href`, el nombre del archivo debe coincidir con el nombre que le dimos cuando lo creamos. Si mas adelante no ves cambios en los estilos, asegurate de que los nombres coincidan.

La cabecera del archivo HTML debería quedar así:

```html
<head>
  <title>Calculadora de hidratación</title>
  <link rel="stylesheet" href="./style.css" />
</head>
```

Ahora que ya tenemos nuestra hoja de estilos externa creada y vinculada con el html, escribir nuestro primer estilo.

Agregá el siguiente código a tu archivo `style.css`:

```css
h1 {
  color: blue;
}
```

✅ ¿Qué colores cambiaron tu aplicación web? ¿Por qué? (explicación mas abajo).

Si hiciste todo bien, no debería haber cambiado el titulo de la calculadora, pero si el titulo de la explicación del calculo.

Al escribir `h1{  }`, estamos diciendo que todos los estilos que escribamos entre las llaves `{}` se deben aplicar a todos los elementos `h1` en el HTML. En este caso, tenemos dos elementos `h1`, pero a uno de ellos le pusimos un estilo en línea para que sea rojo, directo en el HTML.

{: .concept }
`h1{  }` es un **SELECTOR** de etiquetas, porque selecciona todas las etiquetas `h1` del HTML para aplicarles los estilos correspondientes. Se puede usar para seleccionar cualquier etiqueta, por ejemplo: `div{  }`, o `h2{  }`

Ahora el navegador ve en nuestra hoja de estilos que estamos pidiendo que el color sea azul, así que el navegador tiene dos instrucciones contradictorias:

```css
/* EN EL CSS, DECIMOS QUE EL COLOR ES AZUL */
h1 {
  color: blue;
}
```

```html
<!-- EN EL HTML, DECIMOS QUE EL COLOR ES ROJO -->
<h1 style="color: red">Hidratación Basal</h1>
```

Como decide el navegador cual de los dos colores aplicar?

Lo hace siguiendo las reglas de la **cascada**, que dicen que siempre los estilos en linea tienen prioridad. Por eso el navegador sigue mostrando el color rojo, ignorando lo que escribimos en la hoja de estilos.

Si borramos el estilo en línea que aplicamos, el navegador tomará lo que encuentre en la hoja de estilos.

Probá dejando esta línea del HTML como estaba originalmente:

```html
<h1>Hidratación Basal</h1>
```
Si guardas todos los cambios y actualizas la página, deberías ver que el elemento h1 ahora es azul.

---

# Herencia

Ahora que tenemos la hoja de estilos preparada y ya entendemos como y donde escribir CSS, empecemos a ajustar los estilos de nuestra página.

### Actividad:
{: .no_toc }

En primer lugar, queremos cambiar la fuente del texto, esto es el tipo de letra de todo el texto en nuestra página. Para lograrlo, agregá el siguiente código el archivo CSS:

```css
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,800');

body{
    font-family: 'Montserrat', sans-serif;
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
  <h1>Hidratación Basal</h1>
</body>
```

decimos que el elemento `h1` es un hijo del elemento `body`.

Lo que hicimos con el selector `body {  }` es definir un tipo de letra para el elemento `body`, y este todos los estilos que sean aplicados a este elemento serán **heredados** a sus hijos, en este caso, al elemento `h1`. Es por esta herencia que logramos que nuestro título cambie.

Hacemos esto de esta manera a que todo el texto que incluyamos en la página web tenga este tipo de letra, sin tener que aplicar estilos a todos los elementos de texto que queramos cambiar.

{: .concept }
En HTML, los elementos heredan los estilos de todos sus antepasados.

✅ Podés probar agregando otros elementos de texto para verificar cómo funciona la herencia, y te desafiamos a que hagas que otras propiedades sean heredadas (podes probar con la propiedad `color` que ya utilizamos).

---

# Selectores CSS

En CSS, los selectores son patrones o una sintaxis específica que nos permite *seleccionar* los elementos que queremos estilizar.

Nos permiten aplicar estilos elementos específicos. Hasta ahora, solo utilizamos los selectores de etiquetas.

## Selectores de Etiquetas

Hasta ahora, en el archivo `style.css` solo aplicamos estilos a dos elementos HTML: `<body>` y `<h1>`.

Los selectores de etiqueta o elementos nos permiten aplicar estilos a los elementos, buscando por sus etiquetas en el archivo HTML. Por ejemplo, cuando usamos el selector `h1 {  }`, estamos seleccionando **TODOS** los elementos de tipo `h1` en el HTML.

### Actividad:
{: .no_toc }

Vamos a utilizar un selector de elementos para agregarle algunos estilos al `<body>` que queremos que se hereden en todos los elementos.

Necesitamos cambiar el color de fondo, el tipo de letra y el color del texto para toda la pagina.

Asegurate de que tu archivo CSS quede de la siguiente manera (puede que tengas que reemplazar cosas las pruebas que vinimos haciendo):

```css
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,800');

body{
    background: #f6f5f7; 
    font-family: 'Montserrat', sans-serif;
    color: #3E363F;
}
```
---

Pareciera que con este tipo de selector podemos estilizar toda la página, pero el problema es que no podemos seleccionar un solo elemento específico, solo podemos seleccionar **todos** los `h1` o **todos** los `div`, y para continuar necesitamos aplicar estilos solo a un par de elementos de tipo `div`, pero no a los demás.

## Selectores de ID

Cuando en el HTML tenemos muchos elementos del mismo tipo (por ejemplo, muchos `div`) pero solo queremos modificar uno de ellos, podemos utilizar un selector de **ID**.

{: .concept }
En HTML, un ID es un nombre único que usamos para identificar un elemento. Este nombre no se puede repetir.

Si queremos aplicar un estilo a uno solo de los `div` que tenemos en nuestro HTML, necesitamos una forma de indivualizarlo, darle un nombre único. Este nombre único es el **ID**.

Para darle un ID, utilizamos el [atributo](#1-la-cascada) `id`.

{: .concept }
Recordemos que anteriormente usamos el atributo `style` para asignar estilos. El atributo `id` hace otra cosa, pero tiene la misma sintaxis.

Para asignar un identificador a un elemento escribimos el atributo de la siguiente manera, por ejemplo, en un `div`:

```html
<div id='nombre1'></div>
<div id='nombre2'></div>
<div id='nombre1'></div> <!-- NO PERMITIDO, el id 'nombre1' ya existe -->
```

{: .concept }
En el ejemplo vemos como se utiliza el id para nombrar elementos, pero es importante recordar que el id no puede repetirse.

### Actividad:
{: .no_toc }

Necesitamos centrar todo el contenido en la pagina, vertical y horizontalmente. Ya agregamos un div en el HTML, pero nos falta agregarle un id para poder identificarlo.

Para lograr esto, vamos a agregarle el atributo `id=contenedor` al `div` que encapsula todo el contenido, el HTML debe quedar así:

```html
<body>
  <div id="contenedor">
      <div>
          <div>
              <h1>Hidratación Basal</h1>
              <p >Completa todos los datos</p>
              <input type="number" placeholder="Peso en kg" />
              <p>* Debe completar todos los datos</p>
              <button>Calcular</button>
              <p>71cc/h</p>
              <p>m+m/2 : 105cc/h</p>
          </div>
      </div>
      <div>
          <div>
              <h1>¿Como se calcula?</h1>
              <ul>
                  <li>De 0kg a 10kg, se calcula 100cc por cada kilo.</li>
                  <li>Se suman 50cc por cada kilo de peso por arriba de 10kg, hasta 20kg</li>
                  <li>De 20kg para arriba, se suman 20cc por cada kilo adicional</li>
              </ul>
          </div>
      </div>
  </div>
</body>
```

Ahora que tenemos un id en el `div`, podemos utilizarlo para seleccionar ese elemento y darle estilos. Copia este codigp debajo de lo ultimo que hiciste en el CSS:

```css
#contenedor{
    width: 900px;
    height: 500px;
    text-align: center;
    /* Estas 3 lineas se encargan de centrar el div vertical y horizontalmente */
    position: absolute;
    inset: 0;
    margin: auto;
}
```

Utilizamos el selector de id escribiendo `#` seguido del nombre que le dimos al elemento, en este caso: `#tablero-izquierdo {  }`. Todos los estilos en ese selector, serán aplicados solo al `div` con ese ID.

Lo que hacemos con este código es lo siguiente 
* Utilizamos la propiedad `width` para fijar un ancho máximo para el div.
* La propiedad `height` nos permite fijar una altura específica.
* Finalmente, utilizamos las propiedades `position`, `inset` y `margin` centrar nuestro div vertical y horizontalmente.

✅ Investigá como se usan estas propiedades para centrar el div, y cambia los valores para tratar de entender como funciona este posicionamiento.

{: .concept }
La propiedad `inset` es una forma de asignar el mismo valor a los 4 margenes (superior, inferior, derecho e izquierdo), al poner estos valores a 0 y la posición en `absolute`, podemos lograr que el dive quede centrado.

---

### Actividad:
{: .no_toc }

Vamos a seguir con el posicionamiento para dejar todo en su lugar, basándonos en el diseño de la sección de requerimientos.

Nos falta que la sección del formulario y la de la explicación estén lado a lado. Para esto tenemos que seguir los mismos métodos usados para centrar el contenido. Necesitamos agregar identificadores a los `div` que encapsulan los las secciones que queremos modificar.

Modifica el cuerpo del HTML para agregar los identificadores y que quede asi:

```html
<body>
  <div id="contenedor">
      <div id="calculadora">
          <div>
              <h1>Hidratación Basal</h1>
              <p >Completa todos los datos</p>
              <input type="number" placeholder="Peso en kg" />
              <p>* Debe completar todos los datos</p>
              <button>Calcular</button>
              <p>71cc/h</p>
              <p>m+m/2 : 105cc/h</p>
          </div>
      </div>
      <div id="detalle">
          <div>
              <h1>¿Como se calcula?</h1>
              <ul>
                  <li>De 0kg a 10kg, se calcula 100cc por cada kilo.</li>
                  <li>Se suman 50cc por cada kilo de peso por arriba de 10kg, hasta 20kg</li>
                  <li>De 20kg para arriba, se suman 20cc por cada kilo adicional</li>
              </ul>
          </div>
      </div>
  </div>
</body>
```

Fijate como tenemos organizado el HTML en este punto:
* Contenedor: Encapsula todo el contenido.
  * Calculadora: Encapsula el formulario.
  * Detalle: Encapsula la explicacion del calculo.

Ahora, vamos a agregar los siguientes estilos al CSS:

```css
#calculadora{
    background: white;
    /* Con estas 3 lineas vamos a hacer que los divs queden lado a lado */
    width: 50%;
    height: 100%;
    float: left;
}

#detalle{
    background: #FF416C;
    /* Con estas 3 lineas vamos a hacer que los divs queden lado a lado */
    width: 50%;
    height: 100%;
    float: left;
    color: #f6f5f7;
}
```
La clave para lograr el posicionamiento que buscamos es la propiedad `float: left;`, combinada con el ancho del 50% del contenedor padre.

Ademas de posicionar correctamente el contenido, en estas lineas ya definimos los colores apropiados, pero si prestas atención vas a ver que el contenido dentro de los divs esta centrado horizontalmente, pero no verticalmente.

Si te fijas en el HTML que estuvimos escribiendo, el contenido de ambas secciones esta encapsulado en dos `divs`. Tenemos por un lado los divs calculadora y detalle, pero dentro de cada uno tenemos otros divs.

## Clases

Ya vimos como los selectores de etiqueta seleccionan todos los elementos con la misma etiqueta, y los selectores de ID seleccionan únicamente un elemento con el id especificado.

Ahora, que hacemos si necesitamos estilizar solo algunos de los `div`, pero no todos. Por ejemplo, los `divs` dentro de las secciones de calculadora y detalle.

Para resolver esto vamos a usar otro atributo: `class`.

### Actividad:
{: .no_toc }

Modifica el HTML para que quede asi:

```html
<body>
  <div id="contenedor">
      <div id="calculadora">
          <div class="contenido">
              <h1>Hidratación Basal</h1>
              <p >Completa todos los datos</p>
              <input type="number" placeholder="Peso en kg" />
              <p>* Debe completar todos los datos</p>
              <button>Calcular</button>
              <p>71cc/h</p>
              <p>m+m/2 : 105cc/h</p>
          </div>
      </div>
      <div id="detalle">
          <div class="contenido">
              <h1>¿Como se calcula?</h1>
              <ul>
                  <li>De 0kg a 10kg, se calcula 100cc por cada kilo.</li>
                  <li>Se suman 50cc por cada kilo de peso por arriba de 10kg, hasta 20kg</li>
                  <li>De 20kg para arriba, se suman 20cc por cada kilo adicional</li>
              </ul>
          </div>
      </div>
  </div>
</body>
```

Para cambiar el estilo de los elementos div que tienen el atributo `class="contenido"`, tenemos que utilizar un selector de clase.

Para usar los selectores de ID usamos el atributo `id`. Ahora necesitamos usar el atributo `class`, que ya incluimos cuando hicimos el HTML.

La clase es similar al id, pero en este caso se puede repetir. Esto significa que como vemos en el extracto de código de arriba, podemos tener muchos elementos que pertenecen a la misma clase.

Para centrar el contenido verticalmente, vamos a escribir el siguiente código en el CSS:

```css
.contenido{
    /* Estas tres lineas van a centrar el contenido verticalmente dentro de cada div */
    position: relative;
    top: 50%;
    transform: translateY(-50%);
    overflow: hidden;
    padding: 40px;
}
```

Con esto, terminamos el posicionamiento de las partes del HTML! Ahora solo queda modificar algunos estilos mas.

## Cambiando los estilos de elementos HTML

Lo siguiente que vamos a hacer es cambiar el estilo por defecto que tenemos en el `<input>` y `<button>`:

```css
input {
	width: 70%;
    padding: 12px 15px;
    border: none;
    background-color: #eee;
}

button {
  font-size: 15px;
	font-weight: bold;
	padding: 12px 45px;
	border-radius: 30px;
	background-color: #FF416C;
	border: 1px solid #FF416C;
	color: #FFFFFF;
	text-transform: uppercase;
	letter-spacing: 1px;
	transition: transform 20ms ease-in;
}

button:active {
	transform: scale(0.95);
}
```

✅ Escribi estos estilos uno a uno y fijate que cambia con cada linea para entender para que sirven.

Por ultimo, vamos a volver a tocar los estilos del contedor para darle un borde redondeado y una sombra:

```css
#contenedor{
  width: 900px;
  height: 500px;
  text-align: center;
  /* Estas 3 lineas se encargan de centrar el div vertical y horizontalmente */
  position: absolute;
  inset: 0;
  margin: auto;
  border-radius: 10px;
  overflow: hidden; 
  box-shadow: 0 14px 28px rgba(0,0,0,0.25), 
    0 10px 10px rgba(0,0,0,0.22);
}
```

Ya estamos terminando! solo nos falta modificar los estilos de los mensajes de error y de los resultados.

Vamos a hacer esto, vamos a tener que agregar un ID para el mensaje de error, y clases para los resultados. El HTML deberia quedar asi:

```html
<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="./style.css">
        <script src="script.js" defer></script>
    </head>
    <body>
        <div id="contenedor">
            <div id="calculadora">
                <div class="contenido">
                    <h1>Hidratación Basal</h1>
                    <p class="item">Completa todos los datos</p>
                    <input class="item" id="peso" type="number" placeholder="Peso en kg" />
                    <p class="item" id="error">* Debe completar todos los datos</p>
                    <button class="item" id="calcular">Calcular</button>
                    <p class="item resultado" id="flu">71cc/h</p>
                    <p class="item resultado" id="man">m+m/2 : 105cc/h</p>
                </div>
            </div>
            <div id="detalle">
                <div class="contenido">
                    <h1>¿Como se calcula?</h1>
                    <ul>
                        <li>De 0kg a 10kg, se calcula 100cc por cada kilo.</li>
                        <li>Se suman 50cc por cada kilo de peso por arriba de 10kg, hasta 20kg</li>
                        <li>De 20kg para arriba, se suman 20cc por cada kilo adicional</li>
                    </ul>
                </div>
            </div>
        </div>
    </body>
</html>
```

Para cambiar el estilo tenemos que hacer lo siguiente:

```css
#error{
    color: red;
    font-weight: bold;
    display: none;
}

.resultado{
    color: #0A81D1;
    font-weight: bold;
    font-size: 25px;
    margin-bottom: 5px;
    display: none;
}
```

Fijate que con `display: none` lo que hacemos es ocultar los elementos para que no se vean al principio, y mas adelante vamos a modificar estas propiedades con javascript.
---

Terminamos! La página web debería haberte quedado mas o menos como planteamos en la sección de requerimientos.
