# 3.1.1. Funciones (I): Fundamentos

Las funciones son bloques de código que permiten **organizar**, **reutilizar** y **estructurar** mejor un programa.  

---

## 📌 Declaración de funciones tradicionales

Las funciones tradicionales se definen con la palabra clave `function`.  
Se pueden declarar con nombre (funciones nombradas) o sin nombre (funciones anónimas, que veremos más adelante).

```js
// Función nombrada
function saludar(nombre) {
  return `Hola, ${nombre}`;
}

console.log(saludar("Laura")); // Hola, Laura
```

---

## 📌 Funciones flecha (arrow functions)

Las **funciones flecha** se introdujeron en **ES6** y ofrecen una forma más **corta y expresiva** de escribir funciones.
Además, heredan el `this` del contexto donde se crean.

### Sintaxis básica

```js
const saludar = () => {
  console.log("Hola mundo");
};

saludar(); // Hola mundo
```

### Con un solo argumento

```js
const saludar = nombre => {
  console.log(`Hola, ${nombre}`);
};

saludar("Laura"); // Hola, Laura
```

### Con varios argumentos

```js
const sumar = (a, b) => {
  return a + b;
};

console.log(sumar(3, 4)); // 7
```

### Retorno implícito

```js
const cuadrado = x => x * x;

console.log(cuadrado(5)); // 25
```

### Sin argumentos

```js
const obtenerHora = () => new Date().toLocaleTimeString();

console.log(obtenerHora()); // Ejemplo: "10:45:12"
```

---

## 📌 Funciones flecha como callbacks

Las funciones flecha se usan mucho como **callbacks** en métodos de arrays (`map`, `filter`, `reduce`), porque hacen el código más claro.

```js
const numeros = [1, 2, 3, 4, 5];

// Con función tradicional
const dobles1 = numeros.map(function(n) {
  return n * 2;
});

// Con función flecha
const dobles2 = numeros.map(n => n * 2);

console.log(dobles2); // [2, 4, 6, 8, 10]
```

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué palabra clave se utiliza para declarar una función tradicional?
    2. Escribe una función flecha que devuelva el triple de un número.
    3. ¿Qué diferencia hay entre usar llaves `{}` y no usarlas en una función flecha?
    4. Crea una función flecha sin argumentos que devuelva la fecha actual.
    5. Transforma esta función tradicional en una función flecha con retorno implícito:
    ```js
    function resta(a, b) {
      return a - b;
    }
    ```