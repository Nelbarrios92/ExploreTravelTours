# Implementation Plan: Categoría de alojamientos en Experiencias

**Branch**: `003-lodging-category` | **Date**: 2026-09-12 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/003-lodging-category/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

Añadir al catálogo `#experiences` el chip **Alojamientos** y exactamente dos cards (`Apartamento Laguito`, `Apartamento Torices`) con el mismo markup/estilo que las experiencias actuales (`article.service-card`, imagen, h3, párrafo, CTA WhatsApp). El filtro JS existente (`data-filter` / `data-category`) ya es genérico: no hace falta nueva lógica salvo el chip y las cards. Fotos propias en `assets/` (las que suba el negocio). Sin rediseño de cards, sin menú nuevo, sin precios ni motor de reservas.

## Technical Context

**Language/Version**: HTML5, CSS3, JavaScript ES2015+ (vanilla)

**Primary Dependencies**: Las del sitio (`wa.me`, Unicons, Google Fonts). Sin npm ni librerías nuevas.

**Storage**: N/A. Inventario en HTML estático.

**Testing**: Manual en navegador ([quickstart.md](./quickstart.md)). Sin runner.

**Target Platform**: Landing estática `https://www.exploretours.co/`. Viewports 375 / 768 / 1280.

**Project Type**: Landing de una sola página (marketing)

**Performance Goals**: Filtro de catálogo percibido como instantáneo (mismo `setCatalogFilter`; ~13 cards). Imágenes de alojamiento con `alt` descriptivo; peso razonable (mismas convenciones que el resto de `assets/`).

**Constraints**: Constitución v1.1.0 — estático, español, WhatsApp único, vanilla, paleta/tipografía de cards sin `--font-display`. MUST NOT inventar inmuebles, tarifas ni reutilizar fotos de tours. MUST NOT vaciar Schema.org. Ofertas mínimas actuales se conservan.

**Scale/Scope**: +1 chip, +2 cards, intro de sección MAY mencionar alojamientos. Hero, buscador, FAQ, nav: sin cambios de arquitectura.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | Cards en `index.html`; fotos en `assets/`. |
| G2 | II. Español y SEO | PASS | Copy ES; `alt` por inmueble; meta/JSON-LD intactos. |
| G3 | III. WhatsApp único | PASS | `data-wa-title` + `buildWhatsAppUrl` existente. |
| G4 | IV. Identidad | PASS | Reutiliza `.service-card` / `.filter-chip`; Fraunces no se aplica a cards. |
| G5 | V. Vanilla | PASS | Sin dependencias; JS de catálogo ya filtra por `data-category`. |
| G6 | Alcance comercial | PASS | Inventario mínimo de tours/traslados/barcos/destinos se conserva. Alojamientos son **adicionales** autorizados por spec 003 (Laguito y Torices). |
| G7 | Destinos / ancla | PASS | `#destinations` → Destinos Caribe sin cambio. |
| G8 | Verificación | PASS | Quickstart 375 / 768 / 1280; menú y WhatsApp. |

**Post-design (Phase 1):** Gates G1–G8 siguen en PASS. Contratos extienden el catálogo 001; no hay backend. No se enmienda la constitución: el “como mínimo” comercial no se reduce.

## Project Structure

### Documentation (this feature)

```text
specs/003-lodging-category/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── catalog-alojamientos.md
└── tasks.md              # Phase 2 (/speckit-tasks)
```

### Source Code (repository root)

```text
index.html          # Chip Alojamientos + 2 service-card; intro de sección opcional
style.css           # Solo si el wrap de chips lo requiere (preferir 0 cambios)
script.js           # Sin cambios previstos (initCatalog ya cubre chips/cards nuevos)
assets/
├── apartamento-laguito.jpeg
└── apartamento-torices.jpeg
```

**Structure Decision**: Superficie única en raíz. Delta principal: `index.html` + dos archivos de imagen. `script.js` solo si un selector se rompe (no esperado).

## Complexity Tracking

> Sin violaciones. El filtro genérico evita código nuevo de catálogo.
