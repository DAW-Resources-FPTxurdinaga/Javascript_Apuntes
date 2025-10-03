# 3.2.1 Array (I): Fundamentos

Los **arrays** en JavaScript son estructuras de datos que permiten almacenar varios valores en una sola variable.
Son muy útiles cuando queremos trabajar con listas de elementos (números, cadenas, objetos...).

---

## 📌 ¿Qué es un array?

Un **array** es una lista ordenada de elementos que se indexan comenzando desde **0**.
Cada valor dentro del array se llama **elemento**, y se accede a él mediante su índice.

```js
// Declaración de un array
let frutas = ["manzana", "plátano", "naranja"];

// Acceder al primer elemento
console.log(frutas[0]); // "manzana"

// Acceder al segundo elemento
console.log(frutas[1]); // "plátano"
```

---

## 📌 Longitud de un array

La propiedad `.length` devuelve el número total de elementos en el array.

```js
let frutas = ["manzana", "plátano", "naranja"];
console.log(frutas.length); // 3
```

---

## 📌 Arrays multidimensionales

Un array puede contener otros arrays en su interior, formando **arrays multidimensionales**.
Esto es útil, por ejemplo, para representar tablas.

```js
let tabla = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

console.log(tabla[0][1]); // 2 (primera fila, segunda columna)
```

---

## 📌 Métodos básicos para modificar arrays

Los arrays incluyen métodos muy usados para **añadir o eliminar elementos**.

```js
let numeros = [1, 2, 3];

// Añadir al final
numeros.push(4);
console.log(numeros); // [1, 2, 3, 4]

// Eliminar el último
numeros.pop();
console.log(numeros); // [1, 2, 3]

// Añadir al principio
numeros.unshift(0);
console.log(numeros); // [0, 1, 2, 3]

// Eliminar el primero
numeros.shift();
console.log(numeros); // [1, 2, 3]
```

---

!!! note "Diferencia entre arrays y objetos"
    Aunque los arrays son un tipo especial de objeto en JavaScript, están pensados para almacenar datos en **orden numérico** (índices).
    Los objetos, en cambio, almacenan **pares clave-valor**, lo que los hace más adecuados para datos con propiedades.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué índice tiene el primer elemento de un array en JavaScript?
    2. ¿Qué devuelve la propiedad `.length` de un array?
    3. ¿Cómo accederías al número `6` dentro del array bidimensional `[[1,2,3],[4,5,6]]`?
    4. ¿Qué método se usa para añadir un elemento al final de un array?
    5. ¿Qué método elimina el primer elemento de un array?