# 4.2.1 Validación con HTML5

HTML5 incorpora una serie de **atributos nativos** que permiten validar formularios **sin necesidad de programar en JavaScript**.
Estos atributos ayudan a garantizar que los datos introducidos por el usuario cumplen unos **requisitos mínimos** antes de que el formulario se envíe.

La validación con HTML5 es **rápida, accesible y automática**, pero también **limitada**: si se necesitan mensajes o comportamientos personalizados, se puede complementar con JavaScript (lo veremos en la siguiente lección).

---

## 📌 Atributos de validación más comunes

### required

Obliga a que el campo no esté vacío antes de enviar el formulario.

```html
<input type="text" required placeholder="Nombre">
```

---

### type

Define el tipo de dato que se espera (`email`, `number`, `url`, `date`, etc.).
El navegador comprueba automáticamente que el formato sea correcto.

```html
<input type="email" required placeholder="Correo electrónico">
```

---

### min y max

Restringen el rango de valores numéricos o de fechas permitidos.

```html
<input type="number" min="18" max="99" required>
```

---

### minlength y maxlength

Definen la longitud mínima y máxima de los caracteres que puede contener un campo de texto.

```html
<input type="password" minlength="6" maxlength="12" required>
```

---

### pattern

Permite aplicar **expresiones regulares (RegExp)** para validar el formato del texto.
Por ejemplo, el siguiente campo solo acepta letras sin acentos ni espacios:

```html
<input type="text" pattern="[A-Za-z]+" title="Solo letras permitidas">
```

!!! note "Consejo"
    El atributo `title` es muy útil cuando se usa `pattern`, ya que el mensaje que muestra el navegador tomará el texto del `title` como pista para el usuario.

---

## 📌 ¿Qué atributo sirve para cada campo?

No todos los atributos funcionan en todos los tipos de campo. Si pones un atributo en un campo que no lo admite, el navegador simplemente **lo ignora**, sin mostrar ningún error.

| Campo | `required` | `minlength` / `maxlength` | `pattern` | `min` / `max` / `step` |
|-------|:----------:|:-------------------------:|:---------:|:----------------------:|
| `text`, `email`, `url`, `tel`, `password` | ✅ | ✅ | ✅ | ❌ |
| `number`, `range` | ✅ (`range` no) | ❌ | ❌ | ✅ |
| `date`, `time` | ✅ | ❌ | ❌ | ✅ |
| `checkbox`, `radio` | ✅ | ❌ | ❌ | ❌ |
| `file` | ✅ | ❌ | ❌ | ❌ |
| `textarea` | ✅ | ✅ | ❌ | ❌ |
| `select` | ✅ | ❌ | ❌ | ❌ |

Veremos cómo validar los checkboxes, radios, desplegables, áreas de texto y fechas en el apartado 4.2.5.

---

## 📌 Validación automática en los navegadores

Cuando el usuario intenta enviar un formulario con algún campo que no cumple las reglas establecidas, el navegador muestra un mensaje como:

> “Rellene este campo.”
> “Introduzca una dirección de correo electrónico válida.”

Estos mensajes se generan **automáticamente** según el idioma del navegador.

!!! info "Importante"
    - Los mensajes automáticos **no se pueden personalizar completamente**.
    - Para mostrar textos o estilos propios (por ejemplo, debajo del campo), será necesario complementarlo con **validación en JavaScript**, que veremos más adelante.
    - Las validaciones de HTML5 son útiles para una primera capa de control, pero **no sustituyen la validación en el servidor**, que siempre debe realizarse por motivos de seguridad.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué atributo hace que un campo sea obligatorio?
    2. ¿Cómo puedes limitar un número entre 1 y 10 sin usar JavaScript?
    3. ¿Qué atributo permite validar un formato de texto mediante expresiones regulares?
    4. ¿Por qué es recomendable usar también validación en el servidor?
