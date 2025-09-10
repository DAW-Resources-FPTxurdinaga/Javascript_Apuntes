# 1.5.2. Bucles básicos en JavaScript

En programación muchas veces necesitamos **repetir tareas**.  
Los **bucles** permiten ejecutar un bloque de código varias veces, mientras se cumpla una condición.

---

## 📌 Bucle `for`

El bucle `for` es el más común cuando sabemos **cuántas veces** queremos repetir algo.  
Su estructura tiene tres partes: inicialización, condición y actualización.

```js
for (let i = 1; i <= 5; i++) {
  console.log(`Iteración número ${i}`);
}
```

En este ejemplo:

* `let i = 1`: inicializa la variable de control.
* `i <= 5`: condición que se evalúa en cada vuelta.
* `i++`: incrementa la variable en cada iteración.

---

## 📌 Bucle `while`

El bucle `while` repite un bloque de código **mientras la condición sea verdadera**.
Es útil cuando **no sabemos de antemano cuántas iteraciones habrá**.

```js
let contador = 0;

while (contador < 3) {
  console.log(`Contador: ${contador}`);
  contador++;
}
```

---

## 📌 Bucle `do...while`

El bucle `do...while` es similar al `while`, pero garantiza que el código **se ejecute al menos una vez**, aunque la condición sea falsa desde el principio.

```js
let numero = 5;

do {
  console.log(`El número es ${numero}`);
  numero++;
} while (numero < 3);
```

En este caso, aunque la condición es falsa desde el inicio, el bloque se ejecuta **una vez**.

!!! info "Diferencia clave"
    - `while`: primero evalúa la condición y luego ejecuta.
    - `do...while`: ejecuta primero y evalúa después.

---

## 📌 ¿Cuándo usar cada bucle?

* Usa `for` cuando conoces el número de iteraciones.
* Usa `while` cuando **desconoces cuántas veces** se repetirá, pero depende de una condición.
* Usa `do...while` cuando quieras que el bloque se ejecute **al menos una vez**.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia principal hay entre `while` y `do...while`?
    2. Escribe un bucle `for` que muestre los números del 10 al 1 en orden descendente.
    3. ¿Qué ocurriría si olvidas actualizar la variable de control en un bucle `while`?
    4. ¿En qué casos sería más adecuado usar `for` en lugar de `while`?