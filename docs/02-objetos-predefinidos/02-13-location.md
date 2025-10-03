# 3.6 Location

El objeto **`location`** forma parte de **`window`** y proporciona información sobre la **URL de la página actual**, además de métodos para **redirigir** o **recargar** la página.
Cada vez que accedes o modificas sus propiedades, estás trabajando con la dirección en la que se encuentra tu documento.

---

## 📌 Propiedades principales

```js
// URL completa
console.log(location.href);  

// Protocolo (http, https, file...)
console.log(location.protocol);  

// Nombre de dominio
console.log(location.hostname);  

// Puerto utilizado (si existe en la URL)
console.log(location.port);  

// Ruta después del dominio
console.log(location.pathname);  

// Parámetros de la URL (query string)
console.log(location.search);  

// Fragmento o ancla (#)
console.log(location.hash);  
```

---

## 📌 Métodos principales

### Recargar la página

```js
// Recarga desde caché
location.reload();  

// Recarga desde el servidor (forzado)
location.reload(true);
```

### Redireccionar a otra URL

```js
// Redirige a otra página
location.href = "https://www.mozilla.org";

// Equivalente usando assign()
location.assign("https://www.mozilla.org");

// Reemplaza la URL actual (no guarda en el historial)
location.replace("https://www.mozilla.org");
```

---

!!! info "Diferencia entre assign() y replace()"
    - `assign(url)`: cambia la página y **mantiene la actual en el historial** (puedes volver con el botón Atrás).
    - `replace(url)`: cambia la página pero **no guarda la actual en el historial**.

---

## 📌 Ejemplo práctico

```js
// Comprobar si estamos en HTTPS
if (location.protocol !== "https:") {
  console.log("¡Aviso! La conexión no es segura.");
}
```

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué propiedad usarías para obtener el dominio de la página actual?
    2. ¿Qué diferencia hay entre `assign()` y `replace()`?
    3. ¿Qué devuelve `location.search` si la URL es `https://ejemplo.com/index.html?id=5`?
    4. ¿Qué método usarías para forzar una recarga desde el servidor?
    5. ¿Qué pasa si asignas un valor a `location.href`?
