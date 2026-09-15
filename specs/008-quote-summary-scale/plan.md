# Implementation Plan: Escala unificada del resumen de cotización

**Branch**: `008-quote-summary-scale` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/008-quote-summary-scale/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

Unificar la escala del `#quote-summary` con el buscador del mismo `#hero-search`: cuerpo ≥14px, valores ~15px, CTAs **50px** (igual que Pedir cotización), radio 10px. **Quitar** la caja interior gris (`background`/`border`/`padding` extra del resumen) para que, con `.is-quoted`, el contenido use el padding del card (12–14px). Eliminar overrides compactos de `@media (min-width: 1280px)` en `.quote-lines`. Vanilla: casi solo `style.css`. 007 y 006 intactos.

## Technical Context

**Language/Version**: HTML5, CSS3

**Primary Dependencies**: Ninguna. Selectores existentes `.quote-summary`, `.quote-lines`, `.quote-wa-btn`, `.quote-modify`, `.quote-related`

**Storage**: N/A

**Testing**: Manual ([quickstart.md](./quickstart.md))

**Target Platform**: Landing estática. 375 / 1280

**Project Type**: Landing de una sola página

**Performance Goals**: Solo CSS

**Constraints**: Constitución v1.1.0. MUST NOT tocar `initSearch` salvo bug. MUST NOT npm. Fraunces no en el resumen.

**Scale/Scope**: Estilos del resumen + media 1280 que hoy lo compacta. Fuera: grid 006, JS 007.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | CSS de raíz. |
| G2 | II. Español y SEO | PASS | Sin copy nuevo. |
| G3 | III. WhatsApp | PASS | Verde intacto. |
| G4 | IV. Identidad | PASS | Paleta; Montserrat/Playfair; no Fraunces en resumen. |
| G5 | V. Vanilla | PASS | Sin libs. |
| G6 | Alcance comercial | PASS | Fuera. |
| G7 | Destinos | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart 375/1280 escala + padding. |

**Post-design (Phase 1):** G1–G8 PASS.

## Project Structure

### Documentation (this feature)

```text
specs/008-quote-summary-scale/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── quote-scale.md
└── tasks.md
```

### Source Code (repository root)

```text
style.css    # Escala + quitar caja interior; igualar CTAs; no compactar en 1280
index.html   # Sin cambio de copy/ids
script.js    # Sin cambio
```

**Structure Decision**: Tres archivos de raíz. **008 manda** sobre densidad del resumen.

## Complexity Tracking

Ninguna violación de constitución.
