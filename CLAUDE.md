# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single self-contained landing page for the band BALTHVS (`main.html`). No build system, no dependencies installed locally, no git, no tests. All CSS, markup, and JS live inline in `main.html`. All images/fonts are hot-linked from `balthvs.com` (WordPress uploads) and third-party CDNs.

This file is meant to be pasted into a host (WordPress custom-HTML block / landing builder), so it has **no `<html>`, `<head>`, or `<body>` wrapper** — only the content fragment. Keep it that way.

## Preview

Open directly in a browser: `open main.html`. There is no dev server. External assets require network access to render.

## Structure of `main.html`

Three concerns, in order:
1. **Styles** — three `<style>` blocks: Brevo's bundled font-faces/placeholders, then the page layout, then the newsletter-modal overrides. Mobile rules live in a single `@media (max-width: 480px)` block at the end of the second style block.
2. **Markup** — `.popup-overlay` (album promo), `.hero` (logo, album cover, nav, social row), and `.nl-overlay` (newsletter modal containing the Brevo `#sib-form`).
3. **Scripts** — Brevo globals + `main.js` + reCAPTCHA, then two self-invoking IIFEs: newsletter-modal behavior and album-popup behavior.

## Things that will bite you

- **The newsletter modal must never use `display:none`.** It toggles visibility via the `.is-open` class (opacity/visibility/pointer-events) specifically so the embedded reCAPTCHA stays mounted and stable. The CSS comment at `.nl-overlay` says this — respect it.
- **The Brevo form is generated, not hand-written.** `#sib-form`'s `action` URL, field `name`s (`EMAIL`, `COUNTRY`, `CITY`, `OPT_IN`), the `data-sitekey`, and `main.js` are all tied to a specific Brevo form. Don't rename fields or rewrite the form structure; restyle via the `#nlOverlay ...` override selectors instead.
- **Modal auto-close** is driven by a `MutationObserver` watching `#sib-form-container` for a visible `#success-message`, then closing after 900ms. If you change the form's success markup/ids, update `attachAutoCloseObserver`.
- **Album popup** shows on a 2s `setTimeout` and uses `display:flex/none` (independent of the modal's no-display-none rule).
- Layout heights use `vh` units and percentage widths tuned to the hot-linked image proportions; changing an asset URL may require re-tuning the corresponding `.bg-*` width/height.
