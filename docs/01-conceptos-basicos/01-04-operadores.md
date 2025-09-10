# 1.4. Operadores en JavaScript

En esta lección vamos a repasar los **principales operadores de JavaScript** que permiten trabajar con valores, expresiones y condiciones.  

---

## 📌 Tipos de operadores en JavaScript

### Operadores de asignación
Sirven para **dar valor a una variable**.  
El más común es `=`, pero también existen operadores compuestos:

```js
let x = 10;    // asignación
x += 5;        // equivalente a x = x + 5
x -= 2;        // equivalente a x = x - 2
````

---

### Operadores aritméticos

Permiten hacer operaciones matemáticas:

```js
let suma = 5 + 3;      // 8
let resta = 10 - 4;    // 6
let multi = 6 * 2;     // 12
let division = 15 / 3; // 5
let resto = 7 % 2;     // 1 (resto de la división)
let potencia = 2 ** 3; // 8
```

---

### Operadores lógicos

Se utilizan para **combinar condiciones**:

```js
let a = true;
let b = false;

console.log(a && b); // false (AND)
console.log(a || b); // true  (OR)
console.log(!a);     // false (NOT)
```

---

### Operadores de comparación

Sirven para comparar valores:

```js
5 == "5"   // true  (igualdad con conversión implícita)
5 === "5"  // false (igualdad estricta, también compara el tipo)
5 != 4     // true
5 !== "5"  // true
5 > 3      // true
5 <= 5     // true
```

!!! info "Conversión implícita de tipos"
    En JavaScript, el operador `==` intenta **convertir los valores a un mismo tipo** antes de compararlos.
    Por eso `5 == "5"` devuelve `true`, porque el string `"5"` se convierte a número automáticamente.
    Esto puede causar resultados inesperados, como:
    ```js
        0 == false   // true
        "" == false  // true
        null == undefined // true
        ```
    Por este motivo se recomienda usar siempre **`===` y `!==`**, que comparan tanto el valor como el tipo.

---

### Operador ternario

Permite escribir una condición en una sola línea:

```js
let edad = 18;
let mensaje = (edad >= 18) ? "Eres mayor de edad" : "Eres menor de edad";
console.log(mensaje); // "Eres mayor de edad"
```

Equivale a escribir:

```js
let mensaje;
if (edad >= 18) {
  mensaje = "Eres mayor de edad";
} else {
  mensaje = "Eres menor de edad";
}
```

---

### Operadores de cadena

Se utilizan para **trabajar con strings**:

```js
let nombre = "Laura";
let saludo = "Hola " + nombre;          // concatenación clásica
let saludo2 = `Hola ${nombre}, ¿qué tal?`; // plantilla literal con backticks
```

---

## 📌 Plantillas literales (template literals)

Las **plantillas literales** se escriben entre **backticks** (`` ` ``) y ofrecen más flexibilidad que las comillas simples o dobles.

### Ventajas principales:

1. **Interpolación de variables** con `${variable}`:

   ```js
   let nombre = "Laura";
   console.log(`Hola ${nombre}`); // Hola Laura
   ```

2. **Expresiones dentro de `${}`**:

   ```js
   let a = 5, b = 3;
   console.log(`La suma es ${a + b}`); // La suma es 8
   ```

3. **Texto multilínea sin necesidad de `\n`**:

   ```js
   let mensaje = `
   Línea 1
   Línea 2
   Línea 3
   `;
   console.log(mensaje);
   ```

---

## 📌 Operadores rest y spread (`...`)

El operador `...` en JavaScript puede funcionar de **dos formas diferentes** según el contexto:

---

### Spread (propagación)
Permite **expandir** un array o un objeto en sus elementos individuales.  
Es muy útil para copiar, combinar o pasar elementos como argumentos de una función.

```js
// Ejemplo con arrays
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];

console.log(arr2); // [1, 2, 3, 4, 5]

// Ejemplo con objetos
const persona = { nombre: "Laura", edad: 30 };
const copia = { ...persona, profesion: "Desarrolladora" };

console.log(copia); // { nombre: "Laura", edad: 30, profesion: "Desarrolladora" }

```

### Rest (agrupación)

Permite **agrupar** múltiples elementos en un array dentro de funciones o estructuras de datos.
Se usa normalmente en la definición de funciones para recibir un número indefinido de argumentos.

```js
// Ejemplo en funciones
function sumar(...numeros) {
  return numeros.reduce((a, b) => a + b, 0);
}

console.log(sumar(1, 2, 3, 4)); // 10

// Ejemplo con destructuring
const [primero, ...resto] = [10, 20, 30, 40];
console.log(primero); // 10
console.log(resto);   // [20, 30, 40]
```

---

!!! tip "Recuerda"
    **Spread** → "expande" elementos.

    **Rest** → "agrupa" elementos.

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué operador devuelve el resto de una división?
    2. ¿Por qué es más seguro usar `===` en lugar de `==`?
    3. ¿A qué equivale el operador ternario en su forma larga con `if` y `else`?
    4. ¿Cómo escribirías una plantilla literal que muestre un cálculo dentro de `${}`?
    5. ¿Qué ventaja tienen las plantillas literales frente a la concatenación clásica con `+`?