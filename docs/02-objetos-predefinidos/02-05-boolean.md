
# 2.5 Objeto Boolean

El objeto **Boolean** en JavaScript representa valores lógicos: **verdadero (`true`) o falso (`false`)**.
Se utiliza en estructuras de control como condicionales (`if`, `while`, etc.) y en comparaciones.

---

## 📌 Creación de valores booleanos

```js
// Forma literal (recomendada)
let esMayor = true;
let esMenor = false;

// Constructor Boolean (⚠️ evita usarlo, crea un objeto)
let b = new Boolean(true);

console.log(typeof esMayor); // "boolean"
console.log(typeof b);       // "object"
```

!!! warning "No uses `new Boolean()`"
    Si usas `new Boolean(false)`, el resultado es un **objeto** que siempre se evalúa como `true` en contextos lógicos.
    Ejemplo:
    `js
        if (new Boolean(false)) {
        console.log("Esto se ejecuta 😱");
        }
        `

---

## 📌 Conversión a booleano

Cualquier valor en JavaScript puede convertirse a un **booleano**.

```js
// Boolean() convierte de forma explícita
console.log(Boolean(1));       // true
console.log(Boolean(0));       // false
console.log(Boolean("hola"));  // true
console.log(Boolean(""));      // false
```

### Valores *truthy* y *falsy*

* **Falsy**: valores que se convierten a `false` son `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`

* **Truthy**: todos los demás valores (incluidos arrays y objetos vacíos).

```js
console.log(Boolean([]));  // true
console.log(Boolean({}));  // true
```

!!! note "Evaluación de truthy/falsy"
    Este mecanismo es muy usado en condicionales:

        `   let nombre = "";
            if (nombre) {
            console.log("Hay un nombre");
            } else {
            console.log("Cadena vacía → se evalúa como false");
            }
            `

---

## 📌 Operadores lógicos principales

```js
// AND lógico (&&) → true si ambos son verdaderos
console.log(true && false); // false

// OR lógico (||) → true si al menos uno es verdadero
console.log(true || false); // true

// NOT lógico (!) → invierte el valor
console.log(!true); // false
```

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre `true` y `new Boolean(true)`?
    2. Escribe dos ejemplos de valores *falsy*.
    3. ¿Qué valor devuelve `Boolean(" ")` (una cadena con un espacio)?
    4. ¿Cómo funciona el operador `&&` (AND lógico)?
    5. ¿Qué ocurre si evalúas un array vacío (`[]`) en un `if`?
