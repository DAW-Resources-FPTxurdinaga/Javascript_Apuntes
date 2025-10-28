# 4.2.2 Validación personalizada con JavaScript

Aunque HTML5 ofrece una validación automática con atributos como `required`, `minlength` o `pattern`, en muchos casos es necesario tener **más control**: mostrar mensajes personalizados, validar condiciones específicas o definir comportamientos diferentes según el contexto.

Para eso, JavaScript nos permite acceder y gestionar la **Constraint Validation API**, con la que podemos comprobar, mostrar o anular los errores de validación antes de que el formulario se envíe.

---

## 📌 Desactivar la validación automática

Cuando vamos a controlar la validación manualmente desde JavaScript, es recomendable **desactivar los mensajes nativos** del navegador.
Esto se hace con el atributo `novalidate` en el formulario.

```html
<form id="registro" novalidate>
  <input type="text" id="usuario" required minlength="4" placeholder="Usuario">
  <button type="submit">Enviar</button>
</form>
```

!!! info "¿Por qué usar `novalidate`?"
    Si no se usa `novalidate`, el navegador mostrará sus propios mensajes (“Rellene este campo”, “Introduzca un email válido…”) al mismo tiempo que los tuyos.
    Esto puede resultar confuso para el usuario.

---

## 📌 Interceptar el envío del formulario

El evento `submit` permite **comprobar la validez de todos los campos** antes de enviar el formulario.
Si algún campo no cumple las condiciones, se puede **bloquear el envío** con `preventDefault()`.

```html
<form id="registro" novalidate>
  <input type="email" id="correo" required placeholder="Correo electrónico">
  <button type="submit">Registrar</button>
</form>

<script>
  const form = document.getElementById("registro");

  form.addEventListener("submit", (e) => {
    if (!form.checkValidity()) {
      e.preventDefault(); // Bloquea el envío si hay errores
      form.reportValidity(); // Muestra los mensajes del navegador
    }
  });
</script>
```

!!! note "Diferencia entre `checkValidity()` y `reportValidity()`"
    - `checkValidity()` → devuelve `true` o `false`, pero **no muestra mensajes**.
    - `reportValidity()` → hace lo mismo, pero **muestra los mensajes nativos** de los campos no válidos.

---

## 📌 Personalizar y mostrar mensajes con setCustomValidity() y reportValidity()

Podemos sobrescribir los mensajes del navegador con setCustomValidity() y, a continuación, mostrarlos directamente usando reportValidity().

Esto nos permite ofrecer una validación completa e inmediata, sin necesidad de enviar el formulario.

```
<form id="registro" novalidate>
  <input type="number" id="edad" required min="18" max="99" placeholder="Edad (18–99)">
  <button type="button" id="comprobar">Comprobar</button>
</form>

<script>
  const edad = document.getElementById("edad");
  const boton = document.getElementById("comprobar");

  function validarCampo(idCampo) {
    const input = document.getElementById(idCampo);
    const validez = input.validity;

    // Limpiamos siempre el mensaje previo
    input.setCustomValidity("");

    if (validez.valueMissing) {
      input.setCustomValidity("Este campo es obligatorio");
    } else if (validez.rangeUnderflow) {
      input.setCustomValidity("La edad debe ser mayor o igual a 18");
    } else if (validez.rangeOverflow) {
      input.setCustomValidity("La edad debe ser menor o igual a 99");
    }

    // Mostramos el mensaje si hay algún error
    input.reportValidity();
  }

  boton.addEventListener("click", () => validarCampo("edad"));
</script>
```

!!! info "Cuándo usar reportValidity()"
    reportValidity() es ideal para mostrar los mensajes sin enviar el formulario:
    - Al pulsar un botón “Comprobar” o “Verificar”.
    - Al abandonar un campo (blur).
    - O cuando queremos validar un solo campo dentro de un formulario grande.

!!! note "Consejo práctico"
    Siempre que uses setCustomValidity(), recuerda limpiar el mensaje anterior con setCustomValidity("").
    Si no lo haces, el campo seguirá marcado como inválido incluso después de corregir el error.

---

## 📌 El objeto `validity`

Cada campo del formulario incluye la propiedad `.validity`, un objeto con **indicadores booleanos** que describen por qué el campo no es válido.

```html
<input type="email" id="correo" required placeholder="Introduce tu email">
```

```js
const correo = document.getElementById("correo");

correo.addEventListener("input", () => {
  console.log(correo.validity);
});
```

Este objeto contiene propiedades como:

| Propiedad              | Significado                                             |
| ---------------------- | ------------------------------------------------------- |
| `valueMissing`         | El campo está vacío y es obligatorio                    |
| `typeMismatch`         | El valor no coincide con el tipo (`email`, `url`, etc.) |
| `tooShort` / `tooLong` | No cumple con la longitud establecida                   |
| `patternMismatch`      | No coincide con el patrón definido                      |
| `valid`                | Es `true` si el campo cumple todas las condiciones      |

Ejemplo simple de uso:

```js
if (correo.validity.valueMissing) {
  correo.setCustomValidity("El correo es obligatorio");
} else if (correo.validity.typeMismatch) {
  correo.setCustomValidity("Por favor, introduce un email válido");
} else {
  correo.setCustomValidity("");
}
```

---

## 📌 Validar con `pattern`

El atributo `pattern` permite definir **expresiones regulares** para establecer formatos personalizados.

```html
<input 
  type="text" 
  id="usuario" 
  pattern="[A-Za-z0-9]+" 
  required 
  placeholder="Solo letras y números">
```

```js
const usuario = document.getElementById("usuario");

usuario.addEventListener("input", () => {
  usuario.setCustomValidity(""); // Limpia el error previo

  if (usuario.validity.patternMismatch) {
    usuario.setCustomValidity("Solo se permiten letras y números, sin espacios");
  }
});
```

---

## 📌 Validación en cliente y en servidor

La validación en el cliente (HTML5 + JavaScript) mejora la **experiencia del usuario**, pero **no garantiza la seguridad**.
Cualquier persona podría manipular los datos antes de enviarlos al servidor.


Por eso, toda aplicación debe tener:

  1. **Validación en el cliente** → rápida, visual y preventiva.  
  2. **Validación en el servidor** → obligatoria y definitiva, para proteger los datos y evitar ataques.


---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué atributo HTML evita que el navegador muestre sus propios mensajes de error?
    2. ¿Qué diferencia hay entre `checkValidity()` y `reportValidity()`?
    3. ¿Qué método permite establecer un mensaje personalizado de error?
    4. ¿Qué sucede si no limpias el mensaje de `setCustomValidity()` después de corregir el error?
    5. ¿Por qué es importante validar también los datos en el servidor?
