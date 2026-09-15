# Tasks: Ida y vuelta en una sola fila

**Input**: Design documents from `/specs/006-round-trip-single-row/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US2 según spec.md. **006 manda** sobre el grid de Ida y vuelta de 005.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US2
- Cada tarea incluye ruta

## Path Conventions

`style.css` (cambio principal), `index.html` / `script.js` (solo verificar). Contrato: `specs/006-round-trip-single-row/contracts/round-trip-row.md`.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: No romper DOM ni JS de cotización

- [X] T001 Confirmar en `index.html` el orden Origen → swap → Destino → Fecha de ida → `.field-return` → Hora → Pasajeros → submit; en `script.js`, que `updateReturnVisibility` sigue haciendo `classList.toggle('is-round-trip')` en `.search-fields-transport`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Aislar el único bloque CSS a tocar

**⚠️ CRITICAL**: Completar antes de reescribir áreas

- [X] T002 En `style.css`, localizar `@media (min-width: 1280px)` `.search-fields-transport.is-round-trip` (hoy dos `grid-template-areas`); MUST NOT editar aún el stack móvil ni `@media (min-width: 768px)` salvo que T006 lo pida

**Checkpoint**: Se sabe el bloque 1280 a reemplazar; 768 intacto

---

## Phase 3: User Story 1 - Completar ida y vuelta sin ruptura visual (Priority: P1) 🎯 MVP

**Goal**: Una fila a ~1280px con los 8 controles; aire compacto; labels legibles

**Independent Test**: Quickstart pasos 1–4

### Implementation for User Story 1

- [X] T003 [US1] En `style.css` `@media (min-width: 1280px)`, sustituir `.search-fields-transport.is-round-trip` por una sola `grid-template-areas`: `"origin swap dest depart ret time pax cta"` y 8 `grid-template-columns` (`round-trip-row.md`); MUST NOT dos filas `depart ret` / `time pax cta`
- [X] T004 [US1] En el mismo bloque de `style.css`, compactar `minmax` y `min-width` del `.search-submit` en ida-vuelta lo necesario para que quepa a 1280px sin `overflow-x`; MUST NOT bajar labels/inputs de ~14px / ~50px ni ocultar `.field-label`
- [X] T005 [US1] Verificar en `style.css` que Solo ida ≥1280 sigue `"origin swap dest depart time pax cta"` (sin `ret`) y que pills `.trip-option` no entran en esa fila de campos

**Checkpoint**: Ida y vuelta 1280 = una banda; Solo ida intacto

---

## Phase 4: User Story 2 - Seguir usando el cotizador en pantallas estrechas (Priority: P2)

**Goal**: 375 apila; 768 reflujo intencional; 0 overflow-x

**Independent Test**: Quickstart pasos 5–6

### Implementation for User Story 2

- [X] T006 [US2] Confirmar en `style.css` que el stack de `.search-fields-transport` (1 col) y `@media (min-width: 768px)` (varias filas) **no** aplican la fila de 8 columnas; Ida y vuelta en 375/768 no provoca scroll horizontal de `body`

**Checkpoint**: 375/768 OK; desktop US1 intacto

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart y regresiones 005

- [X] T007 Recorrer [quickstart.md](./quickstart.md) en 375 / 768 / 1280: una fila en 1280, apilado en 375, Pedir cotización / resumen / WhatsApp como 005
- [X] T008 Confirmar que no hay npm/datepicker y que `script.js` / `index.html` no cambiaron de negocio (`wa.me/573042143149`, validaciones)

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003–T005** (mismo `style.css`, secuencial)
- **T006** tras T003 (no reintroducir 8 cols bajo 1280)
- **T007–T008** al final

### User Story Dependencies

- **US1**: MVP escritorio una fila
- **US2**: no romper móvil/tablet; no paralela en `style.css` con US1

### Parallel Opportunities

Ninguna real: un solo archivo de producto (`style.css`). T001 puede leer `index.html`/`script.js` antes de T002.

---

## Parallel Example: Setup

```bash
# Un solo hilo:
# T001 → T002 → T003 → T004 → T005 → T006 → T007 → T008
```

---

## Implementation Strategy

### MVP First (US1)

1. Confirmar DOM/JS  
2. Una fila 8 áreas a 1280  
3. Compactar anchos  
4. Demo Ida y vuelta en portátil  

### Incremental

US2 no tocar 768/375 → quickstart

---

## Notes

- 006 manda sobre dos filas 005  
- Siguiente: `/speckit-implement`
