# 2.9 Symbol: Identificadores únicos

El tipo de dato `Symbol` fue introducido en **ES6** y sirve para crear **identificadores únicos e inmutables**.
Se utiliza principalmente para evitar **colisiones de nombres** en propiedades de objetos y para definir **claves privadas o semiprivadas**.

!!! info "Dato importante"
    Cada vez que llamas a `Symbol()`, se genera un **valor nuevo y único**, aunque uses la misma descripción.

---

## 📌 Crear un `Symbol`

### Con descripción opcional

```js
// Crear dos símbolos diferentes aunque tengan la misma descripción
const s1 = Symbol("id");
const s2 = Symbol("id");

console.log(s1 === s2); // false
```

La descripción (`"id"`) es solo un texto útil para depuración, no afecta a la identidad del símbolo.

---

## 📌 Usar `Symbol` como clave en objetos

```js
const ID = Symbol("id");

const usuario = {
  nombre: "Laura",
  [ID]: 12345
};

console.log(usuario.nombre); // "Laura"
console.log(usuario[ID]);    // 12345
```

⚠️ Las propiedades definidas con `Symbol` **no aparecen en bucles normales** como `for...in` o `Object.keys()`.

---

## 📌 Recuperar propiedades `Symbol`

Aunque no aparecen en listados normales, puedes acceder a ellas con métodos especiales:

```js
const simbolos = Object.getOwnPropertySymbols(usuario);
console.log(simbolos); // [ Symbol(id) ]
```

---

## 📌 Symbol global (`Symbol.for`)

Si necesitas reutilizar un símbolo, puedes guardarlo en el **registro global** con `Symbol.for`.

```js
const global1 = Symbol.for("claveGlobal");
const global2 = Symbol.for("claveGlobal");

console.log(global1 === global2); // true
```

Con `Symbol.keyFor()` puedes recuperar la clave de un símbolo global:

```js
console.log(Symbol.keyFor(global1)); // "claveGlobal"
```

---

## 📌 Symbol y las APIs de JavaScript

Existen **símbolos bien conocidos** que el lenguaje usa internamente, como:

* `Symbol.iterator`: define cómo se itera sobre un objeto.
* `Symbol.toPrimitive`: personaliza cómo se convierte un objeto a primitivo.
* `Symbol.toStringTag`: cambia la etiqueta de `Object.prototype.toString`.

Ejemplo con `Symbol.iterator`:

```js
const numeros = [1, 2, 3];
const iterador = numeros[Symbol.iterator]();

console.log(iterador.next()); // { value: 1, done: false }
console.log(iterador.next()); // { value: 2, done: false }
```

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué devuelve `Symbol("x") === Symbol("x")`?
    2. ¿Qué ventaja tiene usar `Symbol` como clave en un objeto frente a una cadena?
    3. ¿Cómo accederías a las propiedades `Symbol` de un objeto?
    4. ¿Qué diferencia hay entre `Symbol("id")` y `Symbol.for("id")`?
    5. ¿Para qué sirve `Symbol.iterator` en JavaScript?