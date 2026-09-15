# Implementation Plan: Buscador más compacto en móvil

**Branch**: `010-mobile-search-compact` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/010-mobile-search-compact/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

En viewport estrecho (**&lt;768px**, componer), compactar **de forma moderada** `#hero-search` (no cotizado): menos padding/aire, campos un paso más bajos, **todo apilado a ancho completo**, y **ocultar** `#swap-places` sin dejar hueco de grid. **Pedir cotización** sigue el CTA principal (~50px). En **≥768px** no se toca 006 ni el intercambio origen/destino. Vanilla: casi solo `style.css`. 007/009 intactos.

## Technical Context

**Language/Version**: HTML5, CSS3

**Primary Dependencies**: Grid `.search-fields-transport` / `.search-fields-hourly`; `#swap-places`; `#hero-search` sin `.is-quoted`

**Storage**: N/A

**Testing**: Manual ([quickstart.md](./quickstart.md))

**Target Platform**: Landing 375 (cambio) / 768 / 1280 (regresión)

**Project Type**: Landing de una sola página

**Performance Goals**: Solo CSS

**Constraints**: Constitución v1.1.0. MUST NOT npm. MUST NOT achicar escritorio 006. MUST NOT emparejar campos en móvil. MUST NOT compactar `.quote-*` / `.is-quoted`. MUST NOT cambiar validación ni `script.js` salvo que el hueco de swap lo exija (no debería).

**Scale/Scope**: Estilos del buscador al componer en &lt;768px. Fuera: catálogo, marca, card cotizado.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | CSS raíz. |
| G2 | II. Español y SEO | PASS | Sin copy. |
| G3 | III. WhatsApp | PASS | Submit naranja y FAB intactos. |
| G4 | IV. Identidad | PASS | Hero más visible en 375; paleta/fuentes igual. |
| G5 | V. Vanilla | PASS | Sin libs. |
| G6 | Alcance | PASS | Fuera. |
| G7 | Destinos | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart 375 compacto + swap 0; 768/1280 swap y una fila. |

**Post-design (Phase 1):** G1–G8 PASS. Campos ~44px y CTA 50px en móvil: táctil usable, CTA sigue principal.

## Project Structure

### Documentation (this feature)

```text
specs/010-mobile-search-compact/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── mobile-search.md
└── tasks.md
```

### Source Code (repository root)

```text
style.css    # Compactar buscador <768px; ocultar swap; grid sin fila swap
index.html   # Sin cambio (el botón de intercambio permanece en el DOM)
script.js    # Sin cambio
```

**Structure Decision**: Tres archivos de raíz. **010 manda** sobre el buscador al componer en vista estrecha. **006 manda** ≥1280 una fila. **009 manda** estado cotizado.

## Complexity Tracking

Ninguna violación de constitución.
