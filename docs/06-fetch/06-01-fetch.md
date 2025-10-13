# 6.1 API Fetch y Promesas

La API Fetch permite realizar **peticiones HTTP** desde JavaScript para **obtener o enviar datos** a un servidor.
Es la forma moderna de comunicarse con APIs y servicios web sin recargar la página.

Antes de usar `fetch()`, conviene entender brevemente qué son las **promesas**, ya que Fetch trabaja con ellas.

---

## 📘 ¿Qué es una promesa en JavaScript?

Una **promesa** (`Promise`) representa una **acción asíncrona**: algo que se completará más adelante, como descargar datos de un servidor.
Mientras tanto, el resto del programa **sigue ejecutándose**.

---

### 📌 Estados de una promesa

| Estado      | Significado                      |
| ----------- | -------------------------------- |
| `pending`   | La operación aún no ha terminado |
| `fulfilled` | Se completó correctamente        |
| `rejected`  | Ocurrió un error                 |

Cuando se cumple (`fulfilled`), se ejecuta el bloque `.then()`.
Si falla (`rejected`), se ejecuta `.catch()`.

```js
const promesa = new Promise((resolve, reject) => {
  const exito = true;
  if (exito) {
    resolve("✅ Todo salió bien");
  } else {
    reject("❌ Ocurrió un error");
  }
});

promesa
  .then(resultado => console.log(resultado)) // si va bien
  .catch(error => console.error(error));     // si falla
```

!!! info "Relación con fetch()"
  `fetch()` **devuelve una promesa**.
  Por eso usamos `.then()` o `async/await` para indicar qué hacer **cuando la respuesta llegue**.
  Mientras tanto, el código principal sigue funcionando normalmente.

---

## 📌 Uso básico de fetch()

`fetch()` se utiliza para **realizar peticiones HTTP** (por ejemplo, obtener datos en formato JSON desde una API).

```js
fetch("https://jsonplaceholder.typicode.com/users")
  .then(respuesta => respuesta.json()) // convierte la respuesta a JSON
  .then(datos => console.log(datos))    // usa los datos
  .catch(error => console.error("Error:", error)); // maneja errores
```

!!! note "Importante"
  `fetch()` no lanza un error si el servidor responde con un código HTTP 404 o 500.
  Solo lanza error real si **no puede conectarse** (por ejemplo, falta de red).

---

## 📌 Versión moderna con async/await

La forma más legible de trabajar con `fetch()` es usando las palabras clave `async` y `await`, que permiten escribir código **asíncrono con aspecto secuencial**.

```js
async function cargarUsuarios() {
  try {
    const respuesta = await fetch("https://jsonplaceholder.typicode.com/users");

    // Comprobamos si la respuesta HTTP es correcta
    if (!respuesta.ok) {
      throw new Error(`Error HTTP: ${respuesta.status}`);
    }

    const datos = await respuesta.json();
    console.log("Usuarios cargados:", datos);
  } catch (error) {
    console.error("Error al cargar los datos:", error.message);
  } finally {
    console.log("Petición finalizada ✅");
  }
}

cargarUsuarios();
```

### 🔍 Explicación paso a paso

1. `async` indica que la función trabajará con operaciones asíncronas.
2. `await` **pausa la ejecución** hasta que la promesa se resuelva.
3. Si ocurre un error (por ejemplo, servidor caído o código 404), `throw` lo envía directamente al bloque `catch`.
4. El bloque `finally` se ejecuta siempre, ocurra o no un error.

---

!!! tip "Ventajas de async/await"
  - Código más **limpio y legible** que con `.then()` anidados.
  - Manejo de errores más **estructurado** con `try...catch`.
  - Permite mezclar código síncrono y asíncrono de forma natural.
  - Es la **forma recomendada** de trabajar con APIs modernas.

---

## 📌 Envío de datos con fetch()

También puedes **enviar información** al servidor (por ejemplo, en formato JSON) usando el método `POST`.

```js
async function enviarDatos() {
  const nuevoUsuario = {
    nombre: "Laura",
    email: "laura@example.com"
  };

  try {
    const respuesta = await fetch("https://jsonplaceholder.typicode.com/users", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(nuevoUsuario)
    });

    if (!respuesta.ok) {
      throw new Error("Error al enviar los datos");
    }

    const datos = await respuesta.json();
    console.log("Usuario creado:", datos);
  } catch (error) {
    console.error("Error:", error.message);
  }
}

enviarDatos();
```

---

## 🧠 Resumen

* `fetch()` **devuelve una promesa**.
* Puede manejarse con `.then()` o con `async/await`.
* Sirve para **obtener o enviar** información a través de la red.
* Se recomienda siempre **comprobar `respuesta.ok`** y manejar errores con `try...catch`.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
  1. ¿Qué representa una promesa en JavaScript?
  2. ¿Qué diferencia hay entre los estados `fulfilled` y `rejected`?
  3. ¿Qué hace `await` dentro de una función `async`?
  4. ¿Por qué es buena práctica comprobar `respuesta.ok`?
  5. ¿Cómo puedes enviar datos al servidor con `fetch()`?
