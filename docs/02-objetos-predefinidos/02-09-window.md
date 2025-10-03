# 3.1 Window: El objeto global del navegador

El objeto `window` representa la **ventana del navegador** en la que se carga la página.
Es el **objeto global en JavaScript del lado del cliente**, lo que significa que prácticamente todo lo que usamos en el navegador "cuelga" de `window`.

---

## 📌 Acceso al objeto `window`

No es necesario escribir `window.` siempre, ya que sus propiedades y métodos están disponibles de forma global.

```js
// Estas dos líneas son equivalentes
window.alert("Hola");
alert("Hola");
```

---

## 📌 Propiedades principales de `window`

### Dimensiones de la ventana

```js
console.log(window.innerWidth);   // Anchura de la ventana en píxeles
console.log(window.innerHeight);  // Altura de la ventana en píxeles
```

### Acceso al documento cargado

```js
console.log(window.document.title); // Título de la página
```

### Información de la URL actual

```js
console.log(window.location.href); // URL completa
console.log(window.location.hostname); // Dominio (ej. www.ejemplo.com)
```

---

## 📌 Control de la ventana

El objeto `window` también permite abrir, cerrar y mover ventanas.
Sin embargo, **muchas funciones están limitadas por seguridad** en navegadores modernos.

```js
// Abre una nueva ventana o pestaña
let nuevaVentana = window.open("https://developer.mozilla.org", "_blank");

// Cierra la ventana abierta
nuevaVentana.close();
```

!!! warning "Cuidado"
    Por motivos de seguridad, la mayoría de navegadores **bloquean ventanas emergentes** si no se abren como respuesta a una acción del usuario (por ejemplo, un clic).

---

## 📌 Objetos relacionados

El objeto `window` contiene otros objetos importantes que estudiaremos en las próximas lecciones:

* `navigator`: información del navegador y sistema.
* `screen`: información de la pantalla.
* `history`: historial de navegación.
* `location`: URL actual y navegación.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué representa el objeto `window` en el navegador?
    2. ¿Por qué normalmente no hace falta escribir `window.` delante de métodos como `alert` o `document`?
    3. ¿Qué información proporcionan `innerWidth` e `innerHeight`?
    4. ¿Qué limitaciones tienen los métodos `window.open` y `window.close` en los navegadores modernos?
    5. ¿Qué objetos importantes forman parte de `window` y se estudiarán en las siguientes lecciones?