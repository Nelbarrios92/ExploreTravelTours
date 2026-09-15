# Tasks: Buscador más compacto en móvil

**Input**: Design documents from `/specs/010-mobile-search-compact/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US3 según spec.md. **010 manda** sobre el buscador al componer en &lt;768px. **006** ≥1280. **009** estado cotizado.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US3
- Cada tarea incluye ruta

## Path Conventions

`style.css`. Contrato: `specs/010-mobile-search-compact/contracts/mobile-search.md`. MUST NOT tocar `script.js`, `index.html` (el `#swap-places` permanece), `.quote-*` ni `.is-quoted`.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: No romper escritorio ni el card cotizado

- [X] T001 Confirmar en `style.css` los bloques `.search-fields-transport` (áreas con `swap`), `.swap-places`, `.field` / `.search-submit` (~50px), `@media (min-width: 768px)` y `(min-width: 1280px)`, y que `.quote-*` / `#hero-search.is-quoted` no se van a mezclar con 010

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Ámbito CSS &lt;768px sin hueco de swap

**⚠️ CRITICAL**: Antes de bajar tipografía de campos

- [X] T002 En `style.css`, en el CSS base (móvil-first) quitar `"swap"` de `grid-template-areas` de `.search-fields-transport` y `.search-fields-transport.is-round-trip`; dejar origen → destino (luego fechas…); los `@media (min-width: 768px)` y `(min-width: 1280px)` MUST seguir incluyendo `swap` en la fila de lugares (`mobile-search.md`)

**Checkpoint**: En 375 la pista de swap ya no reserva fila; en 768+ el grid de intercambio sigue definido

---

## Phase 3: User Story 1 - Primer pantallazo usable en el teléfono (Priority: P1) 🎯 MVP

**Goal**: Compactación moderada; todo apilado; Pedir cotización ~50px

**Independent Test**: Quickstart pasos 1–3 (altura, apilado, CTA)

### Implementation for User Story 1

- [X] T003 [US1] En `style.css` (`max-width: 767px` o equivalente que **no** aplique a 768), compactar `#hero-search` al componer: padding ~8px 10px; `.search-panel` / `.search-fields` / `.field` gaps menores; `.field-label` ≥0.8125rem; inputs/selects height **44px** (±2px), pad ~8px 12px, tipo ~0.875rem; tabs/pills ~36px; MUST NOT ≤0.78rem (`research.md`)
- [X] T004 [US1] En `style.css` &lt;768px, Transporte y Por horas en **una columna** (cada campo y CTA a ancho completo); `.search-submit` height **50px** (±2px). MUST NOT `fecha | hora` ni `origen | destino`. MUST NOT cambiar `.search-submit` / `.field` height en ≥768px

**Checkpoint**: 375 el panel es más bajo; CTA naranja sigue principal; 1280 se ve igual que 006

---

## Phase 4: User Story 2 - Sin control de intercambio en móvil (Priority: P1)

**Goal**: 0 swap visible en teléfono; escritorio intacto

**Independent Test**: Quickstart pasos 1 y 5–6 (375 sin botón; 768/1280 con botón)

### Implementation for User Story 2

- [X] T005 [US2] En `style.css` &lt;768px, `.swap-places` / `#swap-places` con `display: none` (sin pista). MUST NOT quitar el nodo de `index.html`. En ≥768px el botón vuelve a verse (reglas existentes de fila `origin swap dest`)

**Checkpoint**: 375 origen encima de destino sin flechas; 1280 intercambio funciona

---

## Phase 5: User Story 3 - Cotizar y modificar sin perder el arreglo móvil (Priority: P2)

**Goal**: 007/009 intactos; Modificar vuelve a 010

**Independent Test**: Quickstart paso 4

### Implementation for User Story 3

- [X] T006 [US3] Verificar en `style.css` que las reglas 010 **no** aplican bajo `.is-quoted` de forma que inflen o pisen 009; el formulario al componer (tras quitar `.is-quoted`) sigue compacto y sin swap en 375

**Checkpoint**: Resumen 009; Modificar = buscador 010

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart y regresiones

- [X] T007 Recorrer [quickstart.md](./quickstart.md) en 375 / 768 / 1280: compacto apilado, 0 swap en 375, swap en 768+, ida-vuelta una fila en 1280, 0 overflow-x, WhatsApp y validaciones iguales; confirmar que `index.html` y `script.js` no se modificaron

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003–T004** → **T005** → **T006** → **T007**
- Todo `style.css`: secuencial (sin [P] real)

### User Story Dependencies

- **US1**: MVP compactación + apilado
- **US2**: ocultar swap; tras T002 (sin área swap)
- **US3**: no romper 009; tras US1–US2

---

## Parallel Example: Setup

```bash
# T001 → T002 → T003 → T004 → T005 → T006 → T007
```

---

## Implementation Strategy

### MVP First (US1 + US2)

1. Quitar área `swap` en base  
2. Compactar &lt;768px  
3. `display: none` del intercambio  
4. Demo 375 vs 1280  

### Incremental

US3 (Modificar) → quickstart 768/1280

---

## Notes

- 010 es CSS del buscador al componer en teléfono  
- Siguiente: `/speckit-implement`
