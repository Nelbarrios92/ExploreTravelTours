# Implementation Plan: Composición del Hero en móvil

**Branch**: `013-mobile-hero-layout` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/013-mobile-hero-layout/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

En **&lt;768px**, el copy del Hero deja de recentrarse en el hueco del buscador. Un **bloque de mensaje** (marca + regla + descripción) queda **arriba**; un **bloque de acción** (Explorar servicios + redes) queda **abajo del hueco**, pegado al pie. Al abrir Pedir cotización el pie crece, el aire se come, el mensaje se mueve **&lt; 8 px** y el botón sube pero sigue tocable (solo ida). Escritorio y 011/012 sin cambio. Vanilla: wrappers + CSS; **sin JS**.

## Technical Context

**Language/Version**: HTML5, CSS3 (flex: `flex-start` + `margin-top: auto` en &lt;768px)

**Primary Dependencies**: `.hero-layout`, `.hero-content`, `.hero-footer`, `#hero-search` (011/012)

**Storage**: N/A

**Testing**: Manual ([quickstart.md](./quickstart.md))

**Target Platform**: Landing 375 (composición) / 768 / 1280 (sin cambio)

**Project Type**: Landing de una sola página

**Performance Goals**: SC-002 desplazamiento del mensaje &lt; ~8 px al abrir; 0 trabajo extra en JS

**Constraints**: Constitución v1.1.0. MUST NOT npm. MUST NOT cambiar copy, fuentes 002, acordeón 011/012 ni Hero de escritorio.

**Scale/Scope**: Solo composición vertical del Hero en vista estrecha.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | HTML/CSS raíz. |
| G2 | II. Español y SEO | PASS | Sin copy nuevo. |
| G3 | III. WhatsApp | PASS | Fuera. |
| G4 | IV. Identidad | PASS | Hero viewport, overlay, Fraunces solo en `.hero-brand`. |
| G5 | V. Vanilla | PASS | Sin JS de layout. |
| G6 | Alcance | PASS | Fuera catálogo/FAQ. |
| G7 | Destinos | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart 375 cerrado/abierto + 1280. |

**Post-design (Phase 1):** G1–G8 PASS. Wrappers semánticos de agrupación; `display` de escritorio no usa `contents` si rompe foco (flex hijos normales).

## Project Structure

### Documentation (this feature)

```text
specs/013-mobile-hero-layout/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── hero-mobile-layout.md
└── tasks.md
```

### Source Code (repository root)

```text
index.html   # .hero-message + .hero-actions dentro de .hero-content
style.css    # max-width 767: mensaje arriba, acciones margin-top auto
script.js    # sin cambio
```

**Structure Decision**: Tres archivos de raíz. **013 manda** la composición del copy móvil. **011/012** mandan el pie de cotización.

## Complexity Tracking

Ninguna violación de constitución.
