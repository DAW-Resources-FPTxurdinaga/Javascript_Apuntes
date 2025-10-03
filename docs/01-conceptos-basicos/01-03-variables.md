# 1.3. Variables en JavaScript

Las variables son la base de cualquier programa. En esta lección aprenderás a **declararlas**, **entender su ámbito** y comprender conceptos clave como el **hoisting** y el uso de `"use strict"`.

---

## 📌 Declaración de variables

En JavaScript existen tres formas principales de declarar variables:

```js
var nombre = "Ana";
let edad = 25;
const PI = 3.1416;
```

* **`var`**: forma antigua de declarar variables. Tiene **ámbito de función** y permite redeclaración. Hoy en día se desaconseja.
* **`let`**: forma moderna, con **ámbito de bloque**. Es la opción recomendada para variables que cambian.
* **`const`**: igual que `let`, pero no permite reasignación. Úsala para constantes o referencias que no deban cambiar.

---

## 📌 Ámbito de las variables

El **ámbito** determina desde dónde puede accederse a una variable:

* **Global**: accesible en todo el programa.
* **Función**: declarada dentro de una función.
* **Bloque**: declarada dentro de llaves `{ }`, como en un `if` o un `for`.

```js
if (true) {
  let x = 10;   // solo dentro de este bloque
  var y = 20;   // accesible fuera también
}
console.log(y); // 👉 20
console.log(x); // ❌ Error
```

---

## 📌 Hoisting

El **hoisting** significa que JavaScript **eleva las declaraciones al inicio del ámbito** antes de ejecutar el código.

* Con `var`, la variable se inicializa como `undefined`:

```js
console.log(a); // 👉 undefined
var a = 5;
```

* Con `let` y `const`, la variable existe pero está en la **Zona Muerta Temporal (TDZ)** hasta que se declara:

```js
console.log(b); // ❌ ReferenceError
let b = 10;
```

!!! tip "Recuerda"
    El *hoisting* no mueve físicamente tu código: simplemente el motor de JavaScript **reserva memoria para las declaraciones antes de ejecutar**.

---

## 📌 `"use strict"`

El modo estricto introduce reglas más seguras en JavaScript:

```js
"use strict";
x = 10; // ❌ Error: variable no declarada
```

* Evita errores comunes (como usar variables sin declarar).
* Restringe ciertas acciones inseguras.
* Desde **ES6**, los **módulos y clases ya usan `strict mode` por defecto**.

!!! info "Información"
    Hoy en día **no es necesario añadir `"use strict"` manualmente** en proyectos modernos, pero sigue siendo útil para entender cómo mejoró la seguridad del lenguaje a partir de ES5.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Cuál es la diferencia entre `let` y `const`?
    2. ¿Qué ocurre si usas `var` dentro de un bloque como un `if`?
    3. ¿Por qué `console.log(a)` devuelve `undefined` si `a` se declaró con `var` más abajo?
    4. ¿Qué significa que una variable esté en la *Zona Muerta Temporal*?
  