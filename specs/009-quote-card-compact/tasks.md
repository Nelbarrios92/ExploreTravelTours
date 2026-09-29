# Tasks: Card de resumen más compacta

**Input**: Design documents from `/specs/009-quote-card-compact/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US2 según spec.md. **009 manda** sobre talla del estado cotizado (008 grande queda sustituida ahí).

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US2
- Cada tarea incluye ruta

## Path Conventions

`style.css`. Contrato: `specs/009-quote-card-compact/contracts/quoted-card.md`. MUST NOT tocar `.search-submit`, grid 006 ni `script.js`.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: No compactar el buscador

- [X] T001 Confirmar en `style.css` que `.search-submit` / `.field` siguen ~50px / 0.875rem y localizar bloques `.quote-*` y `#hero-search` / `.is-quoted`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Padding del card solo cuando está cotizado

**⚠️ CRITICAL**: Antes de bajar tipografía

- [X] T002 En `style.css`, `#hero-search.is-quoted` con padding menor que el modo buscador (p. ej. 8px 12px); `.quote-summary` sigue sin caja gris anidada

**Checkpoint**: La placa blanca cotizada es más baja de aire; el card al componer no cambia

---

## Phase 3: User Story 1 - Cotizar sin que el card se coma el Hero (Priority: P1) 🎯 MVP

**Goal**: Escala moderada; CTAs &lt; 50px y iguales entre sí

**Independent Test**: Quickstart pasos 1–4

### Implementation for User Story 1

- [X] T003 [US1] En `style.css`, compactar `.quote-summary h2` (~1rem), `.quote-lines` (dt ≥0.8125rem, dd ~0.875rem, gap ~4px 12px) y `.quote-related` (≥0.8125rem); MUST NOT ≤0.78rem (`quoted-card.md`)
- [X] T004 [US1] En `style.css`, `.quote-wa-btn` y `.quote-modify` a height **42px**, font-size **0.8125rem**, misma talla entre ambos; MUST NOT 50px

**Checkpoint**: Resumen más bajo que el buscador; verde = Modificar; Hero no partido

---

## Phase 4: User Story 2 - Compacto también en móvil (Priority: P2)

**Goal**: 375 usable; misma familia que desktop

**Independent Test**: Quickstart paso 5

### Implementation for User Story 2

- [X] T005 [US2] Verificar en `style.css` que no hay override 1280 que reinfle el resumen a escala 008 ni que lo deje admin; en &lt;768 el padding `.hero-search` + `.is-quoted` no genera overflow-x; CTAs ≥40px percibidos

**Checkpoint**: 375 y 1280 compactos del mismo sistema

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart y regresiones

- [X] T006 Recorrer [quickstart.md](./quickstart.md) en 375 y 1280: altura vs buscador, Modificar restaura densidad 006, WhatsApp, 0 overflow-x
- [X] T007 Confirmar que `index.html` / `script.js` y `.search-fields-transport.is-round-trip` ≥1280 no se modificaron

---

## Dependencies & Execution Order

- **T001** → **T002** → **T003–T004** → **T005** → **T006–T007**
- Todo `style.css`: secuencial

### User Story Dependencies

- **US1**: MVP compactación
- **US2**: no reventar móvil; tras T003–T004

---

## Parallel Example: Setup

```bash
# T001 → T002 → T003 → T004 → T005 → T006 → T007
```

---

## Implementation Strategy

### MVP First (US1)

1. Padding `.is-quoted`  
2. Tipo + CTAs 42px  
3. Demo Hero + resumen pie  

### Incremental

Chequeo 375 → quickstart

---

## Notes

- 009 es CSS del estado cotizado  
- Siguiente: `/speckit-implement`
