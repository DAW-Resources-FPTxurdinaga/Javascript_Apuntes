
# 1.5.4 Control de flujo con `break` y `continue`

En algunos casos necesitamos **alterar el flujo normal de un bucle**.  
Para ello, JavaScript ofrece dos instrucciones clave: `break` y `continue`.

---

## 📌 La instrucción `break`

`break` se utiliza para **salir de un bucle inmediatamente**, incluso si la condición aún no se ha cumplido.  

```js
for (let i = 1; i <= 10; i++) {
  if (i === 5) {
    console.log("¡Se interrumpe el bucle en i = 5!");
    break;
  }
  console.log(i);
}
```

Salida:

```
1
2
3
4
¡Se interrumpe el bucle en i = 5!
```

En este caso, el bucle se detiene en cuanto `i` vale 5.

---

## 📌 La instrucción `continue`

`continue` se utiliza para **saltar la iteración actual** y pasar directamente a la siguiente.

```js
for (let i = 1; i <= 5; i++) {
  if (i === 3) {
    console.log("Saltamos el número 3");
    continue;
  }
  console.log(i);
}
```

Salida:

```
1
2
Saltamos el número 3
4
5
```

En este ejemplo, cuando `i` es 3, no se ejecuta el `console.log(i)` y se pasa a la siguiente vuelta.

---

## 📌 Usos prácticos

* **`break`**: útil cuando buscamos un elemento y podemos detener el bucle al encontrarlo.
* **`continue`**: útil para **ignorar casos específicos** dentro de un bucle.

```js
const numeros = [1, 2, -5, 3, 0, 4];

for (let n of numeros) {
  if (n < 0) {
    console.log("Número negativo encontrado, detenemos el bucle");
    break;
  }
  if (n === 0) {
    console.log("Ignoramos el 0");
    continue;
  }
  console.log(`Número válido: ${n}`);
}
```

Salida:

```
Número válido: 1
Número válido: 2
Número negativo encontrado, detenemos el bucle
```

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué hace la instrucción `break` en un bucle?
    2. ¿Qué diferencia hay entre `continue` y `break`?
    3. ¿Cómo escribirías un bucle `for` que muestre los números del 1 al 10, pero se detenga en el 7?
    4. ¿Cómo escribirías un bucle `for` que muestre los números del 1 al 5, pero que **salte** el 2 y el 4?
    5. ¿En qué caso sería más recomendable usar `continue` que un `if` dentro del bucle?