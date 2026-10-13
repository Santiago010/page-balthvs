---
name: BALTHVS
description: Warm, paper-light psychedelia with frosted album-art atmosphere and a live-set warmth.
colors:
  ink: "#141210"
  paper: "#ffffff"
  accent-rust: "#bc3a1e"
  accent-indigo: "#3f33d6"
  oxblood: "#661d1d"
  text-strong: "#16110d"
  text-mid: "#2b2722"
  text-body: "#46403a"
  ash-cream: "#e5dfdf"
  warm-stone: "#56524d"
typography:
  display:
    fontFamily: "Herqin, Cormorant Garamond, Georgia, serif"
    fontSize: "clamp(34px, 4.4vw, 96px)"
    fontWeight: 400
    lineHeight: 1
    letterSpacing: "0.5px"
  headline:
    fontFamily: "Herqin, Cormorant Garamond, Georgia, serif"
    fontSize: "clamp(44px, 4.3vw, 92px)"
    fontWeight: 400
    lineHeight: 1.02
    letterSpacing: "-0.5px"
  title:
    fontFamily: "TASA Orbiter, Helvetica Neue, Arial, sans-serif"
    fontSize: "clamp(21px, 1.45vw, 28px)"
    fontWeight: 600
    lineHeight: 1.2
    letterSpacing: "normal"
  body:
    fontFamily: "TASA Orbiter, Helvetica Neue, Arial, sans-serif"
    fontSize: "clamp(17px, 1.15vw, 23px)"
    fontWeight: 400
    lineHeight: 1.72
    letterSpacing: "normal"
  label:
    fontFamily: "TASA Orbiter, Helvetica Neue, Arial, sans-serif"
    fontSize: "clamp(13px, 1vw, 20px)"
    fontWeight: 600
    lineHeight: 1
    letterSpacing: "0.25em"
rounded:
  sm: "3px"
  md: "8px"
  lg: "10px"
spacing:
  xs: "8px"
  sm: "16px"
  md: "22px"
  lg: "30px"
  section: "clamp(72px, 8vw, 120px)"
components:
  button-primary:
    backgroundColor: "{colors.accent-rust}"
    textColor: "{colors.paper}"
    typography: "{typography.label}"
    rounded: "{rounded.sm}"
    padding: "15px 40px"
  button-primary-hover:
    backgroundColor: "{colors.oxblood}"
    textColor: "{colors.paper}"
  nav-link:
    textColor: "{colors.ink}"
    typography: "{typography.label}"
    padding: "8px 0"
  hero-cover:
    rounded: "{rounded.sm}"
  input-email:
    backgroundColor: "{colors.paper}"
    textColor: "{colors.text-strong}"
    rounded: "{rounded.sm}"
    padding: "14px 16px"
---

# Design System: BALTHVS

## 1. Overview

**Creative North Star: "Lights-Down Alchemy"**

BALTHVS is a psychedelic trio, and every reflex says "psychedelic" should mean neon on black. This system does the opposite on purpose. The base is warm paper light, the darks are warm near-black (never neutral), and the atmosphere comes from the band's own artwork, oversized and blurred to a frosted haze behind the type. It should feel like warm daylight through frosted glass at the top of the page, then the lights going down toward a live set as you go deeper into overlays and the newsletter modal. Hypnotic, borderless, alchemical, not a rave flyer.

The type does the heavy lifting: a decorative display serif (Herqin) carries every name, band and album, like a title card, while a clean grotesque (TASA Orbiter) carries the reading. Layout is a wide poster column that stops growing past its cap so the page reads as a composed sleeve, not a stretched web app. Color is restrained to near-monochrome warmth with two rare sparks (rust and electric indigo) that behave like stage lights, never fields.

This system explicitly rejects: tropical Latin-band cliché (no palm-and-neon shorthand), EDM/crypto neon-on-black psychedelia, interchangeable Spotify-for-Artists and link-in-bio templates, and major-label pop gloss. Warmth and craft over slickness.

**Key Characteristics:**
- Paper-light primary surface with warm near-black darks (`#141210`), never neutral `#000`.
- The background is always the release's own artwork, blurred and bled to paper.
- Herqin display serif for names; TASA Orbiter grotesque for everything read.
- Two spark accents (rust `#bc3a1e`, indigo `#3f33d6`) used as points, never planes.
- Sharp 3px poster radius; one big warm shadow; wide-tracked uppercase labels.

## 2. Colors

A near-monochrome warm palette: paper and warm-black do almost all the work, with two saturated sparks reserved for emphasis.

### Primary
- **Burnt Rust** (`#bc3a1e`, `--accent-red`): The band's signature spark. Primary buttons, active/hover accents, key marks. A point of heat, never a fill.
- **Electric Indigo** (`#3f33d6`, `--accent-blue`): The psychedelic counter-spark to rust. Secondary emphasis and cross-cultural, otherworldly moments. Kept even rarer than rust.

### Neutral
- **Ink** (`#141210`, `--ink`): The house dark. Labels, headings on paper, and the base for warm-dark overlays. This is the "black" of the system; true black is banned.
- **Paper** (`#ffffff`, `--paper`): The primary surface. Landing, album strip, and modal backgrounds.
- **Text Strong / Mid / Body** (`#16110d` / `#2b2722` / `#46403a`): A warm brown-black text ramp on paper. Strong for titles, mid for release subheads, body for reading copy.
- **Ash Cream** (`#e5dfdf`): Warm off-white for text and dividers on warm-dark surfaces.
- **Warm Stone** (`#56524d`): Muted secondary text, captions, and hairline borders.
- **Oxblood** (`#661d1d`): The pressed/deep state of rust. Hover and active on primary actions.

### Named Rules
**The Frosted-Art Rule.** The atmospheric background is always the current release's own artwork, scaled up (~1.18) and blurred (`clamp(46px, 3.2vw, 80px)`) behind a paper gradient scrim. Never a flat color block, stock gradient, or purchased texture. The art is the mood.

**The Warm-Black Rule.** Every dark tilts warm (`#141210`, `#16110d`, `rgba(20,12,6,x)` shadows, `rgba(10,8,6,x)` scrims). `#000` / `#000000` and neutral-gray shadows are forbidden.

**The Two-Spark Rule.** Rust and indigo are sparks, not fields. Combined they cover a small fraction of any screen. If an accent starts to feel like a background, it is wrong.

## 3. Typography

**Display Font:** Herqin (with Cormorant Garamond, Georgia, serif)
**Body Font:** TASA Orbiter (with Helvetica Neue, Arial, sans-serif)

**Character:** A decorative, high-contrast display serif paired with a clean modern grotesque. Herqin is the ceremony, the title card that names the band and each album; TASA Orbiter is the plain, confident voice that carries everything you actually read. The tension between ornate serif and neutral grotesque is the whole personality.

### Hierarchy
- **Display** (Herqin, 400, `clamp(34px, 4.4vw, 96px)`, line-height 1): Hero and page titles, album names. Rendered dark (`#16110d`) over the frosted-art scrim. A poster-scale variant reaches `clamp(56px, 6.4vw, 190px)` for the standalone wordmark.
- **Headline** (Herqin, 400, `clamp(44px, 4.3vw, 92px)`, tight tracking): Section titles on interior and album pages.
- **Title** (TASA Orbiter, 600, `clamp(21px, 1.45vw, 28px)`): Release lines and subheads (`#2b2722`).
- **Body** (TASA Orbiter, 400, `clamp(17px, 1.15vw, 23px)`, line-height 1.72): Reading copy (`#46403a`), capped at a `34em` measure so lines never stretch past comfort.
- **Label** (TASA Orbiter, 600, `clamp(13px, 1vw, 20px)`, uppercase, tracking `2px`–`9px`): Nav (ABOUT, CONTACTS, SUBSCRIBE), eyebrows, album-strip titles. The wide tracking is the ornament.

### Named Rules
**The Herqin-for-Names Rule.** Herqin is reserved for names and titles, the band, albums, page headers. Never set body, labels, buttons, or UI in Herqin. If it is read as a sentence, it is TASA Orbiter.

**The Wide-Label Rule.** Uppercase labels are tracked between `2px` and `9px` (the album-strip title runs a full `9px`). Tracking scales with prominence; it is the decoration, so labels never need borders or bullets.

## 4. Elevation

Almost everything sits flat on paper. Depth is carried by tonal warmth and scrims, not a shadow stack. The single exception is the album cover, which floats. Overlays (nav, modal) darken the world behind a warm scrim rather than lifting a surface.

### Shadow Vocabulary
- **Cover Float** (`box-shadow: 0 34px 90px rgba(20, 12, 6, 0.32)`): The one lift in the system, under the hero album cover. Large, soft, warm.
- **Overlay Scrim** (`background: rgba(10, 8, 6, 0.45)` nav / `rgba(0, 0, 0, 0.6)` modal): Not a shadow but the depth cue for overlays; the page behind recedes into warm dark.
- **Atmosphere Blur** (`backdrop-filter: blur(14px)`): Reserved for sticky/floating chrome over content. Atmosphere, not decoration.

### Named Rules
**The One-Float Rule.** Only the album cover floats. Cards, sections, and buttons stay flat on paper. Do not add drop shadows to make things "pop."

**The Warm-Shadow Rule.** When a shadow exists, its color is `rgba(20,12,6,x)`. Neutral or blue-gray shadows read as generic and are forbidden.

## 5. Components

### Buttons
- **Shape:** Nearly square, sharp poster corners (3px radius, `{rounded.sm}`).
- **Primary:** Burnt Rust background (`#bc3a1e`), paper text, uppercase tracked label, `~15px 40px` padding.
- **Hover / Active:** Deepen to Oxblood (`#661d1d`); short `0.18s ease` on background. No lift, no scale.
- **Secondary / Ghost:** Ink text on paper with a Warm Stone hairline, or plain tracked-uppercase text link (the nav pattern). Rust reserved for the primary action.

### Cards / Containers
- **Corner Style:** 3px (`{rounded.sm}`); modals go to 8–10px.
- **Background:** Paper (`#ffffff`) for content, warm-dark (`#141210` / `rgba(10,8,6,x)`) for overlays.
- **Shadow Strategy:** Flat by default (see The One-Float Rule); no per-card shadows.
- **Border:** Hairline Warm Stone or `rgba(255,255,255,0.1)` on dark. Full borders only, never a colored side stripe.
- **Internal Padding:** Section rhythm from `--sec-y` (`clamp(72px,8vw,120px)`) scaled by ratio (0.62–1.62) for vertical cadence; `--pad-x` gutter horizontally.

### Inputs / Fields (newsletter modal)
- **Style:** Paper background, warm-black text, 3px radius, Warm Stone hairline.
- **Focus:** Border shifts to Burnt Rust; no neutral blue focus glow.
- **Note:** The newsletter form is a generated Brevo embed. Restyle via override selectors, do not rewrite field structure. Its default blues/slate are third-party chrome, not part of this palette.

### Navigation
- **Style:** Uppercase TASA Orbiter labels, tracked, Ink on paper (ABOUT, CONTACTS, SUBSCRIBE). Hover fades toward Burnt Rust (`0.2s ease`).
- **Mobile:** Hamburger toggle opens a full-screen menu over a warm nav-scrim (`rgba(10,8,6,0.45)`), fading in over `0.3s ease`.

### Frosted Album-Art Hero (signature)
The defining component. The release artwork is set as an oversized, blurred, slightly scaled background, veiled by a top-to-bottom paper gradient scrim (opaque near the top, clearing toward the bottom). Over it: Herqin title, TASA release line and body (`34em` measure), and the album cover floating with the Cover Float shadow. Every release re-skins the page through its own art. Motion in and out uses the house ease.

## 6. Do's and Don'ts

### Do:
- **Do** use the release's own artwork, blurred and scrim-veiled, as the page background (The Frosted-Art Rule).
- **Do** keep darks warm: `#141210` and the `rgba(20,12,6,x)` / `rgba(10,8,6,x)` family.
- **Do** reserve Herqin for names and titles; set everything read in TASA Orbiter.
- **Do** track uppercase labels wide (`2px`–`9px`) and let that tracking be the ornament.
- **Do** ease motion out with `cubic-bezier(0.22, 1, 0.36, 1)` (transforms ~`0.34s`, color/opacity `0.18`–`0.2s`).
- **Do** cap reading measure near `34em` and the layout at the `--shell` column width.
- **Do** let scale and the touring resume speak plainly; show the reach, do not boast it.

### Don't:
- **Don't** reach for neon-on-black psychedelia (electric purple/cyan on pure black, laser gradients). Their psychedelia is warm and analog, not rave.
- **Don't** signal "Latin band" with palm-and-neon or tropical-postcard palettes. Global, not exotic.
- **Don't** let it look like an interchangeable Spotify-for-Artists page or link-in-bio template.
- **Don't** use gradient text (`background-clip: text`) or decorative glassmorphism cards. Blur is atmosphere behind art only.
- **Don't** use `#000`/`#000000` or neutral-gray shadows; warm-tint every dark.
- **Don't** add a colored `border-left`/`border-right` stripe to cards, list items, or callouts. Full borders, tints, or nothing.
- **Don't** add per-card drop shadows to make things pop; only the album cover floats.
- **Don't** set body copy, buttons, or labels in Herqin.
