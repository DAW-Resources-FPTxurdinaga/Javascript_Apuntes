# 4.3 Almacenamiento en el navegador (Web Storage)

Los navegadores modernos permiten guardar datos de manera **persistente** o **temporal** directamente en el dispositivo del usuario.
Esto se realiza mediante la **API Web Storage**, que proporciona dos mecanismos principales:
`localStorage` y `sessionStorage`.

---

## 📌 ¿Qué es Web Storage?

El **Web Storage** permite guardar información en el navegador sin necesidad de usar cookies.
A diferencia de las cookies, los datos:

* No se envían en cada petición al servidor.
* Se guardan únicamente en el navegador.
* Pueden almacenar más datos (hasta varios MB).
* Se gestionan fácilmente desde JavaScript.

---

!!! info "Dos tipos de almacenamiento"
    - **localStorage**: Los datos **persisten incluso al cerrar el navegador**.
    - **sessionStorage**: Los datos **se eliminan cuando se cierra la pestaña o ventana**.

    Ambos almacenan la información como **pares clave-valor (key–value)** en formato **cadena de texto (string)**.

---

## 📌 Almacenar datos

Para guardar información, usamos el método `setItem()`.

```js
// localStorage: persiste entre sesiones
localStorage.setItem("usuario", "Laura");

// sessionStorage: desaparece al cerrar la pestaña
sessionStorage.setItem("tema", "oscuro");
```

---

## 📌 Obtener datos

Usamos `getItem()` para recuperar un valor almacenado.

```js
const nombre = localStorage.getItem("usuario");
console.log(nombre); // "Laura"

const tema = sessionStorage.getItem("tema");
console.log(tema); // "oscuro"
```

---

## 📌 Eliminar datos

Podemos borrar un elemento concreto o vaciar todo el almacenamiento.

```js
// Borrar un solo elemento
localStorage.removeItem("usuario");

// Borrar todo
sessionStorage.clear();
```

---

## 📌 Guardar objetos o arrays

Como Web Storage **solo guarda texto**, debemos convertir los objetos a formato **JSON** antes de guardarlos, y volver a convertirlos al leerlos.

```js
const persona = { nombre: "Laura", edad: 30 };

// Guardar objeto
localStorage.setItem("persona", JSON.stringify(persona));

// Recuperar y convertir a objeto
const datos = JSON.parse(localStorage.getItem("persona"));
console.log(datos.nombre); // "Laura"
```

---

!!! warning "Cuidado con los tipos de datos"
    Todo lo que guardes en `localStorage` o `sessionStorage` se convierte en texto.
    Si guardas un número, un booleano o un objeto, conviértelo y recupéralo correctamente con `JSON.stringify()` y `JSON.parse()`.

---

## 📌 Ejemplo práctico

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Ejemplo Web Storage</title>
</head>
<body>
  <h2>Guardar nombre en el navegador</h2>
  <input type="text" id="nombre" placeholder="Escribe tu nombre">
  <button id="guardar">Guardar</button>
  <button id="mostrar">Mostrar</button>
  <p id="resultado"></p>

  <script>
    const input = document.getElementById("nombre");
    const guardar = document.getElementById("guardar");
    const mostrar = document.getElementById("mostrar");
    const resultado = document.getElementById("resultado");

    guardar.addEventListener("click", () => {
      localStorage.setItem("nombreUsuario", input.value);
      alert("Nombre guardado ✅");
    });

    mostrar.addEventListener("click", () => {
      const nombreGuardado = localStorage.getItem("nombreUsuario");
      resultado.textContent = nombreGuardado
        ? `Hola de nuevo, ${nombreGuardado}! 👋`
        : "No hay ningún nombre guardado.";
    });
  </script>
</body>
</html>
```

---

## 📌 ¿Por qué no usar cookies desde JavaScript?

Aunque las **cookies** también almacenan datos, presentan varios inconvenientes:

* Se envían automáticamente al servidor en cada petición, afectando el rendimiento.
* Su tamaño máximo es muy limitado (≈4 KB).
* Son menos seguras: pueden ser leídas o modificadas fácilmente.
* Su gestión manual desde JavaScript es más compleja (`document.cookie`).

Por eso, para guardar datos del **lado del cliente** (por ejemplo, preferencias o configuraciones locales), se recomienda usar **Web Storage**.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre `localStorage` y `sessionStorage`?
    2. ¿Qué tipo de datos guarda Web Storage por defecto?
    3. ¿Por qué es recomendable usar `JSON.stringify()` y `JSON.parse()`?
    4. ¿Qué ventaja ofrece Web Storage frente a las cookies?
    5. ¿Qué método usarías para borrar todos los datos guardados?
