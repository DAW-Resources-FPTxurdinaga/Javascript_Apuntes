# 4.2.3 Validación en tiempo real con JavaScript

Una buena práctica en los formularios modernos es mostrar **feedback inmediato** mientras el usuario escribe, sin esperar a que pulse el botón de enviar.
Esto se logra con los eventos `input` (cuando el usuario modifica un campo) y `blur` (cuando abandona el campo).

---

## 📌 Validación con el evento input

El evento `input` se dispara **cada vez que cambia el valor de un campo**.
Podemos aprovecharlo para comprobar reglas y mostrar mensajes en el momento.

```html
<form id="form">
  <label>Email:</label>
  <input type="email" id="correo" required>
  <span id="error-correo" style="color: red;"></span>
</form>

<script>
  const correo = document.getElementById("correo");
  const errorCorreo = document.getElementById("error-correo");

  correo.addEventListener("input", () => {
    if (correo.validity.valueMissing) {
      errorCorreo.textContent = "El correo es obligatorio";
    } else if (correo.validity.typeMismatch) {
      errorCorreo.textContent = "Introduce un formato de correo válido";
    } else {
      errorCorreo.textContent = "";
    }
  });
</script>
```

---

## 📌 Validación con el evento blur

El evento `blur` se activa cuando el usuario **abandona un campo**.
Es útil para no molestar con mensajes mientras escribe, pero sí avisar si deja un error atrás.

```html
<input type="text" id="usuario" required minlength="4" placeholder="Usuario">
<span id="error-usuario" style="color: red;"></span>

<script>
  const usuario = document.getElementById("usuario");
  const errorUsuario = document.getElementById("error-usuario");

  usuario.addEventListener("blur", () => {
    if (usuario.validity.valueMissing) {
      errorUsuario.textContent = "El nombre de usuario es obligatorio";
    } else if (usuario.validity.tooShort) {
      errorUsuario.textContent = "Debe tener al menos 4 caracteres";
    } else {
      errorUsuario.textContent = "";
    }
  });
</script>
```

---

## 📌 Uso de clases CSS para feedback visual

Podemos añadir clases a los campos según sean válidos o inválidos, para mejorar la experiencia visual.

```css
input:valid {
  border: 2px solid green;
}
input:invalid {
  border: 2px solid red;
}
```

Con estas reglas de CSS, **el propio navegador aplica estilos** a los campos según su validez.

---

!!! info "¿input o blur?"
    - Usa `input` si quieres mostrar feedback en tiempo real mientras escribe.
    - Usa `blur` si prefieres que el aviso aparezca solo cuando el usuario deja un campo incompleto o incorrecto.
    - Lo más común es **combinarlos**: feedback suave en tiempo real y un repaso final en el envío del formulario.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué evento se utiliza para validar mientras el usuario escribe?
    2. ¿Qué evento se dispara cuando el usuario abandona un campo de formulario?
    3. ¿Cómo aplicarías un estilo verde o rojo automáticamente a un campo válido o inválido?
    4. ¿Qué diferencia hay entre mostrar errores con `input` y con `blur`?
    5. ¿Qué propiedad de CSS puedes usar junto con HTML5 para resaltar la validez de los campos sin escribir JavaScript?
