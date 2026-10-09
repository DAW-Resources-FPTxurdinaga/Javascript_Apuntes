# 4.2.5 Ejemplo completo: formulario de registro

En este ejemplo práctico vas a juntar todo lo visto en los apartados anteriores para validar un **formulario de registro** completo: atributos de validación de HTML5, el objeto `validity`, mensajes personalizados con `setCustomValidity()` y el control del envío con `checkValidity()` y `reportValidity()`.

El formulario tiene tres campos:

| Campo | Condiciones |
|-------|-------------|
| Usuario | Obligatorio, al menos 4 caracteres, solo letras, números y espacios |
| Correo | Obligatorio, con formato de correo electrónico válido |
| Edad | Obligatoria, número entero entre 18 y 99 |

---

## 📂 Estructura del proyecto

```
validacion-registro/
├── index.html
└── validacion.js
```

---

## 📝 Paso 1: el formulario HTML

Crea un archivo `index.html` con el siguiente contenido:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Formulario de registro</title>
  <script src="validacion.js" defer></script>
</head>
<body>
  <h1>Registro</h1>

  <form id="registro" novalidate>
    <p>
      <label for="usuario">Usuario:</label>
      <input type="text" id="usuario" name="usuario"
             required minlength="4" pattern="[A-Za-z0-9 ]+">
    </p>

    <p>
      <label for="correo">Correo electrónico:</label>
      <input type="email" id="correo" name="correo" required>
    </p>

    <p>
      <label for="edad">Edad:</label>
      <input type="number" id="edad" name="edad" required min="18" max="99" step="1">
    </p>

    <button type="button" id="comprobar">Comprobar</button>
    <button type="submit">Enviar</button>
  </form>
</body>
</html>
```

Fíjate en que:

- Las **condiciones** de cada campo se definen en el propio HTML (`required`, `minlength`, `pattern`, `type="email"`, `min`, `max`, `step`). JavaScript solo se encarga de **comprobarlas y personalizar los mensajes**.
- El formulario lleva `novalidate` para que el navegador no muestre sus mensajes automáticos al enviar.
- Hay dos botones: **Comprobar** (`type="button"`) solo revisa los datos, mientras que **Enviar** (`type="submit"`) lanza el evento `submit`.

!!! info "¿Por qué `defer`?"
    El script está en el `<head>`, así que sin `defer` se ejecutaría **antes** de que existiera el formulario y `document.getElementById("registro")` devolvería `null`.
    Con `defer`, el script espera a que el HTML se haya leído completo.

---

## 📝 Paso 2: la lógica de validación

Crea un archivo `validacion.js` con el siguiente código:

```js
// Referencias a los elementos del formulario
const formulario = document.getElementById("registro");
const usuario = document.getElementById("usuario");
const correo = document.getElementById("correo");
const edad = document.getElementById("edad");
const botonComprobar = document.getElementById("comprobar");

// ---------- Validación de cada campo ----------

const validarUsuario = function () {
  usuario.setCustomValidity(""); // Limpiamos siempre el mensaje anterior

  if (usuario.validity.valueMissing) {
    usuario.setCustomValidity("El usuario es obligatorio");
  } else if (usuario.validity.tooShort) {
    usuario.setCustomValidity("El usuario debe tener al menos 4 caracteres");
  } else if (usuario.validity.patternMismatch) {
    usuario.setCustomValidity("Solo se permiten letras, números y espacios");
  }
};

const validarCorreo = function () {
  correo.setCustomValidity("");

  if (correo.validity.valueMissing) {
    correo.setCustomValidity("El correo es obligatorio");
  } else if (correo.validity.typeMismatch) {
    correo.setCustomValidity("Introduce un correo válido, por ejemplo: nombre@dominio.com");
  }
};

const validarEdad = function () {
  edad.setCustomValidity("");

  if (edad.validity.valueMissing || edad.validity.badInput) {
    edad.setCustomValidity("La edad es obligatoria y debe ser un número");
  } else if (edad.validity.rangeUnderflow) {
    edad.setCustomValidity("Debes tener al menos 18 años");
  } else if (edad.validity.rangeOverflow) {
    edad.setCustomValidity("La edad no puede ser mayor de 99");
  } else if (edad.validity.stepMismatch) {
    edad.setCustomValidity("La edad debe ser un número entero");
  }
};

// Valida todos los campos a la vez
const validarFormulario = function () {
  validarUsuario();
  validarCorreo();
  validarEdad();
};

// ---------- Botón "Comprobar" ----------

const comprobar = function () {
  validarFormulario();
  formulario.reportValidity(); // Muestra el primer error (si lo hay)
};

// ---------- Envío del formulario ----------

const enviar = function (e) {
  e.preventDefault(); // En este ejemplo no enviamos datos a ningún servidor

  validarFormulario(); // Actualizamos los mensajes antes de comprobar

  if (!formulario.checkValidity()) {
    formulario.reportValidity();
  } else {
    alert("¡Registro correcto!");
    formulario.reset();
  }
};

// ---------- Eventos ----------

botonComprobar.addEventListener("click", comprobar);
formulario.addEventListener("submit", enviar);

// Revalidamos cada campo mientras se escribe, para que el error
// desaparezca en cuanto el usuario lo corrige
usuario.addEventListener("input", validarUsuario);
correo.addEventListener("input", validarCorreo);
edad.addEventListener("input", validarEdad);
```

!!! warning "Valida siempre antes de comprobar"
    `checkValidity()` y `reportValidity()` solo **consultan** el estado de los campos; no ejecutan nuestras funciones `validarUsuario()`, `validarCorreo()`, etc.
    Por eso, en `enviar` llamamos primero a `validarFormulario()`. Si no lo hiciéramos, al pulsar **Enviar** sin haber pulsado antes **Comprobar** aparecerían los mensajes genéricos del navegador en lugar de los nuestros.

!!! note "¿Por qué `preventDefault()` en los dos casos?"
    En un proyecto real, si el formulario es válido dejaríamos que se enviara al servidor (o lo enviaríamos con `fetch`, como veremos en el tema 6).
    Como aquí no hay servidor, bloqueamos siempre el envío y mostramos un `alert` para comprobar que todo funciona.

---

## 📘 Conceptos aprendidos en este ejemplo

   **Una función de validación por campo**

   Cada función limpia el mensaje anterior con `setCustomValidity("")` y, después, revisa las propiedades de `validity` **en orden**, asignando un único mensaje.

   **Propiedades de `validity` utilizadas**

   | Propiedad | Atributo HTML que la provoca |
   |-----------|------------------------------|
   | `valueMissing` | `required` |
   | `tooShort` | `minlength` |
   | `patternMismatch` | `pattern` |
   | `typeMismatch` | `type="email"` |
   | `badInput` | El navegador no puede interpretar el valor (por ejemplo, texto en un `type="number"`) |
   | `rangeUnderflow` / `rangeOverflow` | `min` / `max` |
   | `stepMismatch` | `step` |

   **Tres momentos de validación**

   - Al **escribir** en un campo (`input`): se actualiza su estado sin mostrar mensajes.
   - Al pulsar **Comprobar** (`click`): se validan todos los campos y se muestra el primer error.
   - Al pulsar **Enviar** (`submit`): se validan todos los campos y solo se acepta el formulario si no hay errores.

---

## 🧪 Ejercicios para practicar

1. Añade un campo **Contraseña** (`type="password"`) que sea obligatorio y tenga al menos 8 caracteres, con su función `validarContrasena()`.
2. Añade un campo **Repetir contraseña** y valida que coincida con el anterior. *Pista: aquí no hay ningún atributo HTML que lo compruebe, así que tendrás que comparar los valores y usar `setCustomValidity()` directamente.*
3. Modifica el `pattern` del usuario para que también acepte la `ñ` y las vocales con tilde.
4. Usa las pseudoclases CSS `:valid` e `:invalid` para pintar el borde de cada campo de verde o rojo (repasa el apartado 4.2.3).
5. **Reto:** organiza el código en **módulos** (apartado 3.4). Mueve las funciones de validación a un archivo `validaciones.js` que las exporte, e impórtalas desde un `main.js` que se encargue de los eventos.

---

## 🛠️ Solución de problemas

Si algo no funciona:

1. Abre la consola del navegador (F12 → pestaña "Consola") y revisa si aparece algún error.
2. Si aparece `Cannot read properties of null`, comprueba que el `<script>` tiene `defer` y que los `id` del HTML coinciden con los del JavaScript.
3. Si ves los mensajes del navegador en lugar de los tuyos, comprueba que el formulario tiene `novalidate` y que llamas a `validarFormulario()` antes de `checkValidity()`.
4. Si un campo sigue marcado como erróneo después de corregirlo, revisa que su función empieza con `setCustomValidity("")`.
