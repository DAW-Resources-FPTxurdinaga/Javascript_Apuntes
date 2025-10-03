# 1.2. Entradas y salidas en JavaScript

JavaScript nos ofrece varias formas de **interactuar con el usuario** y de mostrar información.  
En esta lección veremos las más básicas y utilizadas.

---

## 📌 Salidas en la consola del navegador

La consola es una herramienta fundamental para programadores.  
El método más común es `console.log()`, pero existen otros:

```js
console.log("Mensaje normal");
console.info("Mensaje informativo");
console.warn("Mensaje de advertencia");
console.error("Mensaje de error");
```

* `log`: para mensajes generales.
* `info`: para información adicional.
* `warn`: muestra advertencias resaltadas.
* `error`: resalta errores en rojo.

!!! info "Cómo abrir la consola"
    Puedes abrir la consola con F12 o Ctrl+Shift+I (pestaña Consola).
---

## 📌 `alert()`

Muestra un **cuadro emergente** en el navegador con un mensaje.
Se usa solo para pruebas rápidas, ya que interrumpe la experiencia del usuario.

```js
alert("Bienvenido a la página");
```

---

## 📌 `prompt()`

Muestra un cuadro emergente con un **campo de texto** para que el usuario escriba algo.
Devuelve lo que el usuario ha escrito (como cadena).

```js
let nombre = prompt("¿Cómo te llamas?");
alert("Hola, " + nombre);
```

---

## 📌 `confirm()`

Muestra un cuadro con **Aceptar / Cancelar**.
Devuelve `true` si el usuario hace clic en **Aceptar** y `false` si hace clic en **Cancelar**.

```js
let seguro = confirm("¿Quieres continuar?");
console.log("Resultado:", seguro);
```

---

!!! info "Buenas prácticas"
    - Usa `console.log`, `info`, `warn` y `error` para depurar según la situación.
    - `alert`, `prompt` y `confirm` son útiles para ejemplos sencillos o pruebas,
    pero rara vez se utilizan en aplicaciones modernas porque bloquean la página.

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué diferencia hay entre `console.log` y `console.error`?
    2. ¿Qué devuelve `prompt()`?
    3. ¿Qué devuelve `confirm()` si el usuario pulsa **Cancelar**?
    4. Escribe un programa que pregunte tu nombre con `prompt` y lo muestre en un `alert`.