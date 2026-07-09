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

- Es un script de **inyección Temporal**: un update de Pear Desktop/YTM que cambie clases o estructura del DOM puede romper alguna función puntual (los selectores traen *fallbacks*, pero no son infalibles).
- Las fuentes de Portadas Dinámicas son **APIs públicas de terceros** sin autenticación (M8TEC, iTunes, Deezer, MusicBrainz): su disponibilidad no depende de este script.
- Todo el estado (tema, toggles, preferencias) se guarda en `localStorage` del proceso de Pear Desktop — se pierde si limpias los datos de la app.

---

## Proximamente

- Se agregaran mas cosas como OCULTAR SECCIONES ENTERAS EN: (TABS "similares" / PRINCIPAL (Home) / EXPLORAR ) esto con CHIPS para poder seleccionar que quitar:
<img width="1325" height="753" alt="momento" src="https://github.com/user-attachments/assets/f9c80597-d090-4dba-9991-d25f755f7dde" />
<img width="1365" height="627" alt="cover" src="https://github.com/user-attachments/assets/961b4656-ff58-4205-9e88-31871d118124" />
<img width="1365" height="669" alt="playlist" src="https://github.com/user-attachments/assets/44e13879-5089-4104-a9a4-cd295323799b" />
<img width="838" height="132" alt="1" src="https://github.com/user-attachments/assets/06abb74e-7dd1-4725-8c66-668f4b567429" />
<img width="763" height="80" alt="2" src="https://github.com/user-attachments/assets/3f908c52-89c3-4de5-b3f0-a3e87d57ab26" />
<img width="646" height="82" alt="3" src="https://github.com/user-attachments/assets/5dd989f5-dbf5-4b42-9f11-f3f965aef36b" />
<img width="499" height="101" alt="4" src="https://github.com/user-attachments/assets/09feaa60-1e2f-4a0a-a5c2-2e652eaa8d22" />
<img width="714" height="96" alt="5" src="https://github.com/user-attachments/assets/731acef6-ddcc-4e31-961b-caa2f9e82f4a" />
<img width="624" height="131" alt="6" src="https://github.com/user-attachments/assets/3d43a115-e515-4b46-8b89-272fdc263653" />
<img width="729" height="110" alt="1-1" src="https://github.com/user-attachments/assets/8ea47f2b-32ba-4a5d-b026-8c091ab07274" />
<img width="704" height="113" alt="1-2" src="https://github.com/user-attachments/assets/abbd4b97-33e9-45a6-ad30-2ff9e50db7e6" />
<img width="356" height="118" alt="1-3" src="https://github.com/user-attachments/assets/8f4d1129-50a9-4dc1-8be7-7ca33917e8d9" />
<img width="1163" height="471" alt="seleccion rapida" src="https://github.com/user-attachments/assets/26708cef-6b39-4f5e-a0a4-f874f53b4918" />


- agregar temas de la gente que ha creado asi que si tu TEMA si ese tema que tienes CSS cargado en PEAR DESKTOP lo agregare como seccion COMUNIDAD y claro se dara creditos. (esto pues se ha visto que gente a subido temas en github y seria bueno que estuvieran en este 3D1T0R
- se quitaran/mejoraran temas de la seccion DETERMINADOS ya que hay muchos que son parecidos o casi iguales y ahi otros que se siente mucho el cambio igual si tu vez algunos parecido puedes decir quiten ete tema #nombre ej bLANCOXORO u otro.
- arreglar algunos errores como PORTADA AL CENTRO culpa del PORTADAS DINAMICAS: <img width="924" height="612" alt="portada al centro" src="https://github.com/user-attachments/assets/fcdd6c30-1343-4faf-9120-d8c184a8b17a" />


- agregar mas FUENTES de texto en todo el contexto: (WINDOWS/LINUX/MAC OS)
- HACER FUNCIONAR home: <img width="96" height="33" alt="HOME" src="https://github.com/user-attachments/assets/b7125a93-1be5-46e7-986c-b85c9d082495" />

- agregar soporte para SHORTCUT/keys para funciones mapeables ABRIR BUSQUEDA / SIGUIENTE CANCION y mas
- Mejorar algunas funciones como: LIKE no cambia el icono hasta que cambias de TEMA
- Mejorar OCULTAR FILTROS DE BUSQUEDA no lo recuerda hasta que ocultas otro filtro
- Mejorar OCULTAR OPCIONES DEL MENU (los 3 puntos en la barra de reproduccion) no oculta sus opciones.
- quitar opciones repetidas y mejorar sus nombres.

  ---

## DUDAS PROBLEMAS O IDEAS
- Abre un ISSUE sobre alguna funcion que pase por alto algo que deberia estar y lo agregare
- dato este script solo mejora detalles visuales no tecnicos problemas de DEPENDENCIAS EXTERNA O ERRORES de los desarrolladores no se tocaran ej (crossfade)
- este script surge mediante la peticion de gente en el repositorio oficial pidiendo TEMAS y que agreguen posibilidades de ocultar/modificar secciones completas a voluntad cosas donde un CSS no puede tocar o modificar y la forma mas facil es un script que apunte a esos selectores html o js y un panel para tener el control en todo el momento este script lo hace posible
  ¿preguntas?:
- no lo hago para la app Por una sola razon el programa tiene miles de lineas de codigo y es facil romper o dañar algo y que tengas mas errores de los que quisieras tambien que al hacer un fork tendria que migrar cambios compilarlo para prueba/error y mas cosas. lo intentaré pero no prometo mucho.


  Lo que si puedes hacer es:
-  Ir al repositorio De PEAR DESKTOP y decir que si puede agregar este script a la app principal igual si eres un Desarrollador y tienes un fork y quieres agregarlo puedes darle tu toque y usarlo sin problemas.
- Dar ideas de que agregar alguna funcion o algo que debe estar oculto o algo donde el script no llega o no se modifica aun despues de ejecutarlo o algo que te daña visualmente o mejorar algun tema / funcion 


<div align="center">

**Hecho con 🍐 para la comunidad de Pear Desktop**

`by Maguz`

</div>
