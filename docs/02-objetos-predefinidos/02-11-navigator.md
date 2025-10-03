# 3.3 Navigator

El objeto **`navigator`** forma parte de **`window`** y nos proporciona información sobre el **navegador**, el **sistema operativo** y algunas **capacidades del dispositivo**.
Se utiliza para detectar características y adaptar el comportamiento de la aplicación.

---

## 📌 Propiedades principales de `navigator`

### Información básica del navegador

```js
console.log(navigator.userAgent);   // Información del navegador y sistema
console.log(navigator.language);    // Idioma preferido (ej. "es-ES")
console.log(navigator.onLine);      // true si hay conexión a Internet
```

### Información sobre la plataforma

```js
console.log(navigator.platform);   // Sistema operativo (ej. "Win32", "Linux x86_64")
```

### Cookies y almacenamiento

```js
console.log(navigator.cookieEnabled); // true si las cookies están habilitadas
```

---

## 📌 Detección de conexión

Algunas propiedades permiten saber si el dispositivo está conectado o no:

```js
if (navigator.onLine) {
  console.log("Estás conectado a Internet ✅");
} else {
  console.log("No hay conexión ❌");
}
```

---

## 📌 Geolocalización

El objeto `navigator` incluye la API de **geolocalización**, que permite obtener la ubicación del usuario (si acepta compartirla).

```js
navigator.geolocation.getCurrentPosition(
  (pos) => {
    console.log("Latitud:", pos.coords.latitude);
    console.log("Longitud:", pos.coords.longitude);
  },
  (error) => {
    console.error("Error al obtener la ubicación:", error);
  }
);
```

!!! warning "Aviso de seguridad"
    La geolocalización solo funciona si la página se sirve por **HTTPS** y el usuario **acepta explícitamente** compartir su ubicación.

---

## 📌 API de credenciales y dispositivos (mención)

Los navegadores modernos han ido ampliando `navigator` con APIs específicas, como:

* **`navigator.clipboard`**: permite copiar y pegar en el portapapeles.
* **`navigator.mediaDevices`**: acceso a cámara y micrófono.

Podrás encontrar más información sobre estas APIs en la documentación oficial de Javascript. 

---

## 📝 Preguntas de repaso

!!! question "Reflexiona sobre lo aprendido"
    1. ¿Qué tipo de información devuelve `navigator.userAgent`?
    2. ¿Cómo puedes comprobar si un usuario tiene activadas las cookies?
    3. ¿Qué propiedad de `navigator` te dice si hay conexión a Internet?
    4. ¿Qué necesitas para que funcione la API de geolocalización?
    5. ¿Qué otros recursos (además de geolocalización) puedes gestionar a través de `navigator` en navegadores modernos?
