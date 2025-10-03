# 3.2.3 Array (III): Métodos de búsqueda y ordenación

Además de recorrer y transformar arrays, JavaScript proporciona métodos para **buscar elementos** y **ordenar datos** de manera eficiente.

---

## 📌 Métodos de búsqueda

### indexOf() y lastIndexOf()

* `indexOf(valor)` devuelve la **primera posición** en la que aparece un valor (o `-1` si no existe).
* `lastIndexOf(valor)` devuelve la **última posición**.

```js
let frutas = ["manzana", "pera", "naranja", "pera"];

console.log(frutas.indexOf("pera"));     // 1
console.log(frutas.lastIndexOf("pera")); // 3
console.log(frutas.indexOf("kiwi"));     // -1
```

### includes()

Comprueba si un array contiene un valor.

```js
let numeros = [10, 20, 30];

console.log(numeros.includes(20)); // true
console.log(numeros.includes(40)); // false
```

### find() y findIndex()

* `find()` devuelve el **primer elemento** que cumple una condición.
* `findIndex()` devuelve la **posición** de ese elemento.

```js
let numeros = [5, 12, 8, 130, 44];

console.log(numeros.find(n => n > 10));      // 12
console.log(numeros.findIndex(n => n > 10)); // 1
```

### some() y every()

* `some()` devuelve `true` si **algún elemento** cumple la condición.
* `every()` devuelve `true` si **todos los elementos** cumplen la condición.

```js
let numeros = [2, 4, 6, 8];

console.log(numeros.some(n => n > 5));         // true
console.log(numeros.every(n => n % 2 === 0));  // true
```

---

## 📌 Métodos de ordenación

### sort()

Ordena los elementos de un array.
Por defecto, ordena como **strings**, lo que puede dar resultados inesperados.

```js
let letras = ["d", "a", "c", "b"];
console.log(letras.sort()); // ["a", "b", "c", "d"]

let numeros = [10, 2, 30, 1];
// ¡Ojo! Los ordena como strings
console.log(numeros.sort()); // [1, 10, 2, 30]

// Orden numérico correcto
console.log(numeros.sort((a, b) => a - b)); // [1, 2, 10, 30]
```

!!! warning "Cuidado con sort()"
    Si no proporcionas una función de comparación, `sort()` convierte los elementos a **texto** y los ordena alfabéticamente.
    Por eso, al ordenar números, es recomendable siempre dar una función `(a, b) => a - b`.

### reverse()

Invierte el orden de los elementos de un array.

```js
let numeros = [1, 2, 3, 4, 5];
console.log(numeros.reverse()); // [5, 4, 3, 2, 1]
```

---


## 📌 Inciso sobre sort()

El método `sort()` **convierte los elementos a cadenas de texto** antes de ordenarlos, lo que provoca que los números no siempre se ordenen como esperarías.

### Ejemplo con números

```js
let numeros = [2, 100, 15, 7];

// Ordena como si fueran strings
console.log(numeros.sort()); 
// [100, 15, 2, 7]

// Orden correcto con función de comparación
console.log(numeros.sort((a, b) => a - b)); 
// [2, 7, 15, 100]
```

!!! info "Por qué ocurre esto"
    `sort()` sin función compara los valores **como texto**, siguiendo el orden Unicode.
    Por eso `"100"` se coloca antes que `"2"`, igual que en un diccionario "c" va antes que "ca".

---

### Ejemplo con objetos

Si tenemos un array de objetos, también necesitamos una **función de comparación** para ordenar por alguna propiedad.

```js
let personas = [
  { nombre: "Laura", edad: 28 },
  { nombre: "Ana", edad: 22 },
  { nombre: "Pedro", edad: 35 }
];

// Ordenar por edad (de menor a mayor)
console.log(personas.sort((a, b) => a.edad - b.edad));
/*
[
  { nombre: "Ana", edad: 22 },
  { nombre: "Laura", edad: 28 },
  { nombre: "Pedro", edad: 35 }
]*/

// Ordenar por nombre (alfabéticamente)
console.log(personas.sort((a, b) => a.nombre.localeCompare(b.nombre)));
/*
[
  { nombre: "Ana", edad: 22 },
  { nombre: "Laura", edad: 28 },
  { nombre: "Pedro", edad: 35 }
]
*/
```

!!! tip "Consejo"
    Cuando trabajes con arrays de objetos, piensa siempre **qué propiedad** quieres usar para ordenar y define una función de comparación adecuada.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre `find` y `filter`?
    2. ¿Qué método usarías para comprobar si todos los elementos de un array son mayores que 0?
    3. ¿Por qué `sort()` puede dar resultados extraños al ordenar números?
    4. ¿Cómo invertirías un array en JavaScript?
    5. Si tienes `["rojo","azul","verde"]`, ¿qué devuelve `indexOf("verde")`?
