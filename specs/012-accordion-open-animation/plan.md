# Implementation Plan: Animación al abrir y cerrar el acordeón

**Branch**: `012-accordion-open-animation` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/012-accordion-open-animation/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

En **&lt;768px**, el gesto de la franja **Pedir cotización** anima la **altura** de `.search-composer` (~320 ms, `ease`, sin bounce). Cotizar y **Modificar** siguen instantáneos (`display` / `.is-quoted`). `prefers-reduced-motion: reduce` anula la transición. Vanilla: CSS + un wrapper interno; JS de 011 casi igual.

## Technical Context

**Language/Version**: HTML5, CSS3 (grid `0fr`/`1fr` + `overflow: hidden`)

**Primary Dependencies**: `#hero-search.is-collapsed`, `.search-composer`, `setAccordionOpen` (011)

**Storage**: N/A

**Testing**: Manual ([quickstart.md](./quickstart.md))

**Target Platform**: Landing 375 (animación) / 768 / 1280 (sin acordeón)

**Project Type**: Landing de una sola página

**Performance Goals**: Transición &lt; 500 ms; sin libs

**Constraints**: Constitución v1.1.0. MUST NOT npm. MUST NOT animar 009 ni Modificar. MUST NOT bounce.

**Scale/Scope**: Solo toggle de la franja en móvil. Fuera: Hero, FAQ, catálogo.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | CSS/HTML raíz. |
| G2 | II. Español y SEO | PASS | Sin copy nuevo. |
| G3 | III. WhatsApp | PASS | Fuera. |
| G4 | IV. Identidad | PASS | `--transition` / ease; paleta igual. |
| G5 | V. Vanilla | PASS | Sin GSAP. |
| G6 | Alcance | PASS | Fuera. |
| G7 | Destinos | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart 375 + reduced-motion. |

**Post-design (Phase 1):** G1–G8 PASS. `prefers-reduced-motion` cubre FR-005.

## Project Structure

### Documentation (this feature)

```text
specs/012-accordion-open-animation/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── accordion-motion.md
└── tasks.md
```

### Source Code (repository root)

```text
index.html   # Wrapper interno .search-composer-body (un hijo de grid)
style.css    # 0fr/1fr, 320ms, reduced-motion; quitar display:none del colapso
script.js    # Sin cambio funcional salvo que el CSS deje de usar display:none
```

**Structure Decision**: Tres archivos de raíz. **012 manda** el movimiento del toggle. **011** cuándo hay acordeón.

## Complexity Tracking

Ninguna violación de constitución.
