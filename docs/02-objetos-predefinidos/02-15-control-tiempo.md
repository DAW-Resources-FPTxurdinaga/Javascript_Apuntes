# 3.7 Control de tiempo en JavaScript

Los métodos para controlar el tiempo en JavaScript forman parte del objeto **`window`**, ya que dependen del navegador.
Con ellos podemos **programar la ejecución de funciones en el futuro**, ya sea una única vez (`setTimeout`) o de manera repetida (`setInterval`).
Ambos métodos devuelven un identificador que nos permite detener la ejecución con `clearTimeout` y `clearInterval`.

---

¿Quieres que actualice toda la lección con este nuevo arranque, o solo quieres añadir este bloque al principio y dejar lo demás igual?

---

## 📌 setTimeout()

Ejecuta una función **una sola vez** después de que transcurra un tiempo en milisegundos.

```js
// Sintaxis básica
setTimeout(función, tiempoEnMilisegundos);

//Ejemplo con función tradicional
function mostrarMensaje() {
  console.log("Han pasado 2 segundos");
}
setTimeout(mostrarMensaje, 2000);


// Ejemplo con función flecha
setTimeout(() => {
  console.log("Han pasado 2 segundos");
}, 2000);
```

---

## 📌 clearTimeout()

Detiene la ejecución programada por `setTimeout`.

```js
// Programamos un mensaje que debería mostrarse en 3 segundos
let id = setTimeout(() => {
  console.log("Este mensaje no aparecerá");
}, 3000);

// Cancelamos el temporizador inmediatamente
clearTimeout(id);

console.log("El temporizador ha sido cancelado ✅");

```

---

## 📌 setInterval()

Ejecuta una función **de manera repetida** cada cierto intervalo de tiempo (en milisegundos).

```js
let id = setInterval(() => {
  console.log("Esto se repite cada segundo");
}, 1000);
```

---

## 📌 clearInterval()

Detiene la ejecución repetida iniciada con `setInterval`.

```js
let contador = 0;

let id = setInterval(() => {
  contador++;
  console.log("Tick " + contador);

  if (contador === 5) {
    clearInterval(id); // Detener después de 5 repeticiones
  }
}, 1000);
```

---

!!! warning "Precaución con los temporizadores"
    Usar muchos `setInterval` o temporizadores con tiempos muy cortos puede afectar al rendimiento de la página.
    Es recomendable limpiar siempre los temporizadores que ya no sean necesarios.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre `setTimeout` y `setInterval`?
    2. ¿Qué devuelve un temporizador y para qué sirve ese valor?
    3. ¿Cómo detendrías un `setTimeout` antes de que se ejecute?
    4. ¿Qué pasaría si olvidas usar `clearInterval` en un intervalo infinito?
    5. ¿Cómo harías que un mensaje aparezca 5 veces con un intervalo de 1 segundo y luego se detenga automáticamente?