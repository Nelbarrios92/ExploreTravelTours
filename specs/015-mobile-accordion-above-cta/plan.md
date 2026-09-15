# Implementation Plan: Acordeón móvil encima de Explorar servicios

**Branch**: `015-mobile-accordion-above-cta` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/015-mobile-accordion-above-cta/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

En **&lt;768px**, el orden visual es mensaje 013 → **aire** → **Pedir cotización** → **Explorar servicios**. `.hero-content` usa `display: contents` para que `.hero-footer` pueda intercalarse con `order`. `margin-top: auto` pasa al footer (el par baja). Escritorio **014** sin `contents` ni `order`. 011/012 intactos. Vanilla CSS; **sin JS**.

## Technical Context

**Language/Version**: HTML5, CSS3 (`display: contents` + `flex-order` en `max-width: 767px`)

**Primary Dependencies**: `.hero-layout`, `.hero-content`, `.hero-message`, `.hero-actions`, `.hero-footer`

**Storage**: N/A

**Testing**: Manual ([quickstart.md](./quickstart.md))

**Target Platform**: 375 (reorden) / 1280 (014)

**Project Type**: Landing de una sola página

**Performance Goals**: Título Δ &lt; ~8 px al abrir; 0 JS

**Constraints**: Constitución v1.1.0. MUST NOT npm. MUST NOT cambiar 012 ni el DOM de escritorio percibido (014).

**Scale/Scope**: Solo orden móvil cotizador vs Explorar.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | CSS. |
| G2 | II. Español y SEO | PASS | Sin copy. |
| G3 | III. WhatsApp | PASS | Fuera. |
| G4 | IV. Identidad | PASS | Hero intacto. |
| G5 | V. Vanilla | PASS | Sin JS. |
| G6 | Alcance | PASS | Fuera catálogo. |
| G7 | Destinos | PASS | Fuera. |
| G8 | Verificación | PASS | 375 + 1280. |

**Post-design (Phase 1):** G1–G8 PASS. `display: contents` solo en 767 sobre el agrupador, no sobre controles.

## Project Structure

### Documentation (this feature)

```text
specs/015-mobile-accordion-above-cta/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── accordion-above-cta.md
└── tasks.md
```

### Source Code (repository root)

```text
style.css    # 767: contents + order; auto en footer
index.html   # sin cambio de árbol (footer sigue hermano de content)
script.js    # sin cambio
```

**Structure Decision**: Reorden **visual** en CSS. **015** manda el orden móvil. **014** el escritorio.

## Complexity Tracking

Ninguna violación de constitución.
