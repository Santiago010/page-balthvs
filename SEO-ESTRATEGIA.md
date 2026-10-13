---
title: Estrategia SEO BALTHVS
tags: [seo, balthvs, schema, plan]
fecha: 2026-10-13
---

# Estrategia SEO BALTHVS

Documento de plan. No se edita ningún `.html` hasta tu aprobación (Checkpoint 2).

## Decisiones cerradas (Bloque 1 + grill-me)

1. Prioridad: álbumes primero (`albums.html` y las 6 páginas de álbum). `about.html` en segunda ola.
2. Métrica: stream y compra con el mismo peso.
3. Índice `albums.html`: solo nombre y fecha debajo de cada portada. Mínimo cambio visual.
4. Acceso WP: puedes editar los bloques HTML y el `<head>`. Editor de bloques nativo, sin plugin SEO.

## Restricción que define el enfoque

Sin plugin SEO, WordPress nativo no da campo de meta description por página, y el `<title>` sale del título de la página más el nombre del sitio. Por eso el peso real del SEO on-page cae en tres cosas que sí controlas por completo dentro del bloque Custom-HTML:

- **JSON-LD inline** dentro del mismo fragmento. Google lo lee aunque viva en el body, no necesita `<head>`. Este es el mayor lever y no depende de WordPress.
- **Texto rastreable** y jerarquía de encabezados real (un `<h1>` por página, luego `<h2>`/`<h3>`).
- **Anchor text** descriptivo y enlazado interno entre páginas.

El `<title>` lo fijas con el título de la página en WordPress. La meta description queda opcional: sin plugin, Google genera el snippet a partir del texto rastreable que vamos a añadir. Si luego instalas Yoast o Rank Math, te dejo los valores listos.

## Datos base (todo sale del HTML actual, nada inventado)

Banda: BALTHVS. Balthazar Aguirre (guitarra, voz), Johanna Mercuriana (bajo, voz), Santiago Lizcano (batería, voz). Formada a finales de 2019, Bogotá, Colombia. Género: psychedelic funk.

`sameAs` de la banda: Spotify artist `2CtiNJi0zB35RHYXViVjKG`, Apple Music `1502104696`, Instagram `balthvsmusic`, Bandcamp `balthvsmusic.bandcamp.com`, YouTube `@balthvs`.

| Álbum | URL | Fecha | Sello | Spotify album | Bandcamp | Tracks |
|---|---|---|---|---|---|---|
| Macrocosm | /albums/macrocosm/ | 2020 | Cubensis | 2UxFwWypDKDPXlt9dKnLod | /album/macrocosm | 10 |
| Cause & Effect | /albums/causeeffect/ | 2022 | Cubensis | 0dITivzCKB2PwtQj9Txc0d | /album/cause-effect | 10 |
| Third Vibration | /albums/thirdvibration/ | 2023 | Cubensis | 2tk4OOnz9uDT9BLJY4EBLY | /album/third-vibration | 11 |
| Harvest | /albums/harvest/ | 2024 | Mixto | 7hIjNhXoPqyARBpaKpS3nk | /album/harvest | 10 |
| Transmutations | /albums/transmutations/ | 20 Mar 2026 | Cubensis | 0lQFMJpN1AsciO2X1PjKKa (prerelease) | /album/transmutations | 9 |
| Manifest | /albums/manifest/ | 7 Oct 2026 | Mixto | 5MOTbRL1bEJWdBJQOpEiTl | /album/manifest | 11 |

---

## Plan por archivo

### 1. albums.html (índice) — prioridad

**Texto rastreable**
- Promover `<div class="section-title">ALBUMS</div>` a `<h1 class="section-title">`. Añadir `margin:0` a la regla `.section-title` para que quede pixel-idéntico (la UA de `<h1>` mete margen por defecto).
- Debajo de cada portada, dentro de cada `<a>`, añadir nombre del álbum y fecha como texto visible (`<span class="album-name">` + `<span class="album-date">`). CSS nuevo mínimo, centrado, pequeño.
- `alt` descriptivos: "Harvest, portada del álbum de BALTHVS (2024)", etc.

**Schema (JSON-LD inline)**
- Un `@graph` con `MusicGroup` (BALTHVS) y 6 `MusicAlbum`, cada uno con `name`, `url`, `image`, `datePublished`, `byArtist`. Esto le da a Google la lista completa con fechas desde el índice.

**Cambio visual**: sí, nombre + fecha bajo cada portada (lo pediste). El `<h1>` no cambia nada si zeramos el margen.

**WP**
- Título de página: `Albums & Discography — BALTHVS`.
- Meta description (opcional): `Los seis álbumes de BALTHVS, funk psicodélico de Colombia: Macrocosm, Cause & Effect, Third Vibration, Harvest, Transmutations y Manifest. Fechas, tracklists y dónde escuchar o comprar.`

### 2. Páginas de álbum (macrocosm, cause_and_effect, third_vibrations, harvest, transmutations, manifest) — prioridad

Mismo tratamiento en las 6. Ejemplo con Harvest; el resto cambia solo los datos de la tabla.

**Texto rastreable**
- Promover el `<div class="section-title">` del título superior a `<h1 class="section-title">` con `margin:0`. Ese es el `<h1>` real de la página (nombre del álbum).
- Mantener el cuerpo actual (descripción, tracklist, créditos, availability). Ya es texto rastreable y está bien.
- `alt` descriptivo en la portada.

**Schema (JSON-LD inline): `MusicAlbum`**
- `name`, `url`, `image`, `datePublished`, `genre: "psychedelic funk"`.
- `byArtist`: `MusicGroup` BALTHVS con `sameAs`.
- `numTracks` y `track`: lista de `MusicRecording` con `name` y `position` (cada canción del tracklist actual). Esto es lo que hace que "Mango Season" o "Turkish Coffee" lleguen al álbum correcto.
- `recordLabel`, `producer` (de los créditos actuales).
- `offers`: formatos de compra (Bandcamp, y Mixto para vinilo). Streaming (Spotify, Apple) va en `sameAs`/`url`. Así compra y stream pesan igual y el schema queda correcto.

**related-albums**
- En cada `<a>` de `related-albums-inner`, añadir nombre + fecha bajo la miniatura (lo pediste). CSS pequeño, centrado, con `word-break`.

**Cambio visual**: captions de nombre+fecha en related-albums. El `<h1>` no cambia nada.
Nota de diseño: en móvil las miniaturas relacionadas van a 4-5 por fila (17-22% de ancho); el caption quedará muy pequeño. Propongo fuente mínima con wrap, y lo revisamos. Si prefieres, ocultamos el caption bajo cierto ancho y dejamos solo `aria-label`.

### 3. main.html (home) — segunda ola

Lo leo en detalle antes de editarlo. Plan de alto nivel:
- `MusicGroup` (BALTHVS) en JSON-LD con `sameAs`, miembros, género, `foundingDate`, `foundingLocation`. Ancla la entidad para "funk psicodélico BALTHVS".
- Un `<h1>` real (hoy el hero es imagen/logo; necesita un encabezado de texto, aunque sea visualmente discreto).
- Revisar que el texto del manifiesto/hero sea rastreable y no solo imagen.
- No tocar: modal Brevo, observer de auto-cierre, popup de álbum, iframes.

### 4. about.html — segunda ola

Ya tiene buen texto rastreable (bio, lineup, festivales con nombre/lugar/fecha, movies/TV/branding, interviews). Falta jerarquía y schema.

**Texto rastreable**
- `• ABOUT •` → `<h1>`. `• FESTIVALS •`, `• MOVIES, TV & BRANDING •`, `• INTERVIEWS •` → `<h2>`. Visual idéntico (la clase ya fija font-size y margin).

**Schema (JSON-LD inline)**
- `MusicGroup` (BALTHVS) con miembros y `sameAs`.
- `MusicEvent` por cada festival de la lista (performer BALTHVS, `name`, `startDate`, `location`). Esto es el lever directo para "balthvs burning man", "balthvs outside lands", etc. Se genera de la lista existente, sin inventar nada.
- Placements (movies/TV/branding) e interviews: el lever principal es el texto rastreable + los `<h2>` + anchor text, ya que el contenido vive fuera del sitio. Opcional: `subjectOf` en el `MusicGroup` apuntando a esas piezas. Para "balthvs interviews" y "balthvs outer banks", un `<h2>` claro + texto + enlaces nombrados ya hace el trabajo.

**Cambio visual**: ninguno (solo cambia el tag, no el estilo).

**WP**
- Título de página: `About BALTHVS — Bio, Festivals, Press & Interviews`.

---

## Dónde pegar cada cosa en WordPress (editor de bloques nativo)

- **JSON-LD**: dentro del mismo bloque Custom-HTML de cada página, junto al resto del fragmento. No necesita `<head>`. Es la pieza que más mueve y la controlas tú al 100%.
- **`<title>`**: campo Título de la página en el editor. Queda `Título de la página – BALTHVS`. Te doy los títulos recomendados arriba.
- **Meta description**: WordPress nativo no tiene campo. Dos caminos: (a) dejar que Google arme el snippet con el texto que añadimos (cero dependencias, recomendado por ahora); (b) si instalas Yoast o Rank Math, pegas las meta descriptions que te dejé. No metas la meta en el body: en el body Google la ignora.

---

## Invariantes que NO se tocan

- Modal newsletter: nunca `display:none`, togglea `.is-open` (mantiene reCAPTCHA montado).
- Form Brevo `#sib-form`: no renombrar `EMAIL`/`COUNTRY`/`CITY`/`OPT_IN`, ni `action`, ni `data-sitekey`. Reestilizar solo vía `#nlOverlay`.
- `attachAutoCloseObserver`: depende de `#sib-form-container`/`#success-message`.
- Popup de álbum: usa `display:flex/none`.
- Alturas `vh` y anchos `%` calibrados a las imágenes hot-linked. No cambiar URLs de assets.

## Orden de implementación propuesto

1. `albums.html` (índice: h1, captions nombre+fecha, JSON-LD de los 6 álbumes).
2. Las 6 páginas de álbum (h1, alt, MusicAlbum+tracks, captions en related-albums).
3. `main.html` (leo primero, luego MusicGroup + h1 + texto rastreable).
4. `about.html` (h1/h2, MusicGroup, MusicEvent de festivales).

Cada archivo con checkpoint: te muestro el diff antes de pasar al siguiente.
