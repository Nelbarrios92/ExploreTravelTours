# Implementation Plan: Card de resumen más compacta

**Branch**: `009-quote-card-compact` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/009-quote-card-compact/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

En `#hero-search.is-quoted`, compactar **de forma moderada** el resumen para que no parta el Hero: menos padding del card, tipo un paso bajo 008, CTAs **~40–44px** (no 50px de Pedir cotización, no 0.78rem admin). El buscador al componer (006/005, submit 50px) **no** se toca. Vanilla: `style.css` acotado a `.quote-*` y `#hero-search.is-quoted`. 007 intacto.

## Technical Context

**Language/Version**: HTML5, CSS3

**Primary Dependencies**: Clase `.is-quoted` (007). Selectores `.quote-summary`, `.quote-lines`, `.quote-wa-btn`, `.quote-modify`, `.quote-related`

**Storage**: N/A

**Testing**: Manual ([quickstart.md](./quickstart.md))

**Target Platform**: Landing 375 / 1280

**Project Type**: Landing de una sola página

**Performance Goals**: Solo CSS

**Constraints**: Constitución v1.1.0. MUST NOT achicar `.search-submit` / grid 006. MUST NOT npm. MUST NOT caja gris anidada.

**Scale/Scope**: Estilos del estado cotizado. Fuera: JS, catálogo, marca.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | CSS raíz. |
| G2 | II. Español y SEO | PASS | Sin copy. |
| G3 | III. WhatsApp | PASS | Verde más bajo, mismo destino. |
| G4 | IV. Identidad | PASS | Hero vuelve a dominar; paleta igual. |
| G5 | V. Vanilla | PASS | Sin libs. |
| G6 | Alcance | PASS | Fuera. |
| G7 | Destinos | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart 375/1280 altura vs buscador. |

**Post-design (Phase 1):** G1–G8 PASS. CTAs 40–44px cumplen táctil 375 (min ~40px) sin igualar 50px.

## Project Structure

### Documentation (this feature)

```text
specs/009-quote-card-compact/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── quoted-card.md
└── tasks.md
```

### Source Code (repository root)

```text
style.css    # Compactar .quote-* y padding de #hero-search.is-quoted
index.html   # Sin cambio
script.js    # Sin cambio
```

**Structure Decision**: Tres archivos de raíz. **009 manda** sobre talla del estado cotizado (008 talla grande queda sustituida ahí).

## Complexity Tracking

Ninguna violación de constitución.
