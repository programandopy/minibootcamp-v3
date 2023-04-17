---
title: Eventos en JavaScript
has_children: false
parent: Proyecto Wordle PPY
nav_order: 1
---

# Eventos

Usualmente cuando creamos una aplicación para nuestro navegador creamos lo que se conoce como una "Interfaz Gráfica de Usuario" (GUI por sus siglas en inglés, Graphic User Interface) para interactuar con el usuario. De esta manera el usuario puede comunicarse con nuestro programa a través de "clicks" en diferentes elementos de nuestro programa o ingresando texto, por ejemplo.

Es así que nuestro principal desafío al programar es controlar esas acciones que realiza el usuario, y poder planear una respuesta para ellas, sin poder saber cuando van a suceder. Como aprendimos en lecciones anteriores, nuestra manera de crear respuesta por parte de nuestro programa es utilizando funciones pero para que nuestras funciones estén relacionadas a una acción determinada del usuario (click en un botón, escribir texto, etc.) necesitamos un nuevo componente que se conoce como "event listeners" que no son otra cosa que funciones que se dedican a escuchar las acciones posibles y una vez que estas ocurren ejecutar una respuesta. Podemos agregar un event listener usando el código **addEventListener** y asignando una función a ejecutarse.

---

# Eventos comunes

Existen [muchos eventos](https://developer.mozilla.org/es/docs/Web/Events){:target="_blank"} disponibles para escuchar al crear una aplicación. Básicamente, todo lo que hace un usuario en una página genera un evento, lo que nos da, como desarrollador, mucho control para asegurar que el usuario obtenga la experiencia que deseamos. Por suerte, normalmente solo vamos a usar unos pocos eventos principales. Les compartimos una breve lista con algunos de los más comunes (incluidos los dos que se necesitan al crear un juego en nuestra próxima lección):

- [clic](https://developer.mozilla.org/es/docs/Web/API/Element/click_event){:target="_blank"}: el usuario hizo clic en algo, generalmente un botón o hipervínculo
- [contextmenu](https://developer.mozilla.org/en-US/docs/Web/API/Element/contextmenu_event){:target="_blank"}: el usuario hizo clic derecho
- [select](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/select_event){:target="_blank"}: el usuario resaltó algún texto
- [input](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/input_event){:target="_blank"}: el usuario ingresó algún texto

**TIP:** Vale la pena señalar que hay varias formas de crear detectores de eventos. Se puede usar funciones anónimas o crear funciones con nombre, también se puede configurar la propiedad "clic" o usar "addEventListener". En esta lección vamos a manejar "addEventLister" y funciones anónimas, ya que es probablemente la técnica más común utilizada por los desarrolladores web. También es el método más flexible porque "addEventListener" funciona para todos los eventos y el nombre del evento se puede agregar como parámetro.
