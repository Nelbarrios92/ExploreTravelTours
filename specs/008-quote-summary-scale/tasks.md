# Tasks: Escala unificada del resumen de cotización

**Input**: Design documents from `/specs/008-quote-summary-scale/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US2 según spec.md. **008 manda** sobre densidad/caja del resumen.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US2
- Cada tarea incluye ruta

## Path Conventions

`style.css` (cambio principal). Contrato: `specs/008-quote-summary-scale/contracts/quote-scale.md`. MUST NOT tocar ids ni JS de 007 ni grid 006.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Localizar estilos actuales del resumen

- [X] T001 Confirmar en `style.css` los bloques `.quote-summary`, `.quote-lines`, `.quote-wa-btn`, `.quote-modify`, `.quote-related` y el override en `@media (min-width: 1280px)`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Quitar la caja interior (clarificación A)

**⚠️ CRITICAL**: Antes de retocar tipografía

- [X] T002 En `style.css`, dejar `.quote-summary` sin recuadro anidado (`background` `#f8fafc`, `border`, padding 8–10px); el aire MUST ser el de `.hero-search`; ajustar `#hero-search.is-quoted .quote-summary` si hace falta (`margin-bottom: 0`)

**Checkpoint**: El resumen llena el card blanco, no una cajita gris

---

## Phase 3: User Story 1 - Leer el resumen como un solo bloque (Priority: P1) 🎯 MVP

**Goal**: Una escala; CTAs a la misma altura que Pedir cotización

**Independent Test**: Quickstart pasos 1–3

### Implementation for User Story 1

- [X] T003 [US1] En `style.css`, `.quote-summary h2` ~1.125rem Playfair/`--brand-blue` (MUST NOT Fraunces); `.quote-lines` y `.quote-related` ≥0.875rem; `dd` 0.9375rem (`quote-scale.md`)
- [X] T004 [US1] En `style.css`, `.quote-wa-btn` y `.quote-modify` con height/min-height **50px**, `font-size` 0.9375rem, `border-radius` 10px, `width: 100%`; MUST NOT alturas distintas

**Checkpoint**: Título, datos y botones de la misma familia; verde = Modificar en alto

---

## Phase 4: User Story 2 - Mismo card en móvil y escritorio (Priority: P2)

**Goal**: No compactar el resumen solo en escritorio

**Independent Test**: Quickstart pasos 4 y 6

### Implementation for User Story 2

- [X] T005 [US2] En `style.css` `@media (min-width: 1280px)`, eliminar o no aplicar padding/font-size que achiquen `.quote-summary` / `.quote-lines` por debajo de la escala de T003 (hoy `0.85rem` en líneas)

**Checkpoint**: 1280 no es “modo admin”; 375 CTAs táctiles

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart y regresiones

- [X] T006 Recorrer [quickstart.md](./quickstart.md) en 375 y 1280: padding del card, escala, CTAs iguales, 007 (solo resumen / Modificar), 006 al componer, 0 overflow-x
- [X] T007 Confirmar que `index.html` y `script.js` no cambiaron de negocio y que el grid `.is-round-trip` ≥1280 no se tocó

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003–T004** → **T005** → **T006–T007**
- Todo en `style.css`: secuencial, sin [P] real

### User Story Dependencies

- **US1**: MVP escala + CTAs
- **US2**: no compactar 1280; después de T003

---

## Parallel Example: Setup

```bash
# T001 → T002 → T003 → T004 → T005 → T006 → T007
```

---

## Implementation Strategy

### MVP First (US1)

1. Quitar caja interior  
2. Tipografía + CTAs 50px  
3. Demo resumen vs buscador  

### Incremental

Quitar compactación 1280 → quickstart

---

## Notes

- 008 es CSS del resumen  
- Siguiente: `/speckit-implement`
