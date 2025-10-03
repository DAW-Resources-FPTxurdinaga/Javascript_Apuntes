# 2.1 Objeto String

El objeto **String** en JavaScript se utiliza para trabajar con **cadenas de texto**.
Aunque los strings son un **tipo primitivo**, cuando usas métodos sobre ellos el motor crea temporalmente un **objeto wrapper** para darte acceso a sus propiedades y métodos.

!!! note "Inmutabilidad de las cadenas"
    Las **cadenas son inmutables**: ningún método modifica la cadena original.
    Todos los métodos devuelven **una nueva cadena**.

---

## 📌 Creación de cadenas

Se pueden crear de dos formas aunque se recomienda siempre usar la primera: la forma literal.

```js
// Forma literal (recomendada)
let texto1 = "Hola mundo";

// Constructor: crea un objeto String (⚠️ evita usarlo)
let texto2 = new String("Hola mundo");
```

!!! warning "No uses `new String()` para crear cadenas"
    - `new String("hola")` crea un **objeto**, no una cadena primitiva.
    - Puede romper comparaciones estrictas: `"hola" === new String("hola")` es `false`.
    - `typeof "hola"` es `"string"`, pero `typeof new String("hola")` es `"object"`.
    **Recomendación**: usa siempre **literales** con comillas (`"..."`, `'...'`) o **plantillas** (`` `...` ``).
---

## 📌 Propiedades principales

```js
// .length → longitud de la cadena (número de caracteres)
let mensaje = "JavaScript";
console.log(mensaje.length); // 10
```

---

## 📌 Métodos más utilizados de String

### Cambio de mayúsculas y minúsculas

```js
// .toUpperCase() → convierte a MAYÚSCULAS
console.log("hola".toUpperCase()); // "HOLA"

// .toLowerCase() → convierte a minúsculas
console.log("HOLA".toLowerCase()); // "hola"
```

### Obtener partes de una cadena

```js
let cadena = "JavaScript";

// .substring(inicio, finExclusivo) → sin índices negativos
console.log(cadena.substring(0, 4)); // "Java"

// .slice(inicio, finExclusivo) → acepta índices negativos
console.log(cadena.slice(4));   // "Script"
console.log(cadena.slice(-6));  // "Script"
```

### Búsqueda de texto

```js
let texto = "Aprendiendo JavaScript";

// .indexOf(subcadena) → índice de la primera aparición o -1
console.log(texto.indexOf("Java")); // 12

// .includes(subcadena) → true si contiene
console.log(texto.includes("Script")); // true

// .startsWith(subcadena) → true si empieza por...
console.log(texto.startsWith("Apr")); // true

// .endsWith(subcadena) → true si termina con...
console.log(texto.endsWith("pt")); // true

// .charAt(indice) → caracter en la posición dada
console.log(texto.charAt(12)); // "J"
```

### Reemplazo de texto

```js
let saludo = "Hola Laura";

// .replace(buscar, reemplazo) → reemplaza la primera coincidencia
console.log(saludo.replace("Laura", "Mundo")); // "Hola Mundo"

// .replaceAll(buscar, reemplazo) → reemplaza todas (ES2021)
console.log("lala".replaceAll("la", "na")); // "nana"

// Con expresiones regulares globales (alternativa a replaceAll)
console.log("lala".replace(/la/g, "na")); // "nana"
```

### Eliminación de espacios

```js
let espacio = "   Hola   ";

// .trim() → elimina espacios al inicio y al final
console.log(espacio.trim()); // "Hola"

// .trimStart() → solo al inicio
console.log(espacio.trimStart()); // "Hola   "

// .trimEnd() → solo al final
console.log(espacio.trimEnd()); // "   Hola"
```

### Repetición y división

```js
// .repeat(n) → repite la cadena n veces
console.log("ha".repeat(3)); // "hahaha"

// .split(separador) → divide y devuelve un array
const colores = "rojo verde azul".split(" "); // ["rojo", "verde", "azul"]

// (Array) .join(separador) → une un array en una cadena
console.log(colores.join(" - ")); // "rojo - verde - azul"
```

---

## 📌 Plantillas literales (Template literals)

Desde **ES6**, las **comillas invertidas** (`` ` ``) permiten interpolar variables/expresiones y escribir **múltiples líneas**.

```js
let nombre = "Laura";
let edad = 25;

// Interpolación con ${expresión}
console.log(`Me llamo ${nombre} y el año que viene tendré ${edad + 1} años.`);

// Multilínea sin caracteres especiales
let poema = `Esto es
una cadena
multilínea.`;
console.log(poema);
```

!!! tip "Cuándo usar plantillas"
    - Cuando necesites **interpolación** (`${...}`).
    - Para **cadenas multilínea** sin `\n`.
    - Para construir cadenas complejas de forma **legible**.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Por qué no es recomendable usar `new String()`?
    2. ¿Qué devuelve la propiedad `.length`?
    3. ¿Qué diferencias prácticas hay entre `slice` y `substring`?
    4. Escribe un ejemplo de plantilla literal que incluya una **expresión** dentro de `${}`.
    5. ¿Qué método usarías para quitar espacios al inicio y al final de una cadena?
