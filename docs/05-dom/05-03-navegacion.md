# 5.3 Acceso y navegación por elementos del DOM

Una vez que conocemos cómo crear y modificar nodos, el siguiente paso es **recorrer y acceder** a diferentes partes del árbol del DOM.
El **DOM (Document Object Model)** representa la estructura jerárquica de una página web, donde cada etiqueta HTML es un **nodo**.
JavaScript nos permite movernos entre esos nodos como si fueran miembros de una familia: padres, hijos y hermanos.

---

## 📌 Tipos de nodos

Los más comunes son:

| Tipo       | Descripción                                          |
| ---------- | ---------------------------------------------------- |
| `document` | Nodo raíz de todo el documento HTML                  |
| `element`  | Representa etiquetas HTML como `<div>`, `<p>`, `<a>` |
| `text`     | Contiene el texto dentro de un elemento              |
| `comment`  | Representa los comentarios `<!-- ... -->`            |

!!! info "DOM jerárquico"
    Piensa en el DOM como un **árbol genealógico**:
    cada nodo tiene un **padre**, puede tener **hijos** y puede tener **hermanos** (otros nodos al mismo nivel).

---

## 📌 Acceso a nodos hijos y padres

### Hijos

Para acceder a los elementos hijos de un nodo usamos:

```js
const lista = document.querySelector("ul");

console.log(lista.children);       // HTMLCollection con los elementos hijos
console.log(lista.firstElementChild); // Primer hijo
console.log(lista.lastElementChild);  // Último hijo
```

!!! note "children vs childNodes"
    - `children` devuelve **solo elementos HTML**.
    - `childNodes` incluye **también nodos de texto y comentarios** (por ejemplo, ANsaltos de línea).

### Padre

Para acceder al elemento padre:

```js
const item = document.querySelector("li");
console.log(item.parentElement); // Devuelve el <ul> contenedor
```

---

## 📌 Navegar entre hermanos

Los nodos del mismo nivel se llaman **hermanos**.
Podemos desplazarnos entre ellos con las siguientes propiedades:

```js
const item = document.querySelector("li:nth-child(2)");

console.log(item.previousElementSibling); // Hermano anterior
console.log(item.nextElementSibling);     // Hermano siguiente
```

!!! note "Element vs Node"
    Los métodos con `Element` (por ejemplo, `nextElementSibling`) **ignoran los saltos de línea y los espacios**.
    Los métodos sin “Element” (`nextSibling`, `previousSibling`) pueden devolver **nodos de texto**.

---

## 📌 Búsqueda dentro de un elemento específico

Podemos usar `querySelector()` o `querySelectorAll()` no solo en `document`, sino **dentro de cualquier elemento**.

```js
const seccion = document.querySelector(".articulo");
const parrafos = seccion.querySelectorAll("p");

console.log(parrafos.length); // Número de párrafos dentro de la sección
```

Esto es útil para **acotar búsquedas** y trabajar solo dentro de una parte del documento, evitando conflictos con otros elementos que tengan la misma clase o etiqueta.

---

## 📌 Crear relaciones entre nodos

Podemos recorrer el DOM desde un nodo y **construir relaciones** dinámicas, por ejemplo:

```js
const lista = document.querySelector("ul");

// Acceder al primer elemento y crear uno nuevo después
const primerItem = lista.firstElementChild;
const nuevoItem = document.createElement("li");
nuevoItem.textContent = "Elemento insertado después del primero";

primerItem.after(nuevoItem);
```

---

## 📌 Métodos útiles para recorrer el DOM

| Método / Propiedad                                | Descripción                                                  |
| ------------------------------------------------- | ------------------------------------------------------------ |
| `.parentElement`                                  | Devuelve el elemento padre                                   |
| `.children`                                       | Colección de elementos hijos                                 |
| `.firstElementChild` / `.lastElementChild`        | Primer / último hijo                                         |
| `.nextElementSibling` / `.previousElementSibling` | Hermano siguiente / anterior                                 |
| `.querySelector()` / `.querySelectorAll()`        | Búsqueda dentro del nodo                                     |
| `.closest(selector)`                              | Busca el **ancestro más cercano** que cumpla un selector CSS |

### Ejemplo con `.closest()`

```js
const boton = document.querySelector("button");
const seccionPadre = boton.closest("section");

console.log(seccionPadre); // Muestra el <section> más cercano que contiene el botón
```

!!! info "Uso de closest()"
    Muy útil en formularios o listas cuando un evento ocurre en un elemento hijo
    (por ejemplo, un botón dentro de una tarjeta) y necesitamos acceder a su contenedor.

---

## 📌 Iterar sobre colecciones de nodos

Los métodos como `querySelectorAll()` devuelven una **NodeList**, que puede recorrerse con `forEach`.

```js
const items = document.querySelectorAll("li");

items.forEach((el, i) => {
  console.log(`Elemento ${i + 1}: ${el.textContent}`);
});
```

!!! note "HTMLCollection vs NodeList"
    - `HTMLCollection` (por ejemplo, devuelta por `children`) **se actualiza automáticamente** si el DOM cambia.
    - `NodeList` (por ejemplo, de `querySelectorAll`) **es estática**: no refleja cambios posteriores.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
      1. ¿Qué diferencia hay entre `children` y `childNodes`?
      2. ¿Qué devuelve `parentElement` y para qué sirve?
      3. ¿Cómo podrías acceder al hermano siguiente de un elemento?
      4. ¿Qué hace el método `.closest()`?
      5. ¿Qué diferencia hay entre una `NodeList` y una `HTMLCollection`?
