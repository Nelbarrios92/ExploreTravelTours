# Implementation Plan: Consistencia UX del buscador del Hero

**Branch**: `004-search-form-consistency` | **Date**: 2026-09-14 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/004-search-form-consistency/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

Unificar visualmente `#hero-search` (Transporte / Por horas) sin tocar la lógica de `initSearch`: mismos `id`, `name`, validaciones, resumen y WhatsApp. Pasar de etiquetas flotantes a **label arriba + control**; meter el CTA en la **misma grid** que los campos en desktop; tabs iguales (activo `--brand-blue`, inactivo neutro); franja `.search-chrome` de altura fija en ambos modos (radios solo en Transporte). Corregir solape Duración/Selecciona. Responsive: 1 columna en móvil, fila compacta en ≥1280px. Superficie: `index.html` + `style.css`; `script.js` solo si un selector de `.field-return` o radios se mueve.

## Technical Context

**Language/Version**: HTML5, CSS3, JavaScript ES2015+ (vanilla)

**Primary Dependencies**: Ninguna nueva. Fecha/hora nativas. Unicons ya en el sitio. Paleta `:root` existente.

**Storage**: N/A (estado en el DOM)

**Testing**: Manual ([quickstart.md](./quickstart.md)). Sin TypeScript ni bundler en este repo.

**Target Platform**: Landing estática. Viewports 375 / 768 / 1024 / 1280.

**Project Type**: Landing de una sola página

**Performance Goals**: Sin JS extra de layout; cambio de tab percibido como instantáneo (ya es `hidden` en formularios).

**Constraints**: Constitución v1.1.0. MUST NOT npm/framework/datepicker. MUST NOT cambiar reglas de cotización. Selectores JS a conservar: `#search-form-transporte`, `#search-form-hourly`, `name` de campos, `.field-return`, `input[name="trip-type"]`, `#same-place-prompt`, `#switch-to-hourly`, `#quote-summary`.

**Scale/Scope**: Un panel al pie del Hero. Catálogo, navbar, marca del Hero fuera de alcance.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | Solo HTML/CSS(/JS mínimo). |
| G2 | II. Español y SEO | PASS | Labels y errores en ES; meta intactos. |
| G3 | III. WhatsApp único | PASS | Buscar no abre WhatsApp; el resumen sí. |
| G4 | IV. Identidad | PASS | `--brand-blue` / `--brand-orange` / verde solo WA; Montserrat en UI del buscador; Fraunces no se aplica al panel. Overlay y pie del hero se conservan. |
| G5 | V. Vanilla | PASS | Grid/flex; sin librerías. |
| G6 | Alcance comercial | PASS | Sin ofertas nuevas. |
| G7 | Destinos / ancla | PASS | Fuera de alcance. |
| G8 | Verificación | PASS | Quickstart 375 / 768 / 1280; tabs, submit, origen=destino. |

**Post-design (Phase 1):** Gates G1–G8 PASS. Contratos de layout no introducen backend.

## Project Structure

### Documentation (this feature)

```text
specs/004-search-form-consistency/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── search-layout.md
└── tasks.md
```

### Source Code (repository root)

```text
index.html    # Markup: .search-chrome, labels estáticos, CTA dentro de .search-fields
style.css     # Reemplazo del bloque floating-label / grid / tabs / submit
script.js     # initSearch intacto salvo ajuste de selector si .field-return se reubica
```

**Structure Decision**: Delta de presentación en el pie del hero. Dos `<form>` se mantienen (menos riesgo en JS) con **el mismo esqueleto CSS**.

## Complexity Tracking

> Sin violaciones de constitución. Unificar a un solo `<form>` con campos hidden se rechazó (más riesgo en `initSearch`).
