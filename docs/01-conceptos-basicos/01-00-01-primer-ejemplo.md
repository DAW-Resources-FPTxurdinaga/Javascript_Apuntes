# 1.0.1 Tu primer script en JavaScript

En este ejemplo práctico, vas a comprobar cómo funciona el **tipado dinámico y débil** en JavaScript con un pequeño programa que se ejecuta directamente en el navegador.

---

## 📂 Estructura del proyecto

```
01-tipado/
├── index.html
└── script.js
```

---

## 📝 Paso 1: configuración inicial

Crea un archivo `index.html` con el siguiente contenido:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mi primer script JS</title>
  <script src="script.js"></script>
</head>
<body>
  <h1>Consulta la consola del navegador</h1>

</body>
</html>
```

---

## 📝 Paso 2: lógica del script

Crea un archivo `script.js` con el siguiente código:

```javascript
// Tipado dinámico
let x = 42;
console.log("Valor de x:", x);
console.log("Tipo de x:", typeof x);

x = "ahora soy un texto";
console.log("Nuevo valor de x:", x);
console.log("Nuevo tipo de x:", typeof x);

// Tipado débil
let resultado1 = "5" + 3;
console.log('"5" + 3 =', resultado1);

let resultado2 = 5 + "3";
console.log("5 + '3' =", resultado2);

let resultado3 = 5 + 3;
console.log("5 + 3 =", resultado3);
```

---

## 📘 Conceptos aprendidos en este ejemplo

   **Tipado dinámico**

   Una variable puede cambiar de tipo a lo largo del programa.

   ```javascript
   let x = 10;     // número
   x = "hola";     // ahora string
   ```

   **Tipado débil**

   JavaScript convierte automáticamente los tipos cuando combina datos distintos.

   ```javascript
   "5" + 3 // → "53" (concatenación)
   5 + 3   // → 8   (suma aritmética)
   ```

   **Ejecución en el cliente**

   El código se ejecuta directamente en el navegador, sin compilación previa.

---

## 🧪 Ejercicios para practicar

1. Cambia el valor inicial de `x` a `true` y observa el tipo que muestra `typeof`.
2. Prueba con `null` y `undefined`. ¿Qué tipo devuelve cada uno?
3. Modifica la operación `"5" + 3` por `"5" * 3`. ¿Qué ocurre?
4. Crea una variable `y = "10"` y súmale un número: `y + 2`. ¿Qué resultado obtienes?

---

## 🛠️ Solución de problemas

Si algo no funciona:

1. Asegúrate de que el archivo `script.js` está en la misma carpeta que `index.html`.
2. Abre la consola del navegador (F12 → pestaña "Consola").
3. Revisa si aparece algún error de sintaxis.
