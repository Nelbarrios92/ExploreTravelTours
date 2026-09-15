# Implementation Plan: Buscador de escritorio otra vez en el pie del Hero

**Branch**: `014-desktop-search-footer` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/014-desktop-search-footer/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

En **≥768px**, el Hero vuelve a **altura de ventana** y `#hero-search` queda **siempre abierto en `.hero-footer`** (barra 005/006). La clase `is-collapsed` no pliega el compositor. La franja Pedir cotización sigue `display: none`. En **&lt;768px** MUST NOT cambiar 011/012/013: `height: auto` del Hero y el acordeón se quedan en el media **767**. Vanilla CSS; **sin JS**.

## Technical Context

**Language/Version**: HTML5, CSS3 (`min-width: 768px` ancla; `max-width: 767px` congelado)

**Primary Dependencies**: `.hero-section`, `.hero-layout`, `.hero-footer`, `#hero-search.is-collapsed`, `.search-accordion-toggle`

**Storage**: N/A

**Testing**: Manual ([quickstart.md](./quickstart.md))

**Target Platform**: 1280 (pie) / 768 (pie, sin acordeón) / 375 (sin cambio)

**Project Type**: Landing de una sola página

**Performance Goals**: 0 JS; pie del buscador alineado al borde inferior del Hero en escritorio

**Constraints**: Constitución v1.1.0. MUST NOT npm. MUST NOT editar reglas 013/011/012 de `max-width: 767px` salvo mover `height: auto` del Hero fuera de `max-width: 768px` hacia 767.

**Scale/Scope**: Solo pin del buscador en vista ancha.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | CSS raíz. |
| G2 | II. Español y SEO | PASS | Sin copy. |
| G3 | III. WhatsApp | PASS | Fuera. |
| G4 | IV. Identidad | PASS | Hero viewport en escritorio (principio IV). |
| G5 | V. Vanilla | PASS | Sin JS. |
| G6 | Alcance | PASS | Fuera catálogo. |
| G7 | Destinos | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart 1280 + 375. |

**Post-design (Phase 1):** G1–G8 PASS. Congelar 767; restaurar 100vh solo ≥768.

## Project Structure

### Documentation (this feature)

```text
specs/014-desktop-search-footer/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── desktop-search-footer.md
└── tasks.md
```

### Source Code (repository root)

```text
style.css    # 767: height auto (móvil). ≥768: 100vh + compositor visible
index.html   # sin cambio de estructura
script.js    # sin cambio (is-collapsed ignorado en CSS desktop)
```

**Structure Decision**: CSS de corte 767/768. **014 manda** el pie en escritorio. **011–013 mandan** el móvil.

## Complexity Tracking

Ninguna violación de constitución.
