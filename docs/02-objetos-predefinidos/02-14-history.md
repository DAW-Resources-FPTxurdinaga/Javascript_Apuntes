# 3.5 History

El objeto **`history`** forma parte de **`window`** y permite acceder y manipular el **historial de páginas visitadas** en la sesión del navegador.
Con él podemos avanzar, retroceder o cargar URLs específicas dentro del historial.

---

## 📌 Propiedades principales

### Número de páginas en el historial

```js
console.log(history.length);  
// Devuelve cuántas entradas hay en el historial actual
```

---

## 📌 Métodos principales

### Ir hacia atrás y hacia adelante

```js
history.back();   // Equivale a pulsar el botón "Atrás" del navegador
history.forward(); // Equivale al botón "Adelante"
```

### Navegar a una posición concreta

```js
history.go(-1); // Una página atrás
history.go(1);  // Una página adelante
history.go(0);  // Recarga la página actual
```

### Añadir o modificar entradas del historial

Desde HTML5, `history` permite **manipular el historial sin recargar la página**, lo que resulta muy útil en aplicaciones SPA (Single Page Applications).

```js
// Añade una nueva entrada
history.pushState({ usuario: "Laura" }, "Título", "/perfil");

// Modifica la entrada actual
history.replaceState({ usuario: "Laura" }, "Título", "/inicio");
```

Los objetos pasados como primer argumento (`{ usuario: "Laura" }`) quedan almacenados y se pueden recuperar más adelante.

---

## 📌 Eventos relacionados

Cuando el usuario navega hacia atrás o hacia adelante y cambia el estado de la URL, se dispara el evento **`popstate`**:

```js
window.addEventListener("popstate", (event) => {
  console.log("Estado actual:", event.state);
});
```

---

!!! warning "Compatibilidad"
    Aunque `history.pushState` y `history.replaceState` están soportados en todos los navegadores modernos, requieren que la página esté servida desde un **servidor web**. Si pruebas con archivos locales (`file://`), algunos navegadores pueden dar errores.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué hace `history.back()`?
    2. ¿Qué diferencia hay entre `pushState` y `replaceState`?
    3. ¿Qué ocurre si ejecutas `history.go(0)`?
    4. ¿Qué evento se dispara al cambiar de estado en el historial?
    5. ¿Qué devuelve `history.length`?
