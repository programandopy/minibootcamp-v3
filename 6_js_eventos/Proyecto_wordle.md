---
title: Proyecto Wordle PPY
has_children: true
nav_order: 7
has_toc: true
---

# Como programar un juego de palabras con JavaScript
{: .no_toc }

Eventos
{: .label }

Arrays
{: .label }

Manipulación del DOM
{: .label }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>
---

En este tutorial, aprenderás cómo funcionan los eventos y como modificar el HTML desde JavaScript.

Para esto, vamos a trabajar con una version del juego en linea “Wordle”, que es un juego en el que el jugador debe adivinar una palabra de cinco letras. El juego tiene una interfaz simple, por lo que es fácil de entender y es un buen ejemplo para este tutorial.

# Requerimientos

Antes de empezar cualquier proyecto, tenemos que recopilar toda la información que podamos sobre las funcionalidades y características que debe tener, ya que entre estas podremos encontrar cosas importantes que van a definir la forma de empezar.

En este caso, vamos a implementar una version del juego “Wordle” simplificada: [https://wordlegame.org/](https://wordlegame.org/).

### Actividad - Conocer el juego

Entra a [https://wordlegame.org/](https://wordlegame.org/) y juega un par de rondas para entender como tiene que funcionar el juego.

---

No queremos copiar todas las características originales, pero tratemos de hacer algo aproximado:

- Necesitamos obtener una palabra de alguna lista.
    - Podemos empezar con una palabra fija, y después tenemos dos opciones:
        - Podemos crear un array de palabras y seleccionar una al azar.
        - Podemos obtener una palabra de un diccionario en internet usando una API.
    - Las palabras solo tendrán 5 letras.
- Necesitamos un lugar donde el usuario escriba la palabra.
    - Wordle muestra un teclado, nosotros podemos simplificar esto mostrando un campo (`<input>`) y un botón de `Adivinar`.
- Se le debe indicar al jugador qué letras están correctas y cuáles mal, y también cuáles son todas las palabras o letras que ya usó.
    - El original usa el mismo teclado para resolver esto. Si no vamos a tener un teclado, tenemos que mostrar las letras jugadas de otra forma.
- El juego tiene que indicarme si gané, y qué letras están acertadas o erradas:
    - Letras que están en el lugar correcto se deben mostrar en VERDE
    - Letras que existen en la palabra, pero no están en el lugar correcto, se deben mostrar en AMARILLO
    - Letras que no existen se deben mostrar en GRIS
- Se cuenta con un número limitado de intentos. En principio, 6.

# Configuración del proyecto

En este tutorial vamos a centrarnos en el algoritmo y en JavaScript, por lo que no necesitamos adentrarnos mucho en lo que es HTML o CSS.

### Actividad - HTML y CSS

Antes de empezar, debemos preparar el proyecto:

1. Como siempre lo primero es crear una carpeta, esta vez con el nombre `wordleppy`.
2. Dentro de esa carpeta, vamos a crear un archivo `index.html`, y vamos a pegar ahi el siguiente código:
    
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <title>Wordle PPY</title>
    		<link rel="stylesheet" href="style.css">
        <script src="script.js" defer></script>
      </head>
      <body>
        <h1>Wordle PPY</h1>
        <input type="text" id="guess-input">
        <button id="guess-button">Intentar</button>
        <div id="grid"></div>
        <p id="guesses">
      </body>
    </html>
    ```
    
3. El siguiente paso es crear un archivo CSS llamado `style.css`. Recordemos que el nombre debe coincidir con la referencia en el HTML.
    
    ```css
    body {
      font-family: Arial, sans-serif;
    }
    
    h1 {
      text-align: center;
      margin-top: 50px;
    }
    
    #guess-input {
      display: block;
      margin: 0 auto 20px;
      padding: 10px;
      font-size: 18px;
      width: 250px;
      border: 1px solid #ccc;
    }
    
    #guess-button {
      display: block;
      margin: 0 auto;
      padding: 10px 20px;
      font-size: 18px;
      background-color: #0CBABA;
      color: #fff;
      border: none;
      border-radius: 3px;
    }
    
    button:active {
    	transform: scale(0.95);
    }
    
    .letter {
        border: 1px solid black;
        padding: 3px;
        margin: 3px;
        min-width: 20px;
        text-align: center;
        display: inline-block
    }
    
    .row{
        margin-bottom: 10px;
    }
    
    .input-area{
        margin: 30px;
    }
    ```
    
    Este código es bastante largo, pero es solo para que se vea mejor nuestra aplicación mientras trabajamos. Ya deberías poder entender este código, asi que no vamos a entrar en detalles.
    
4. Finalmente, tenemos que crear el archivo `script.js`. Este archivo es donde vamos a escribir nuestro algoritmo y todas las funcionalidades del juego. Vamos a ir completando este archivo de a poco.
    
    ```jsx
    console.log("Hola Mundo")
    ```
    
    Como antes, podemos imprimir algo en la consola para verificar que toda la estructura del proyecto esta funcionando, y deberías ver algo asi en la pantalla: 
    
    ![Untitled](images/wordle.png)

---

# Inicialización del archivo `script.js`

Nuestro archivo tendrá una sección de preparación en la parte

Lo primero que tenemos que hacer es preparar algunas variables globales. Estos son valores que necesitamos recordar durante toda la partida.

En nuestro caso tenemos dos:

- La cantidad de intentos.
- La palabra que vamos a usar.

{: .concept }
Recordemos que las variables tienen un SCOPE o ÁMBITO, que define donde se puede acceder a la misma.

El scope en JavaScript se refiere al alcance de una variable, es decir, dónde en el código se puede acceder a ella. Las variables pueden ser declaradas en diferentes ámbitos, como a nivel global o dentro de una función, y su alcance se limita a ese ámbito específico. Es importante entender el scope en JavaScript para evitar errores y escribir código más limpio y eficiente.

### Actividad - Variables globales

Antes que nada, borramos la linea que habíamos incluido para imprimir en la consola.

Vamos a declarar estas variables en las primeras lineas del archivo:

```jsx
let intentos = 6;
let palabra = "APPLE";
```

- El jugador podrá intentar adivinar la palabra 6 veces. La variable intento almacenara la cantidad de intentos restantes que tenemos.
- La variable palabra, almacena la palabra que tenemos que adivinar. Inicialmente guardamos una sola palabra, pero mas adelante podemos complicar el código para elegir una palabra al azar.

---

Podemos seguir escribiendo el código debajo de las lineas que agregamos, pero lo que vamos a hacer es usar un evento, para ejecutar nuestro algoritmo cuando se carga nuestra pagina web.

Un evento en JavaScript es una acción que ocurre en la página web, como hacer clic en un botón o mover el mouse. Los eventos son detectados por el navegador y desencadenan una función de JavaScript que se ejecuta en respuesta al evento. Las funciones de evento se utilizan a menudo para hacer que la página web sea más interactiva y permitir que los usuarios interactúen con la página de formas específicas.

### Actividad - Evento `'load'`

Vamos a agregar la siguiente linea debajo de las variables que declaramos:

```jsx
window.addEventListener('load', init)
```

Esto que agregamos es un “Event Listener”, que es un mecanismo que permite detectar cuando ocurre un evento en una página web. Cuando se detecta un evento, se llama a una función que se encarga de manejarlo.

En este caso, estamos agregando el event listener al objeto `window`.

El objeto `window` es un objeto global en JavaScript que representa la ventana del navegador. Proporciona métodos y propiedades para interactuar con la ventana actual, como cambiar la URL de la página, abrir nuevas ventanas y establecer temporizadores. También proporciona un acceso seguro a los objetos globales del navegador, como `document` y `console`. El objeto `window` es un objeto de nivel superior y todas las variables y funciones globales se definen en él.

El event listener toma dos argumentos:

- `'load'`: Es el nombre del evento. En este caso el evento se dispara cuando se carga completamente la pagina web.
- `init`: El segundo argumento es el nombre de la función que se va a disparar cuando se dispara el evento. En este caso, una función llamada `init`, que todavía no implementamos.

Utilizamos este evento para asegurarnos de que el código en el archivo `script.js` se ejecute después de que se haya cargado la página web.

Ahora podemos verificar que el evento este funcionando, implementando la función `init`:

```jsx
function init(){
    console.log('Esto se ejecuta solo cuando se carga la pagina web')
}
```
---

# Evento “click”

El usuario va a escribir una palabra en el `<input>`, vamos a hacer un intento presionando el botón `Intentar`. Entonces, lo que nos falta es una forma de detectar cuando el usuario presiona el botón.

El evento "click" se dispara cuando un elemento HTML es presionado con el mouse. Podemos agregar un event listener para detectar cuando el botón de "Intentar" es presionado y llamar a la función "intentar".

### Actividad - Evento `'click'`

Primero necesitamos encontrar el elemento en cuestión:

```jsx
const button = document.getElementById("guess-button");
```

Ahora, podemos agregar el evento a este elemento:

```jsx
button.addEventListener("click", intentar);
```

En este caso, estamos agregando el event listener al botón. usando su ID "guess-button". Cuando el botón es presionado, la función "intentar" se ejecuta.

Recuerda que la función "intentar" debe ser definida antes de agregar el event listener:

```jsx
function intentar(){
    console.log("Intento!")
}
```
---

# Leer intentos - Separación de responsabilidades

Dentro de la función intentar, tenemos que leer la palabra que el usuario quiere probar. Para esto vamos a acceder al valor del elemento `<input>`.

Podemos acceder al valor ingresado utilizando el método `value` del elemento. Por ejemplo, si tenemos un input con el id "guess-input", podemos acceder a su valor de la siguiente manera:

```jsx
const input = document.getElementById("guess-input");
const valor = input.value;
```

El valor ingresado por el usuario se almacenará en la variable `valor`.

### Actividad - Leer `<input>`

Vamos a modificar la función `intentar()` para que obtenga el valor ingresado:

```jsx
function intentar(){
    const INTENTO = leerIntento();
    console.log(INTENTO)
}
```

Obtenemos el valor desde otra función: `leerIntento()`. 

La separación de responsabilidades es un patrón de diseño en el desarrollo de software que consiste en dividir un programa en módulos o componentes que tienen una única responsabilidad. Cada módulo o componente se encarga de una tarea específica y no tiene conocimiento de las tareas que realizan los demás componentes. Esto permite una mayor escalabilidad y mantenibilidad del código.

Esto es lo que hacemos al pasar la lógica de leer el valor ingresado a otra función, que se encarga solo de eso:

```jsx
function leerIntento(){
    let intento = document.getElementById("guess-input");
    intento = intento.value;
    intento = intento.toUpperCase(); 
    return intento;
}
```
---

# El algoritmo

Ahora que ya tenemos el valor que el usuario ingreso, podemos concentrarnos en el algoritmo que vamos a aplicar para procesar el intento.

### Actividad - Algoritmo

Pueden existir muchas formas de resolver este problema, y por lo tanto muchos posibles algoritmos.

Para desarrollar un algoritmo, piensa en los pasos que vas a seguir para resolver el problema.

Ya tenes el intento, ahora tenes que determinar si el usuario gano, si se equivocó, y si las posiciones de las letras están bien.

Podemos ir pensando de esta manera:

1. Obtener la palabra de alguna lista (ahora tenemos una palabra fija para empezar).
2. Pedirle al usuario que escriba una palabra de 5 letras. (por el momento no estamos validando que sea de 5 letras).
3. Procesar intento:
    1. Si coincide con `palabra` → Usuario gana.
    2. Si no, iteramos sobre `palabra`, y por cada letra:
        1. Si la letra de `palabra` coincide con la letra en esa posición de `intento`, marcamos en verde.
        2. Si no coinciden, pero en `palabra` existe la letra, marcamos en amarillo.
        3. Las letras que no existen marcamos en gris.
    3. Si llegamos a este punto, es porque la palabra es incorrecta, asi que descontamos un intento.
    4. Si ya no nos quedan intentos, el usuario pierde, y deshabilitamos el input y el botón.

Esta es una version a “alto nivel”, o con menos detalles, pero podemos ir refinando el algoritmo para agregar mas detalle sobre como implementaríamos cada parte paso a paso.

---

# Procesamos los intentos

Según nuestro algoritmo, el siguiente paso es iterar sobre la variable `palabra`, que es la palabra que debemos adivinar, e identificar si ganamos. Por cada letra de la palabra, debemos comparar con la letra correspondiente del intento.

Recordemos, Iterar es un término utilizado en programación para describir la acción de repetir un proceso o conjunto de instrucciones varias veces. En este caso, queremos ejecutar una serie de instrucciones para cada letra.

Para hacer eso podemos usar un ciclo `for..in` para iterar sobre la variable `palabra`. Esta es una forma simplificada de iterar sobre las propiedades de un objeto:

```jsx
for (let i in palabra){
	console.log(palabra[i]);
}
```

En este caso, estamos iterando sobre los índices de la cadena `palabra`. La variable `i` tomará el valor de cada índice en sucesión, y podemos usar ese valor para acceder a la letra correspondiente en la cadena `palabra`. Por ejemplo, si `palabra` es "APPLE", entonces en la primera iteración `i` será 0 y `palabra[i]` será "A". Podemos usar esta letra para compararla con la letra correspondiente en la cadena `intento`.

### Actividad - Bucle `for...in`

Vamos a volver a modificar la función `intentar()` para incorporar el ciclo `for...in`:

```jsx
function intentar(){
    const INTENTO = leerIntento();
    if (INTENTO === palabra ) {
        console.log("GANASTE!")
        return
    }
    for (let i in palabra){
        if (INTENTO[i]===palabra[i]){
            console.log(INTENTO[i], "VERDE")
        } else if( palabra.includes(INTENTO[i]) ) {
            console.log(INTENTO[i], "AMARILLO")
        } else {
            console.log(INTENTO[i], "GRIS")
        }
    }
		intentos--
    if (intentos==0){
        console.log("PERDISTE!")
    }
}
```

Por el momento, solo estamos imprimiendo mensajes en la consola, pero analicemos este código linea por linea.

Lo primero que hacemos es verificar si el intento es la palabra correcta, en ese caso el usuario gana.

Si se cumple esta primera condición, hacemos `return`. Esto evita que el resto de la función se ejecute cuando no es necesario.

Seguidamente, implementamos el bucle para iterar sobre `palabra`.

Por cada letra hacemos tres comparaciones:

1. `INTENTO[i]===palabra[i]`: esto significa que la letra del intento es igual que la letra de la palabra, por ejemplo, si la palabra es “APPLE” y el intento es “ANGEL”. En este caso debemos indicar la letra con el color verde.
2. `palabra.includes(INTENTO[i])`: Si la letra del intento no coincide con la correspondiente en `palabra`, verificamos si la letra existe en `palabra` pero esta mal posicionada. Si la palabra es “APPLE” y el intento es “ANGEL”, la E del Angel debe mostrarse en amarillo.
3. Si no se cumple ninguna de esas condiciones, es porque la letra del intento no existe en la palabra. Esto se debe mostrar de color gris.

Al terminar el ciclo, restamos 1 de la variable `intentos`, y si llegamos a 0, el usuario pierde.

---

Con esto, ya tenemos un juego básico funcionando! Aunque tengamos que jugar mirando la consola.

### Actividad - Inyectar HTML

Lo siguiente que podemos hacer es mostrar mejores mensajes cuando el usuario gana o pierde. Para esto vamos a volver a modificar la función `intentar()` de la siguiente manera:

```jsx
if (INTENTO === palabra ) {
        terminar("<h1>GANASTE!😀</h1>")
        return
    }
```

```jsx
if (intentos==0){
        terminar("<h1>PERDISTE!😖</h1>")
    }
```

En vez de imprimir un mensaje en la consola, vamos a llamar a una nueva función que va a mostrar en pantalla el contenido que queramos. En este caso mensajes encapsulados en un `<h1>`.

Ahora, la función `terminar():`

```javascript
function terminar(mensaje){
    const INPUT = document.getElementById("guess-input");
    INPUT.disabled = true;
    BOTON.disabled = true;
    let contenedor = document.getElementById('guesses');
    contenedor.innerHTML = mensaje;
}
```

Antes que nada, deshabilitamos los controles para terminar el juego.

Luego, obtenemos en elemento `'guesses'`, e insertamos dentro el mensaje. Esto hará que se muestre en pantalla.

# Grilla de letras

El siguiente paso sera ir mostrando las letras ingresadas con cuadros de colores indicando si son correctas o no.

Para hacer eso, podemos inyectar html dinámicamente. Similar a lo que hicimos con los mensajes anteriores.

Cada letra que vamos a mostrar estará encapsulada en un `<span>` con clase `letter`, que si nos fijamos en el CSS que copiamos, le da bordes y margenes.

Cada uno de esos `<span>` debe estar dentro de un `<div>`.

Lo que buscamos es algo asi:

```html
<div id='grid'>

<!-- PRIMER INTENTO -->
	<div class='row'>
		<span class='letter'> A </span>
		<span class='letter'> N </span>
		<span class='letter'> G </span>
		<span class='letter'> E </span>
		<span class='letter'> L </span>
	</div>

<!-- SEGUNDO INTENTO -->
	<div class='row'>
		<span class='letter'> A </span>
		<span class='letter'> P </span>
		<span class='letter'> P </span>
		<span class='letter'> L </span>
		<span class='letter'> E </span>
	</div>

</div>
```

Si nos fijamos en el CSS, tenemos una clase `'row'` que preparamos para que hayan margenes entre las letras.

Esto debería quedar asi:

![Untitled](images\grilla.png)

### Actividad - Inyección dinámica de HTML

Ahora tenemos que implementar esta grilla de letras.

Para hacer esto, podemos pensar en filas y columnas. Cada letra sera una columna, y cada intento sera una fila.

Hagamos un pseudocódigo simple para ir entendiendo lo que pasa. Primero, obtenemos el `<div>` en el que vamos a armar la grilla, este esta en el HTML con el ID “grid”:

```jsx
const GRID = document.getElementById("grid");
```

Luego, creamos un div nuevo para nuestra fila, y le ponemos la clase `'row'`:

```jsx
const ROW = document.createElement('div');
ROW.className = 'row';
```

{: .concept }
Hay que entender que este elemento todavía no se encuentra en el DOM. Por el momento, esta en la constante ROW.

Ahora, tenemos que agregar las letras dentro de elementos `<span>`, y para eso, tenemos que iterar sobre `palabra`. Ya tenemos un bucle implementado para hacer esta iteración, asi que podríamos aprovecharlo. Modificamos asi la función `intentar()`:

```jsx
const GRID = document.getElementById("grid");
    const ROW = document.createElement('div');
    ROW.className = 'row';
    for (let i in palabra){
        const SPAN = document.createElement('span');
        SPAN.className = 'letter';
        if (INTENTO[i]===palabra[i]){ //VERDE
            SPAN.innerHTML = INTENTO[i];
            SPAN.style.backgroundColor = 'green';
        } else if( palabra.includes(INTENTO[i]) ) { //AMARILLO
            SPAN.innerHTML = INTENTO[i];
            SPAN.style.backgroundColor = 'yellow';
        } else {      //GRIS
            SPAN.innerHTML = INTENTO[i];
            SPAN.style.backgroundColor = 'grey';
        }
        ROW.appendChild(SPAN)
    }
    GRID.appendChild(ROW)
```

Podemos mejorar un poco los colores. Cambia los colores por defecto que pusimos por estos:

- Verde: `'#79b851’`
- Amarillo: `'#f3c237’`
- Gris: `'#a4aec4'`

También podes poner los colores que quieras, y mejorar un poco los estilos en el CSS. Una recomendación es cambiar el color de los bordes (o eliminarlos) y redondear los cuadros de las letras.

Y listo! con esto ya tenemos el juego funcionando.

---

# Selección de palabras - random()

Lo que le esta faltando al juego es una mejor selección de palabras. Ahora solo selecciona APPLE como palabra a adivinar.

Para hacer esto, podemos armar un diccionario en un array que contenga la lista de palabras que podemos seleccionar:

```jsx
let diccionario = ['APPLE', 'HURLS', 'WINGS', 'YOUTH']
```

Los índices del array `diccionario` son números enteros que empiezan en 0 y terminan en la cantidad de elementos del array menos 1. Es decir, si `diccionario` tiene 4 elementos, entonces sus índices van desde 0 hasta 3.

- 0: APPLE
- 1: HURLS
- 2: WINGS
- 3: YOUTH

Ahora, queremos guardar en la variable `palabra` uno de los elementos del diccionario, pero cual?

Para resolver esto podemos usar la función `random()` de javascript.

`random()` es una función del objeto `Math` de JavaScript que devuelve un número aleatorio entre 0 y 1. Para obtener un número aleatorio dentro de un rango específico, podemos utilizar una fórmula como esta:

```jsx
Math.floor(Math.random() * (max - min + 1)) + min;
```

Por ejemplo, si quisiéramos obtener un número aleatorio entre 1 y 10, podríamos usar esta fórmula:

```jsx
Math.floor(Math.random() * 10) + 1;
```

Esto nos daría un número entero aleatorio entre 1 y 10. Podemos utilizar este número para seleccionar un elemento aleatorio del array `diccionario`, de la siguiente manera:

```jsx
const palabra = diccionario[Math.floor(Math.random() * diccionario.length)];
```

Con esto, la variable `palabra` contendrá una palabra aleatoria del diccionario.

### Actividad - `random()`

Implementa estos cambios al juego por tu cuenta, para poder seleccionar palabras de una lista mas larga.

![Untitled](images\complete.png)
