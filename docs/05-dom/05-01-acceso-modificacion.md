# 5.1 Acceso y modificación de elementos. Texto y atributos

El **DOM (Document Object Model)** es una representación en forma de árbol del documento HTML.
Cada etiqueta es un **nodo** que JavaScript puede leer, crear, modificar o eliminar.

Mediante el DOM, podemos **interactuar con la página**: cambiar textos, imágenes, estilos, clases, o atributos de manera dinámica.

---

## 📌 Seleccionar elementos del DOM

Para modificar un elemento, primero hay que **acceder a él**.
Existen varias formas de seleccionar nodos en el DOM.

### Métodos clásicos

```js
// Devuelve un único elemento
document.getElementById("titulo");

// Devuelve un HTMLCollection (similar a un array)
document.getElementsByClassName("caja");
document.getElementsByTagName("p");
```

### Métodos modernos

```js
// Devuelve el primer elemento que cumpla el selector CSS
document.querySelector("h1");
document.querySelector("#principal");
document.querySelector(".importante");

// Devuelve una lista (NodeList) con todos los que coincidan
document.querySelectorAll(".item");

// Ejemplo: recorrer todos los elementos seleccionados
document.querySelectorAll(".item").forEach(el => {
  el.style.color = "blue";
});
```

!!! note "Métodos recomendados"
    En JavaScript moderno, se recomienda usar `querySelector()` y `querySelectorAll()`
    porque permiten trabajar con **selectores CSS** y son más flexibles.

---

## 📌 Modificar el contenido de un elemento

Podemos cambiar el **texto** o el **HTML interno** de un nodo.

### Cambiar texto

```js
const titulo = document.querySelector("h1");

// Sustituye el texto del elemento
titulo.textContent = "Nuevo título";
```

### Cambiar HTML interno

```js
const contenedor = document.querySelector("#info");

// Permite incluir etiquetas HTML
contenedor.innerHTML = "<strong>Actualizado:</strong> contenido dinámico";
```

!!! warning "innerHTML vs textContent"
    - `textContent` solo cambia el texto plano, sin interpretar etiquetas.
    - `innerHTML` interpreta el código HTML que insertas.
    Úsalo con cuidado si el contenido proviene del usuario, ya que puede generar **riesgos de seguridad (XSS)**.

---

## 📌 Acceso y modificación de atributos

Podemos leer o cambiar los **atributos** de una etiqueta (por ejemplo, `src`, `href`, `alt`, `title`…).

```js
const imagen = document.querySelector("img");

// Leer el valor de un atributo
console.log(imagen.getAttribute("src"));

// Cambiar un atributo
imagen.setAttribute("alt", "Logo actualizado");
imagen.setAttribute("src", "img/nuevo-logo.png");

// Eliminar un atributo
imagen.removeAttribute("title");
```

También es posible acceder directamente a muchas propiedades:

```js
imagen.src = "img/nuevo-logo.png";
imagen.alt = "Logo actualizado";
```

!!! note "getAttribute() vs propiedades directas"
    - Las propiedades (`imagen.src`) reflejan el **estado actual** del elemento en el DOM.
    - Los atributos (`getAttribute("src")`) reflejan el **valor original** definido en el HTML.
    - En la mayoría de los casos se pueden usar indistintamente, pero es importante conocer la diferencia.

---

## 📌 Manipulación de clases y estilos

Las clases permiten modificar la apariencia mediante CSS sin tocar directamente los estilos.

### Añadir, quitar o alternar clases

```js
const caja = document.querySelector(".caja");

caja.classList.add("activa");
caja.classList.remove("oculta");
caja.classList.toggle("resaltada"); // la añade si no la tiene, la quita si la tiene
```

### Cambiar estilos desde JavaScript

```js
const titulo = document.querySelector("h1");

titulo.style.color = "red";
titulo.style.backgroundColor = "yellow";
```

!!! warning "Buenas prácticas"
    Es preferible cambiar **clases CSS** en lugar de modificar estilos directamente desde JavaScript.
    Así se mantiene la **separación entre contenido, estilo y comportamiento.**

---

## 📌 Inserción de contenido dinámico con plantillas literales

En JavaScript moderno, los **template literals** (comillas invertidas) facilitan insertar contenido dinámico en el DOM.

```js
const usuario = "Laura";
const contenedor = document.querySelector("#saludo");

contenedor.innerHTML = `
  <p>Bienvenida, <strong>${usuario}</strong> 🎉</p>
`;
```

De esta forma, podemos construir fragmentos HTML reutilizando variables o resultados de funciones.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué método moderno permite seleccionar varios elementos usando un selector CSS?
    2. ¿Qué diferencia hay entre `textContent` e `innerHTML`?
    3. ¿Qué hace el método `setAttribute()`?
    4. ¿Por qué conviene usar `classList` en lugar de `style` para cambiar la apariencia?
    5. ¿Qué ventaja tienen los *template literals* al generar contenido dinámico?
