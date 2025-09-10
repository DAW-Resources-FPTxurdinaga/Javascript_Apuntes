# 1.1. Dónde colocar el código JavaScript en HTML

Cuando escribimos código JavaScript en una página web, tenemos varias formas de incluirlo dentro de nuestro archivo HTML.  
Veamos las principales opciones y sus ventajas.

---

## 📌 Opción 1: JavaScript en el `<head>`

Podemos colocar el código JavaScript en el `<head>`.  
Si lo hacemos así, es recomendable usar el atributo `defer` para que el script no bloquee la carga de la página.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Ejemplo con head</title>
  <script src="script.js" defer></script>
</head>
<body>
  <h1>Página con JS en el head</h1>
</body>
</html>
```

!!! note "¿Qué hace `defer`?"
    Con `defer`, el navegador descarga el script en paralelo mientras carga el HTML,
    pero lo ejecuta solo cuando el DOM ya está listo.

---

## 📌 Opción 2: JavaScript en el `<body>`

Otra práctica común es colocar el script justo **antes de cerrar la etiqueta `</body>`**.
Así nos aseguramos de que todo el HTML ya está cargado cuando se ejecute el JavaScript.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Ejemplo con body</title>
</head>
<body>
  <h1>Página con JS en el body</h1>

  <script src="script.js"></script>
</body>
</html>
```

---

## 📌 Opción 3: Código embebido directamente

También podemos escribir el JavaScript directamente en el propio archivo HTML.
Esto se usa solo para **ejemplos muy sencillos**, ya que lo recomendable es mantener el código en un archivo externo.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Ejemplo con script embebido</title>
</head>
<body>
  <h1>Ejemplo con código directo</h1>

  <script>
    console.log("Hola desde un script embebido");
  </script>
</body>
</html>
```

---

!!! info "Buenas prácticas"
    Hoy en día, tanto **colocar el script al final del body** como **en el head con `defer`** son opciones válidas.
    La opción preferida en proyectos modernos suele ser **usar `defer` en el head**, porque mantiene los scripts organizados y asegura que no bloqueen la carga del HTML.
