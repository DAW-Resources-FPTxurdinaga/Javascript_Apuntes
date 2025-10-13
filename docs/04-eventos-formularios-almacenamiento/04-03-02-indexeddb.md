# 4.3.2 IndexedDB: almacenamiento avanzado en el navegador

El objeto `IndexedDB` permite almacenar **grandes cantidades de datos estructurados** directamente en el navegador.
A diferencia de `localStorage` o `sessionStorage`, que solo guardan texto, **IndexedDB** permite almacenar **objetos completos**, realizar **búsquedas por índice** y gestionar los datos de forma **asíncrona**.

---

## 📌 ¿Qué es IndexedDB?

**IndexedDB** es una base de datos orientada a objetos integrada en los navegadores.
Permite guardar información compleja (como objetos, listas o archivos) de forma persistente y eficiente, incluso sin conexión a internet.

!!! info "Ventajas principales"
    - Permite guardar **grandes volúmenes** de datos (decenas de MB o más).
    - Soporta **objetos complejos**, no solo texto.
    - Es **asíncrona**, evitando bloquear la interfaz.
    - Permite **búsquedas e índices** como una base de datos real.
    - Los datos **persisten** entre sesiones.

---

## 📌 Apertura o creación de una base de datos

El primer paso es abrir (o crear) una base de datos con `indexedDB.open()`.

```js
// Abrir o crear la base de datos "miBD" versión 1
let request = indexedDB.open("miBD", 1);
```

El método devuelve un **objeto de solicitud** (`IDBOpenDBRequest`) que dispara varios eventos:

* `onupgradeneeded`: se ejecuta la **primera vez** o cuando se cambia la versión.
* `onsuccess`: cuando la base de datos se abre correctamente.
* `onerror`: si ocurre un error.

---

## 📌 Crear un almacén de objetos (object store)

El **almacén de objetos** (`object store`) es el equivalente a una tabla.
Se define dentro del evento `onupgradeneeded`.

```js
request.onupgradeneeded = (e) => {
  const db = e.target.result;
  
  // Creamos un almacén llamado "personas" con clave primaria "id"
  const store = db.createObjectStore("personas", { keyPath: "id" });

  console.log("Almacén 'personas' creado");
};
```

---

## 📌 Insertar datos

Para añadir datos, se usa una **transacción** (`transaction`) sobre el almacén correspondiente.

```js
request.onsuccess = (e) => {
  const db = e.target.result;
  const transaccion = db.transaction("personas", "readwrite");
  const store = transaccion.objectStore("personas");

  // Insertar objetos
  store.add({ id: 1, nombre: "Laura", edad: 30 });
  store.add({ id: 2, nombre: "Carlos", edad: 25 });

  console.log("Datos añadidos correctamente");
};
```

---

## 📌 Leer datos

Podemos obtener un elemento por su clave con `get()`:

```js
const solicitud = store.get(1);

solicitud.onsuccess = (e) => {
  console.log("Resultado:", e.target.result);
};
```

O recorrer todos los registros con un **cursor**:

```js
const cursor = store.openCursor();

cursor.onsuccess = (e) => {
  const puntero = e.target.result;
  if (puntero) {
    console.log("ID:", puntero.key, "Datos:", puntero.value);
    puntero.continue(); // Avanza al siguiente
  } else {
    console.log("Fin del recorrido");
  }
};
```

---

## 📌 Actualizar y eliminar datos

Para actualizar, basta con volver a usar `put()` con el mismo `id`.

```js
store.put({ id: 1, nombre: "Laura", edad: 31 }); // Actualiza edad
```

Y para eliminar un registro:

```js
store.delete(2); // Borra la persona con id 2
```

---

!!! note "Las transacciones son obligatorias"
    En IndexedDB **todas las operaciones se realizan dentro de una transacción**, que puede ser:

      * `"readonly"`: solo lectura.
      * `"readwrite"`: lectura y escritura.
      * `"versionchange"`: se usa solo al crear o actualizar la base de datos.

---

## 📌 Ejemplo completo

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Ejemplo IndexedDB</title>
</head>
<body>
  <h1>Gestión de personas con IndexedDB</h1>
  <button id="add">Añadir persona</button>
  <button id="show">Mostrar todas</button>

  <script>
    let db;

    // 1️⃣ Abrimos o creamos la base de datos
    const request = indexedDB.open("miBD", 1);

    // 2️⃣ Creamos el almacén si no existe
    request.onupgradeneeded = (e) => {
      db = e.target.result;
      db.createObjectStore("personas", { keyPath: "id" });
      console.log("Almacén 'personas' creado");
    };

    // 3️⃣ Conectamos con éxito
    request.onsuccess = (e) => {
      db = e.target.result;
      console.log("Base de datos abierta correctamente");
    };

    // 4️⃣ Manejamos errores
    request.onerror = (e) => {
      console.error("Error al abrir la base de datos", e);
    };

    // Botón: añadir persona
    document.getElementById("add").addEventListener("click", () => {
      const transaccion = db.transaction("personas", "readwrite");
      const store = transaccion.objectStore("personas");
      const id = Date.now();
      store.add({ id, nombre: "Usuario " + id, edad: Math.floor(Math.random() * 40) + 20 });
      console.log("Persona añadida");
    });

    // Botón: mostrar todas las personas
    document.getElementById("show").addEventListener("click", () => {
      const transaccion = db.transaction("personas", "readonly");
      const store = transaccion.objectStore("personas");
      const cursor = store.openCursor();

      cursor.onsuccess = (e) => {
        const puntero = e.target.result;
        if (puntero) {
          console.log(puntero.value);
          puntero.continue();
        } else {
          console.log("Fin de los registros");
        }
      };
    });
  </script>
</body>
</html>
```

---

## 📌 IndexedDB vs localStorage

| Característica | IndexedDB                                     | localStorage                 |
| -------------- | --------------------------------------------- | ---------------------------- |
| Tipo de datos  | Objetos, arrays, binarios                     | Solo texto                   |
| Capacidad      | Muy alta (MB o más)                           | Limitada (5–10 MB)           |
| Asincronía     | ✅ Asíncrono                                   | ❌ Síncrono                   |
| Rendimiento    | Alto                                          | Medio                        |
| Estructura     | Base de datos con índices                     | Clave–valor simple           |
| Ideal para...  | Aplicaciones complejas (PWA, catálogos, etc.) | Preferencias o datos simples |

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia principal hay entre IndexedDB y localStorage?
    2. ¿Qué es un *object store* y qué papel cumple?
    3. ¿Qué hace el evento `onupgradeneeded`?
    4. ¿Por qué IndexedDB funciona de forma asíncrona?
    5. ¿Qué tipo de transacción se necesita para modificar datos?
