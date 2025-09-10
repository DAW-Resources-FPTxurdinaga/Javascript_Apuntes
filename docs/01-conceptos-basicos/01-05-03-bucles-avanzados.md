# 1.5.3. Bucles avanzados con objetos y arrays

Además de los bucles tradicionales (`for`, `while`, `do...while`), JavaScript ofrece estructuras especiales para trabajar con **arrays** y **objetos**.  
Estos bucles hacen el código más **legible** y **moderno**.

---

## 📌 Bucle `for...in`

El bucle `for...in` se utiliza para **recorrer las propiedades enumerables de un objeto**.

```js
const persona = {
  nombre: "Laura",
  nif: 12345678A,
  ciudad: "Zamora"
};

for (let clave in persona) {
  console.log(`${clave}: ${persona[clave]}`);
}
```

Salida:

```
nombre: Laura
edad: 12345678A
ciudad: Zamora
```

!!! warning "Cuidado con `for...in`"
    `for...in` no está pensado para recorrer arrays, ya que puede incluir propiedades añadidas al prototipo.

---

## 📌 Bucle `for...of`

El bucle `for...of` se introdujo en **ES6** y se usa para **recorrer elementos de arrays, strings, Maps, Sets y otros iterables**.

```js
const frutas = ["manzana", "pera", "plátano"];

for (let fruta of frutas) {
  console.log(fruta);
}
```

Salida:

```
manzana
pera
plátano
```

---

## 📌 Métodos modernos para arrays

Los arrays en JavaScript tienen métodos especiales que reemplazan muchos usos de bucles tradicionales que veremos en lecciones posteriores.

### forEach

Ejecuta una función para cada elemento.

```js
const numeros = [1, 2, 3];

numeros.forEach(n => console.log(n * 2));
// 2, 4, 6
```

### map

Crea un **nuevo array** aplicando una función a cada elemento.

```js
const dobles = numeros.map(n => n * 2);
console.log(dobles); // [2, 4, 6]
```

### filter

Crea un **nuevo array** con los elementos que cumplen una condición.

```js
const pares = numeros.filter(n => n % 2 === 0);
console.log(pares); // [2]
```

### reduce

Reduce los elementos a un único valor (por ejemplo, una suma).

```js
const suma = numeros.reduce((acum, n) => acum + n, 0);
console.log(suma); // 6
```

!!! tip "Bucles modernos"
    Siempre que trabajes con arrays, considera usar `map`, `filter`, `reduce` o `forEach`.
    El código suele ser más legible y expresivo que con `for` tradicional.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre `for...in` y `for...of`?
    2. ¿Por qué no es recomendable usar `for...in` con arrays?
    3. Escribe un ejemplo con `for...of` que recorra un string y muestre cada carácter.
    4. ¿Qué método de arrays usarías para obtener solo los números mayores que 10 de un array?
    5. ¿Qué devuelve el método `map` frente a `forEach`?

