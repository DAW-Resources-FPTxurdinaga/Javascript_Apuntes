# 4.2.5 Validar otros tipos de campo

Hasta ahora hemos validado sobre todo campos de texto (`text`, `email`, `number`, `password`). Pero un formulario real suele tener también **casillas de verificación**, **botones de opción**, **desplegables**, **áreas de texto** o **fechas**.

La forma de trabajar es la misma que ya conoces (atributos HTML5 + `validity` + `setCustomValidity()`), pero cada tipo de campo tiene sus particularidades: algunos se validan solo con HTML y otros necesitan algo de lógica en JavaScript.

---

## 📌 Checkbox único

Es el caso típico de *"Acepto las condiciones de uso"*. Con `required`, el campo es inválido mientras **no esté marcado**, y se activa `valueMissing`.

```html
<form id="registro" novalidate>
  <label>
    <input type="checkbox" id="condiciones" required>
    Acepto las condiciones de uso
  </label>
  <button type="submit">Enviar</button>
</form>
```

```js
const condiciones = document.getElementById("condiciones");

const validarCondiciones = function () {
  condiciones.setCustomValidity("");

  if (condiciones.validity.valueMissing) {
    condiciones.setCustomValidity("Debes aceptar las condiciones para continuar");
  }
};

condiciones.addEventListener("change", validarCondiciones);
```

Para saber desde JavaScript si una casilla está marcada se usa la propiedad **`checked`** (no `value`):

```js
console.log(condiciones.checked); // true o false
```

!!! note "`value` en un checkbox"
    La propiedad `value` de un checkbox **no cambia** al marcarlo o desmarcarlo: siempre devuelve el valor de su atributo `value` (o `"on"` si no lo tiene).
    Para saber si está marcado, utiliza siempre `checked`.

---

## 📌 Radio buttons

Los botones de opción se agrupan por su atributo **`name`**: dentro de un grupo solo se puede marcar uno.
Basta con poner `required` en **uno** de ellos para que todo el grupo sea obligatorio; si no hay ninguno marcado, **todos** los del grupo tienen `valueMissing`.

```html
<fieldset>
  <legend>Turno</legend>
  <label><input type="radio" name="turno" value="manana" required> Mañana</label>
  <label><input type="radio" name="turno" value="tarde"> Tarde</label>
</fieldset>
```

Para mostrar un mensaje propio, se lo asignamos al **primer** botón del grupo, que es donde el navegador mostrará el aviso:

```js
const formulario = document.getElementById("registro");
const radiosTurno = document.querySelectorAll('input[name="turno"]');

const validarTurno = function () {
  radiosTurno[0].setCustomValidity("");

  if (radiosTurno[0].validity.valueMissing) {
    radiosTurno[0].setCustomValidity("Elige un turno");
  }
};

radiosTurno.forEach((radio) => radio.addEventListener("change", validarTurno));
```

Para saber qué opción se ha elegido, la forma más cómoda es acceder al grupo a través de `formulario.elements` usando su `name`:

```js
console.log(formulario.elements.turno.value); // "manana", "tarde" o "" si no hay ninguno marcado
```

!!! tip "Agrupa con `fieldset` y `legend`"
    Envolver los grupos de radios y checkboxes en un `<fieldset>` con su `<legend>` no es obligatorio, pero mejora la **accesibilidad**: los lectores de pantalla leen la pregunta (`legend`) junto a cada opción.

---

## 📌 Desplegables (`select`)

En un `<select>` siempre hay alguna opción seleccionada, así que para que `required` tenga efecto la **primera opción** debe tener `value=""`. Esa opción hace de texto de ayuda (*"-- Elige una provincia --"*) y, mientras esté seleccionada, el campo tiene `valueMissing`.

```html
<label for="provincia">Provincia:</label>
<select id="provincia" required>
  <option value="">-- Elige una provincia --</option>
  <option value="araba">Araba</option>
  <option value="bizkaia">Bizkaia</option>
  <option value="gipuzkoa">Gipuzkoa</option>
</select>
```

```js
const provincia = document.getElementById("provincia");

const validarProvincia = function () {
  provincia.setCustomValidity("");

  if (provincia.validity.valueMissing) {
    provincia.setCustomValidity("Selecciona una provincia");
  }
};

provincia.addEventListener("change", validarProvincia);
```

### Desplegables de selección múltiple

Con el atributo `multiple` se pueden elegir varias opciones (manteniendo pulsado Ctrl o Cmd). En este caso `required` exige **al menos una**, y las opciones elegidas se obtienen con `selectedOptions`:

```html
<select id="idiomas" multiple required>
  <option value="eu">Euskera</option>
  <option value="es">Castellano</option>
  <option value="en">Inglés</option>
  <option value="fr">Francés</option>
</select>
```

```js
const idiomas = document.getElementById("idiomas");

const validarIdiomas = function () {
  idiomas.setCustomValidity("");

  if (idiomas.selectedOptions.length === 0) {
    idiomas.setCustomValidity("Selecciona al menos un idioma");
  } else if (idiomas.selectedOptions.length > 2) {
    idiomas.setCustomValidity("Puedes seleccionar como máximo 2 idiomas");
  }
};
```

Fíjate en que el **máximo** de opciones no se puede indicar con ningún atributo HTML, así que lo comprobamos nosotros contando `selectedOptions`.

---

## 📌 Áreas de texto (`textarea`)

Un `<textarea>` admite `required`, `minlength` y `maxlength`, igual que un `input` de texto. Sin embargo, **no admite el atributo `pattern`**.
Si necesitamos comprobar un formato, usamos una expresión regular desde JavaScript (repasa el apartado 4.2.4):

```html
<label for="comentario">Comentario:</label>
<textarea id="comentario" required minlength="10" maxlength="200"></textarea>
```

```js
const comentario = document.getElementById("comentario");
const contieneEnlace = /https?:\/\//;

const validarComentario = function () {
  comentario.setCustomValidity("");

  if (comentario.validity.valueMissing) {
    comentario.setCustomValidity("Escribe un comentario");
  } else if (comentario.validity.tooShort) {
    comentario.setCustomValidity("El comentario debe tener al menos 10 caracteres");
  } else if (contieneEnlace.test(comentario.value)) {
    comentario.setCustomValidity("El comentario no puede contener enlaces");
  }
};

comentario.addEventListener("input", validarComentario);
```

!!! info "`maxlength` no genera errores"
    Con `maxlength` el navegador directamente **no deja escribir** más caracteres, así que `tooLong` prácticamente nunca se activa. No hace falta comprobarlo.

---

## 📌 Fechas (`date`)

Un `<input type="date">` muestra un calendario y su `value` es siempre un texto con el formato **`aaaa-mm-dd`** (por ejemplo, `"2026-10-09"`), o `""` si está vacío.
Con `min` y `max` se puede limitar el rango, y se activan `rangeUnderflow` y `rangeOverflow`:

```html
<label for="cita">Fecha de la cita:</label>
<input type="date" id="cita" required min="2026-01-01" max="2026-12-31">
```

### Fechas relativas al día de hoy

Muchas veces el límite depende de la **fecha actual**: *"la fecha no puede ser futura"* o *"debes ser mayor de edad"*. Como esos valores cambian cada día, no podemos escribirlos en el HTML.

La solución más sencilla es **calcular la fecha límite con JavaScript y asignarla al atributo `max`** al cargar la página. A partir de ahí, la validación la hace el propio navegador (repasa el objeto `Date` en el apartado 2.4):

```html
<label for="nacimiento">Fecha de nacimiento:</label>
<input type="date" id="nacimiento" required>
```

```js
const nacimiento = document.getElementById("nacimiento");

// Convierte un objeto Date al formato "aaaa-mm-dd" que usan los campos date
const formatearFecha = function (fecha) {
  const anio = fecha.getFullYear();
  const mes = String(fecha.getMonth() + 1).padStart(2, "0");
  const dia = String(fecha.getDate()).padStart(2, "0");
  return `${anio}-${mes}-${dia}`;
};

// Fecha de hoy, pero hace 18 años
const hoy = new Date();
const limite = new Date(hoy.getFullYear() - 18, hoy.getMonth(), hoy.getDate());
nacimiento.max = formatearFecha(limite);

const validarNacimiento = function () {
  nacimiento.setCustomValidity("");

  if (nacimiento.validity.valueMissing || nacimiento.validity.badInput) {
    nacimiento.setCustomValidity("Introduce una fecha completa");
  } else if (nacimiento.validity.rangeOverflow) {
    nacimiento.setCustomValidity("Debes ser mayor de edad");
  }
};

nacimiento.addEventListener("input", validarNacimiento);
```

!!! warning "No uses `toISOString()` para formatear la fecha"
    `toISOString()` devuelve la fecha en **hora UTC**, no en la hora local. Cerca de la medianoche puede darte el día anterior o el siguiente.
    Por eso construimos el texto `aaaa-mm-dd` a mano con `getFullYear()`, `getMonth()` y `getDate()`.

---

## 📌 Grupo de checkboxes: "elige al menos uno"

Este es el único caso de la página que **HTML no puede validar por sí solo**. Si ponemos `required` en un grupo de checkboxes, el navegador exigiría marcar **todos**, porque cada checkbox es un campo independiente (a diferencia de los radios, que comparten `name`).

Por eso no usamos `required` y escribimos la lógica nosotros: contamos cuántos hay marcados y, si no hay ninguno, asignamos el error al **primero** del grupo.

```html
<fieldset>
  <legend>Intereses (elige al menos uno)</legend>
  <label><input type="checkbox" name="intereses" value="frontend"> Front-end</label>
  <label><input type="checkbox" name="intereses" value="backend"> Back-end</label>
  <label><input type="checkbox" name="intereses" value="diseno"> Diseño</label>
</fieldset>
```

```js
const intereses = document.querySelectorAll('input[name="intereses"]');

const validarIntereses = function () {
  const marcados = document.querySelectorAll('input[name="intereses"]:checked');

  if (marcados.length === 0) {
    intereses[0].setCustomValidity("Elige al menos un interés");
  } else {
    intereses[0].setCustomValidity("");
  }
};

intereses.forEach((casilla) => casilla.addEventListener("change", validarIntereses));
```

Para obtener los valores elegidos, recorremos los marcados:

```js
const elegidos = [...document.querySelectorAll('input[name="intereses"]:checked')]
  .map((casilla) => casilla.value);

console.log(elegidos); // por ejemplo: ["frontend", "diseno"]
```

!!! note "Por qué el error se pone en el primer checkbox"
    `setCustomValidity()` solo se puede aplicar a un campo concreto, no a un grupo. Al ponerlo en el primero, el formulario pasa a ser inválido (`checkValidity()` devuelve `false`) y `reportValidity()` muestra el aviso junto a esa casilla.
    Fíjate en que aquí **no hay ningún atributo HTML implicado**: el error depende únicamente de nuestro `setCustomValidity()`.

---

## 📌 Otros campos que conviene conocer

| Campo | Qué valida HTML | Qué hay que hacer con JavaScript |
|-------|-----------------|----------------------------------|
| `type="url"` | Que tenga formato de URL (`typeMismatch`) | Normalmente nada más |
| `type="tel"` | **Nada**: acepta cualquier texto | Añadir un `pattern`, por ejemplo `[0-9]{9}` |
| `type="password"` | `required`, `minlength`, `pattern` | Comprobar que coincide con el campo *"repetir contraseña"* |
| `type="file"` | Solo `required` | Comprobar el tipo y el tamaño del archivo con `campo.files[0].type` y `campo.files[0].size` |
| `type="range"` / `type="color"` | Siempre tienen un valor | Normalmente no necesitan validación |

!!! warning "`accept` no valida archivos"
    En un `<input type="file" accept="image/*">`, el atributo `accept` solo **filtra** lo que se muestra en el selector de archivos, pero el usuario puede elegir otro tipo de archivo igualmente. Si el tipo es importante, compruébalo con JavaScript (y, por supuesto, en el servidor).

---

## 📌 ¿`input` o `change`?

En los apartados anteriores revalidábamos los campos de texto con el evento `input`, que se lanza con cada tecla pulsada.
En **checkboxes, radios y desplegables** lo habitual es usar **`change`**, que se lanza cuando el usuario marca, desmarca o elige una opción.

| Campo | Evento recomendado |
|-------|--------------------|
| `input` de texto, `email`, `number`, `textarea`... | `input` |
| `checkbox`, `radio`, `select` | `change` |
| `date` | `input` o `change` |

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué propiedad usarías para saber si un checkbox está marcado? ¿Por qué no sirve `value`?
    2. ¿En cuántos radio buttons de un grupo hay que poner `required` para que el grupo sea obligatorio?
    3. ¿Qué tiene que tener la primera opción de un `select` para que `required` funcione?
    4. ¿Por qué no se puede validar con `required` un grupo de checkboxes en el que hay que marcar al menos uno? ¿Cómo lo resolverías?
    5. Escribe el código necesario para que un campo `date` no admita fechas futuras.
