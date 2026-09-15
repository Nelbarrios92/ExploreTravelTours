# Tasks: Consistencia UX del buscador del Hero

**Input**: Design documents from `/specs/004-search-form-consistency/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No hay tareas de tests automatizados (no hay TypeScript/runner). Cierre = [quickstart.md](./quickstart.md).

**Organization**: US1–US3 según spec.md. Producto en la raíz.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Paralelo solo si el archivo no choca
- **[Story]**: US1, US2, US3
- Cada tarea incluye ruta de archivo

## Path Conventions

`index.html`, `style.css`, `script.js`. Contrato: `specs/004-search-form-consistency/contracts/search-layout.md`. Conservar `id`/`name` de `initSearch`.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Inventario de selectores para no romper `initSearch`

- [x] T001 Anotar y no eliminar en `index.html` / `script.js` los selectores del contrato: `#search-form-transporte`, `#search-form-hourly`, `.search-tab[data-mode]`, `.field-return`, `input[name="trip-type"]`, `name` de campos, `#errors-transporte`, `#errors-hourly`, `#same-place-prompt`, `#switch-to-hourly`, `#quote-summary`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Mismo esqueleto HTML en ambos formularios (chrome + fields + submit dentro del grid)

**⚠️ CRITICAL**: Completar antes del CSS de historias

- [x] T002 En `#search-form-transporte` (`index.html`): envolver Solo ida / Ida y vuelta en `.search-chrome`; reordenar cada `.field` a `.field-label` + control (quitar `placeholder=" "` trampa); dejar `.field-return` con clase e `input[name="return-date"]`; mover `.search-submit` **dentro** de `.search-fields` como último hijo; errores y `#same-place-prompt` **después** del grid (`specs/004-search-form-consistency/contracts/search-layout.md`)
- [x] T003 En `#search-form-hourly` (`index.html`): añadir `.search-chrome` vacío (`aria-hidden="true"`) con la misma estructura de altura; labels estáticos (Lugar de recogida, Duración, Fecha, Hora, Pasajeros); `select[name="duration"]` con opción vacía “Selecciona” y opciones 1–12; mover `.search-submit` dentro de `.search-fields`; **sin** radios de viaje

**Checkpoint**: DOM alineado; JS de tabs/submit debe seguir encontrando los `name`; el look aún puede ser el viejo hasta el CSS

---

## Phase 3: User Story 1 - Percibir un solo buscador con dos modos (Priority: P1) 🎯 MVP

**Goal**: Tabs iguales, franja chrome misma altura, CTA en la fila en desktop, inactivo neutro / activo azul

**Independent Test**: Alternar tabs en ~1280px: sin salto de tabs ni de chrome; CTA no se vuelve barra full-width solo por cambiar de modo. Quickstart pasos 1–2

### Implementation for User Story 1

- [x] T004 [US1] En `style.css`, tabs `.search-tab`: `flex: 1 1 0`, `min-height` ~36–40px; `.is-active` `--brand-blue` + texto blanco; inactivo fondo `#f1f5f9`, texto `#64748b`, borde `#e2e8f0`
- [x] T005 [US1] En `style.css`, `.search-chrome` con `min-height` igual en ambos paneles (radios alineados en Transporte; hueco en Por horas)
- [x] T006 [US1] En `style.css` ≥1280px: `.search-fields` `grid-template-columns: repeat(5, minmax(0, 1fr)) auto`; `.search-submit` naranja, `align-self: end`, altura = input (no full-width)
- [x] T007 [US1] Suavizar `box-shadow` de `.hero-search` en `style.css` (más corta que `0 -8px 40px`); no tocar overlay/foto/marca del Hero

**Checkpoint**: Un componente, dos modos; CTA estable en desktop Solo ida / Por horas

---

## Phase 4: User Story 2 - Labels claros y Duración / ida-vuelta (Priority: P1)

**Goal**: Label arriba en todos los campos; Duración sin solape; fecha de regreso en segunda fila sin echar el CTA

**Independent Test**: Quickstart pasos 3–5; Duración “Duración” + “Selecciona” separados; Ida y vuelta no desborda

### Implementation for User Story 2

- [x] T008 [US2] En `style.css`, reemplazar el bloque floating-label (`.field > span` absoluto y reglas `:placeholder-shown`) por `.field` en columna: `.field-label` pequeño arriba, input/select altura uniforme, `position` estático
- [x] T009 [US2] Verificar en `index.html` que Duración no superpone textos (label fuera del select; placeholder/option “Selecciona” solo en el control)
- [x] T010 [US2] En `style.css` ≥1280px: `.field-return` visible en segunda fila (`grid-column` que no ocupe la columna del CTA); `.search-submit { grid-row: 1; grid-column: 6; }`
- [x] T011 [US2] Confirmar en `script.js` que `updateReturnVisibility` y `querySelector('.field-return')` siguen funcionando; ajustar el selector **solo** si el nodo se movió

**Checkpoint**: Labels consistentes; ida-vuelta usable; `initSearch` intacto en reglas de negocio

---

## Phase 5: User Story 3 - Tablet y móvil (Priority: P2)

**Goal**: Sin overflow; pila en 375; 2 y 3 columnas en tablet; CTA full width al final en móvil

**Independent Test**: Quickstart paso 8 (375 / 768 / 1024)

### Implementation for User Story 3

- [x] T012 [US3] En `style.css` default/&lt;768: `.search-fields` 1 columna; `.search-submit` `width: 100%`, min-height ≥44px, última fila
- [x] T013 [US3] En `style.css` 768–1023: 2 columnas; submit full width al cierre. En 1024–1279: 3 columnas según `search-layout.md`
- [x] T014 [US3] Tabs en una fila en móvil (`.search-tabs` flex); sin `overflow-x` en `.hero-search` / `body`; `.search-chrome` no provoca corte de radios

**Checkpoint**: Desktop US1/US2 intacto; móvil usable

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Regresión de negocio y quickstart

- [x] T015 Recorrer [quickstart.md](./quickstart.md): cotización, WhatsApp del resumen (verde), origen=destino → Por horas, errores en español, `#quote-summary` encima
- [x] T016 Confirmar en `script.js` que no se cambiaron mensajes, `buildWhatsAppUrl` ni `relatedSuggestions`; no hay datepicker/npm nuevos
- [x] T017 Confirmar que catálogo, navbar y bloque de marca del Hero no se rediseñaron en `index.html` / `style.css`

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup T001**: inmediato
- **Foundational T002–T003**: bloquea CSS de historias (mismo archivo `index.html`: secuencial T002 luego T003)
- **US1 T004–T007**: CSS sobre el nuevo DOM
- **US2 T008–T011**: CSS de labels (puede solaparse con T004–T007 en `style.css` → secuencial)
- **US3 T012–T014**: media queries encima del grid desktop
- **Polish**: al final

### User Story Dependencies

- **US1**: Tras T003. MVP visual de “un solo buscador”
- **US2**: Tras US1 (labels y Duración sobre la grid ya estable)
- **US3**: Tras US2 (breakpoints no pelean con floating-label ya eliminado)

### Parallel Opportunities

- T002 y T003 tocan el mismo `index.html` → **no** paralelo
- T004–T014 son `style.css` → **no** paralelo entre sí
- T001 es lectura; T016 puede hacerse en cuanto no se haya editado JS

---

## Parallel Example: Setup

```bash
# No hay archivos distintos para paralelizar el markup.
# Orden: T001 → T002 → T003 → CSS T004…T014 → T015–T017
```

---

## Implementation Strategy

### MVP First (US1)

1. T001–T003 esqueleto
2. T004–T007 tabs, chrome, CTA fila, sombra
3. Validar cambio de tab en 1280
4. T008–T011 labels / Duración / regreso
5. T012–T014 responsive
6. Quickstart

### Incremental Delivery

Tras US1 ya se percibe un solo componente. US2 arregla uso (labels). US3 cierra móvil.

---

## Notes

- No fusionar los dos `<form>`
- CTA naranja; verde solo WhatsApp del resumen
- Siguiente: `/speckit-implement`
