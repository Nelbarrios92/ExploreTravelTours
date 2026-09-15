# Tasks: Buscador desplegable en móvil

**Input**: Design documents from `/specs/011-mobile-search-accordion/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US3 según spec.md. **011 manda** visibilidad del compositor en &lt;768px. **010** densidad abierto. **007/009** cotizado.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US3
- Cada tarea incluye ruta

## Path Conventions

`index.html`, `style.css`, `script.js`. Contrato: `specs/011-mobile-search-accordion/contracts/accordion.md`. MUST NOT persistir en storage ni usar `<details>` del FAQ.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Encajar 007/010 sin romper selectores

- [X] T001 Localizar en `index.html` el bloque `#hero-search` (quote, tabs, formularios) y en `script.js` `renderQuote` / `hideQuote` / `.is-quoted`; confirmar que 010 (`max-width: 767px`) sigue en `style.css`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Markup del acordeón

**⚠️ CRITICAL**: Antes de CSS/JS de toggle

- [X] T002 En `index.html`, añadir `button type="button"` de cabecera (texto **Pedir cotización**, chevron Unicons, `aria-expanded="false"`) y envolver tabs + paneles + errores en `.search-composer`; en `#hero-search` clase inicial `is-collapsed`. MUST NOT meter el resumen dentro del compositor

**Checkpoint**: DOM listo; escritorio aún se ve completo hasta que el CSS oculte la cabecera

---

## Phase 3: User Story 1 - Primer pantallazo con el Hero libre (Priority: P1) 🎯 MVP

**Goal**: Cerrado al cargar; abrir/cerrar la misma franja

**Independent Test**: Quickstart pasos 1–3

### Implementation for User Story 1

- [X] T003 [P] [US1] En `style.css` (`max-width: 767px`): con `#hero-search.is-collapsed:not(.is-quoted)` ocultar `.search-composer`; cabecera como **barra** (no naranja 50px) + chevron que rote al abrir. En `min-width: 768px` y en `.is-quoted` ocultar la cabecera; el compositor visible en ≥768 (`accordion.md`)
- [X] T004 [P] [US1] En `script.js`, click de la cabecera: toggle `is-collapsed` y `aria-expanded` solo si no `.is-quoted`. MUST NOT ser `type=submit`. MUST NOT `localStorage`

**Checkpoint**: 375 carga en franja; toggle abre 010 debajo; 1280 sin cabecera

---

## Phase 4: User Story 2 - Completar cotización con el panel abierto (Priority: P1)

**Goal**: Errores visibles; naranja envía; pestañas dentro

**Independent Test**: Quickstart pasos 4–5 (error y envío)

### Implementation for User Story 2

- [X] T005 [US2] Verificar en `script.js` que el submit **no** añade `is-collapsed`; errores y `#same-place-prompt` viven en `.search-composer` en `index.html`. Tras envío válido, 007 sigue (`is-quoted` oculta cabecera y compositor vía T003)

**Checkpoint**: Fallo = panel abierto; éxito = solo resumen 009

---

## Phase 5: User Story 3 - Modificar vuelve a un formulario usable (Priority: P2)

**Goal**: Modificar abre el acordeón

**Independent Test**: Quickstart paso 5 (Modificar)

### Implementation for User Story 3

- [X] T006 [US3] En `script.js`, `hideQuote` MUST quitar `is-collapsed` y poner `aria-expanded="true"` en la cabecera. Los valores del form no se limpian al toggle (FR-006)

**Checkpoint**: Modificar en 375 = formulario 010 visible

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart y regresiones

- [X] T007 Recorrer [quickstart.md](./quickstart.md) en 375 / 768 / 1280: cerrado al cargar, toggle, valores al reabrir, error abierto, 009, Modificar abierto, 0 acordeón en escritorio, 0 overflow-x; 010 (apilado, sin swap) y 006 una fila intactos

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003** y **T004** (archivos distintos) → **T005** → **T006** → **T007**

### User Story Dependencies

- **US1**: MVP acordeón
- **US2**: no colapsar en error; tras T003–T004
- **US3**: Modificar; tras T004

---

## Parallel Example: User Story 1

```bash
# Tras T002:
# T003 style.css
# T004 script.js
```

---

## Implementation Strategy

### MVP First (US1)

1. Markup cabecera + compositor  
2. CSS &lt;768 + toggle JS  
3. Demo Hero + franja  

### Incremental

Errores/007 → Modificar → quickstart 768/1280

---

## Notes

- 011 es visibilidad del compositor en teléfono  
- Siguiente: `/speckit-implement`
