---
title: BALTHVS — Análisis de indexación y plan de mejora SEO
tags: [seo, balthvs, indexacion, plan]
fecha: 2026-10-14
---

# BALTHVS — Por qué Google se comporta así y cómo lo mejoramos

Este documento explica, con evidencia, por qué unas búsquedas funcionan y otras no tras la implementación del 13 oct 2026, y deja un plan priorizado para los casos que fallan. También sirve como mi plan de implementación.

---

## Estado de ejecución — 14 oct 2026 (tarde)

- ✅ **P0 COMPLETO**: propiedad verificada en GSC (etiqueta HTML vía SeoPress, propiedad "Prefijo de URL"), `sitemaps.xml` enviado y Correcto, indexación solicitada para las 9 URLs.
- ✅ **P1 COMPLETO**: un solo plugin SEO (**SeoPress**; se encontró y **desactivó Rank Math**, que estaba duplicado). Títulos + meta de las **9 páginas en vivo y verificados** (corregido el doble `– BALTHVS` quitando el añadido de la plantilla de Pages). Sitemap XML activo. Open Graph + `og:image` (Facebook + Twitter large image). **BreadcrumbList** en vivo y verificado en los 7 (6 álbumes + índice).
- ⏸️ **P2 cerrado por decisión**: el enlazado interno **ya existía** (índice `/albums/` → 6 álbumes). Las frases visibles por canción **no se hacen**: los nombres ya son visibles (tracklist) y reforzados en title/meta; el contexto (Netflix/Outer Banks) no tiene campo en schema y no justifica tocar el diseño.
- ➕ **Páginas extra (14 oct, tarde — en vivo y auditadas)**: `/contact/` (JSON-LD `ContactPage` + `BreadcrumbList` + `h1`), `/tour/` (`BreadcrumbList` + `h1`), `/manifest-multilink/` (`MusicAlbum` + `BreadcrumbList` + fix del `alt`), las tres con título/meta propios. **Bug de diseño arreglado**: en las 6 páginas de álbum las "related albums" ahora envuelven (`flex-wrap`) y la 5ª portada cae centrada debajo en vez de recortarse.
- ✅ **Auditoría completa de las 12 URLs (14 oct)**: títulos/meta correctos y sin duplicar, `index,follow`, `og:image`, canonical propio y JSON-LD presentes en TODAS. Única observación menor: la meta de `/albums/` son 174 car. (Google la recorta ~160). *(`BreadcrumbList` Home › About añadido a `/about/` el 14 oct — ⚠️ pendiente re-pegar ese bloque en WP.)*
- ⬜ **P3 PENDIENTE**: backlinks a las URLs de álbum (el lever principal que falta) + Core Web Vitals.
- 📏 **Medición**: repetir las 9 búsquedas en 2–4 semanas + revisar GSC (Páginas / Rendimiento).

---

## 1. El hallazgo central: Google aún no re-rastrea los cambios

Los cambios se publicaron el 13 oct. Las búsquedas se hicieron el 14 oct. Google re-rastrea cada URL en su propio calendario, normalmente **días a semanas**. La evidencia de que todavía estamos viendo la versión vieja:

- **Títulos viejos en el SERP.** Google muestra `Official Website – Albums – Harvest` y `BALTHVS – Official Website – About`. Esos son los títulos que genera el tema, no los nuestros (`Harvest (2024) — BALTHVS Album with Mango Season`). Si Google hubiera re-rastreado, mostraría el título nuevo.
- **Alt viejo en el snippet del índice.** Para "third vibration" el snippet del índice dice `Third Vibration album cover Cause and Effect album cover Macrocosm album cover`. Ese es el alt anterior. El nuevo es `Third Vibration, BALTHVS album cover (2023)`.

Conclusión: **casi todo lo que se ve en Google ahora refleja la web ANTES de nuestro trabajo.** Esto cambia la lectura de todo lo demás.

---

## 2. Por qué cada caso se comporta como se comporta

### Casos satisfactorios

- **mango season → Harvest.** "Mango Season" ya estaba en el tracklist de Harvest como texto rastreable desde antes, y es una canción con señales externas fuertes (apareció en la película de Netflix *Remarkably Bright Creatures*). La página Harvest ya estaba indexada. Nuestra implementación aún no influyó; cuando se re-rastree, la reforzará.
- **harvest → Harvest.** La página ya estaba indexada con su descripción ("Harvest is the 4th album...").
- **burning man → /about.** "Burning Man" ya estaba en la lista de festivales (texto visible) desde antes. /about ya indexada.

Qué tienen en común: **la página ya estaba indexada** y **el término ya existía como texto** en esa página. Esos dos factores, no el schema nuevo, son los que están produciendo el resultado hoy.

### Casos no satisfactorios

- **third vibration → índice en vez de la página del álbum.** Es **canibalización de keyword**. El índice `/albums/` recibe enlaces internos desde el menú (MUSIC) y desde los "related-albums" de las 6 páginas, así que acumula más autoridad que cada página de álbum. Cuando dos páginas tuyas compiten por el mismo término, Google elige la que juzga más fuerte: el índice. Además la página del álbum aún no se re-rastrea con su título exacto nuevo.
- **cause & effect → nada.** La página `causeeffect` está débilmente indexada y con el título genérico viejo. Sin un título/encabezado que grite "Cause & Effect" (eso ya lo arreglamos, falta re-rastreo) y sin autoridad, no sale.
- **turkish coffee → nada.** Es un track de Cause & Effect. El término vive enterrado en un `<li>` de una lista, que pesa poco, en una página que ya de por sí rankea mal. Tiene fama externa (Outer Banks, Netflix) pero esa fama apunta a terceros, no a tu página.
- **famagusta port → nada.** Corrección: Famagusta Port es de **Third Vibration**, no de Harvest. Misma causa que arriba: término de bajo peso en una página débil/no re-rastreada.
- **liminal stages → nada.** Es un track de **Manifest**, página nueva (álbum salió el 7 oct). Las páginas nuevas tardan en indexarse; es la que menos historial tiene en Google.
- **interview → /about en página 2.** "interview" es un término genérico y competido. Los propios medios que publicaron las entrevistas (RIFF, Sabana Sounds, etc.) tienen más autoridad para ese término que tu /about. Estás indexado, pero no ganas la primera página para una palabra tan amplia.

### Patrón general

Tres causas, por orden de impacto:
1. **Tiempo de re-rastreo** (afecta a todos). Aún no leen lo nuevo.
2. **Indexación y autoridad por URL.** Las páginas de álbum individuales son más débiles que el índice.
3. **Canibalización.** El índice le roba términos a las páginas de álbum.
4. **Peso del término.** Un nombre de canción en una lista pesa poco por sí solo.

---

## 3. Qué hizo (y hará) nuestra implementación

Honestamente: a día de hoy, poco visible, porque no se ha re-rastreado. Pero cada pieza ataca una causa concreta y rendirá al re-rastrear:

- **Títulos exactos por página** (`Harvest (2024) — ...`): atacan la canibalización y el match de intención. Una página con el término en el `<title>` y el `<h1>` le gana al índice para ese término.
- **`<h1>` por página**: refuerza de qué trata cada URL.
- **JSON-LD `MusicAlbum` + `MusicRecording`**: le dice a Google explícitamente que "Turkish Coffee" es una canción del álbum Cause & Effect de BALTHVS. Mejora el entendimiento de entidad para los términos de canción enterrados.
- **JSON-LD `MusicEvent`**: asocia la entidad BALTHVS con cada festival (refuerza "balthvs burning man").
- **Captions nombre + fecha** y **alt descriptivos**: texto rastreable nuevo que refuerza el término en cada página.

---

## 4. Cómo mejorar los casos que fallan (plan priorizado)

### P0 — Ahora mismo (acelerar re-rastreo) — ✅ COMPLETADO
- ✅ **Google Search Console**: verifica la propiedad si no está. Luego, con "Inspección de URL", pulsa **Solicitar indexación** para cada una de las 9 URLs, con prioridad en: `causeeffect`, `thirdvibration`, `manifest`, `transmutations`, `macrocosm`. Es el lever que convierte "semanas" en "días". *(Hecho: verificada por etiqueta HTML vía SeoPress con propiedad "Prefijo de URL" — no hubo acceso al DNS; indexación solicitada para las 9.)*
- ✅ **Envía el sitemap** en GSC (Sitemaps → añadir `sitemap_index.xml`). Si no tienes sitemap, lo genera el plugin del paso P1. *(Hecho: `sitemaps.xml` enviado y en estado "Correcto".)*

### P1 — Esta semana (control de título/meta y sitemap) — ✅ COMPLETADO
- ✅ Instala **un** plugin SEO (ver sección 6). *(Hecho: **SeoPress**; se desactivó **Rank Math** que estaba activo en paralelo y generaba señales cruzadas.)* Con él:
  - ✅ Pon los títulos y meta descriptions de `tittles-for-pages.md` por página, quitando el genérico `Official Website – Albums – X` del tema. *(Hecho: las 9 en vivo y verificadas; home en SEO → Titles & Metas → Home, resto en el metabox de cada página. Se corrigió el doble `– BALTHVS` dejando la plantilla de Pages en solo `%%post_title%%`.)*
  - ✅ Activa el **sitemap XML** automático. *(Hecho: `sitemaps.xml`.)*
  - ✅ Activa **Open Graph** (previews al compartir en WhatsApp/IG/X). *(Hecho: OG activo con los títulos/metas nuevos + `og:image` por defecto en Facebook y Twitter card grande.)*
  - ✅ Activa **breadcrumbs** con schema `BreadcrumbList` (ayuda a Google a ver que las páginas de álbum son hijas de /albums/, lo que combate la canibalización). *(Hecho: implementado como JSON-LD `BreadcrumbList` dentro del bloque Custom-HTML de los 6 álbumes + índice, porque el breadcrumb de SeoPress requiere plantilla y el sitio usa fragmentos autocontenidos.)* ✅ **Re-pegado y verificado en vivo (14 oct).**

### P2 — Contenido y enlazado (ganar los términos de canción) — ⏸️ CERRADO POR DECISIÓN
- ⏸️ **Añade una frase única por canción con fama externa** en su página de álbum, para que el término tenga peso real y no solo viva en una lista: *(Decisión: NO se hace. Los nombres de canción ya son texto visible (tracklist) y ahora están reforzados en title/meta ("home of Turkish Coffee", "home of Mango Season"). El contexto (Netflix/Outer Banks) no tiene campo en schema.org, meterlo al alt sería keyword-stuffing, y añadir párrafos visibles nuevos rompería el diseño calibrado. Retorno decreciente frente a P3.)*
  - En `causeeffect`: una línea sobre "Turkish Coffee" y su aparición en *Outer Banks* (Netflix).
  - En `harvest`: una línea sobre "Mango Season" (*Remarkably Bright Creatures*, Netflix) y "Like Coconut Water" (campaña Sun Cruiser).
  - En `thirdvibration`: contexto de "Famagusta Port" / "Ojos Verdes".
  - En `manifest`: una línea sobre "Liminal Stages" (tiene video en el home) y los singles.
- ✅ **Enlaces internos con anchor exacto**: desde el home enlaza a cada álbum por su nombre; considera enlazar los nombres de canción famosas a la página de su álbum donde se mencionen. Esto reparte autoridad del índice hacia las páginas de álbum. *(Ya existía: el índice `/albums/` enlaza a los 6 álbumes — las portadas son links.)*

### P3 — Autoridad y rendimiento (largo plazo) — ⬜ PENDIENTE
- ⬜ **Backlinks a las URLs de álbum**: pon los links `balthvs.com/albums/<álbum>` en el bio de Spotify/Bandcamp, en notas de prensa, en el Linktree/Laylo y en redes. Los enlaces externos son el mayor lever de ranking y es lo único que falta de verdad.
- ⬜ **Core Web Vitals**: las páginas hot-linkean imágenes grandes desde balthvs.com. Comprime y usa lazy-load (plugin de imágenes + caché). Google premia velocidad.

### Medición
- Repite las mismas 9 búsquedas en **2–4 semanas**. Revisa en GSC: Cobertura (¿indexadas?), Rendimiento (¿para qué queries apareces y en qué posición?). El éxito real se mide ahí, no en una búsqueda a mano.

---

## 5. Otras estrategias (más allá de JSON-LD, alt y h1/h2/h3)

1. ✅ **Títulos y meta descriptions por página** (plugin). Reemplaza el genérico del tema.
2. ✅ **Sitemap XML + envío a GSC + solicitar indexación.**
3. ✅ **Breadcrumbs + `BreadcrumbList` schema.** Jerarquía clara, combate canibalización. *(vía JSON-LD en los bloques Custom-HTML; verificado en vivo en los 7 + contact/tour/multilink.)*
4. ✅ **Canonical por página** (self-canonical). Evita que Google trate páginas parecidas como duplicadas. *(SeoPress emite canonical propio en cada página, verificado en vivo.)*
5. ✅ **Enlazado interno contextual** con anchors descriptivos; un hub de discografía; links del home a cada álbum. *(El índice `/albums/` ya enlaza a los 6 álbumes; base cubierta.)*
6. ⬜ **Profundidad de contenido**: más texto único por página (notas por canción, créditos ampliados, contexto) = más términos por los que rankear. *(No hecho — ver decisión en P2.)*
7. ✅ **Open Graph / Twitter Cards**: mejores previews al compartir (CTR social).
8. ⬜ **Core Web Vitals / velocidad**: optimización de imágenes y caché.
9. ⬜ **Backlinks**: la palanca off-page más fuerte.
10. ✅ **robots.txt / sitemap sanos**: que nada bloquee el rastreo. *(robots en `index, follow` en las 9; sitemap limpio.)*

---

## 6. Plugins de WordPress recomendados

Elige **un solo** plugin SEO (no apiles Yoast + Rank Math, se pisan):

> ✅ **Elegido e instalado: SeoPress.** Durante el setup se detectó que **Rank Math también estaba activo** (dos plugins SEO a la vez → títulos/canonical/schema cruzados) y **se desactivó Rank Math**. Con SeoPress se fijaron títulos/meta, sitemap XML, Open Graph y verificación de GSC.

- **Rank Math** (recomendado). Gratis cubre: títulos y meta por página, sitemap XML, schema (incluido BreadcrumbList), Open Graph, control de canonical, redirecciones. Más features gratis que la competencia.
- **Yoast SEO**. Alternativa sólida y muy popular; en gratis cubre lo esencial (títulos, meta, sitemap, OG, breadcrumbs).
- ✅ **SEOPress**. Alternativa ligera si quieres algo más simple. **← el que quedó instalado.**

Complementos (no SEO, pero suman):
- **Imágenes / CWV**: ShortPixel, Imagify o EWWW Image Optimizer (comprimen y sirven WebP).
- **Caché / velocidad**: WP Rocket (de pago, el mejor) o LiteSpeed Cache / W3 Total Cache (gratis).
- **Redirecciones**: Redirection (o la que trae Rank Math).

Nota: con un plugin SEO desaparece el problema que vimos del título `Official Website – Albums – X`; podrás fijar títulos limpios por página sin tocar el tema, y tendrás por fin la meta description que hoy no existe.

---

## 7. Resumen en una frase

Lo que construimos está bien y es lo correcto; el motivo de que unas búsquedas fallen hoy es **tiempo de re-rastreo + autoridad por página + canibalización del índice**, no un error de implementación. Acelera con GSC (solicitar indexación), instala un plugin SEO para títulos/meta/sitemap, refuerza las canciones famosas con texto y enlaces, y mide de nuevo en 2–4 semanas.
