# 5.2 Creación, sustitución y borrado de elementos

Además de modificar elementos existentes, JavaScript permite **crear nuevos nodos**, **insertarlos**, **sustituirlos** o **eliminarlos** dinámicamente en el árbol del DOM.
Estas operaciones son fundamentales para construir contenido interactivo: menús, listas, tarjetas o componentes que se generan al cargar datos.

---

## 📌 Crear nuevos elementos

El método `document.createElement()` permite crear un nodo vacío del tipo indicado.

```js
// Crear un nuevo elemento <p>
const parrafo = document.createElement("p");

// Añadir contenido de texto
parrafo.textContent = "Este párrafo ha sido creado con JavaScript.";

// Insertarlo en el documento
document.body.appendChild(parrafo);
```

También se pueden combinar con **propiedades y clases** antes de insertarlos:

```js
const enlace = document.createElement("a");
enlace.textContent = "Ir a la página principal";
enlace.href = "index.html";
enlace.classList.add("boton");
document.body.appendChild(enlace);
```

!!! note "Diferencia entre crear e insertar"
    `createElement()` **solo genera el nodo en memoria**.
    No aparecerá en la página hasta que lo insertes en el DOM con métodos como `appendChild()`, `append()` o `prepend()`.

---

## 📌 Añadir elementos al documento

Una vez creado el nodo, existen varias formas de **insertarlo** en el DOM.

```js
const lista = document.querySelector("#lista");
const nuevo = document.createElement("li");
nuevo.textContent = "Nuevo elemento";

// Métodos de inserción
lista.appendChild(nuevo);     // al final
lista.prepend(nuevo);         // al principio
lista.before(nuevo);          // antes de la lista
lista.after(nuevo);           // después de la lista
```

!!! info "Métodos modernos"
    En JavaScript moderno, se recomienda `append()` y `prepend()` porque permiten insertar **múltiples nodos o texto directamente** sin usar `createTextNode()`.

```js
lista.append("Elemento 1", "Elemento 2");
```

---

## 📌 Reemplazar elementos

Podemos sustituir un nodo existente por otro.

```js
const viejo = document.querySelector("#viejo");
const nuevo = document.createElement("p");
nuevo.textContent = "Este párrafo reemplaza al anterior.";

// Forma clásica
viejo.parentNode.replaceChild(nuevo, viejo);

// Forma moderna
viejo.replaceWith(nuevo);
```

!!! note "replaceWith() y replaceChildren()"
    - `replaceWith()` sustituye un elemento por otro.
    - `replaceChildren()` borra todos los hijos de un nodo y añade nuevos de una sola vez.

---

## 📌 Eliminar elementos

Para borrar un elemento del DOM se puede usar el método moderno `.remove()` o el clásico `removeChild()`.

```js
const tarjeta = document.querySelector(".tarjeta");

// Forma moderna
tarjeta.remove();

// Forma clásica (aún válida)
tarjeta.parentNode.removeChild(tarjeta);
```

---

## 📌 Uso de fragmentos para mejorar el rendimiento

Cuando se crean **muchos elementos**, añadirlos uno por uno al DOM puede ser lento.
Para evitar repintados innecesarios, se utiliza un **DocumentFragment**, que actúa como un contenedor temporal.

```js
const lista = document.querySelector("#lista");
const fragmento = document.createDocumentFragment();

for (let i = 1; i <= 5; i++) {
  const li = document.createElement("li");
  li.textContent = `Elemento ${i}`;
  fragmento.appendChild(li);
}

// Insertamos todo de una vez
lista.appendChild(fragmento);
```

!!! info "Ventaja de los fragmentos"
    Un `DocumentFragment` existe solo en memoria.
    Insertarlo en el DOM actualiza la página **una sola vez**, haciendo el proceso mucho más eficiente.

---

## 📌 Plantillas reutilizables con `<template>`

El elemento `<template>` permite definir contenido **invisible** en el HTML que se puede clonar y reutilizar con JavaScript.

```html
<template id="tarjeta">
  <div class="card">
    <h3 class="titulo"></h3>
    <p class="texto"></p>
  </div>
</template>

<div id="contenedor"></div>

<script>
  const plantilla = document.getElementById("tarjeta");
  const contenedor = document.getElementById("contenedor");

  // Clonamos la plantilla
  const clon = plantilla.content.cloneNode(true);
  clon.querySelector(".titulo").textContent = "Hola mundo";
  clon.querySelector(".texto").textContent = "Esta tarjeta proviene de un template";

  contenedor.appendChild(clon);
</script>
```

!!! note "Por qué usar plantillas"
    Usar `<template>` facilita mantener el HTML separado del JavaScript
    y permite **repetir estructuras complejas** (como tarjetas o filas de tabla) sin tener que escribirlas desde cero.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué hace `createElement()` y por qué el elemento no aparece inmediatamente en la página?
    2. ¿Qué diferencia hay entre `appendChild()` y `append()`?
    3. ¿Qué método moderno sustituye a `replaceChild()`?
    4. ¿Por qué se recomienda usar `DocumentFragment` al insertar muchos nodos?
    5. ¿Para qué sirve el elemento `<template>` en HTML?
