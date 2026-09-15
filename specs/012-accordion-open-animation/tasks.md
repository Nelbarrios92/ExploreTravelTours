# Tasks: Animación al abrir y cerrar el acordeón

**Input**: Design documents from `/specs/012-accordion-open-animation/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US3 según spec.md. **012 manda** el movimiento de altura al toggle. **011** cuándo hay acordeón.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US3
- Cada tarea incluye ruta

## Path Conventions

`index.html`, `style.css`. Contrato: `specs/012-accordion-open-animation/contracts/accordion-motion.md`. `script.js` solo si hace falta; MUST NOT animar `hideQuote` / `renderQuote`.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: No romper 011 cotizado

- [X] T001 Localizar en `style.css` `#hero-search.is-collapsed:not(.is-quoted) .search-composer { display: none }` y en `index.html` `#search-composer`; confirmar `.is-quoted` oculta el compositor

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Un hijo de grid para interpolar altura

**⚠️ CRITICAL**: Antes de quitar `display: none`

- [X] T002 En `index.html`, envolver el contenido de `#search-composer` (tabs + formularios) en `.search-composer-body`

**Checkpoint**: DOM con un hijo; escritorio se ve igual

---

## Phase 3: User Story 1 - Abrir y cerrar se siente fluido (Priority: P1) 🎯 MVP

**Goal**: Desplegar/plegar en altura ~320 ms al pulsar la franja

**Independent Test**: Quickstart pasos 1–3

### Implementation for User Story 1

- [X] T003 [US1] En `style.css` (`max-width: 767px`), `.search-composer` como grid `1fr` / `0fr` según `is-collapsed`; `.search-composer-body { overflow: hidden }`; `transition: grid-template-rows 320ms ease`; **quitar** `display: none` del colapso. Chevron MAY 320 ms. MUST NOT bounce (`accordion-motion.md`)

**Checkpoint**: 375 la franja abre/cierra con crecimiento de altura, &lt; 0,5 s

---

## Phase 4: User Story 2 - La animación no estorba cotizar (Priority: P1)

**Goal**: Quote y Modificar instantáneos; toques rápidos coherentes

**Independent Test**: Quickstart pasos 4–5

### Implementation for User Story 2

- [X] T004 [US2] Verificar en `style.css` que `.is-quoted .search-composer` sigue `display: none !important` **sin** transición; `script.js` `hideQuote` / `renderQuote` / `setAccordionOpen` no añaden delay. Toques rápidos no se bloquean

**Checkpoint**: Resumen y Modificar de golpe; toggle interpola hacia el último estado

---

## Phase 5: User Story 3 - Respeto a menos movimiento (Priority: P2)

**Goal**: Instantáneo si el sistema pide menos movimiento

**Independent Test**: Quickstart paso 7

### Implementation for User Story 3

- [X] T005 [US3] En `style.css`, `@media (prefers-reduced-motion: reduce)` con `transition: none` en `.search-composer` y chevron del toggle

**Checkpoint**: Con reducir movimiento, abrir/cerrar es un corte (como 011)

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart y regresiones

- [X] T006 Recorrer [quickstart.md](./quickstart.md) en 375 / 1280: altura al toggle, 009/Modificar instantáneos, 0 recorte al terminar, 0 acordeón en escritorio, 010/011 intactos

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003** → **T004** → **T005** → **T006**
- HTML antes de CSS de grid

### User Story Dependencies

- **US1**: MVP altura
- **US2**: no animar 007; tras T003
- **US3**: reduced-motion; tras T003

---

## Parallel Example: Setup

```bash
# T001 → T002 → T003 → T004 → T005 → T006
```

---

## Implementation Strategy

### MVP First (US1)

1. Wrapper interno  
2. 0fr/1fr 320 ms  
3. Demo franja  

### Incremental

Quote/Modificar → reduced-motion → 1280

---

## Notes

- 012 es CSS de altura en el toggle  
- Siguiente: `/speckit-implement`
