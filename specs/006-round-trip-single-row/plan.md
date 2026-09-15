# Implementation Plan: Ida y vuelta en una sola fila

**Branch**: `006-round-trip-single-row` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/006-round-trip-single-row/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

En escritorio típico (~1280px), Transporte **Ida y vuelta** MUST mostrar origen, swap, destino, fecha de ida, fecha de regreso, hora, pasajeros y **Pedir cotización** en **una sola fila**. Eso **sustituye** el grid de dos filas de 005 (`origin swap dest depart ret` / `time time pax pax cta`). Compactar anchos (`minmax` más bajos, CTA un poco menos ancho); MUST NOT recortar labels, MUST NOT scroll horizontal, MUST NOT bajar tipografía a densidad admin. Móvil/tablet (375 / 768) conservan reflujo. Vanilla: delta casi solo en `style.css`; `initSearch` ya pone `.is-round-trip`.

## Technical Context

**Language/Version**: HTML5, CSS3 Grid (`grid-template-areas`), JavaScript ES2015+ (sin cambio de negocio)

**Primary Dependencies**: Ninguna nueva. Clase `.is-round-trip` existente.

**Storage**: N/A

**Testing**: Manual ([quickstart.md](./quickstart.md)). Sin runner.

**Target Platform**: Landing estática. Verificación 375 / 768 / 1280.

**Project Type**: Landing de una sola página

**Performance Goals**: Solo CSS; 0 JS extra en el camino crítico.

**Constraints**: Constitución v1.1.0. MUST NOT npm/datepicker. MUST NOT tocar validaciones, WhatsApp, copy, catálogo, FAQ, marca. Conservar `name` de campos y `.is-round-trip`.

**Scale/Scope**: Media query `@media (min-width: 1280px)` de `.search-fields-transport.is-round-trip` (y columnas asociadas). Tablet/móvil fuera de cambio salvo regresión.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | Solo CSS de raíz. |
| G2 | II. Español y SEO | PASS | Sin copy nuevo de producto; labels existentes. |
| G3 | III. WhatsApp único | PASS | CTA naranja y `wa.me` intactos. |
| G4 | IV. Identidad | PASS | Paleta y Montserrat del panel; no Fraunces en el cotizador. |
| G5 | V. Vanilla | PASS | Grid CSS; sin librerías. |
| G6 | Alcance comercial | PASS | Sin ofertas nuevas. |
| G7 | Destinos / ancla | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart 375/768/1280: una fila en 1280; sin overflow-x. |

**Post-design (Phase 1):** G1–G8 PASS. Compactar `minmax` no viola densidad 005 si labels ≥14px y altura de input ~48–52px se mantienen.

## Project Structure

### Documentation (this feature)

```text
specs/006-round-trip-single-row/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── round-trip-row.md
└── tasks.md
```

### Source Code (repository root)

```text
style.css    # ≥1280: .is-round-trip una fila (8 áreas); anchos compactos
index.html   # Sin cambio de orden DOM (ya correcto)
script.js    # Sin cambio (toggle .is-round-trip ya existe)
```

**Structure Decision**: Tres archivos de raíz. **006 manda** sobre el layout de Ida y vuelta de 005; el resto de 005 sigue vigente.

## Complexity Tracking

Ninguna violación de constitución.
