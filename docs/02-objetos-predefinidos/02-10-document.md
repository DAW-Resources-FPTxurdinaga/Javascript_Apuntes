# 3.2 Document

El objeto **`document`** forma parte del objeto **`window`** y representa la **página web cargada en el navegador**.
A través de él podemos **leer** y **modificar** el contenido, la estructura y los estilos del HTML.
Es la puerta de entrada al **DOM (Document Object Model)**.

---

## 📌 Acceso al objeto `document`

Se accede simplemente con la palabra clave `document`.
No hace falta escribir `window.document`, aunque ambos son equivalentes.

```js
console.log(document.title); // Devuelve el título de la página
console.log(document.URL);   // Devuelve la URL actual
```

---

## 📌 Propiedades principales de `document`

### Información del documento

```js
console.log(document.title);   // Título de la página
console.log(document.URL);     // URL completa
console.log(document.domain);  // Dominio de la página
```

### Acceso a elementos

```js
// Devuelve el elemento con id="principal"
let elemento = document.getElementById("principal");

// Devuelve todos los elementos <p>
let parrafos = document.getElementsByTagName("p");

// Devuelve todos los elementos con clase="destacado"
let destacados = document.getElementsByClassName("destacado");
```

---

## 📌 Métodos modernos de selección

En versiones más recientes de JavaScript se introdujeron **querySelector** y **querySelectorAll**, mucho más flexibles:

```js
// Devuelve el primer <p> que encuentre
let parrafo = document.querySelector("p");

// Devuelve todos los elementos con clase="item"
let items = document.querySelectorAll(".item");
```

!!! tip "Recomendación"
    Hoy en día se recomienda usar **querySelector** y **querySelectorAll** en lugar de los métodos antiguos, porque permiten usar selectores **CSS**.

En la Unidad sobre DOM aprenderemos más sobre manipulación de elementos del documento. 

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué representa el objeto `document` en el navegador?
    2. ¿Qué diferencia hay entre `getElementById` y `querySelector`?
    3. ¿Qué métodos usarías para seleccionar todos los elementos con una clase específica?
    4. ¿Cómo puedes crear un nuevo párrafo y añadirlo al final del documento?
    5. ¿Qué diferencia hay entre `innerText` y `innerHTML` al modificar el contenido de un elemento?