---
title: Qué es Programación
has_children: false
parent: Introducción a la programación
nav_order: 1
---

# ¿Qué es programación?

La programación es el proceso de escribir instrucciones para una computadora. Las instrucciones se escriben en un lenguaje de programación, que luego es interpretado por el computador. Estos conjuntos de instrucciones pueden recibir varios nombres:  programa, programa de computadora, aplicación (app), ejecutable, etc. 


Un programa puede ser cualquier cosa que esté escrita con código; los sitios web, los juegos y las aplicaciones móviles son programas. 

✅ Busca en google: ¿quién fue el primer programador/a informático del mundo?

---
# ¿Qué es lenguaje de programación?
Todo lo que hacemos en un computador o teléfono inteligente tiene algún tipo de código indicándole qué tiene que hacer. 

Pero, alguna vez te preguntaste, cómo está escrito? Así como hay miles de idiomas en el mundo en el mundo digital hay muchos lenguajes de programación, y son estos los que hacen funcionar gran parte de la tecnología que usamos hoy en día. 

Así como los idiomas son el mecanismo mediante el cual nos comunicamos entre humanos, los lenguajes de programación son el vehículo para la comunicación entre humanos y computadoras.

{: .important }
Un lenguaje de programación es un sistema estructurado de instrucciones, el cual está conformado por conjuntos de símbolos, palabras claves, reglas semánticas y sintácticas que permiten el entendimiento entre un programador y una máquina. Básicamente, lo que nos ofrece un lenguaje de programación es la posibilidad de darle instrucciones a la computadora y hacer cosas con ella.

Los lenguajes de programación vienen en diferentes formatos y pueden servir para diferentes propósitos. Por ejemplo, JavaScript se usa principalmente para aplicaciones web, mientras que Bash se usa principalmente para sistemas operativos.

Los Lenguajes de **bajo nivel** generalmente requieren menos pasos que los de **alto nivel** para que un dispositivo interprete las instrucciones. Sin embargo, lo que hace que los lenguajes de alto nivel sean populares es su legibilidad y compatibilidad. JavaScript se considera un lenguaje de alto nivel.

El siguiente código ilustra la diferencia entre un lenguaje de alto nivel con JavaScript y un lenguaje de bajo nivel con código ensamblador ARM.

```javascript
let number = 10
let n1 = 0, n2 = 1, nextTerm;

for (let i = 1; i <= number; i++) {
    console.log(n1);
    nextTerm = n1 + n2;
    n1 = n2;
    n2 = nextTerm;
}
```

```c
 area ascen,code,readonly
 entry
 code32
 adr r0,thumb+1
 bx r0
 code16
thumb
 mov r0,#00
 sub r0,r0,#01
 mov r1,#01
 mov r4,#10
 ldr r2,=0x40000000
back add r0,r1
 str r0,[r2]
 add r2,#04
 mov r3,r0
 mov r0,r1
 mov r1,r3
 sub r4,#01
 cmp r4,#00
 bne back
 end
```
✅ Observá la diferencia. Un lenguaje de programación de alto nivel expresa las instrucciones de forma mas entendible para los humanos.  
