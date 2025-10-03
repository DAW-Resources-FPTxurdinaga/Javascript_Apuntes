# 1.7 Ejercicio Práctico: Mini-Trivial

Ha llegado el momento de poner en práctica lo aprendido sobre **variables, funciones, arrays, objetos y control de flujo**.  
En este ejercicio crearás una versión simplificada del **Trivial**, donde el objetivo es responder al menos **4 de 6 preguntas** para ganar la partida.

---

## 🎯 Requisitos del Ejercicio

1. **Preguntas y categorías**  
    - Dispones de 6 preguntas, una por cada categoría clásica del Trivial:  
        Geografía, Historia, Arte, Ciencias, Deportes y Espectáculos.  
    - Cada pregunta debe tener su enunciado, una respuesta correcta y opcionalmente varias respuestas incorrectas.

2. **Mecánica del juego**  
    - El jugador empieza con **0 puntos**.  
    - Se mostrarán preguntas hasta que:  
        - Responda correctamente **4 preguntas** (gana).  
        - Responda incorrectamente **3 preguntas** (pierde).  
        - O se terminen todas las preguntas.  
    - Cada vez que el jugador responde, esa pregunta no vuelve a aparecer.  

3. **Estructura del código**  
    - Define las preguntas en un **array de objetos**.  
    - Crea funciones separadas para las distintas responsabilidades:  
        - Mostrar una pregunta disponible.  
        - Comprobar si la respuesta es correcta.  
        - Actualizar el marcador de aciertos y errores.  
        - Determinar si la partida termina (ganada o perdida).  

4. **Restricciones técnicas**  
    - Todo el código debe estar en un archivo **`script.js`** independiente (no dentro del HTML).  
    - No es necesario diseño avanzado: basta con `alert`, `prompt` o `console.log` para interactuar con el usuario.  

---

## 🧩 Código inicial (varias opciones)

### 🔹 Opción 1: Variables individuales
```js
let pregunta1 = "¿Cuál es la capital de Francia?";
let respuesta1 = "París";

let pregunta2 = "¿En qué año comenzó la Segunda Guerra Mundial?";
let respuesta2 = "1939";

// ... hasta completar 6 preguntas
```

### 🔹 Opción 2: Array bidimensional
```js
let preguntas = [
  ["Geografía", "¿Cuál es la capital de Francia?", "París"],
  ["Historia", "¿En qué año comenzó la Segunda Guerra Mundial?", "1939"],
  ["Arte", "¿Quién pintó La noche estrellada?", "Van Gogh"],
  ["Ciencias", "¿Cuál es el planeta más grande del sistema solar?", "Júpiter"],
  ["Deportes", "¿Cuántos jugadores hay en un equipo de fútbol?", "11"],
  ["Espectáculos", "¿Quién dirigió la película Titanic?", "James Cameron"]
];
```

###🔹 Opción 3: Array de objetos

```js
let preguntas = [
  { categoria: "Geografía", enunciado: "¿Cuál es la capital de Francia?", respuesta: "París" },
  { categoria: "Historia", enunciado: "¿En qué año comenzó la Segunda Guerra Mundial?", respuesta: "1939" },
  { categoria: "Arte", enunciado: "¿Quién pintó La noche estrellada?", respuesta: "Van Gogh" },
  { categoria: "Ciencias", enunciado: "¿Cuál es el planeta más grande del sistema solar?", respuesta: "Júpiter" },
  { categoria: "Deportes", enunciado: "¿Cuántos jugadores hay en un equipo de fútbol?", respuesta: "11" },
  { categoria: "Espectáculos", enunciado: "¿Quién dirigió la película Titanic?", respuesta: "James Cameron" }
];
```

---

## ✅ Objetivos de Aprendizaje

Con este ejercicio practicarás:

* **Declaración y uso de variables** (`let`, `const`).
* **Arrays y objetos** para almacenar preguntas.
* **Funciones** para estructurar el código.
* **Bucles y control de flujo** (`for`, `while`, `break`, `continue`).
* **Condicionales** (`if`, `else if`, `else`).

---

## 📝 Retos adicionales (opcional)

1. Permite que las preguntas se seleccionen en un **orden aleatorio**.
2. Haz que cada pregunta tenga varias opciones de respuesta y que el jugador seleccione la correcta.
4. Muestra un resumen final con las categorías acertadas y falladas.
