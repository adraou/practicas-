---
description: Guía detallada de tareas CRO móvil para Enigma Madrid (juegoenigmamadrid.es) repartidas por compañero.
---

# Plan CRO Móvil — Enigma Madrid (`juegoenigmamadrid.es`)

{% hint style="warning" %}
**Contexto y máxima prioridad hoy (24/11/2026):** Enigma Madrid ya tiene activas las campañas de pago en **Google Ads** y **Meta Ads**, y la mayoría de visitas y reservas entran desde **móvil (`390×844`)**. Todos los cambios deben validarse siempre en vista móvil antes de subir PR.
{% endhint %}

Al auditar la web en producción móvil detectamos varios frenos directos de conversión: calendario hundido a `1.369 px`, hero sin ubicación ni precio, menú con enlaces rotos, texto blanco sobre blanco en Keylock City y un zoom-out permanente a `508 px` al abrir el mapa. Hemos dividido el trabajo por bloques y archivos independientes para avanzar en paralelo sin conflictos en Git.

---

## Resumen del reparto

| Responsable | Bloque de tareas | Archivos principales | Objetivo |
| :--- | :--- | :--- | :---: |
| **Hassan** | 1. Reservas móvil + WhatsApp *(PR 1 lista)*<br>2. Hero móvil + Comparativa salas + Flexibilidad<br>3. Bloque de reseñas Google/Tripadvisor | `reservas.php`, `gracias.php`, `index.php` (hero y `.servicios`), `style.css` | Hoy (24/11)<br>Reseñas: 25/11 |
| **Luiggi** | 0. Mergear PRs #15 y #16 en `Juegoenigmabcn`<br>1. Cabecera y menú móvil limpios<br>2. Réplica versión en inglés | `include/header.php`, `style.css` (header), `ingles/reservas-en.html`, `ingles/index-en.html` | Hoy (24/11)<br>Inglés: 25/11 |
| **Michael** | 1. Ubicación visible en Home + fix zoom-out `508 px`, `.retos` y footer móvil<br>2. Unificación de correo oficial (ES/EN) | `index.php` (`.retos`, ubicación y footer), `include/footer.php`, `style.css`, páginas ES/EN | Hoy (24/11) |
| **Externo (AION / Ads)** | Pasos 1–3 internos del widget AION (`calendar.gestorempresas.es`) y ajustes de Google Ads / GA4 | Fuera del repo `juegoenigmamadrid` | 25/11 |

---

## Tareas de Hassan

### 1. Optimización móvil de `reservas.php` y textos predefinidos de WhatsApp
> **Estado:** Implementada y probada en local (`feat/cro-p1-reservas-whatsapp-movil`, lista para abrir PR) · **Prioridad:** Urgente · **Entrega:** 24/11/2026

- **Situación actual en producción móvil:** El calendario AION empieza en `y = 1.369 px` (~1,6 pantallas de scroll) empujado por 5 bloques de texto; los CSS/JS y el div del widget AION se cargan duplicados; hay una barra sticky `RESERVAR` redundante y los enlaces de WhatsApp tienen texto genérico.
- **Qué se ha hecho:**
  - Subido el calendario `#reservasPage` a `y = 350 px` (**−74 % de scroll**, visible en el 1.er pantallazo móvil).
  - Añadido banner compacto arriba con precio (*Desde 19 €/persona*), duración (~75 min), nota de flexibilidad grupal y botones rápidos de **WhatsApp** y **teléfono (`673 423 738`)**.
  - Movidos los 5 bloques de normas a un acordeón `<details>` debajo del calendario, corrigiendo tildes y unificando la llegada a **10 minutos antes** (igual que `gracias.php`).
  - Eliminada carga duplicada de CSS/JS/divs de AION, quitada la barra sticky redundante y ocultado el WhatsApp flotante en móvil dentro de `.page-reservas` para no tapar el día `29` del calendario.
  - Actualizado el texto predefinido de WhatsApp en toda la web (ES/EN) a consulta de disponibilidad y en `gracias.php` (`/es/gracias/`) a soporte post-reserva.
- **Archivos:** `reservas.php`, `gracias.php`, `style.css`, enlaces `wa.me` en páginas ES/EN.

### 2. Hero móvil (`Tetuán / 19 €`), comparativa rápida de salas y flexibilidad
> **Estado:** Pendiente · **Prioridad:** Urgente · **Entrega:** 24/11/2026

- **Situación actual en producción móvil:** El `<h1>` solo dice *"JUEGO DE ESCAPE EN VIVO"* (sin ubicación, jugadores ni precio); `flecha_header.webp` pisa `"MINUTOS."`; no hay CTA dentro del hero; falta comparativa rápida y dificultad entre salas; y `"¿LOGRARÉIS CAZAR AL ASESINO?"` en Keylock City es blanco sobre blanco (ilegible).
- **Qué hay que hacer:**
  - Actualizar el titular principal (`<h1>`) y subtítulo a: **Escape Room inmersivo en Madrid (Tetuán) — Salas de 2 a 24 jugadores · Desde 19 €/persona**.
  - Añadir botón CTA directo (`RESERVAR AHORA` → `reservas.php`) visible sin scroll en `390×844` y corregir solapamiento + `alt` de `flecha_header.webp`.
  - Crear bloque compacto de **comparativa rápida móvil** entre *El Virus* (`2–12 jugadores`, 1 o 2 salas, temática biológica, dificultad) y *El asesino de Keylock City* (`8–24 jugadores` o a domicilio, investigación/thriller, dificultad) con acceso directo a reservar.
  - Corregir el contraste de `"¿LOGRARÉIS CAZAR AL ASESINO?"` en Keylock City.
  - Acompañar el precio (*Desde 19 €/persona*) con micro-copy de flexibilidad para ajustar jugadores o cambiar fecha/hora.
- **Archivos:** `index.php` (`.main-container` y `.servicios`), `style.css`.

### 3. Bloque de prueba social (Google y Tripadvisor) debajo de las salas
> **Estado:** Pendiente (esperando confirmación de notas/reseñas reales) · **Prioridad:** Alta · **Entrega:** 25/11/2026

- **Qué hay que hacer:** Insertar justo debajo de `.servicios` en `index.php` tarjetas compactas móviles con las puntuaciones reales de **Google** y **Tripadvisor** y 2–3 reseñas breves verificadas.
- **Archivos:** `index.php`, `style.css`.

---

## Tareas de Luiggi

{% hint style="info" %}
**Paso previo rápido (10 min):** Mergear a `main` tus dos PRs ya aprobadas y sin conflictos en `Juegoenigmabcn` (PR #15 y PR #16) antes de empezar en `juegoenigmamadrid`.
{% endhint %}

### 1. Simplificar cabecera y corregir menú móvil
> **Estado:** Pendiente · **Prioridad:** Alta · **Entrega:** 24/11/2026

- **Situación actual en producción móvil:** El botón `+` está cortado arriba (`y = -36 px`) y abre el modal `Mapa Enigma España` (fuga a `colaboremos.php`); `Colaboremos` sigue en el menú principal; `Contáctanos` (`href="#"`) está roto y no abre nada; y `.btn-reservar-sticky` mide `390,4 px` desbordando ligeramente.
- **Qué hay que hacer:**
  - Quitar `Colaboremos` de la barra superior y del menú móvil (puede mantenerse en el footer).
  - Quitar el botón `+` cortado y el modal distractor `Mapa Enigma España` de la cabecera.
  - Arreglar el enlace `Contáctanos` del menú móvil (scroll a ubicación/contacto o modal funcional) o sustituirlo por acceso directo a **Salas** / **Ubicación**.
  - Centrar la navegación en **Salas**, **Ubicación** y **Reservar**, evitando botones duplicados y asegurando que el drawer cubra el 100 % del ancho en móvil.
  - Ajustar `.btn-reservar-sticky` (`width: 100%; box-sizing: border-box;`) para eliminar el desbordamiento horizontal.
- **Archivos:** `include/header.php`, bloque header de `style.css`.

### 2. Replicar optimizaciones CRO móviles en versión en inglés
> **Estado:** Pendiente (tras cerrar español) · **Prioridad:** Media · **Entrega:** 25/11/2026

- **Qué hay que hacer:** Replicar en `ingles/reservas-en.html`, `ingles/index-en.html` y cabeceras/pies de `ingles/*.html` todas las mejoras móviles cerradas en español, manteniendo coherencia 1:1 y respetando las rutas relativas (`../assets/...`).
- **Archivos:** `ingles/reservas-en.html`, `ingles/index-en.html`, `ingles/*.html`.

---

## Tareas de Michael

### 1. Ubicación visible en Home + fix zoom-out `508 px`, `.retos` y footer móvil
> **Estado:** Pendiente · **Prioridad:** Alta · **Entrega:** 24/11/2026

- **Situación actual en producción móvil:** La dirección y metros están ocultos en un modal; al abrir `¿DÓNDE ESTAMOS?`, `#panel-donde` provoca un **desbordamiento permanente a `508 px`** incluso tras cerrarlo (y el embed lanza `PLACES_GET_PLACE`); en `.retos` hay huecos de `160 px` y *"Sé protagonista"* se solapa con *"DIVERSIÓ / N ANTE / TODO"*; y `index.php` tiene un doble `<footer>` sin mostrar teléfono escrito, correo ni enlaces legales en móvil.
- **Qué hay que hacer:**
  - Añadir bloque visible directamente en `index.php` con **Calle Nuestra Señora del Carmen, 7 (28039 Madrid)**, metros (**Estrecho y Tetuán a 5 min · Francos Rodríguez a 10 min**) y botón **"Cómo llegar"** hacia Google Maps.
  - Corregir `#panel-donde` y su `<iframe>` (`width: 100%; max-width: 100%; box-sizing: border-box;`) para que abrir y cerrar el modal nunca ensanche la web por encima de `390 px`.
  - Corregir el CSS móvil de `.retos` / `.retos-container-1` / `.retos-container-2` (quitar alturas fijas de `40 px` y márgenes gigantes de `28em/25em`) para eliminar solapamientos y palabras partidas.
  - Eliminar el `<footer>` duplicado en `index.php` (líneas 177–198) para usar únicamente `include/footer.php` y mostrar de forma limpia teléfono (`673 423 738`), correo oficial y enlaces legales en móvil.
- **Archivos:** `index.php` (`.retos`, ubicación y footer), `include/footer.php`, `style.css`.

### 2. Unificación del correo electrónico oficial en toda la web (ES/EN)
> **Estado:** Pendiente (esperando confirmación de `clientes@` vs `info@`) · **Prioridad:** Alta · **Entrega:** 24/11/2026

- **Situación actual:** Conviven 3 direcciones distintas (`info@enigmamadrid.es`, `clientes@enigmamadrid.es` e `info@juegoenigma.es`).
- **Qué hay que hacer:** En cuanto el responsable confirme cuál queda como dirección única oficial, reemplazar todas las apariciones visibles y `mailto:` en páginas PHP en español y en `ingles/*.html`.
- **Archivos:** `include/header.php`, `include/footer.php`, `index.php`, `gracias.php`, `pago-error.php`, `colaboremos.php`, `empresas.php`, legales e `ingles/*.html`.

---

## Dependencias externas (fuera de `juegoenigmamadrid`)

| Área externa | Alcance según Auditoría CRO | Relación con nuestro trabajo |
| :--- | :--- | :--- |
| **Equipo AION** (`calendar.gestorempresas.es`) | Paso 1: abrir en disponibilidad cercana + duración.<br>Paso 2: precio/persona (desde 19 €) en vivo + flexibilidad.<br>Paso 3: formulario móvil mínimo (nombre, teléfono/WhatsApp y email) + resumen visible. | Vive en el widget Vue externo; nosotros optimizamos todo el envoltorio móvil de `reservas.php`. |
| **Marketing / Google Ads & GA4** | Limpiar palabras clave negativas/redundantes, concordancia exacta, verificar recuento de conversión `/es/gracias/` en **Una** y medir tras desplegar. | No alterar el `dataLayer` (`booking_complete`) de `gracias.php`. |

---

## Flujo Git y Checklist obligatorio de QA móvil (`390×844`)

- [ ] Crear rama nueva desde `main` actualizado (`git checkout main && git pull && git checkout -b feat/cro-...`).
- [ ] Si se edita `style.css`, ejecutar `node build/minify-css.js` antes de commitear.
- [ ] Probar en DevTools a **`390×844`**: `0 px` de desbordamiento horizontal, contraste legible, sin botones superpuestos y `0` errores nuevos en consola JS.
- [ ] No tocar el tracking `dataLayer` de `gracias.php` ni el hook de liberación de `pago-error.php`.
- [ ] En cuanto la PR reciba el aprobado en GitHub, el propio autor resuelve conflictos (si los hubiera) y hace el **merge a `main`** el mismo día.
