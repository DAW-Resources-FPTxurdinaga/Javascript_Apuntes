# 3.4 Screen

El objeto **`screen`** forma parte de **`window`** y proporciona información acerca de la **pantalla física del dispositivo** en el que se ejecuta la página web.
A diferencia de `innerWidth` o `innerHeight` (que miden el área visible de la ventana del navegador), `screen` ofrece datos de **toda la pantalla**.

---

## 📌 Propiedades principales de `screen`

### Tamaño total de la pantalla

```js
console.log(screen.width);   // Anchura total de la pantalla en píxeles
console.log(screen.height);  // Altura total de la pantalla en píxeles
```

### Área disponible para el navegador

```js
console.log(screen.availWidth);   // Anchura disponible, sin contar barras del sistema operativo
console.log(screen.availHeight);  // Altura disponible
```

### Profundidad de color

```js
console.log(screen.colorDepth);  // Bits por píxel (ej. 24 para 16 millones de colores)
```

### Orientación de la pantalla

Muchos navegadores incluyen la propiedad `orientation`, que indica si la pantalla está en **vertical** o **horizontal**.

```js
console.log(screen.orientation.type); // "landscape-primary" o "portrait-primary"
```

---

## 📌 Diferencia entre `window` y `screen`

* `window.innerWidth` / `window.innerHeight`: se refieren al **tamaño de la ventana del navegador** (el área donde se dibuja la web).
* `screen.width` / `screen.height`: se refieren al **tamaño físico de la pantalla completa**.

!!! info "Importante"
    Para diseñar interfaces web **adaptables**, normalmente se usa `window.innerWidth` y `window.innerHeight`, no `screen.width`.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre `screen.width` y `window.innerWidth`?
    2. ¿Qué devuelve `screen.colorDepth`?
    3. ¿Qué utilidad tienen las propiedades `availWidth` y `availHeight`?
    4. ¿Cómo puedes saber si la pantalla está en orientación vertical u horizontal?
    5. ¿Por qué en diseño responsive suele ser más importante usar `window` que `screen`?
