# Implementation Plan: Buscador desplegable en móvil

**Branch**: `011-mobile-search-accordion` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/011-mobile-search-accordion/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

En **&lt;768px**, al **componer**, `#hero-search` es un acordeón: cabecera **Pedir cotización** (siempre visible, `aria-expanded` + chevron) y cuerpo 010 debajo. Cerrado al cargar (`is-collapsed`). El naranja sigue siendo el único submit. En **≥768px** y en **`.is-quoted`** no hay acordeón (006 / 009). Vanilla: `index.html` (cabecera + wrapper), `style.css`, poco JS (toggle, abrir en Modificar).

## Technical Context

**Language/Version**: HTML5, CSS3, JavaScript (vanilla, `DOMContentLoaded`)

**Primary Dependencies**: `#hero-search`, `.is-quoted` (007), densidad 010, `hideQuote` / `renderQuote`

**Storage**: N/A (sin persistir abierto/cerrado)

**Testing**: Manual ([quickstart.md](./quickstart.md))

**Target Platform**: Landing 375 (acordeón) / 768 / 1280 (siempre abierto)

**Project Type**: Landing de una sola página

**Performance Goals**: Toggle instantáneo (CSS); sin librerías

**Constraints**: Constitución v1.1.0. MUST NOT npm. MUST NOT persistir en storage. MUST NOT aplicar acordeón al resumen. MUST NOT usar la franja como submit.

**Scale/Scope**: Pie del Hero al componer en móvil. Fuera: catálogo, 006, 009 visual.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | HTML/CSS/JS raíz; sin persistencia. |
| G2 | II. Español y SEO | PASS | Copy **Pedir cotización**. |
| G3 | III. WhatsApp | PASS | Submit naranja y `wa.me` intactos. |
| G4 | IV. Identidad | PASS | Hero más visible en 375. |
| G5 | V. Vanilla | PASS | Sin `<details>` de FAQ mezclado; botón + clase. |
| G6 | Alcance | PASS | Fuera. |
| G7 | Destinos | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart 375 abierto/cerrado + 1280. |

**Post-design (Phase 1):** G1–G8 PASS. `aria-expanded` + texto fijo cumplen a11y táctil.

## Project Structure

### Documentation (this feature)

```text
specs/011-mobile-search-accordion/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── accordion.md
└── tasks.md
```

### Source Code (repository root)

```text
index.html   # Botón cabecera + wrapper del compositor
style.css    # Mostrar/ocultar cuerpo <768px; ocultar cabecera ≥768 y .is-quoted
script.js    # Toggle; default cerrado; Modificar quita is-collapsed
```

**Structure Decision**: Tres archivos de raíz. **011 manda** visibilidad del compositor en móvil. **010** densidad abierto. **007/009** cotizado.

## Complexity Tracking

Ninguna violación de constitución.
