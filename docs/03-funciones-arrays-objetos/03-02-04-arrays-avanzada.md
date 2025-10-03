
# 3.2.4 Array (IV): Manipulación avanzada y buenas prácticas

En esta lección veremos cómo **copiar, reordenar, insertar, eliminar y aplanar** arrays, con especial atención a los **métodos no mutables** introducidos recientemente y a patrones recomendados.

---

## 📌 Métodos que **no** mutan el array original (recomendados)

Estos devuelven **nuevos** arrays y dejan intacto el original. Son ideales cuando quieres mantener **inmutabilidad** (por ejemplo, en interfaces reactivas).

### Copias y cortes (no destructivos)

```js
const nums = [10, 20, 30, 40];

// slice(inicio, finExcl) → devuelve una porción sin modificar el original
const parte = nums.slice(1, 3);     // [20, 30]

// concat(...arrs) → une arrays, no muta
const unidos = [1, 2].concat([3, 4]); // [1, 2, 3, 4]

// spread (...) → copia superficial o unión rápida
const copia = [...nums];              // [10, 20, 30, 40]
const unidos2 = [...[1, 2], ...[3, 4]]; // [1, 2, 3, 4]
```

### Reordenación no destructiva (ES2023)

```js
const a = [3, 1, 2];

// toSorted(cmp?) → como sort() pero NO muta
const ordenado = a.toSorted((x, y) => x - y); // [1, 2, 3]; a sigue [3,1,2]

// toReversed() → como reverse() pero NO muta
const invertido = a.toReversed(); // [2,1,3]; a sigue [3,1,2]

// toSpliced(idx, del, ...ins) → como splice() pero NO muta
const sinPrimero = a.toSpliced(0, 1);      // [1,2]
const conInsercion = a.toSpliced(1, 0, 9); // [3,9,1,2]

// with(index, value) → copia cambiando un solo índice (no muta)
const b = [0, 1, 2];
const b2 = b.with(1, 99); // [0, 99, 2]; b sigue [0,1,2]
```

### Acceso cómodo

```js
const letras = ["a", "b", "c", "d"];

// at(i) → acepta índices negativos
letras.at(-1); // "d"
letras.at(-2); // "c"
```

!!! tip "¿Por qué preferir métodos no mutables?"
    Al no modificar el array original, evitas **efectos colaterales** y facilitas el **razonamiento** y el **depurado** del código, especialmente en UIs reactivas.

---

## 📌 Métodos que **sí** mutan el array (úsalos con cuidado)

Estos cambian el contenido del array original.

### Inserción/eliminación flexible

```js
const frutas = ["manzana", "pera", "plátano"];

// splice(idx, deleteCount, ...items) → elimina/insertar/reemplaza en el sitio (muta)
frutas.splice(1, 1);                // elimina "pera" → ["manzana","plátano"]
frutas.splice(1, 0, "kiwi");        // inserta en 1 → ["manzana","kiwi","plátano"]
frutas.splice(2, 1, "uva");         // reemplaza en 2 → ["manzana","kiwi","uva"]
```

### Ordenación y reverso en sitio

```js
const nums = [10, 2, 30, 1];

// sort(cmp?) → ordena como strings si no pasas comparador (muta)
nums.sort((a, b) => a - b); // [1,2,10,30]

// reverse() → invierte en sitio (muta)
nums.reverse(); // [30,10,2,1]
```

!!! warning "Cuidado con `sort()` por defecto"
    Sin comparador, `sort()` convierte a **texto** y puede ordenar números de forma inesperada (p. ej., `10` antes que `2`).
    Usa siempre `(a,b) => a - b` para orden numérico.

### Relleno y copia en bloque

```js
const arr = [1, 2, 3, 4];

// fill(valor, inicio=0, fin=arr.length) → rellena en sitio
arr.fill(0, 1, 3);         // [1,0,0,4]

// copyWithin(dest, inicio, finExcl) → copia un segmento dentro del propio array
const z = [10, 20, 30, 40];
z.copyWithin(1, 2);        // copia [30,40] sobre idx≥1 → [10,30,40,40]
```

---

## 📌 Aplanado y mapeo

```js
// flat(profundidad=1) → aplana arrays anidados
[1, [2, 3], [4, [5, 6]]].flat();   // [1, 2, 3, 4, [5, 6]]
[1, [2, 3], [4, [5, 6]]].flat(2);  // [1, 2, 3, 4, 5, 6]

// flatMap(fn) → mapea y aplana un nivel
[1, 2, 3].flatMap(n => [n, n * 2]); // [1,2, 2,4, 3,6]
```

---

## 📌 Creación y verificación de arrays

```js
// Array.isArray(valor) → comprueba si es un array
Array.isArray([1, 2, 3]); // true

// Array.of(...valores) → crea array con los argumentos
Array.of(3);        // [3]
Array.of(1, 2, 3);  // [1,2,3]

// Array.from(iterable, mapFn?) → crea desde iterable o array-like, con mapeo opcional
Array.from("hola");                 // ["h","o","l","a"]
Array.from({ length: 4 }, (_, i) => i * 2); // [0,2,4,6]
```

---

## 📌 Patrones útiles (inmutables)

### Insertar, reemplazar y eliminar sin mutar

```js
const arr = [10, 20, 30, 40];

// Insertar 99 en la posición 2 (sin mutar)
const insertado = arr.toSpliced(2, 0, 99); // [10,20,99,30,40]

// Reemplazar el valor en la posición 1 por 77 (sin mutar)
const reemplazado = arr.with(1, 77);       // [10,77,30,40]

// Eliminar el elemento en la posición 0 (sin mutar)
const sinPrimero = arr.toSpliced(0, 1);    // [20,30,40]
```

### Ordenar sin mutar

```js
const datos = [3, 1, 2];

// Orden ascendente sin tocar el original
const asc = datos.toSorted((a, b) => a - b); // [1,2,3]
```

### Clonar de forma segura (superficial)

```js
const original = [{ id: 1 }, { id: 2 }];

// Copia superficial con spread
const copia = [...original];        // los objetos internos se comparten
```

!!! note "Copia superficial vs profunda"
    `[...]`, `slice()` o `Array.from()` hacen **copias superficiales**:
    si el array contiene **objetos**, estos se siguen compartiendo.
    Para una copia profunda, necesitas una estrategia específica (por ejemplo, estructurada con `structuredClone` en entornos que lo soportan).

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué ventajas ofrecen `toSorted` y `toReversed` frente a `sort` y `reverse`?
    2. ¿Qué diferencia práctica hay entre `splice` y `toSpliced`?
    3. ¿Para qué sirve `with(index, value)` y por qué no muta el array original?
    4. ¿Cómo aplanarías `const x = [1,[2,3],[4,[5]]]` para obtener `[1,2,3,4,5]`?
    5. ¿Qué método usarías para crear un array de longitud 5 con los valores `[0,2,4,6,8]`?
