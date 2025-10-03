# 3.1.3. Funciones (III): Parámetros y closures

En esta lección aprenderás a manejar funciones que aceptan un número variable de argumentos  
y a comprender el concepto de **closure**, clave en JavaScript.

---

## 📌 El objeto `arguments`

Antes de ES6, cuando queríamos que una función aceptara un número indefinido de argumentos,  
se usaba el objeto especial `arguments`.  

Este objeto se genera automáticamente dentro de cualquier **función tradicional** (no funciona en funciones flecha).

```js
function sumar() {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

console.log(sumar(1, 2, 3)); // 6
```

!!! warning "Problemas de `arguments`"
    * No es un array real, sino un objeto parecido a array (*array-like*).
    * No funciona en funciones flecha.
    * Hace el código menos claro y menos moderno.

---

## 📌 Parámetros rest (`...`)

Con **ES6** llegaron los **parámetros rest**, que sustituyen a `arguments` de una forma más clara.
Los valores extra se agrupan en un **array real**, mucho más cómodo de usar.

```js
function sumar(...numeros) {
  return numeros.reduce((a, b) => a + b, 0);
}

console.log(sumar(1, 2, 3));     // 6
console.log(sumar(4, 5, 6, 7));  // 22
```

!!! tip "Ventajas frente a `arguments`"
    - Genera arrays reales (con métodos como `.map`, `.filter`, `.reduce`).  
    - Funciona en cualquier tipo de función, incluidas las flecha.  
    - Hace el código más legible y moderno.  

---

## 📌 Closures (cierres)

Un **closure** ocurre cuando una función recuerda el entorno en el que fue creada,
incluso después de que ese entorno haya terminado.

Sirve para **encapsular datos** y crear variables privadas.

```js
function crearContador() {
  let contador = 0;

  return function() {
    contador++;
    return contador;
  };
}

const contar = crearContador();

console.log(contar()); // 1
console.log(contar()); // 2
console.log(contar()); // 3
```

En este ejemplo, la variable `contador` se mantiene en memoria gracias al closure,
aunque la función `crearContador` ya haya terminado su ejecución.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué limitaciones tiene el objeto `arguments`?
    2. ¿En qué se diferencian `arguments` y los parámetros rest (`...`)?
    3. Escribe una función que reciba cualquier número de valores y devuelva su promedio.
    4. ¿Qué es un closure y para qué se utiliza?
    5. Crea un closure que guarde un valor secreto y devuelva una función para leerlo.