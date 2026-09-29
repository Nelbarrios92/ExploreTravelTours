# Implementation Plan: Identidad tipográfica del Hero

**Branch**: `002-hero-brand-typography` | **Date**: 2026-09-11 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/002-hero-brand-typography/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

Reestructurar el bloque izquierdo del Hero para que “Explore Travel Tours” sea un identificador de marca contemporáneo (Fraunces, `--font-display`) subordinado al único H1 de página “Tu viaje comienza con la forma de moverte.” (Montserrat, ~tres líneas en desktop). Subtítulo de movilidad, regla de separación sobria, CTA “Explorar servicios”. Sin tocar buscador, catálogo, FAQ ni tipografía global. Enmienda de constitución IV v1.1.0. Solo `index.html` y `style.css` (enlace de Google Fonts existente).

## Technical Context

**Language/Version**: HTML5, CSS3 (vanilla); JS existente sin cambios previstos

**Primary Dependencies**: Google Fonts — Montserrat y Playfair Display (ya en uso) + **Fraunces** (pesos 400–600, `display=swap`) solo para `.hero-brand`. Unicons y `wa.me` sin cambios.

**Storage**: N/A

**Testing**: Verificación manual en navegador (constitución: sin runner). Recorrido en [quickstart.md](./quickstart.md): 375px, 768px, 1024px, 1280×800.

**Target Platform**: Sitio estático `https://www.exploretours.co/`. Viewports 375 / 768 / 1024 / 1280.

**Project Type**: Landing de una sola página (marketing)

**Performance Goals**: Fuente extra con `display=swap`; el primer pantallazo sigue usable con fallback serif. Sin JS nuevo. Overlay + text-shadow conservados.

**Constraints**: Constitución v1.1.0 — estático, español, WhatsApp, vanilla, `--font-display` solo en el identificador del Hero. Jerarquía por `clamp()` / breakpoints 768 y 1024, no píxeles fijos de una sola resolución. MUST NOT npm/framework. MUST NOT rediseñar adornos SVG/swoosh.

**Scale/Scope**: Un bloque del Hero (marca, regla, H1, subtítulo, CTA label). Resto del sitio intacto.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | Solo HTML/CSS de raíz; sin API/DB. |
| G2 | II. Español y SEO | PASS | H1 de documento = mensaje de viaje; `title`, OG, JSON-LD `TravelAgency` conservan el nombre de agencia. |
| G3 | III. WhatsApp único | PASS | Header, flotante y cards sin cambio. |
| G4 | IV. Identidad | PASS tras enmienda 1.1.0 | Fraunces solo en identificador Hero; Montserrat UI + H1; Playfair títulos de sección; paleta, logo, overlay, nav, breakpoints. |
| G5 | V. Vanilla | PASS | Tercera familia vía el `<link>` de Google Fonts existente; sin npm. |
| G6 | Alcance comercial | PASS | Subtítulo de movilidad no inventa destinos/precios/flota. |
| G7 | Destinos como sección | PASS | Fuera de alcance. |
| G8 | Verificación | PASS | [quickstart.md](./quickstart.md) en 375 / 768 / 1280; contraste overlay. |

**Post-design (Phase 1):** Gates G1–G8 siguen en PASS. Contratos de tipografía/copy no introducen backend. Constitución actualizada a 1.1.0 en el mismo ciclo de plan.

## Project Structure

### Documentation (this feature)

```text
specs/002-hero-brand-typography/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   ├── hero-typography.md
│   └── hero-copy.md
└── tasks.md              # Phase 2 (/speckit-tasks)
```

### Source Code (repository root)

```text
index.html          # Markup del bloque hero-content: .hero-brand, regla, h1, subtítulo, CTA
style.css           # --font-display, jerarquía clamp, saltos de H1 desktop, media 768/1024
script.js           # Sin cambios previstos
logo.jpeg           # Sin cambios
assets/
└── fondoexploretours.png
```

**Structure Decision**: Superficie única en la raíz. Delta: `index.html` (semántica + copy) y `style.css` (tokens y layout del bloque izquierdo). No `src/`. El buscador `.hero-footer` no se rediseña.

## Complexity Tracking

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| Tercera familia (Fraunces vía Google Fonts) | Clarificación B: carácter de marca contemporáneo exclusivo del identificador | Reusar Playfair/Montserrat (opción A) se percibe ornamental o genérico; agrandar el título actual no cumple FR-008 |
