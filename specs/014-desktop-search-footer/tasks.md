# Tasks: Buscador de escritorio otra vez en el pie del Hero

**Input**: Design documents from `/specs/014-desktop-search-footer/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US3 según spec.md. **014 manda** el pie en ≥768px. **011–013** el móvil.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US3
- Cada tarea incluye ruta

## Path Conventions

`style.css`. Contrato: `specs/014-desktop-search-footer/contracts/desktop-search-footer.md`. `index.html` y `script.js` MUST NOT cambiar.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Ver dónde el Hero deja de ser viewport

- [X] T001 Localizar en `style.css` `@media (max-width: 768px)` `.hero-section { height: auto }`, `@media (max-width: 767px)` `#hero-search.is-collapsed … height: 0`, y `.search-accordion-toggle { display: none }`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: El acordeón móvil puede crecer **solo** bajo 767

**⚠️ CRITICAL**: Mover `height: auto` antes de anclar escritorio

- [X] T002 En `style.css`, pasar `.hero-section` `height: auto; min-height: 100vh` (y padding de Hero si va ligado) desde `@media (max-width: 768px)` a `@media (max-width: 767px)`. Dejar menú/tipografía 768. MUST NOT tocar `.hero-message` / `.hero-actions`

**Checkpoint**: 375 sigue pudiendo alargar el Hero; 768+ ya no hereda `height: auto` por ese recorte

---

## Phase 3: User Story 1 - En el ordenador el cotizador vuelve al pie (Priority: P1) 🎯 MVP

**Goal**: 1280: barra siempre abierta al borde inferior del Hero; 0 franja

**Independent Test**: Quickstart pasos 1 y 3 (1280 / 768)

### Implementation for User Story 1

- [X] T003 [US1] En `style.css` (`min-width: 768px`), `.hero-section { height: 100vh }`; `.hero-layout` mantiene el pie abajo; `.search-accordion-toggle { display: none }`; `.search-composer` altura automática **aunque** `#hero-search.is-collapsed` (`desktop-search-footer.md`). MUST NOT animar 012 en escritorio

**Checkpoint**: 1280 buscador al pie, 006 intacto, 0 acordeón

---

## Phase 4: User Story 2 - El teléfono no se mueve (Priority: P1)

**Goal**: 375 = 011/012/013 actuales

**Independent Test**: Quickstart paso 4

### Implementation for User Story 2

- [X] T004 [US2] Verificar en `style.css` el bloque `max-width: 767px`: `flex-start` / `margin-top: auto` (013), compositor `height: 0` colapsado y toggle visible (011/012). MUST NOT cambiar esos selectores

**Checkpoint**: 375 franja Pedir cotización; título no salta al abrir

---

## Phase 5: User Story 3 - Cotizar y Modificar en el pie de escritorio (Priority: P2)

**Goal**: 009/Modificar siguen en `.hero-footer` en escritorio

**Independent Test**: Quickstart paso 2

### Implementation for User Story 3

- [X] T005 [US3] Verificar en `style.css` que `#hero-search.is-quoted` sigue ocultando compositor/toggle y mostrando el resumen **en el pie**; MUST NOT mover `.quote-summary` fuera de `.hero-footer`

**Checkpoint**: 1280 cotizar/Modificar en el mismo pie

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart

- [X] T006 Recorrer [quickstart.md](./quickstart.md) en 1280 / 768 / 375: pie escritorio, 0 acordeón ≥768, móvil intacto, 006/009, WhatsApp

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003** → **T004** → **T005** → **T006**
- Mover `height: auto` (T002) antes del 100vh desktop (T003)

### User Story Dependencies

- **US1**: MVP pie escritorio
- **US2**: congelar 767; tras T002
- **US3**: 009 en el pie; tras T003

---

## Parallel Example: Setup

```bash
# T001 → T002 → T003 → T004 → T005 → T006
```

---

## Implementation Strategy

### MVP First (US1)

1. `height: auto` solo 767  
2. 100vh + compositor visible ≥768  
3. Demo 1280  

### Incremental

Regresión 375 → quote/Modificar → 768

---

## Notes

- 014 es CSS de corte 767/768, no rediseño del form  
- Siguiente: `/speckit-implement`
