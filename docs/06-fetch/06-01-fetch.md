# 6. Comunicación con APIs: Fetch

La **API Fetch** permite realizar peticiones HTTP (GET, POST, etc.) para obtener o enviar datos a un servidor, sustituyendo a la antigua `XMLHttpRequest`.

Su uso es **asíncrono** y se basa en **promesas**, lo que la hace más simple y legible.

---

## 📌 Sintaxis básica

```js
fetch("https://jsonplaceholder.typicode.com/users")
  .then(response => response.json()) // transforma la respuesta a JSON
  .then(data => console.log(data))    // usa los datos
  .catch(error => console.error("Error:", error));
```

1. `fetch(url)` realiza la petición.
2. Devuelve una **promesa** que se resuelve con un objeto `Response`.
3. Usamos `.json()`, `.text()` o `.blob()` para procesar la respuesta.
4. Si hay error de red o en la respuesta, lo capturamos con `.catch()`.

---

## 📌 Uso con `async/await`

El mismo ejemplo con sintaxis moderna:

```js
async function cargarUsuarios() {
  try {
    const respuesta = await fetch("https://jsonplaceholder.typicode.com/users");
    const datos = await respuesta.json();
    console.log(datos);
  } catch (error) {
    console.error("Error al obtener los datos:", error);
  }
}

cargarUsuarios();
```

!!! note "Por qué usar async/await"
    Hace el código **más legible** y se comporta como si fuera secuencial, pero sigue siendo asíncrono.

---

## 📌 Comprobación del estado de la respuesta

El método `fetch()` **no lanza un error automáticamente** si la respuesta del servidor es un 404 o 500, por lo que debemos comprobarlo.

```js
async function cargarUsuarios() {
  try {
    const respuesta = await fetch("https://jsonplaceholder.typicode.com/users");

    if (!respuesta.ok) {
      throw new Error(`Error HTTP: ${respuesta.status}`);
    }

    const datos = await respuesta.json();
    console.log(datos);
  } catch (error) {
    console.error("Error en la petición:", error.message);
  }
}
```

---

## 📌 Mostrar los datos en el DOM

Podemos usar `fetch()` para generar contenido dinámico.

```html
<ul id="lista"></ul>

<script>
async function cargarUsuarios() {
  const respuesta = await fetch("https://jsonplaceholder.typicode.com/users");
  const usuarios = await respuesta.json();

  const lista = document.getElementById("lista");
  lista.innerHTML = ""; // limpia antes de insertar

  usuarios.forEach(u => {
    const li = document.createElement("li");
    li.textContent = `${u.name} (${u.email})`;
    lista.appendChild(li);
  });
}

cargarUsuarios();
</script>
```

---

## 📌 Enviar datos con `POST`

`fetch()` también permite **enviar información** al servidor (por ejemplo, al enviar un formulario).

```js
async function enviarDatos() {
  const nuevoUsuario = {
    nombre: "Laura",
    correo: "laura@example.com"
  };

  const respuesta = await fetch("https://jsonplaceholder.typicode.com/users", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(nuevoUsuario)
  });

  const resultado = await respuesta.json();
  console.log("Respuesta del servidor:", resultado);
}

enviarDatos();
```

---

## 📌 Diferencias con AJAX clásico

| Característica          | `XMLHttpRequest` | `fetch()`                          |
| ----------------------- | ---------------- | ---------------------------------- |
| Sintaxis                | Verbosa          | Clara y moderna                    |
| Soporta Promesas        | ❌ No             | ✅ Sí                               |
| Cuerpo JSON             | Manual           | Automático con `.json()`           |
| Control de errores HTTP | Implícito        | Debe comprobarse con `response.ok` |

!!! info "En la práctica"
    - Usa siempre `fetch()` con `async/await`.
    - Comprueba el código de estado (`response.ok`).
    - Convierte la respuesta con `.json()`.
    - Maneja errores con `try...catch`.

---

## 📌 Ejemplo completo: cargar y mostrar publicaciones

```html
<h1>Publicaciones</h1>
<ul id="posts"></ul>

<script>
async function cargarPosts() {
  try {
    const respuesta = await fetch("https://jsonplaceholder.typicode.com/posts?_limit=5");

    if (!respuesta.ok) throw new Error("No se pudieron cargar las publicaciones");

    const posts = await respuesta.json();
    const lista = document.getElementById("posts");

    lista.innerHTML = posts.map(p => `
      <li>
        <strong>${p.title}</strong><br>
        ${p.body}
      </li>
    `).join("");

  } catch (error) {
    document.getElementById("posts").textContent = "❌ Error al cargar las publicaciones.";
    console.error(error);
  }
}

cargarPosts();
</script>
```

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué devuelve la función `fetch()`?
    2. ¿Por qué debemos usar `response.json()`?
    3. ¿Qué ocurre si el servidor devuelve un error 404?
    4. ¿Cómo se envían datos en formato JSON con `fetch()`?
    5. ¿Por qué es recomendable usar `async/await` en lugar de `.then()`?
