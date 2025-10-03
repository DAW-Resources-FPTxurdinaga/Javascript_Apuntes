# 4.2.2 Validación personalizada con JavaScript

Aunque HTML5 permite validar formularios de forma básica con sus atributos, en muchos casos se necesita **más control**: mostrar mensajes propios, validar condiciones específicas o aplicar estilos personalizados a los campos.

Para esto utilizamos **JavaScript moderno** junto con la API de validación.

---

## 📌 Interceptar el envío del formulario

Podemos usar el evento `submit` para **detener el envío** si los datos no son correctos.

```html
<form id="registro">
  <input type="text" id="usuario" required placeholder="Nombre de usuario">
  <input type="password" id="clave" required minlength="6" placeholder="Contraseña">
  <button type="submit">Registrar</button>
</form>

<script>
  const form = document.getElementById("registro");

  form.addEventListener("submit", (e) => {
    if (!form.checkValidity()) {
      e.preventDefault(); // Bloquea el envío si hay errores
      alert("Por favor, revisa los campos antes de enviar.");
    }
  });
</script>
```

---

## 📌 Mensajes personalizados con setCustomValidity()

Podemos **reemplazar** los mensajes genéricos del navegador.

```html
<input type="password" id="clave" required minlength="6" placeholder="Contraseña">

<script>
  const clave = document.getElementById("clave");

  clave.addEventListener("input", () => {
    if (clave.value.length < 6) {
      clave.setCustomValidity("La contraseña debe tener al menos 6 caracteres");
    } else {
      clave.setCustomValidity(""); // Limpia el error
    }
  });
</script>
```

---

## 📌 Ejemplo: Confirmar contraseñas

Un caso muy común es validar que **dos contraseñas coinciden**.

```html
<form id="registro">
  <input type="password" id="clave1" placeholder="Contraseña" required>
  <input type="password" id="clave2" placeholder="Repite la contraseña" required>
  <button type="submit">Registrar</button>
</form>

<script>
  const clave1 = document.getElementById("clave1");
  const clave2 = document.getElementById("clave2");

  clave2.addEventListener("input", () => {
    if (clave1.value !== clave2.value) {
      clave2.setCustomValidity("Las contraseñas no coinciden");
    } else {
      clave2.setCustomValidity("");
    }
  });
</script>
```

---

## 📌 El objeto validity

Cada campo de formulario tiene la propiedad `.validity`, que devuelve un objeto con **banderas booleanas** que indican por qué un campo no es válido.

Las más comunes son:

* `valueMissing`: el campo está vacío y es obligatorio.
* `typeMismatch`: el valor no coincide con el tipo (`email`, `url`, etc.).
* `tooShort` o `tooLong`: el valor no cumple con la longitud mínima o máxima.
* `patternMismatch`: el valor no coincide con el patrón definido en `pattern`.
* `valid`: es `true` si el campo cumple todas las condiciones.

```html
<input type="email" id="correo" required placeholder="Introduce tu email">

<script>
  const correo = document.getElementById("correo");

  correo.addEventListener("input", () => {
    if (correo.validity.valueMissing) {
      correo.setCustomValidity("El correo es obligatorio");
    } else if (correo.validity.typeMismatch) {
      correo.setCustomValidity("Por favor, introduce un email válido");
    } else {
      correo.setCustomValidity("");
    }
  });
</script>
```

---

## 📌 Ejemplo con pattern

Con el atributo `pattern` podemos definir **expresiones regulares** para validar un formato específico.
Por ejemplo, supongamos que queremos que el **usuario solo contenga letras y números** (sin espacios ni caracteres especiales).

```html
<form id="registro">
  <input 
    type="text" 
    id="usuario" 
    pattern="[A-Za-z0-9]+" 
    required 
    placeholder="Nombre de usuario (solo letras y números)">
  <button type="submit">Registrar</button>
</form>

<script>
  const usuario = document.getElementById("usuario");

  usuario.addEventListener("input", () => {
    if (usuario.validity.patternMismatch) {
      usuario.setCustomValidity("El nombre solo puede contener letras y números, sin espacios");
    } else {
      usuario.setCustomValidity("");
    }
  });
</script>
```

---

## 📌 Validar en cliente y en servidor

!!! warning "No basta con validar en el cliente"
    La validación con JavaScript es útil para mejorar la **experiencia del usuario**: evita envíos innecesarios, muestra mensajes inmediatos y guía al usuario a rellenar bien los campos.
    Sin embargo, **no es suficiente**.
    Un usuario avanzado puede desactivar JavaScript o manipular los datos antes de enviarlos.

    Por eso, siempre se recomienda:

    1. **Validación en el cliente** → rápida, amigable y visual.
    2. **Validación en el servidor** → obligatoria, garantiza que los datos que llegan cumplen con las reglas de seguridad y formato.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué evento se utiliza para detener el envío de un formulario?
    2. ¿Qué método sirve para mostrar un mensaje de error personalizado en un campo?
    3. ¿Cómo puedes comprobar con JavaScript si un email tiene un formato válido?
    4. ¿Qué atributo HTML5 se usa para validar un formato con expresiones regulares?
    5. ¿Por qué es necesario validar también en el servidor?
