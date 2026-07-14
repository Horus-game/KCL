# Convertir FuelTrack en app instalable (PWA)

No hace falta Play Store ni App Store ni compilar nada: con estos archivos tu web se vuelve
una app instalable de verdad (ícono en el celular, pantalla completa, funciona offline
para la parte de datos/local).

## 1. Archivos que tenés que subir al repo (mismo nivel que `index.html`)

- `manifest.json`
- `sw.js`
- `icon-192.png`
- `icon-512.png`
- `icon-maskable-512.png`
- `apple-touch-icon.png`
- `index.html` (el actualizado, ya tiene los `<link>` y el registro del service worker)

Subilos todos a la raíz del repo (o a la misma carpeta donde ya está `index.html` si está en
una subcarpeta — en ese caso, los `href` relativos ya van a funcionar solos).

## 2. Activar GitHub Pages (necesario: PWA requiere HTTPS)

1. En tu repo → **Settings** → **Pages**.
2. En "Build and deployment" → Source: **Deploy from a branch**.
3. Elegí la rama (`main`) y la carpeta (`/root` o `/docs`, según donde esté `index.html`).
4. Guardar. En 1-2 minutos te da una URL tipo `https://tuusuario.github.io/tu-repo/`.

Esa URL con HTTPS es obligatoria para que el navegador permita instalar la PWA.

## 3. Instalar en el celular

**Android (Chrome):**
- Entrás a la URL de GitHub Pages.
- Va a aparecer automáticamente el banner "📲 Instalá la app" (ya está programado en el HTML),
  o desde el menú ⋮ → **"Instalar app"** / **"Agregar a pantalla de inicio"**.
- Queda como app normal, con ícono, sin barra del navegador.

**iPhone (Safari):**
- Entrás a la URL.
- Tocás el botón compartir (cuadrado con flecha) → **"Agregar a pantalla de inicio"**.
- iOS no dispara el banner automático (Apple no soporta `beforeinstallprompt`), por eso
  siempre hay que usar ese paso manual — es una limitación de Apple, no del código.

## 4. Qué gana con esto

- Ícono propio en el home del celular, abre en pantalla completa (sin barra de Chrome/Safari).
- El `sw.js` cachea la app shell, así abre rápido y funciona aunque no tengas señal (para ver
  tus datos guardados). Las llamadas a la IA (Groq/Anthropic) sí necesitan internet, obvio.
- Cero costo, cero revisión de tienda, se actualiza solo cuando actualizás el repo (el service
  worker detecta la nueva versión y la sirve fresca en la siguiente carga de red).

## Nota sobre subida real a Play Store (opcional, a futuro)

Si en algún momento querés que esté *en* Google Play (no solo instalable desde el navegador),
se puede envolver esta misma PWA con **Bubblewrap** o **PWABuilder** (pwabuilder.com), que generan
un `.aab` listo para subir, apuntando a esta misma URL. No hace falta reescribir nada del código.
