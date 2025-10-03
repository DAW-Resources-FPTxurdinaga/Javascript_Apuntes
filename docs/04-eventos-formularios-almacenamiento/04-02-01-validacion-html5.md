# 4.2.1 Validación con HTML5

HTML5 incorpora una serie de atributos que permiten validar formularios **sin necesidad de escribir JavaScript**.
Estos atributos aseguran que los datos introducidos cumplen unos requisitos mínimos antes de enviar el formulario.

La validación con HTML5 es **rápida y sencilla**, pero se puede complementar con JavaScript para personalizar los mensajes y el comportamiento.

---

## 📌 Atributos de validación más comunes

### required

Obliga a que el campo no esté vacío.

```html
<input type="text" required placeholder="Nombre">
```

### type

Define el tipo de dato esperado (`email`, `number`, `url`, `date`, etc.).
El navegador comprobará automáticamente que el formato sea correcto.

```html
<input type="email" required placeholder="Correo electrónico">
```

### min y max

Restringen un rango de valores (para `number`, `date`, etc.).

```html
<input type="number" min="18" max="99" required>
```

### minlength y maxlength

Definen la longitud mínima y máxima de texto.

```html
<input type="password" minlength="6" maxlength="12" required>
```

### pattern

Permite usar una **expresión regular** para validar el contenido.

```html
<input type="text" pattern="[A-Za-z]+" title="Solo letras permitidas">
```

---

## 📌 API de validación de formularios

Además de los atributos, HTML5 incluye métodos que permiten interactuar con el formulario desde JavaScript:

### checkValidity()

Devuelve `true` si todos los campos cumplen las reglas de validación.

```html
<form id="miFormulario">
  <input type="email" required>
  <button type="submit">Enviar</button>
</form>

<script>
  const form = document.getElementById("miFormulario");
  console.log(form.checkValidity()); // true o false
</script>
```

### reportValidity()

Muestra los mensajes de error nativos del navegador si hay campos inválidos.

```js
form.reportValidity(); // Muestra un mensaje si algún campo es incorrecto
```

---

!!! note "Mensajes del navegador"
    Los navegadores modernos muestran mensajes automáticos en el idioma configurado del sistema (por ejemplo, *“Rellene este campo”*).
    Estos mensajes no siempre se pueden personalizar con HTML5, por eso a menudo se complementan con JavaScript.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué atributo utilizarías para que un campo de texto sea obligatorio?
    2. ¿Cómo puedes limitar un campo `number` para que solo acepte valores entre 1 y 10?
    3. ¿Qué diferencia hay entre `checkValidity()` y `reportValidity()`?
    4. ¿Cómo podrías validar que un campo solo acepte letras usando HTML5?
