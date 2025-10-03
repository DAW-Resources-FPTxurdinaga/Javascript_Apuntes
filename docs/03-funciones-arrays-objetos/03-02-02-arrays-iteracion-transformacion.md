# 3.2.2 Array (II): Iteración y transformación

Además de almacenar datos, los arrays en JavaScript ofrecen muchos métodos para **recorrerlos** y **transformarlos**.
Estos métodos son fundamentales para trabajar de forma moderna y clara con colecciones de datos.

---

## 📌 Recorrer un array con bucles tradicionales

Puedes recorrer un array con los bucles que ya conoces (`for`, `for...of`, etc.).

```js
let frutas = ["manzana", "plátano", "naranja"];

// Con un for clásico
for (let i = 0; i < frutas.length; i++) {
  console.log(frutas[i]);
}

// Con for...of
for (let fruta of frutas) {
  console.log(fruta);
}
```
## 📌 Otros métodos de iteración y transformación

### forEach()

El método `.forEach()` ejecuta una función para **cada elemento** del array.

```js
let numeros = [1, 2, 3, 4];

numeros.forEach((n) => {
  console.log(n * 2);
});
// 2, 4, 6, 8
```


### map()

El método `.map()` crea un **nuevo array** aplicando una función a cada elemento.

```js
let numeros = [1, 2, 3, 4];

// Crear un nuevo array con los números al cuadrado
let cuadrados = numeros.map((n) => n * n);

console.log(cuadrados); // [1, 4, 9, 16]
```


### filter()

El método `.filter()` devuelve un **nuevo array** con los elementos que cumplen una condición.

```js
let numeros = [1, 2, 3, 4, 5, 6];

// Filtrar los pares
let pares = numeros.filter((n) => n % 2 === 0);

console.log(pares); // [2, 4, 6]
```


### reduce()

El método `.reduce()` acumula los valores del array en un único resultado.

```js
let numeros = [1, 2, 3, 4];

// Sumar todos los números
let suma = numeros.reduce((acumulador, actual) => acumulador + actual, 0);

console.log(suma); // 10
```

---

!!! info "Elegir el método adecuado"
    - Usa **forEach** cuando solo quieras ejecutar algo para cada elemento.
    - Usa **map** si necesitas **transformar** el array en otro.
    - Usa **filter** si quieres **seleccionar** algunos elementos.
    - Usa **reduce** si necesitas **un único valor** como suma, producto o concatenación.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre `forEach` y `map`?
    2. ¿Qué devuelve el método `filter`?
    3. ¿Qué valor inicial puede recibir `reduce` como segundo argumento?
    4. Si tienes `[1,2,3,4,5]`, ¿cómo obtendrías solo los números mayores que 3 usando `filter`?
    5. ¿Qué método usarías para calcular la multiplicación de todos los números de un array?
