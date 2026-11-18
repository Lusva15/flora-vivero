# Inventario Flora · PWA instalable

Versión **web instalable** del inventario botánico. No requiere `.ipa`, App Store ni cuenta de Apple. Se abre en el navegador del iPhone y se agrega a la pantalla de inicio; desde ahí se ve como una app a pantalla completa y funciona **sin internet**.

## Archivos

```
flora-pwa/
├── index.html            App completa (HTML + CSS + JS, sin dependencias ni compilación)
├── manifest.webmanifest  Configuración PWA (nombre, iconos, pantalla completa)
├── sw.js                 Service worker: caché offline
├── icon-192.png          Icono / apple-touch-icon
└── icon-512.png          Icono para Android
```

## Ponerla en línea (necesario para el iPhone)

iOS solo permite instalar PWA desde una URL **HTTPS** (o `localhost`). No basta con abrir el archivo desde Archivos.

Opción rápida y gratuita:

1. Crea un repositorio en GitHub y sube **todo** el contenido de `flora-pwa/`.
2. En el repo: **Settings → Pages → Source: Deploy from a branch → main → /root → Save**.
3. En unos segundos tendrás `https://TU-USUARIO.github.io/NOMBRE-REPO/`.
4. Abre esa URL en **Safari** en tu iPhone.

También sirve Netlify, Vercel, Firebase Hosting o cualquier hosting con HTTPS.

## Instalar en el iPhone

1. Abre la URL en **Safari** (iOS no permite instalar PWA desde Chrome).
2. Toca el botón **Compartir** (cuadrado con flecha hacia arriba).
3. Selecciona **Agregar a pantalla de inicio**.
4. Confirma el nombre **Flora**.

A partir de ahí abre el icono 🌿 de la pantalla de inicio: se ejecuta a pantalla completa, sin barra de Safari.

## Permisos del dispositivo

- **Cámara:** al tocar *Tomar foto*, Safari pedirá permiso. El botón *Elegir archivo* abre la galería.
- **GPS:** al tocar *Usar mi ubicación actual*, Safari pedirá permiso de ubicación. Requiere HTTPS y señal GPS.
- **Fotos:** se redimensionan a 1600 px y se guardan como JPEG dentro de IndexedDB, junto al registro.

Si deniegas un permiso, puedes reactivarlo en **Ajustes → Safari → Cámara / Ubicación** (o Ajustes → Sitios web, según la versión de iOS).

## Funcionalidad incluida

- Los **15 campos obligatorios** con validación y mensajes por campo.
- ID único generado automáticamente (UUID).
- Nombre científico en cursiva, editor de texto enriquecido saneado para la descripción.
- Captura de cámara / galería con vista previa.
- Coordenadas manuales o automáticas por GPS.
- Filtros rápidos por familia, tipo de vegetación y estado físico + búsqueda.
- Consulta detallada con enlace a OpenStreetMap.
- Edición y eliminación con confirmación.
- Exportación a CSV (Excel en español) y JSON.
- **Modo campo** de alto contraste para luz solar.
- Persistencia offline en IndexedDB y caché del service worker.

## Probar en el PC antes de subirlo

Sirve la carpeta por HTTP (el service worker no funciona con `file://`):

```powershell
cd flora-pwa
python -m http.server 8080
```

Luego abre `http://localhost:8080`. En iPhone, para probar antes de publicar, necesitas HTTPS (por ejemplo usando un túnel como `npx localtunnel` o desplegando en GitHub Pages).

## Notas

- Los datos quedan **solo en el dispositivo**. Si borras los datos del sitio en Safari, se pierden. Exporta a JSON antes de limpiar el navegador o cambiar de teléfono.
- Al publicar una versión nueva, cambia `CACHE = 'flora-pwa-v1'` en `sw.js` a `v2`, etc., para que los dispositivos actualicen la caché.
-Esta PWA **no es un `.ipa`**: no se distribuye en App Store ni aparece en Ajustes como app nativa, pero sí se instala y funciona como app en el iPhone.
