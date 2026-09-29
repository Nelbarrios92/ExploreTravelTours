# Tasks: Composición del Hero en móvil

**Input**: Design documents from `/specs/013-mobile-hero-layout/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US3 según spec.md. **013 manda** la composición del copy en &lt;768px. **011/012** el pie de cotización.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US3
- Cada tarea incluye ruta

## Path Conventions

`index.html`, `style.css`. Contrato: `specs/013-mobile-hero-layout/contracts/hero-mobile-layout.md`. `script.js` MUST NOT cambiar.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Confirmar el re-centrado actual sin tocar 011/012

- [X] T001 Localizar en `style.css` `.hero-content { justify-content: center; flex: 1 }` y `.hero-layout`; en `index.html` `.hero-brand`, `.hero-subtitle`, `.lets-go-btn`, `.hero-social`, `.hero-footer`. Confirmar acordeón en `max-width: 767px`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Dos zonas DOM para el aire automático

**⚠️ CRITICAL**: Wrappers antes del CSS de ancla

- [X] T002 En `index.html`, envolver marca + regla + descripción en `.hero-message` y `.lets-go-btn` + `.hero-social` en `.hero-actions`, ambos dentro de `.hero-content`. Escritorio se ve igual hasta T003

**Checkpoint**: DOM con dos hijos de contenido; copy y WhatsApp intactos

---

## Phase 3: User Story 1 - El mensaje queda arriba, el botón no se pega al título (Priority: P1) 🎯 MVP

**Goal**: En 375 cerrado: título arriba, descripción acto seguido, Explorar servicios más abajo

**Independent Test**: Quickstart paso 1

### Implementation for User Story 1

- [X] T003 [US1] En `style.css` (`max-width: 767px`), `.hero-content { justify-content: flex-start }` (MUST NOT `center`); `.hero-actions { margin-top: auto }`. Hueco título–descripción pequeño; botón cerca del pie. `min-width: 768px` sin este ancla (`hero-mobile-layout.md`)

**Checkpoint**: 375 cerrado: título en tercio superior; botón visiblemente más bajo

---

## Phase 4: User Story 2 - Abrir Pedir cotización no mueve el mensaje (Priority: P1)

**Goal**: El aire absorbe el crecimiento del pie; mensaje Δ &lt; ~8 px

**Independent Test**: Quickstart pasos 2–3

### Implementation for User Story 2

- [X] T004 [US2] En `style.css`, asegurar que el crecimiento de `.hero-footer` / `#hero-search` **no** recentre `.hero-message`. MUST NOT `position: sticky`/`fixed` en el título. MUST NOT tocar `setAccordionOpen` en `script.js`

**Checkpoint**: 375 abrir/cerrar: título y descripción casi quietos; el botón MAY subir

---

## Phase 5: User Story 3 - El botón puede ceder; el mensaje no (Priority: P2)

**Goal**: Solo ida abierto: Explorar servicios entero y tocable encima del buscador

**Independent Test**: Quickstart paso 2 (botón usable)

### Implementation for User Story 3

- [X] T005 [US3] En `style.css`, `.lets-go-btn` en flujo encima de `.hero-footer` (MUST NOT `position` sobre el formulario). Redes MAY compactarse. Ida y vuelta MAY scroll; MUST NOT recortar el título

**Checkpoint**: Solo ida: botón clicable encima de Pedir cotización

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart y regresiones

- [X] T006 Recorrer [quickstart.md](./quickstart.md) en 375 / 1280: composición cerrada, mensaje estable al abrir, botón tocable, 009/Modificar, Hero escritorio igual, 011/012 intactos

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003** → **T004** → **T005** → **T006**
- HTML wrappers antes del CSS de `flex-start` / `auto`

### User Story Dependencies

- **US1**: MVP composición en reposo
- **US2**: estabilidad al abrir; tras T003
- **US3**: botón usable; tras T003

---

## Parallel Example: Setup

```bash
# T001 → T002 → T003 → T004 → T005 → T006
```

---

## Implementation Strategy

### MVP First (US1)

1. Wrappers  
2. `flex-start` + `margin-top: auto`  
3. Demo 375 cerrado  

### Incremental

Abrir acordeón (US2) → botón tocable (US3) → 1280

---

## Notes

- 013 es layout del Hero móvil, no el acordeón  
- Siguiente: `/speckit-implement`
