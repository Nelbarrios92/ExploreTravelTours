# Tasks: Solo el resumen tras cotizar

**Input**: Design documents from `/specs/007-quote-summary-only/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US2 según spec.md. **007 manda** sobre el formulario visible bajo el resumen de 005.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US2
- Cada tarea incluye ruta

## Path Conventions

`index.html`, `style.css`, `script.js`. Contrato: `specs/007-quote-summary-only/contracts/quote-view.md`. Conservar ids de `initSearch`.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: No romper cotización ni WhatsApp

- [X] T001 Confirmar en `index.html` / `script.js` `#hero-search`, `#quote-summary`, `#quote-wa-btn`, `#search-form-transporte`, `#search-form-hourly`, `renderQuote` / `hideQuote`; MUST NOT reintroducir `.has-request`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Markup del control Modificar (visible solo con el resumen)

**⚠️ CRITICAL**: El botón debe existir antes de cablear JS

- [X] T002 En `index.html`, dentro de `#quote-summary` (después de `#quote-wa-btn`), añadir `<button type="button" class="quote-modify" id="quote-modify">Modificar</button>`; MUST NOT ponerlo en el header

**Checkpoint**: Modificar en el card; forms aún se ven junto al resumen (hasta US1)

---

## Phase 3: User Story 1 - Ver solo la confirmación después de cotizar (Priority: P1) 🎯 MVP

**Goal**: Tras submit válido, solo el resumen; tabs y campos ocultos

**Independent Test**: Quickstart pasos 1–2 y 5

### Implementation for User Story 1

- [X] T003 [US1] En `style.css`, con `#hero-search.is-quoted`, ocultar `.search-tabs`, `.search-panel`, `.search-errors`, `#same-place-prompt`; `#quote-summary` sigue visible cuando no tiene `hidden`
- [X] T004 [US1] En `script.js`, `renderQuote` MUST hacer `document.getElementById('hero-search').classList.add('is-quoted')` y dejar `quoteSummary.hidden = false` (MUST NOT `hidden = true` en éxito)
- [X] T005 [US1] En `script.js`, `hideQuote` MUST quitar `is-quoted` además de ocultar el resumen; los caminos de error (origen=destino, fechas, etc.) siguen llamando `hideQuote` y MUST NOT añadir `is-quoted`

**Checkpoint**: Transporte y Por horas válidos = solo resumen; errores = buscador

---

## Phase 4: User Story 2 - Corregir o volver a cotizar (Priority: P2)

**Goal**: **Modificar** restaura el buscador con los valores previos

**Independent Test**: Quickstart pasos 3–4 y 6

### Implementation for User Story 2

- [X] T006 [US2] En `script.js`, listener de `#quote-modify` que llame a `hideQuote` (o equivalente) **sin** `form.reset()`; el resumen se oculta y reaparecen tabs/campos
- [X] T007 [US2] En `style.css`, `.quote-modify` como control secundario (borde/azul, no naranja ni `--whatsapp-green`); no rivalizar con `#quote-wa-btn`

**Checkpoint**: Modificar → buscador con datos; nuevo éxito → otra vez solo resumen

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart y regresiones 005/006

- [X] T008 Recorrer [quickstart.md](./quickstart.md) en 375 y 1280: solo resumen, Modificar, errores, FAB no tapa el verde
- [X] T009 Confirmar que no hay npm/datepicker, que `wa.me/573042143149` no cambió, y que el grid de Ida y vuelta 006 no se tocó en `style.css` salvo reglas `.is-quoted` / `.quote-modify`

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003–T005** (US1)
- **T006–T007** tras T002 (el botón existe) y tras T004–T005 (`hideQuote` ya quita `is-quoted`)
- **T008–T009** al final

### User Story Dependencies

- **US1**: MVP ocultar buscador
- **US2**: Modificar; necesita T002 + `hideQuote` de US1

### Parallel Opportunities

- T003 (`style.css`) puede ir en paralelo conceptual con T004 (`script.js`) **si** nadie más edita esos archivos a la vez
- T007 (`style.css`) no paralelo con T003

---

## Parallel Example: Setup

```bash
# Un solo hilo:
# T001 → T002 → T003 → T004 → T005 → T006 → T007 → T008 → T009
```

---

## Implementation Strategy

### MVP First (US1)

1. Confirmar ids  
2. CSS `.is-quoted` + `renderQuote`  
3. Demo: Pedir cotización → solo resumen  

### Incremental

Modificar + estilos → quickstart

---

## Notes

- 007 manda sobre form bajo el resumen  
- Siguiente: `/speckit-implement`
