# 3.4 Módulos ES (`import`/`export`)

A medida que un programa crece, tener todo el código en un único archivo `.js` se vuelve difícil de leer y de mantener.
Los **módulos ES** (ES6+) permiten dividir el código en varios archivos, cada uno con su propia responsabilidad, y decidir qué partes de cada archivo se comparten con el resto mediante `export` e `import`.

---

## 📌 ¿Qué es un módulo?

Un **módulo** es simplemente un archivo JavaScript que se carga de una forma especial. Sus principales características son:

- Tiene su **propio ámbito**: las variables y funciones declaradas en un módulo **no son globales**, solo existen dentro de ese archivo.
- Solo se puede usar desde fuera aquello que el módulo **exporta** de forma explícita.
- Otro archivo puede **importar** lo que necesite, indicando de qué módulo lo obtiene.

De esta forma evitamos problemas típicos de los scripts clásicos, como que dos archivos usen el mismo nombre de variable y se "pisen", o tener que cuidar el orden en el que se cargan los `<script>`.

---

## 📌 Cargar un módulo en HTML

Para que el navegador trate un archivo como módulo hay que añadir el atributo `type="module"` a la etiqueta `<script>`:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Módulos ES</title>
  <script type="module" src="js/main.js"></script>
</head>
<body>
  <h1>Ejemplo de módulos</h1>
</body>
</html>
```

Solo hace falta enlazar el **archivo principal** (`main.js`). El resto de módulos los cargará el propio navegador a partir de los `import` que encuentre.

!!! info "Los módulos se comportan como `defer`"
    Un `<script type="module">` no bloquea la carga de la página: se descarga en paralelo y se ejecuta **cuando el HTML ya se ha leído completo**.
    Por eso puede ir en el `<head>` y acceder igualmente a los elementos del DOM.

---

## 📌 Exportar: `export`

### Exportaciones con nombre

Podemos exportar tantas variables, funciones o clases como queramos, poniendo `export` delante de su declaración:

```js
// archivo: js/utilidades.js
export const IVA = 0.21;

export function precioConIva(precio) {
  return precio * (1 + IVA);
}

export function formatearEuros(cantidad) {
  return `${cantidad.toFixed(2)} €`;
}

// Esta función NO se exporta: solo se puede usar dentro de este archivo
function redondear(numero) {
  return Math.round(numero * 100) / 100;
}
```

También se pueden exportar todas juntas al final del archivo:

```js
const IVA = 0.21;

function precioConIva(precio) {
  return precio * (1 + IVA);
}

function formatearEuros(cantidad) {
  return `${cantidad.toFixed(2)} €`;
}

export { IVA, precioConIva, formatearEuros };
```

### Exportación por defecto

Cada módulo puede tener, como máximo, **una** exportación por defecto (`export default`). Se suele usar cuando el archivo contiene un único elemento principal, por ejemplo una clase:

```js
// archivo: js/persona.js
export default class Persona {
  constructor(nombre, edad) {
    this.nombre = nombre;
    this.edad = edad;
  }

  saludar() {
    return `Hola, soy ${this.nombre} y tengo ${this.edad} años.`;
  }
}
```

---

## 📌 Importar: `import`

### Importar exportaciones con nombre

Se escriben entre llaves `{ }` y **el nombre debe coincidir** con el exportado:

```js
// archivo: js/main.js
import { precioConIva, formatearEuros } from "./utilidades.js";

console.log(formatearEuros(precioConIva(100))); // "121.00 €"
```

Si queremos usar otro nombre (por ejemplo, para evitar un conflicto), usamos `as`:

```js
import { formatearEuros as euros } from "./utilidades.js";

console.log(euros(50)); // "50.00 €"
```

### Importar la exportación por defecto

Va **sin llaves**, y podemos darle el nombre que queramos:

```js
import Persona from "./persona.js";

const p = new Persona("Ane", 20);
console.log(p.saludar()); // "Hola, soy Ane y tengo 20 años."
```

### Importar todo un módulo

Con `* as` agrupamos todas las exportaciones con nombre en un objeto:

```js
import * as utils from "./utilidades.js";

console.log(utils.IVA);               // 0.21
console.log(utils.precioConIva(10));  // 12.1
```

!!! warning "Las rutas en el navegador"
    En el navegador, la ruta del `import` debe ser **completa**:

    - Debe empezar por `./`, `../` o `/`. Escribir `"utilidades.js"` a secas da error.
    - Debe incluir la **extensión** `.js`. Escribir `"./utilidades"` no funciona.

    Las rutas son **relativas al archivo que hace el `import`**, no al HTML.

| Exportación | Cómo se exporta | Cómo se importa |
|-------------|-----------------|-----------------|
| Con nombre | `export function sumar() {}` | `import { sumar } from "./mates.js";` |
| Con nombre y alias | `export function sumar() {}` | `import { sumar as add } from "./mates.js";` |
| Por defecto | `export default class Persona {}` | `import Persona from "./persona.js";` |
| Todo el módulo | (exportaciones con nombre) | `import * as mates from "./mates.js";` |

---

## 📌 Ejemplo completo

Estructura de carpetas del proyecto:

```
mi-proyecto/
├── index.html
└── js/
    ├── main.js
    ├── persona.js
    └── utilidades.js
```

`index.html` solo carga `main.js`:

```html
<script type="module" src="js/main.js"></script>
```

`main.js` importa lo que necesita de los otros dos módulos:

```js
// archivo: js/main.js
import Persona from "./persona.js";
import { precioConIva, formatearEuros } from "./utilidades.js";

const cliente = new Persona("Mikel", 30);
console.log(cliente.saludar());

const total = precioConIva(80);
console.log(`Total a pagar: ${formatearEuros(total)}`); // "Total a pagar: 96.80 €"
```

---

## 📌 Aviso práctico: los módulos necesitan un servidor

Si abres el `index.html` haciendo **doble clic** sobre él, el navegador lo abre con una dirección que empieza por `file://`. Con scripts clásicos esto funciona, pero **con módulos no**: el script no se ejecuta y en la consola aparece un error parecido a este:

```
Access to script at 'file:///C:/mi-proyecto/js/main.js' from origin 'null'
has been blocked by CORS policy
```

**¿Por qué ocurre?** Por seguridad, el navegador carga los módulos aplicando la política **CORS**, que comprueba desde qué **origen** (protocolo + dominio + puerto) se pide cada archivo.
Una página abierta con `file://` no tiene un origen válido (su origen es `null`), así que el navegador se niega a cargar los módulos aunque estén en tu propio ordenador.

**Solución:** abrir el proyecto a través de un **servidor local**, de modo que la dirección sea del tipo `http://127.0.0.1:5500/index.html`. Algunas opciones:

- **Live Server** (extensión de VS Code): clic derecho sobre `index.html` → *Open with Live Server*. Es la opción más cómoda y además recarga la página al guardar.
- Desde la terminal, en la carpeta del proyecto, con Python instalado:

```bash
python -m http.server 8000
```

Y después abrir `http://localhost:8000` en el navegador.

!!! tip "Si \"no pasa nada\", mira la consola"
    Cuando un módulo falla al cargarse, la página no muestra ningún error visible. Abre siempre las **herramientas de desarrollo** (F12) y revisa la pestaña **Consola**: ahí verás si el problema es de CORS, de una ruta mal escrita o de un nombre importado que no existe.

---

## 📌 Otras diferencias con los scripts clásicos

| Característica | Script clásico | Módulo (`type="module"`) |
|----------------|----------------|--------------------------|
| Ámbito de las variables | Global (compartido entre scripts) | Propio de cada archivo |
| Modo estricto | Solo si se escribe `"use strict"` | Siempre activado |
| Momento de ejecución | En cuanto se lee (salvo `defer`/`async`) | Al terminar de leer el HTML (como `defer`) |
| Abrir con `file://` | Funciona | No funciona (CORS) |
| `await` fuera de una función | No permitido | Permitido |

!!! warning "Las funciones de un módulo no son globales"
    Como cada módulo tiene su propio ámbito, una función definida en un módulo **no se puede llamar desde un atributo HTML** como `onclick="saludar()"`: el navegador no la encontrará.
    En su lugar, asigna los eventos desde el propio JavaScript con `addEventListener` (lo veremos en el tema 4):

    ```js
    document.querySelector("#boton").addEventListener("click", saludar);
    ```

!!! note "Módulos en Node.js"
    Node.js también admite módulos ES, aunque históricamente usaba otro sistema (`require` y `module.exports`, llamado *CommonJS*).
    Si en algún ejemplo ves `require(...)`, se trata de ese sistema antiguo; en el navegador usaremos siempre `import`/`export`.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué atributo hay que añadir a la etiqueta `<script>` para cargar un archivo como módulo?
    2. ¿Qué diferencia hay entre una exportación con nombre y una exportación por defecto? ¿Cuántas de cada tipo puede tener un módulo?
    3. ¿Por qué `import { sumar } from "mates"` da error en el navegador? Corrígelo.
    4. Has abierto tu `index.html` con doble clic y el código no hace nada. ¿Qué ha pasado y cómo lo solucionas?
    5. Crea un módulo `calculadora.js` que exporte las funciones `sumar` y `restar`, y un `main.js` que las importe y muestre el resultado por consola.
