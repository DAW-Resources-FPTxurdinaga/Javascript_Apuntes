
# 2.2 Objeto Number

El objeto **Number** en JavaScript se utiliza para representar y trabajar con **valores numéricos**.
JavaScript no distingue entre enteros y decimales: todos los números se representan internamente como **números de coma flotante de 64 bits (doble precisión, IEEE 754)**.

!!! note "Enteros y decimales en JavaScript"
    Aunque escribas `10` o `10.5`, ambos se representan con el mismo tipo: **number**.
    Esto puede generar resultados inesperados con operaciones de decimales (por ejemplo, `0.1 + 0.2 ≠ 0.3` exactamente).

---

## 📌 Creación de números

```js
// Forma literal (recomendada)
let a = 42;
let b = 3.14;

// Constructor Number (⚠️ evita usarlo, crea un objeto Number)
let c = new Number(42);

console.log(typeof a); // "number"
console.log(typeof c); // "object"
```

---

## 📌 Propiedades estáticas de Number

```js
// Número máximo representable
console.log(Number.MAX_VALUE);

// Número mínimo positivo representable
console.log(Number.MIN_VALUE);

// Valor especial "no es un número"
console.log(Number.NaN);

// Valores infinitos
console.log(Number.POSITIVE_INFINITY);
console.log(Number.NEGATIVE_INFINITY);
```

---

## 📌 Métodos de instancia más comunes

Estos métodos se aplican a valores numéricos.

```js
let x = 123.456;

// .toFixed(n) → fija el número de decimales
console.log(x.toFixed(2)); // "123.46"

// .toPrecision(n) → total de cifras significativas
console.log(x.toPrecision(4)); // "123.5"

// .toString(base) → convierte a string en otra base (por defecto, base 10)
console.log((255).toString(16)); // "ff"
```

---

## 📌 Métodos estáticos de Number

```js
// Number.isInteger(n) → true si es un entero
console.log(Number.isInteger(42)); // true
console.log(Number.isInteger(3.14)); // false

// Number.isNaN(valor) → comprueba si es NaN real (mejor que isNaN global)
console.log(Number.isNaN("hola")); // false
console.log(Number.isNaN(NaN));    // true

// Number.isFinite(valor) → true si es un número finito
console.log(Number.isFinite(100));    // true
console.log(Number.isFinite(Infinity)); // false

// Number.parseInt(cadena) → convierte a entero
console.log(Number.parseInt("42px")); // 42

// Number.parseFloat(cadena) → convierte a número decimal
console.log(Number.parseFloat("3.14 metros")); // 3.14
```

!!! warning "Cuidado con parseInt() sin base"
    Si no indicas la **base numérica** (radix), `parseInt()` puede interpretarlo de forma distinta en navegadores antiguos.
    Siempre es recomendable usar:
    `js
        parseInt("1010", 2); // 10 en base 2
        `

---

## 📌 BigInt: números muy grandes

En **ES2020** se introdujo **BigInt** para trabajar con enteros más grandes que `Number.MAX_SAFE_INTEGER`.

```js
// Sintaxis: añadir "n" al final o usar BigInt()
let grande = 9007199254740991n; // Mayor que MAX_SAFE_INTEGER
let otro = BigInt("123456789012345678901234567890");

console.log(typeof grande); // "bigint"

// Operaciones con BigInt (solo entre BigInt)
console.log(grande + 2n);
console.log(otro * 10n);
```

!!! info "BigInt y Number no se mezclan"
    No puedes sumar un `Number` normal y un `BigInt` directamente.
    Debes convertir uno al otro de forma explícita.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre `Number` como tipo primitivo y `new Number()` como objeto?
    2. ¿Qué propiedad de `Number` usarías para saber el valor más grande representable?
    3. ¿Qué método convierte un número a una cadena en base binaria o hexadecimal?
    4. ¿Qué método usarías para comprobar si un valor es realmente `NaN`?
    5. ¿Qué limitación tienen los números normales en JavaScript y cómo la soluciona `BigInt`?