# Implementation Plan: Solo el resumen tras cotizar

**Branch**: `007-quote-summary-only` | **Date**: 2026-09-15 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/007-quote-summary-only/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

Tras **Pedir cotización** válido, `#hero-search` muestra **solo** `#quote-summary` (datos, verde Continuar por WhatsApp, relacionados). Tabs y ambos formularios se ocultan. Botón **Modificar** en el resumen (no el header) restaura el buscador con los valores en los `input` (no se recarga). Envíos inválidos no ocultan el buscador. Vanilla: `index.html` (botón), `style.css` (estado `.is-quoted`), `script.js` (`renderQuote` / `hideQuote` / listener Modificar). 006 y validaciones intactos.

## Technical Context

**Language/Version**: HTML5, CSS3, JavaScript ES2015+ (vanilla)

**Primary Dependencies**: Ninguna. Reutilizar `#quote-summary`, `renderQuote`, `hideQuote`.

**Storage**: N/A (valores viven en el DOM de los forms)

**Testing**: Manual ([quickstart.md](./quickstart.md))

**Target Platform**: Landing estática. 375 / 768 / 1280.

**Project Type**: Landing de una sola página

**Performance Goals**: Toggle de `hidden`/clase; sin red de cotización.

**Constraints**: Constitución v1.1.0. MUST NOT `has-request` en navbar. MUST NOT npm. `wa.me/573042143149` y `name` de campos inmutables.

**Scale/Scope**: Card `#hero-search` + `initSearch`. Fuera: catálogo, FAQ, marca, grid 006.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Gate | Principle | Verdict | Notes |
|------|-----------|---------|-------|
| G1 | I. Sitio estático | PASS | Solo raíz HTML/CSS/JS. |
| G2 | II. Español y SEO | PASS | Copy **Modificar**; meta intactos. |
| G3 | III. WhatsApp único | PASS | Verde abre WA; naranja no; FAB se conserva (observer sobre `#hero-search`). |
| G4 | IV. Identidad | PASS | Paleta; Modificar ghost/secundario, no rivaliza el verde. |
| G5 | V. Vanilla | PASS | `hidden` + clase. |
| G6 | Alcance comercial | PASS | Sin ofertas nuevas. |
| G7 | Destinos / ancla | PASS | Fuera. |
| G8 | Verificación | PASS | Quickstart: éxito, error, Modificar, 375/1280. |

**Post-design (Phase 1):** G1–G8 PASS. Ocultar forms no viola WhatsApp (CTA del resumen + header + FAB condicional).

## Project Structure

### Documentation (this feature)

```text
specs/007-quote-summary-only/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── quote-view.md
└── tasks.md
```

### Source Code (repository root)

```text
index.html   # Botón type=button.quote-modify “Modificar” dentro de #quote-summary
style.css    # #hero-search.is-quoted oculta tabs/paneles; estilo ghost de Modificar
script.js    # renderQuote → is-quoted; Modificar → hideQuote + quitar is-quoted
```

**Structure Decision**: Tres archivos de raíz. **007 manda** sobre “formulario visible bajo el resumen” de 005.

## Complexity Tracking

Ninguna violación de constitución.
