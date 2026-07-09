<div align="center">

# 🍐 Pear Theme Editor

### El editor de temas más completo para **Pear Desktop**

*95+ temas · Portadas Dinámicas animadas · Reproductor circular · UI a tu medida*

`by Maguz`

</div>

---

> [!IMPORTANT]
> **Hecho específicamente para [Pear Desktop](https://github.com/pear-devs/pear-desktop).**
> Se inyecta directamente vía DevTools (consola) y modifica el DOM/CSS en tiempo real — no requiere recompilar la app ni tocar sus archivos fuente. También funciona en forks basados en el mismo core (p. ej. `https://github.com/michei69/pear-desktop, https://github.com/ArjixWasTaken/pear-desktop `), ya que muchos comparten la estructura de `ytmusic-player-bar`.

---

## 📋 Tabla de contenidos

- [¿Qué es esto?](#-qué-es-esto)
- [Cómo inyectarlo](#-cómo-inyectarlo)
- [Todo lo que incluye](#-todo-lo-que-incluye)
  - [🎨 Temas y personalización visual](#-temas-y-personalización-visual)
  - [🎬 Portadas Dinámicas v4](#-portadas-dinámicas-v4)
  - [💿 Reproductor](#-reproductor)
  - [🖥️ Interfaz](#️-interfaz)
  - [🎤 Letras / Lyrics](#-letras--lyrics)
  - [🧪 Experimental](#-experimental)
  - [⚙️ Robustez interna](#️-robustez-interna)
- [Novedades de v12](#-novedades-de-v12)
- [Advertencias](#-advertencias)
- [Créditos](#-créditos)

---

## ✨ ¿Qué es esto?

**Pear Theme Editor (PTE)** es un único script de JavaScript, sin dependencias que instalar, que transforma la interfaz de **Pear Desktop** por completo: temas, tipografías, logo, reproductor circular tipo vinilo, portadas de álbum animadas en tiempo real, y decenas de ajustes finos de interfaz — todo gestionado desde un panel flotante propio, sin tocar un solo archivo del programa original.

## 🚀 Cómo inyectarlo

1. Abre **Pear Desktop** y espera a que cargue una canción.
2. Abre las **DevTools**: `Ctrl + Shift + I` (o `OPCIONES-opciones avanzadas-activar devtools`).
3. Ve a la pestaña **Console**.
4. Pega el contenido completo de [`pear-theme-editor.js`](./pear-theme-editor.js) y presiona `Enter`.
5. Verás un botón flotante 🎨 aparecer en la esquina — ese es el menú del editor.

> 💡 **Tip:** si usas un gestor de userscripts para Electron (o simplemente quieres que se inyecte solo al abrir la app), guarda el `.js` y automatiza su carga en el `preload` de Pear Desktop. El script ya trae su propio *guard* de re-inyección (`window._pte5_loaded`), así que pegarlo dos veces por accidente no rompe nada.

Para **desactivarlo**, simplemente recarga Pear Desktop (`Ctrl + R`).

---

## 🗂 Todo lo que incluye

### 🎨 Temas y personalización visual

| Función | Detalle |
|---|---|
| **temas predefinidos** | Clásicos (YouTube Music, Spotify, Océano, Galaxia...), AMOLED × color, Blanco × color, temas brillantes |
| **tipografías** | Desde Inter/Roboto/Poppins hasta fuentes decorativas cargadas por Google Fonts o locales (Pixel, Fiolex Girls, Impact...) |
| **Selector de logo** | YouTube Music, Spotify, Apple Music, GitHub, GIFs (Pocoyo, Kuromi, Gengar, etc.), o URL personalizada — con control de tamaño |
| **Ancho de ventana personalizado** | Layout forzado al 110%|
| **RGB en bordes / Frosted Glass** | Efectos visuales adicionales para el panel y bordes |

### 🎬 Portadas Dinámicas v4

El módulo insignia del editor: reemplaza la miniatura estática de YouTube Music por la **portada real del álbum** (o su versión **animada**, tipo Apple Music Motion Art) buscándola en tiempo real en 4 fuentes públicas, en paralelo, con matching difuso por título+artista:

| Fuente | Qué aporta | Prioridad |
|---|---|---|
| 🎥 **M8TEC** | Portada **animada** (Apple Motion Art vía `.m3u8`) | 1ª — una animada siempre gana a cualquier estática |
| 💿 **MusicBrainz / Cover Art Archive** | Portadas de álbum sin marcas de agua, alta fidelidad | 2ª |
| 🍎 **iTunes Search API** | Artwork estático hasta 3000×3000 | 3ª |
| 🎧 **Deezer** | Fallback adicional de imagen | 4ª |

Características del pipeline:
- **Matching inteligente**: similitud Jaccard normalizada (acentos, `feat.`, `ft.`, `vs.`) + penalización automática de versiones Live/Remix/Karaoke no solicitadas.
- **Precarga**: detecta la siguiente canción en la cola y busca su portada *antes* de que empiece a sonar.
- **Caja de fuentes**: hover sobre la portada muestra qué proveedores tienen resultado disponible; click en uno lo fija como preferido.
- **Multi-contenedor**: sincroniza mini-player y vista grande a la vez, incluso al minimizar/maximizar sin cambiar de canción.
- **Reproducción HLS** (`.m3u8`) vía `hls.js`, cargado solo cuando realmente hace falta.
- Nunca pisa el video real: se desactiva sola en modo Video/Fullscreen de YTM.

### 💿 Reproductor

- Portadas circulares tipo vinilo, con animación de giro que se pausa junto con la canción.
- **Jewel Case**: marco tipo estuche de CD alrededor de la portada. (aun falta mejorarlo)
- 6 estilos de knob para la barra de progreso (círculo, cuadrado, diamante, línea, anillo, triángulo).
- Transiciones de portada configurables (fundido, deslizamiento, etc.).
- Reloj en la barra + tiempo dividido (transcurrido/restante).
- Playbar "pegada al fondo" (estilo app, sin flotar).

### 🖥️ Interfaz

- Ocultar: cuenta/avatar, barra lateral, "A continuación", pestaña Similares, metadatos de búsqueda/playbar, año en cola, reproducciones, artista/tipo en resultados.
- Etiquetado y ocultamiento selectivo de ítems del menú contextual (⋮): PiP, descargar, compartir, denunciar, estadísticas, etc.
- Filtros de búsqueda (chips) por tipo: videos, artistas, álbumes, playlists, podcasts.
- Modales propios (prompt / confirm / toast) que reemplazan los nativos del navegador.
- Botón de inicio propio junto al menú PEAR.
- Atajo `Ctrl + Shift + T` para reabrir el panel rápido.

### 🎤 Letras / Lyrics

- 2 efectos: Default o ninguno.
- Control fino de tipografía del texto (negrita, cursiva, subrayado, small caps, etc.)
- **Fix de scroll**: al cambiar de canción, la vista de letras sincronizadas vuelve siempre a la primera línea (antes se quedaba "pegada" en la posición de la canción anterior).

### 🧪 Experimental

- Invertir panel: mueve "A continuación"/Letras/Similares al lado izquierdo (espejo CSS).
- Auto-cierre de los Popup nativos de "Me gusta" / "Agregado a..." /  "COMPRAR YOUTUBE PREMIUM".

### ⚙️ Robustez interna

Detalles pensados para que el script sea estable en sesiones largas:
- Parche del `Response.prototype.json` para evitar `Illegal invocation` al re-inyectar. (este parra la version de v3.11.4 de https://github.com/ArjixWasTaken)
- Guard global (`window._pte5_loaded`) que impide dobles inyecciones y sus efectos en cascada (fetch envuelto dos veces, recursión, etc.).
- Un único `MutationObserver` "lento" (debounce 180ms) coordina todos los watchers de UI en vez de tener uno por función.
- Botón de emergencia 🎨 (rojo) si algo del script lanza una excepción, con el error visible en consola.

---

## 🆕 Novedades

Esta versión se enfocó en endurecer el motor de **Portadas Dinámicas**:

- 🐞 **Fix de condición de carrera**: si cambiabas de canción mientras una búsqueda anterior seguía en vuelo, la portada vieja podía llegar tarde y pisar la de la canción actual. Ahora cada ciclo tiene un token de generación y los resultados obsoletos se descartan.
- ⏱️ **Timeout en las 4 fuentes**: una API lenta o caída ya no bloquea el resto del pipeline indefinidamente.
- 🐢 **Throttle real de MusicBrainz** (1 request/1.1s en toda la sesión) para respetar su política de uso y evitar un baneo temporal.
- 💾 **Cache positiva en memoria** (hasta 40 canciones): repetir una canción ya resuelta la reinyecta al instante, sin volver a golpear las APIs.

---

## ⚠️ Advertencias

- Es un script de **inyección en tiempo de ejecución**: un update de Pear Desktop/YTM que cambie clases o estructura del DOM puede romper alguna función puntual (los selectores traen *fallbacks*, pero no son infalibles).
- Las fuentes de Portadas Dinámicas son **APIs públicas de terceros** sin autenticación (M8TEC, iTunes, Deezer, MusicBrainz): su disponibilidad no depende de este script.
- Todo el estado (tema, toggles, preferencias) se guarda en `localStorage` del proceso de Pear Desktop — se pierde si limpias los datos de la app.

---

<div align="center">

**Hecho con 🍐 para la comunidad de Pear Desktop**

`by Maguz`

</div>
