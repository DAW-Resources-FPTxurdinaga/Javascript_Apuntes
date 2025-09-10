# 1.1. Características de JavaScript

Esta es la primera lección del curso de **JavaScript moderno**, donde vamos a repasar las **características esenciales del lenguaje** y las mejoras que trajo la versión **ES6** respecto a versiones anteriores como **ES5**.

---

## 📌 ¿Qué tipo de lenguaje es JavaScript?

JavaScript es un lenguaje de programación muy extendido en el desarrollo web, especialmente en el **entorno cliente**, aunque también puede ejecutarse en el **servidor** gracias a entornos como Node.js.

### Lenguaje del lado del cliente (cliente-side)

JavaScript se ejecuta, por defecto, **en el navegador del usuario**, lo que permite crear **páginas interactivas** sin necesidad de recargar el sitio.

### Interpretado (aunque...)

Tradicionalmente se ha dicho que es un **lenguaje interpretado**, ya que el navegador lo ejecuta directamente sin necesidad de compilar previamente.  
No obstante, los motores modernos (como V8 de Chrome) **compilan JIT (just in time)** para mejorar el rendimiento.  

### Imperativo y estructurado

JavaScript sigue el paradigma imperativo, lo que significa que describes **cómo debe hacerse algo paso a paso**.  
Permite escribir código estructurado con funciones, bloques, condiciones y bucles.

### Tipado débil y dinámico

Las variables no declaran su tipo explícitamente.  
Además, **pueden cambiar de tipo en tiempo de ejecución**, lo que hace que JavaScript sea flexible, pero también puede provocar errores inesperados si no se tiene cuidado.

```js
let x = 5;     // tipo número
x = "hola";    // ahora es string
```

### Basado en objetos y prototipos

JavaScript no usa clases tradicionales como en Java o C++, sino que se basa en un sistema de **prototipos** para la herencia y reutilización de código.
Desde **ES6**, sin embargo, se introdujo una **sintaxis de clases**, aunque sigue funcionando con prototipos por debajo.

### Orientado a objetos

Puedes crear objetos, asignarles propiedades y métodos, y estructurar el código de forma modular.
La orientación a objetos en JavaScript es **menos rígida** que en otros lenguajes y muy flexible.

---

## 📌 ¿Y qué es ECMAScript?

ECMAScript es el **estándar que define el lenguaje JavaScript**.
El organismo encargado de mantenerlo es **ECMA International**, y se actualiza cada año desde 2015.

Las versiones más importantes son:

* **ES5 (2009)**: amplió la compatibilidad y estabilidad en navegadores.
* **ES6 (2015)**: revolución del lenguaje. Introdujo `let`, `const`, funciones flecha, clases, `Promise`, `Map`, `Set`, etc.
* **ES2022–ES2024**: siguen añadiendo mejoras como `top-level await`, `private fields`, `Array.prototype.at()` y más.

!!! info "Compatibilidad de versiones"
    Las versiones de JavaScript **ES5 y ES6+ son compatibles entre sí**.
    Pero como dice el refrán: **"No mezcles churras con merinas"**.
    Es recomendable usar un estilo coherente y moderno, basado en **ES6+**.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Dónde se ejecuta normalmente JavaScript: en el cliente o en el servidor?
    2. Si declaras `let x = 5;` y después haces `x = "hola";`, ¿qué ocurre con el tipo de la variable?
    3. ¿Qué ventaja tiene la compilación JIT en los navegadores modernos?
    4. ¿Qué estándar define el lenguaje JavaScript?
    5. ¿Cuál es la versión que introdujo `let`, `const` y las funciones flecha?

