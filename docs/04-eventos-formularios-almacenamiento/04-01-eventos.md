# 4.1 Eventos en JavaScript

Los **eventos** permiten que una página web responda a las acciones del usuario o del navegador: un clic, mover el ratón, escribir en el teclado, enviar un formulario, etc.
Gracias a ellos, JavaScript convierte una web estática en una experiencia **interactiva**.

---

## 📌 Definición y uso de eventos

Un **evento** es un suceso detectado por el navegador.
Ejemplos comunes:

* `click`: cuando el usuario hace clic.
* `mouseover`: cuando el ratón entra en un elemento.
* `mouseout`: cuando el ratón sale de un elemento.
* `keydown`: al pulsar una tecla.
* `submit`: al enviar un formulario.

---

## 📌 Event listeners: escuchar y eliminar eventos

La manera más flexible de escuchar eventos es con `addEventListener`.

```js
elemento.addEventListener("tipoEvento", funcion);
```

### Función anónima tradicional

```js
const boton = document.getElementById("btn");

boton.addEventListener("click", function (e) {
  console.log("Se pulsó el botón");
  console.log(`Tipo: ${e.type}, Elemento: ${e.target.id}`);
});
```

### Función flecha anónima

```js
const caja = document.getElementById("caja");

caja.addEventListener("mouseover", (e) => {
  e.target.style.backgroundColor = "lightblue";
  console.log("El ratón entró en la caja");
});
```

### Función con nombre

Las funciones con nombre permiten reutilizar o eliminar el listener.

```js
function mostrarAlerta(e) {
  alert("Has hecho clic en el párrafo");
}

const parrafo = document.getElementById("texto");
parrafo.addEventListener("click", mostrarAlerta);

// Para eliminarlo
parrafo.removeEventListener("click", mostrarAlerta);
```

!!! info "¿Cuál elegir?"
    - Usa **funciones anónimas** para código rápido y sencillo.
    - Usa **funciones con nombre** si quieres reutilizarlas o eliminarlas con `removeEventListener`.

---

## 📌 Reutilizar la misma función en varios elementos

Un mismo manejador puede usarse en distintos elementos.
Con la propiedad `event.target` distinguimos cuál disparó el evento.

```js
function resaltar(e) {
  e.target.style.color = "red";
  console.log(`Clic en: ${e.target.tagName}`);
}

document.getElementById("opcion1").addEventListener("click", resaltar);
document.getElementById("opcion2").addEventListener("click", resaltar);
```

---

## 📌 Manipulación del objeto `event`

El parámetro `event` (o `e`) contiene información sobre el suceso.

* `event.type`: tipo de evento (`click`, `mouseover`, etc.).
* `event.target`: elemento que originó el evento.
* `event.preventDefault()`: evita el comportamiento por defecto del navegador.

### Ejemplo con `preventDefault`

```js
const enlace = document.getElementById("miEnlace");

enlace.addEventListener("click", function (e) {
  e.preventDefault(); // Bloquea la acción por defecto
  alert("El enlace no se abrirá, hemos usado preventDefault()");
});
```

!!! warning "Cuándo usar preventDefault"
    Empléalo solo cuando quieras **modificar el comportamiento normal** del navegador, por ejemplo:
    - Evitar que un enlace abra otra página.
    - Impedir que un formulario se envíe automáticamente.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre usar una función anónima y una función con nombre en un evento?
    2. ¿Qué devuelve `event.target` dentro de un manejador?
    3. ¿Qué sucede si llamas a `preventDefault()` en el evento `submit` de un formulario?
    4. ¿Cómo eliminarías un listener previamente añadido a un elemento?
    5. ¿Qué ventaja tiene reutilizar la misma función en varios elementos?