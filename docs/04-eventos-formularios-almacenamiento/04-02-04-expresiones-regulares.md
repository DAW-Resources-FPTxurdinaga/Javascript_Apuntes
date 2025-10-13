# 4.2.4 Expresiones regulares en JavaScript y HTML5

Las **expresiones regulares** (o *regex*) son patrones que permiten **buscar, validar o reemplazar texto**.
Son una herramienta muy potente para validar datos, filtrar entradas o realizar búsquedas complejas dentro de cadenas.

En esta lección aprenderás:

* Cómo usar expresiones regulares en **campos de formulario HTML5** mediante el atributo `pattern`.
* Cómo validarlas y aplicarlas en **JavaScript**.
* Qué **símbolos y estructuras** forman parte de una expresión regular.
* Y cómo construir tus propias expresiones paso a paso.

---

## 📌 1. Usar expresiones regulares en HTML5

El atributo `pattern` permite definir un **patrón de validación** directamente en un elemento de formulario.

El navegador comprobará que el valor introducido **coincida** con la expresión regular antes de enviar el formulario.

```html
<form>
  <label>Nombre de usuario:</label>
  <input 
    type="text" 
    name="usuario" 
    pattern="[A-Za-z0-9]+" 
    title="Solo letras y números, sin espacios"
    required>
  <button type="submit">Enviar</button>
</form>
```

* `[A-Za-z0-9]+` → permite **una o más letras o números**.
* Si el usuario introduce un carácter no válido (como `@` o `#`), el navegador muestra el mensaje definido en `title`.

!!! note "Recomendación"
    El atributo `pattern` solo se aplica cuando el campo **no está vacío**.
    Si quieres que sea obligatorio, añade también `required`.

---

## 📌 2. Validar expresiones regulares con JavaScript

Para tener un control más preciso, JavaScript permite usar expresiones regulares mediante el **objeto `RegExp`** o con **literales** entre `/ /`.

### Ejemplo básico

```js
const patron = /^[A-Za-z0-9]+$/; // Literal de expresión regular
const texto = "Proficientes2025";

if (patron.test(texto)) {
  console.log("✅ Texto válido");
} else {
  console.log("❌ Texto no válido");
}
```

* `.test(cadena)` → devuelve `true` o `false` según coincida o no.
* Los símbolos `^` y `$` indican el **inicio y fin de la cadena**, asegurando que toda la cadena cumpla el patrón.

---

### Ejemplo con un formulario

```html
<form id="formulario">
  <label>Teléfono:</label>
  <input type="text" id="telefono" placeholder="Ej: 612345678" required>
  <button type="submit">Validar</button>
</form>

<script>
  const form = document.getElementById("formulario");
  const tel = document.getElementById("telefono");
  const patron = /^[6-9][0-9]{8}$/; // Empieza por 6-9 y tiene 9 dígitos

  form.addEventListener("submit", (e) => {
    e.preventDefault();
    if (patron.test(tel.value)) {
      alert("✅ Teléfono válido");
    } else {
      alert("❌ Teléfono incorrecto");
    }
  });
</script>
```

!!! info "Ventaja del uso en JavaScript"
    Usar `.test()` permite validar en tiempo real, controlar los mensajes y adaptar las reglas dinámicamente (por ejemplo, si cambian los requisitos del formato).

---

## 📌 3. Elementos de una expresión regular

Las expresiones regulares se construyen combinando **caracteres especiales** y **símbolos** que indican el tipo de coincidencia.
A continuación tienes los más importantes:

| Tipo                     | Símbolo          | Significado                     | Ejemplo             | Coincide con            |       |                 |
| ------------------------ | ---------------- | ------------------------------- | ------------------- | ----------------------- | ----- | --------------- |
| **Anclas**               | `^` / `$`        | Inicio / fin de cadena          | `^abc$`             | Solo "abc"              |       |                 |
| **Clases de caracteres** | `[abc]`          | Uno de esos caracteres          | `[abc]`             | "a", "b" o "c"          |       |                 |
|                          | `[^abc]`         | Cualquier carácter excepto esos | `[^0-9]`            | No numérico             |       |                 |
| **Rangos**               | `[a-z]`          | Letras minúsculas               | `[A-Z0-9]`          | Mayúsculas o dígitos    |       |                 |
| **Cuantificadores**      | `*`              | 0 o más repeticiones            | `a*`                | "", "a", "aa"           |       |                 |
|                          | `+`              | 1 o más repeticiones            | `a+`                | "a", "aa"               |       |                 |
|                          | `?`              | 0 o 1 repetición                | `a?`                | "", "a"                 |       |                 |
|                          | `{n}`            | Exactamente n veces             | `[0-9]{5}`          | 5 dígitos               |       |                 |
|                          | `{n,}`           | Al menos n veces                | `[a-z]{3,}`         | 3 o más letras          |       |                 |
|                          | `{n,m}`          | Entre n y m veces               | `[A-Z]{2,4}`        | 2 a 4 letras mayúsculas |       |                 |
| **Grupos**               | `(abc)`          | Agrupa varios caracteres        | `(ab)+`             | "ab", "abab"            |       |                 |
| **Alternancia**          | `                | `                               | O bien... o bien... | `rojo                   | azul` | "rojo" o "azul" |
| **Metacaracteres**       | `.`              | Cualquier carácter              | `a.b`               | "acb", "a-b", etc.      |       |                 |
|                          | `\d`             | Dígito (`[0-9]`)                | `\d{3}`             | "123"                   |       |                 |
|                          | `\w`             | Letra o número (`[A-Za-z0-9_]`) | `\w+`               | "abc123"                |       |                 |
|                          | `\s`             | Espacio o tabulación            | `\s+`               | "   "                   |       |                 |
|                          | `\D`, `\W`, `\S` | Negaciones de los anteriores    | `\D+`               | No numérico             |       |                 |

---

## 📌 4. Ejemplos prácticos de validación con expresiones regulares

### 🔹 Validar un nombre (solo letras y espacios)

```js
const patronNombre = /^[A-Za-zÁÉÍÓÚáéíóúñÑ\s]+$/;
patronNombre.test("Laura Pérez"); // true
patronNombre.test("Laura_2025");  // false
```

---

### 🔹 Validar un correo electrónico (versión básica)

```js
const patronCorreo = /^[^\s@]+@[^\s@]+\.[a-z]{2,}$/i;
patronCorreo.test("usuario@dominio.com"); // true
patronCorreo.test("usuario@@com");        // false
```

---

### 🔹 Validar una contraseña segura

Debe tener al menos **8 caracteres**, una **mayúscula**, una **minúscula**, un **número** y un **símbolo especial**.

```js
const patronClave = /^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[!@#$%^&*]).{8,}$/;
patronClave.test("Abcde123!"); // true
patronClave.test("abcd1234");  // false
```

---

### 🔹 Validar un código postal (España)

```js
const patronCP = /^(0[1-9]|[1-4][0-9]|5[0-2])[0-9]{3}$/;
patronCP.test("39002"); // true (Cantabria)
patronCP.test("99000"); // false
```

---

### 🔹 Validar una matrícula española moderna

```js
const patronMatricula = /^\d{4}\s?[BCDFGHJKLMNPRSTVWXYZ]{3}$/;
patronMatricula.test("1234 BCD"); // true
patronMatricula.test("12AB");     // false
```

---

### 🔹 Validar una fecha en formato dd/mm/aaaa

```js
const patronFecha = /^(0[1-9]|[12][0-9]|3[01])\/(0[1-9]|1[0-2])\/\d{4}$/;
patronFecha.test("13/10/2025"); // true
patronFecha.test("32/01/2025"); // false
```

---

### 🔹 Validar un número decimal

```js
const patronDecimal = /^\d+(\.\d{1,2})?$/;
patronDecimal.test("12.34"); // true
patronDecimal.test("12.345"); // false
```

---

!!! warning "Evita expresiones demasiado complejas"
    Aunque las expresiones regulares son potentes, pueden volverse difíciles de leer y mantener.
    Usa **nombres descriptivos**, **comentarios** y **validaciones adicionales** si el formato es muy específico.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué atributo HTML permite usar expresiones regulares en un formulario?
    2. ¿Qué diferencia hay entre `test()` y `pattern`?
    3. ¿Qué significan los símbolos `^` y `$` en una expresión regular?
    4. ¿Qué patrón podrías usar para aceptar solo letras y espacios?
    5. ¿Cómo validarías un número de teléfono español que empiece por 6, 7, 8 o 9 y tenga 9 dígitos?
