# Implementation Plan: Booking bar premium del Hero

**Branch**: `005-hero-booking-bar` | **Date**: 2026-09-14 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/005-hero-booking-bar/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

Sustituir el cotizador denso de `#hero-search` por una **booking bar** de movilidad: orden de viaje correcto, densidad ≥14px / campos ~48–52px, CTA naranja **Pedir cotización** + resumen inline + verde **Continuar por WhatsApp**, 0 overlap del FAB, pills/segmented, swap origen↔destino, datalist enriquecido, locale es-CO. **Supera 004**: no chrome vacío, no “Buscar / Continuar”, no `has-request` en el header. Validaciones y `wa.me/573042143149` iguales. Vanilla: `index.html`, `style.css`, `script.js` (delta en `initSearch` + observer del FAB).

## Technical Context

**Language/Version**: HTML5, CSS3, JavaScript ES2015+ (vanilla; `IntersectionObserver` para el FAB)

**Primary Dependencies**: Ninguna nueva. Fecha/hora nativas. `datalist` existente. Paleta `:root`.

**Storage**: N/A

**Testing**: Manual ([quickstart.md](./quickstart.md)). Sin runner/TypeScript.

**Target Platform**: Landing estática. 375 / 768 / 1024 / 1280.

**Project Type**: Landing de una sola página

**Performance Goals**: Observer no bloquea render (`DOMContentLoaded`). Submit &lt;100 ms percibidos (DOM only).

**Constraints**: Constitución v1.1.0. MUST NOT npm/datepicker/backend. MUST NOT precios. Selectores de negocio a conservar: `name` de campos, `#search-form-*`, `#quote-summary`, `#same-place-prompt`. Dejar de usar `#nav-request` / `.has-request` como confirmación.

**Scale/Scope**: `#hero-search` + FAB + mínimo header (quitar bloque TU SOLICITUD) + de-énfasis leve de `.lets-go-btn` / `.hero-social`. Catálogo/FAQ/marca del Hero fuera.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | Solo raíz HTML/CSS/JS. |
| G2 | II. Español y SEO | PASS | Copy ES; `lang`; placeholders es-CO; meta intactos. |
| G3 | III. WhatsApp único | PASS | Submit no abre WA; resumen sí. FAB y header Contactar Ya se conservan (FAB se oculta solo mientras el cotizador está en vista). |
| G4 | IV. Identidad | PASS | Paleta; Montserrat UI del panel; Fraunces no en el cotizador; hero viewport + overlay. |
| G5 | V. Vanilla | PASS | Observer nativo; sin npm. |
| G6 | Alcance comercial | PASS | Sin ofertas nuevas; datalist = destinos ya publicados. |
| G7 | Destinos / ancla | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart 375/768/1280: overlap, orden, un feedback. |

**Post-design (Phase 1):** G1–G8 PASS. Quitar `has-request` no viola WhatsApp (quedan 3 superficies: header, FAB condicional, CTA del resumen).

## Project Structure

### Documentation (this feature)

```text
specs/005-hero-booking-bar/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── booking-bar.md
└── tasks.md
```

### Source Code (repository root)

```text
index.html   # Orden campos, copy CTA, pills, swap, datalist, quitar nav-request
style.css    # Densidad, grid 2 filas ida-vuelta, segmented/pills, FAB hidden
script.js    # renderQuote sin activateRequestState; swap; IntersectionObserver FAB
```

**Structure Decision**: Tres archivos de raíz. 004 queda documentación histórica; **005 manda**.

## Complexity Tracking

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| `IntersectionObserver` para ocultar `.floating-wa` | 0 overlap FAB↔CTA (FR-008) | Solo `bottom` más alto no cubre móvil + resumen; no oculta competencia visual |
