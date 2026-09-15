# Tasks: Acordeón móvil encima de Explorar servicios

**Input**: Design documents from `/specs/015-mobile-accordion-above-cta/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US3 según spec.md. **015 manda** el orden móvil. **014** el escritorio.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US3
- Cada tarea incluye ruta

## Path Conventions

`style.css`. Contrato: `specs/015-mobile-accordion-above-cta/contracts/accordion-above-cta.md`. `index.html` y `script.js` MUST NOT cambiar.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Confirmar hermanos layout vs acciones

- [x] T001 Localizar en `index.html` `.hero-content` (mensaje + acciones) y `.hero-footer`; en `style.css` `@media (max-width: 767px)` `.hero-actions { margin-top: auto }` y reglas 014 `min-width: 768px`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Un solo flex para poder `order`

**⚠️ CRITICAL**: `contents` antes del reorden

- [x] T002 En `style.css` (`max-width: 767px`), `.hero-content { display: contents }`; `.hero-message { order: 1 }`; `.hero-footer { order: 2; margin-top: auto }`; `.hero-actions { order: 3; margin-top: 0 }`. MUST NOT `contents`/`order` en `min-width: 768px`

**Checkpoint**: Los tres bloques son ítems de `.hero-layout` en 375; escritorio agrupado

---

## Phase 3: User Story 1 - Pedir cotización está sobre Explorar (Priority: P1) 🎯 MVP

**Goal**: 375 cerrado: aire, luego franja, luego Explorar (par abajo)

**Independent Test**: Quickstart paso 1

### Implementation for User Story 1

- [x] T003 [US1] Ajustar en `style.css` el par inferior (`accordion-above-cta.md`): franja **encima** de `.lets-go-btn`, tercio inferior, no pegada a `.hero-subtitle`. Redes siguen en `.hero-actions`

**Checkpoint**: 375 cerrado: Pedir cotización sobre Explorar, abajo

---

## Phase 4: User Story 2 - Abrir no desordena el mensaje (Priority: P1)

**Goal**: Título Δ &lt; ~8 px; Explorar bajo el form

**Independent Test**: Quickstart paso 2

### Implementation for User Story 2

- [x] T004 [US2] Verificar en `style.css` que 012 sigue interpolando altura en `.search-composer`; MUST NOT `position` absoluto del footer. Abrir come el aire / baja Explorar; `.hero-message` arriba

**Checkpoint**: 375 abrir: título quieto; Explorar tocable debajo

---

## Phase 5: User Story 3 - Cotizar y Modificar respetan el orden (Priority: P2)

**Goal**: 009/Modificar encima de Explorar en móvil

**Independent Test**: Quickstart paso 3

### Implementation for User Story 3

- [x] T005 [US3] Verificar que `#hero-search.is-quoted` sigue en `.hero-footer` (`order: 2`); MUST NOT recolocar el resumen bajo `.lets-go-btn`

**Checkpoint**: Cotizado y Modificar: cotizador sobre Explorar

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart

- [x] T006 Recorrer [quickstart.md](./quickstart.md) en 375 / 1280: orden móvil, 013/012, pie escritorio 014, WhatsApp

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003** → **T004** → **T005** → **T006**
- `display: contents` antes de fiar el `order`

### User Story Dependencies

- **US1**: MVP orden cerrado
- **US2**: apertura; tras T002
- **US3**: 009; tras T002

---

## Parallel Example: Setup

```bash
# T001 → T002 → T003 → T004 → T005 → T006
```

---

## Implementation Strategy

### MVP First (US1)

1. `contents` + `order`  
2. `auto` en footer  
3. Demo 375 cerrado  

### Incremental

Abrir 012 → quote → 1280

---

## Notes

- 015 es CSS de orden, no un segundo buscador  
- Siguiente: `/speckit-implement`
