# 3.1.2. Funciones (II): Uso avanzado

En esta lección vamos a profundizar en otros usos comunes de las funciones en JavaScript:  
funciones anónimas, funciones de callback y parámetros por defecto.

---

## 📌 Funciones anónimas

Una **función anónima** es aquella que no tiene nombre propio.  
Se suelen usar asignándolas a una variable o pasándolas directamente como argumento a otra función.

```js
// Asignada a una variable
const cuadrado = function(x) {
  return x * x;
};

console.log(cuadrado(4)); // 16
```

---

## 📌 Funciones de callback

Un **callback** es una función que se pasa como argumento a otra y que se ejecuta después de que esta la llame.
Son muy comunes en JavaScript, especialmente en asincronía y en métodos de arrays.

```js
function procesarUsuario(nombre, callback) {
  console.log(`Procesando usuario: ${nombre}`);
  callback();
}

// Pasamos una función anónima como callback
procesarUsuario("Laura", function() {
  console.log("Callback ejecutado ✅");
});

// O una función flecha
procesarUsuario("Laura", () => {
  console.log("Callback con función flecha ✅");
});
```

---

## 📌 Parámetros por defecto

Los **parámetros por defecto** permiten dar un valor inicial a un argumento de la función si no se proporciona al llamarla.
Esto evita tener que comprobar manualmente si el parámetro existe.

```js
function saludar(nombre = "invitado") {
  console.log(`Hola, ${nombre}`);
}

saludar();        // Hola, invitado
saludar("Laura"); // Hola, Laura
```

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué es una función anónima y en qué casos se suele usar?
    2. ¿Qué es un callback? Pon un ejemplo sencillo.
    3. Crea una función que reciba un nombre y un callback, y que ejecute el callback con ese nombre.
    4. Declara una función con un parámetro por defecto llamado `idioma` que valga `"es"`.
    5. Escribe una llamada a esa función con y sin pasarle el argumento.

```