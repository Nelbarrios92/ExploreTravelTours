# Tasks: Booking bar premium del Hero

**Input**: Design documents from `/specs/005-hero-booking-bar/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No suite automatizada. Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US5 según spec.md. **005 manda** sobre 004.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si no choca el mismo archivo
- **[Story]**: US1–US5
- Cada tarea incluye ruta

## Path Conventions

`index.html`, `style.css`, `script.js`. Contrato: `specs/005-hero-booking-bar/contracts/booking-bar.md`. Conservar `name` de campos e ids de `initSearch` de negocio.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: No romper selectores de cotización

- [X] T001 Confirmar en `index.html` / `script.js` los ids/names del contrato (`#search-form-transporte`, `#search-form-hourly`, `trip-type`, campos, `#quote-summary`, `#same-place-prompt`, `#switch-to-hourly`, `#quote-wa-btn`); no eliminarlos al reestructurar

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: DOM y copy base; quitar dual feedback del header

**⚠️ CRITICAL**: Completar antes del pulido visual de historias

- [X] T002 En `index.html`, reordenar `#search-form-transporte` `.search-fields`: Origen, swap (botón placeholder), Destino, Fecha de ida, `.field-return` (no primero), Hora, Pasajeros, submit; placeholders reales (`Cartagena`, `Aeropuerto…`); `lang="es-CO"` en fechas si aplica (`booking-bar.md`)
- [X] T003 En `index.html`, quitar `.search-chrome` vacío de Por horas; alinear slots de `#search-form-hourly` (recogida, duración 1–12, fecha, hora, pasajeros, submit); labels estáticos sin solape
- [X] T004 En ambos submits de `index.html`, texto **Pedir cotización**; `#quote-wa-btn` **Continuar por WhatsApp**; MUST NOT “Buscar”
- [X] T005 Quitar de `index.html` el bloque `.nav-request` y los `.request-action` del header; conservar Contactar Ya

**Checkpoint**: Orden de viaje correcto en el DOM; header sin “TU SOLICITUD”

---

## Phase 3: User Story 1 - Traslado, orden mental y CTA usable (Priority: P1) 🎯 MVP

**Goal**: Segmented + pills; densidad premium; ida y vuelta en dos filas; 0 overlap FAB↔CTA

**Independent Test**: Quickstart pasos 1–4 (1280 y 375: orden fechas, CTA clicable, FAB no tapa)

### Implementation for User Story 1

- [X] T006 [US1] En `style.css`, segmented `.search-tab` (activo `--brand-blue`, inactivo neutro) y pills `.trip-option` (no radio crudo); densidad labels ≥14px, inputs 48–52px
- [X] T007 [US1] En `style.css` ≥1280px: solo ida una fila 5 campos + CTA; `.search-fields.is-round-trip` dos filas (fechas arriba; hora, pasajeros, CTA abajo) según contrato
- [X] T008 [US1] En `script.js`, al cambiar `trip-type`, toggle `.is-round-trip` en el grid de transporte (además de `hidden` en `.field-return`)
- [X] T009 [US1] En `script.js` + `style.css`, `IntersectionObserver` sobre `#hero-search` para suprimir `.floating-wa` (sin clics) mientras intersecta el viewport; restaurar al hacer scroll al catálogo

**Checkpoint**: Ida y vuelta legible; CTA naranja usable en 1280 y 375

---

## Phase 4: User Story 2 - Por horas con la misma calidad (Priority: P1)

**Goal**: Misma densidad/CTA; altura estable sin spacer vacío

**Independent Test**: Quickstart pasos 2 y 8

### Implementation for User Story 2

- [X] T010 [US2] En `style.css`, aplicar la misma grid/densidad de solo ida a `#search-form-hourly` `.search-fields` (5 + CTA en ≥1280)
- [X] T011 [US2] Verificar en `index.html` que no queda franja hueca tipo 004; Duración: label + option “Selecciona” sin superposición

**Checkpoint**: Alternar tabs no parece otro producto

---

## Phase 5: User Story 3 - Un solo feedback (WhatsApp) (Priority: P1)

**Goal**: Pedir cotización → resumen inline; no `has-request`

**Independent Test**: Quickstart pasos 6–7

### Implementation for User Story 3

- [X] T012 [US3] En `script.js`, eliminar `activateRequestState` / `deactivateRequestState` y listeners de `requestModifyBtn`; en submit válido llamar a `renderQuote` con `#quote-summary` **visible** (MUST NOT `quoteSummary.hidden = true` en el éxito)
- [X] T013 [US3] En `style.css`, borrar o dejar inerte reglas `.main-header.has-request` / `.nav-request` / `.request-action` para que no reaparezca el patrón dual
- [X] T014 [US3] Conservar en `script.js` validaciones y textos (origen=destino, fechas, pasajeros, `buildWhatsAppUrl`, `relatedSuggestions`)

**Checkpoint**: Un confirmación en el card; naranja no abre WhatsApp

---

## Phase 6: User Story 4 - Tablet y móvil (Priority: P2)

**Goal**: 1 columna, CTA full width, sin overflow, FAB sin tapar

**Independent Test**: Quickstart paso 9

### Implementation for User Story 4

- [X] T015 [US4] En `style.css` &lt;768: `.search-fields` 1 columna; submit 100% min-height ≥44px; tabs en una fila; 768–1279 reflujo 2/3 columnas sin 7-en-una-fila
- [X] T016 [US4] Confirmar en `style.css` que `.hero-search` / `body` no generan overflow-x; FAB suppressed cubre también el resumen inline

**Checkpoint**: 375/768 OK; desktop US1 intacto

---

## Phase 7: User Story 5 - Swap y sugerencias (Priority: P2)

**Goal**: Intercambiar origen/destino; ≥5 lugares reales

**Independent Test**: Quickstart paso 5

### Implementation for User Story 5

- [X] T017 [US5] Completar el botón swap en `index.html` y, en `script.js`, intercambiar `origin`/`destination` `.value`; `type="button"` para no submitir
- [X] T018 [US5] En `index.html`, enriquecer `#place-suggestions` (≥5 destinos reales del negocio: Cartagena, aeropuerto, Barú, etc.) y conectar pickup/origen/destino al `list`

**Checkpoint**: Swap + datalist; texto libre sigue permitido

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Primacía del cotizador y quickstart

- [X] T019 En `style.css`, de-énfasis de `.lets-go-btn` / `.hero-social` (ghost/menor peso); no tocar `.hero-brand` ni catálogo/FAQ
- [X] T020 Recorrer [quickstart.md](./quickstart.md) en 375 / 768 / 1280: overlap, orden, un feedback, WhatsApp del resumen, validaciones
- [X] T021 Confirmar que no hay npm/datepicker y que `wa.me/573042143149` no cambió en `script.js` / `index.html`

---

## Dependencies & Execution Order

- **T001** → **T002–T005** (DOM/copy/header)
- **US1 T006–T009** (CSS + FAB + round-trip class) tras T002
- **US2 T010–T011** tras T003 y T006
- **US3 T012–T014** puede ir en paralelo conceptual con US1 CSS, pero `script.js` choca con T008–T009 → secuencial en JS: T008, T009, T012, T014, T017
- **US4** tras grids desktop
- **US5** tras markup origen/destino (T002)
- **Polish** al final

### User Story Dependencies

- **US1**: MVP traslado + FAB
- **US2**: misma barra en Por horas
- **US3**: confirmación única (puede demo-se con US1 si T012 va temprano; el plan la deja tras densidad)
- **US4 / US5**: P2

### Parallel Opportunities

- T013 (`style.css` header muerto) puede ir tras T005; no paralelo con T006–T007
- T018 (`index.html` datalist) paralelo a CSS **si** nadie más edita `index.html`
- En la práctica: un implementador secuencial T001→T021

---

## Parallel Example: Setup

```bash
# Un solo hilo recomendado (mismos tres archivos):
# T001 → T002–T005 → T006–T009 → T010–T014 → T015–T018 → T019–T021
```

---

## Implementation Strategy

### MVP First (US1 + T012)

1. DOM orden + Pedir cotización + quitar nav-request  
2. Densidad + dos filas + FAB observer  
3. `renderQuote` visible (aunque US3 esté listado después, T012 es el cierre de conversión)  
4. Demo traslado  

### Incremental

US2 Por horas → US4 responsive → US5 swap → de-énfasis Hero → quickstart

---

## Notes

- Naranja no abre WhatsApp; verde del resumen sí  
- No reintroducir chrome vacío 004  
- Siguiente: `/speckit-implement`
