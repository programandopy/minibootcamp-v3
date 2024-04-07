---
title: Manipulación del DOM
has_children: false
# parent: Introducción a JavaScript
nav_order: 5
# nav_exclude: true
---

# Proyecto de Diseño Parte 3: Introducción a Manipulación del DOM
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

Manipular el DOM, o el "Modelo de objetos de documento", es un aspecto clave del desarrollo web. Según [MDN](https://developer.mozilla.org/es/docs/Web/API/Document_Object_Model/Introduction){:target="_blank"}:

> "El modelo de objeto de documento (DOM) es una interfaz de programación para los documentos HTML y XML. Facilita una representación estructurada del documento y define de qué manera los programas pueden acceder, al fin de modificar tanto su estructura, estilo y contenido. El DOM da una representación del documento como un grupo de nodos y objetos estructurados que tienen propiedades y métodos. Esencialmente, conecta las páginas web a scripts o lenguajes de programación. ". 

> Pensá en el DOM como un árbol, que representa todas las formas en que se puede manipular un documento de página web. Se han escrito varias API (interfaces de programas de aplicación) para que los programadores, utilizando el lenguaje de programación de su elección, puedan acceder al DOM y editarlo, cambiarlo, reorganizarlo y administrarlo de otro modo.

![representacion DOM](images/dom-tree.png){: width="650" }{: .center-image}

### Actividad:
{: .no_toc }

En la carpeta de tu proyecto, creá un nuevo archivo llamado `script.js`. 

Ahora tenemos que pedirle al navegador que incluya nuestro archivo. Como siempre, hacemos esto en la sección `<head>`:

```html
	<script src="./script.js" defer></script>
```

{: .note }
Usá `defer` cuando importes un archivo JavaScript externo en el archivo html para permitir que el JavaScript se ejecute sólo después de que el archivo HTML se haya cargado por completo. También podría usar el atributo `async`, que permite que el script se ejecute mientras se analiza el archivo HTML, pero en nuestro caso, es importante tener los elementos HTML completamente disponibles para arrastrar antes de permitir que se ejecute el script de arrastre.

Para probar que todo esta funcionando, podemos imprimir un mensaje en la consola:

```javascript
	console.log('hola mundo')
```

✅ ¿Donde escribimos esta instrucción de javascript? si no esta funcionando podes volver a mirar las lecciones anteriores.

---

# Los elementos DOM

Lo primero que debemos hacer es crear referencias a los elementos que queremos manipular en el DOM. En nuestro caso, son los componentes y productos que esperan actualmente en las barras laterales.

Te invitamos a leer mas sobre como funciona el DOM en esta página: [MDN](https://developer.mozilla.org/es/docs/Web/API/Document_Object_Model/Introduction){:target="_blank"}.

Con cada etiqueta HTML que escribimos en nuestro código, el navegador crea un **ELEMENTO**, con un montón de funcionalidad que nos permite trabajar con el usando javascript.

Hagamos un experimento para entender mejor.

### Actividad:
{: .no_toc }

Vamos a tratar de modificar el color de fondo del `div` del formulario.

Como sabemos, esto lo podemos hacer editando el CSS, pero si lo hacemos asi, el cambio será estático. Se aplica el color que especificamos y esto queda escrito en piedra.

Para tener un comportamiento mas dinámico hagamos lo siguiente:

```javascript
	let form = document.getElementById('calculadora');
```

Lo que hacemos con esto es guardar en la variable `form` el elemento que tenga el id `calculadora`, en este caso el `div` que contiene todos los elementos del formulario.

Desglosemos esta linea de código:
* `document` hace referencia al DOM (modelo de objeto de documento), y con el `.`, podemos pedir algo que se encuentre dentro de ese *objeto*
* `getElementById()`, es un **método** o función que nos devuelve un elemento. Tal como dice el nombre (obtener elemento por id), busca un elemento en el DOM por el ID que especificamos en el HTML.
* `let form =`: Creamos una variable llamada form, y la inicializamos con un valor. Hasta ahora vimos solo algunos tipos de dato que podemos asignar a una variable, en este caso, la variable `form`, tiene un ELEMENTO, que es una estructura de datos llamada  **OBJETO**

{: .important }
El **método** `getElementById`, recibe como **argumento** el ID del elemento que queremos obtener.

Ahora podemos manipular el elemento seleccionado como queramos. En este caso queremos cambiar el color, asi que vamos a acceder a un objeto llamado **style** que se encuentra dentro del elemento, allí encontraremos todas las propiedades de estilo que podemos cambiar.

```javascript
	form.style.backgroundColor = 'blue';
```

Guarda los cambios y actualiza la pagina para ver lo que pasa.

De esta misma forma, interactuar con la pagina para cambiar cosas en cualquier momento y de forma dinámica con JavaScript, gracias a estas herramientas que nos da el DOM para manipular los elementos.

---

### Actividad:
{: .no_toc }

Para continuar con la calculadora, lo primero que tenemos que hacer es obtener todos los elementos que vamos a tener que manipular.

En primer lugar, necesitamos obtener el dato de entrada, para esto necesitamos el `<input>`.

Luego, vamos a necesitar detectar cuando el usuario presiona el botón `calcular`.

Una vez que presionamos el botón, tenemos que poder mostrar los resultados o el mensaje de error, según corresponda.

Para esto, vamos a declarar unas constantes con los elementos que tenemos que manipular:

```js
const CALCULAR = document.getElementById('calcular');
const ERROR = document.getElementById('error');
const FLU = document.getElementById('flu');
const MAN = document.getElementById('man');
```

¿Que está pasando acá? Estamos haciendo referencia al documento y mirando a través de su DOM para encontrar un elemento con un Id particular. Con esto, seleccionamos los elementos y podemos empezar a manipularlos.

✅ ¿Por qué hacemos referencia a elementos por Id? ¿Por qué no por su clase de CSS? Podés consultar la lección anterior sobre CSS para responder a esta pregunta.

---

# Event Listener

En javascript utilizamos algo llamado `eventListener` para definir acciones a tomar cuando ocurre un evento. Vamos a aprender mas sobre eventos en otro proyecto, pero por ahora basta con decir que al presionar el botón para calcular se genera un evento de `click`.

Con un `eventListener` podemos hacer que al presionar el botón, se ejecute una función en la que podemos hacer el calculo y cualquier otra cosa que queramos.

### Actividad:
{: .no_toc }

Escribí esta sección de código en tu archivo script.js para agregar un event listener que espere el click en el botón:

```javascript
CALCULAR.addEventListener('click', () => {
    console.log('Se hizo click!')
})
```

✅ Al hacer click en el botón, se va a ejecutar una función anónima, o `arrow function`. Estas funciones no tienen un nombre, por eso son anónimas, y la sintaxis es asi: `() => { ... }`

Si probas esto vas a ver que al hacer click se imprime algo a la consola.

Funciona!

# Obtener datos de entrada

Ahora ya estamos preparados para calcular la hidratación basal cuando hacemos click en el botón, pero necesitamos obtener el dato de entrada.

Para ello podemos acceder a la propiedad value el elemento `<input>`

### Actividad:
{: .no_toc }

Agregamos lo siguiente a nuestro `eventListener`

```javascript
CALCULAR.addEventListener('click', () => {
    const DATO = document.getElementById('peso').value
    console.log('dato ingresado: ', DATO)
})
```

# Mostrar y ocultar elementos

El siguiente paso va a ser preparar nuestro código para que cuando apretamos el botón se haga el calculo, se muestren los resultados y se oculte el mensaje de error.

### Actividad:
{: .no_toc }

to Javascript deberia estar quedando asi:

```javascript
const CALCULAR = document.getElementById('calcular');
const ERROR = document.getElementById('error');
const FLU = document.getElementById('flu');
const MAN = document.getElementById('man');

CALCULAR.addEventListener('click', () => {
    const DATO = document.getElementById('peso').value
    //validamos que se cargue un dato:
    if (DATO > 0){
        ERROR.style.display = 'none'
        let flujo = calcFlujo(DATO);
        let mantenimiento = flujo*1.5;
        FLU.innerHTML = flujo + ' cc/hr';
        MAN.innerHTML = 'm+m/2 ' + mantenimiento + ' cc/hr';
        FLU.style.display = 'block';
        MAN.style.display = 'block';
    } else {
        ERROR.style.display = 'block';
        FLU.style.display = 'none';
        MAN.style.display = 'none';
    }
})
```

Con esto, hicimos que si se presiona el botón pero el dato estaba vacío o era 0, se muestra el mensaje de error, y por otro lado si el dato se ingreso correctamente, se oculta el mensaje de error y se muestran los mensajes de resultado.

Esto todavia no esta funcionando, porque no declaramos la función `calcFlujo()`, podes comentar esa linea y darle un valor a la variable `flujo` para probar.

---

# El algoritmo

Ya estamos terminando! ahora nos falta solo la parte mas importante, el calculo de los valores que necesitamos mostrar.

### Actividad:
{: .no_toc }

Declará la función calcFlujo() e implementa el algoritmo que diseñaste previamente.

```javascript
function calcFlujo(peso){
    let resto = peso;
    let flujo = 0;
    if (resto>20){
        let aux = resto-20;
        flujo += aux*1;
        resto -= aux;
    } 
    if (resto>10){
        let aux = resto-10;
        flujo += aux*2;
        resto -= aux;
    }
    flujo += resto*4;
    return flujo;
}
```

Listo! con esto el funcionamiento básico de la calculadora esta terminado. Ahora falta calcular según el segundo método para los casos en los que el peso sea mayor a 30kg, pero eso ya podes hacerlo por cuenta propia.

Suerte!