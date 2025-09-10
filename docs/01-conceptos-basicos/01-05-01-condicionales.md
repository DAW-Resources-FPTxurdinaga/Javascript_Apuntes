# 1.5.1. Condicionales en JavaScript

En programación, los **condicionales** nos permiten tomar decisiones: ejecutar un bloque de código u otro en función de si una condición se cumple.

---

## 📌 Sentencia `if`

La sentencia `if` evalúa una condición.  
Si es **verdadera (`true`)**, se ejecuta el bloque de código asociado.

```js
let edad = 20;

if (edad >= 18) {
  console.log("Eres mayor de edad");
}
```

---

## 📌 `if...else`

Con `else` podemos ejecutar un bloque alternativo si la condición no se cumple.

```js
let edad = 16;

if (edad >= 18) {
  console.log("Eres mayor de edad");
} else {
  console.log("Eres menor de edad");
}
```

---

## 📌 `if...else if...else`

Sirve para evaluar múltiples condiciones en orden.
El primer bloque que sea verdadero detiene la evaluación.

```js
let nota = 7;

if (nota >= 9) {
  console.log("Sobresaliente");
} else if (nota >= 7) {
  console.log("Notable");
} else if (nota >= 5) {
  console.log("Aprobado");
} else {
  console.log("Suspenso");
}
```

---

## 📌 Condiciones compuestas

Podemos combinar condiciones con **operadores lógicos**:

* `&&` (AND): ambas deben cumplirse
* `||` (OR): al menos una debe cumplirse
* `!` (NOT): niega el resultado

```js
let usuario = "Laura";
let logueado = true;

if (usuario === "Laura" && logueado) {
  console.log("Acceso permitido");
}
```

---

## 📌 Sentencia `switch`

El `switch` permite comparar un valor con múltiples casos.
Es útil cuando se evalúa **una sola variable con varios posibles valores**.

```js
let dia = "martes";

switch (dia) {
  case "lunes":
    console.log("Inicio de semana");
    break;
  case "martes":
  case "miércoles":
  case "jueves":
    console.log("Semana en curso");
    break;
  case "viernes":
    console.log("¡Viernes!");
    break;
  default:
    console.log("Fin de semana");
}
```

!!! tip "Consejo"
    Recuerda siempre usar `break` en cada caso, salvo que quieras que la ejecución continúe en el siguiente bloque.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué palabra clave se utiliza para evaluar una condición en JavaScript?
    2. ¿Cómo escribirías una condición que muestre `"Bienvenido"` solo si `usuario` es `"Laura"` **y** la variable `activo` es `true`?
    3. ¿Para qué sirve la sentencia `switch`? Pon un ejemplo.
    4. ¿Qué operador lógico usarías para comprobar si alguien **tiene más de 18 años o vive en Euskadi**?
