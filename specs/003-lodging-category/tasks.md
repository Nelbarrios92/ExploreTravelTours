# Tasks: Categoría de alojamientos en Experiencias

**Input**: Design documents from `/specs/003-lodging-category/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No hay tareas de tests automatizados. Verificación manual ([quickstart.md](./quickstart.md)).

**Organization**: Tareas por user story (US1–US3). Producto en la raíz.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Puede ir en paralelo (otro archivo)
- **[Story]**: US1, US2, US3
- Cada tarea incluye ruta de archivo

## Path Conventions

`index.html`, `style.css`, `script.js`, `assets/`. No crear `src/` ni `package.json`. Contrato: `specs/003-lodging-category/contracts/catalog-alojamientos.md`. Fotos ya en repo: `assets/apartamento-laguito.jpeg`, `assets/apartamento-torices.jpeg`.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Confirmar assets reales (no fotos de tours)

- [x] T001 Verificar que `assets/apartamento-laguito.jpeg` y `assets/apartamento-torices.jpeg` existen y no son copias de fotos de city tours/destinos; usar esas rutas en las cards (data-model)

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Chip de categoría en el DOM para que el filtro genérico tenga un valor nuevo

**⚠️ CRITICAL**: Completar antes de las user stories de cards

- [x] T002 Añadir el chip `<button class="filter-chip" data-filter="alojamientos">Alojamientos</button>` al final del grupo `.catalog-filters` en `index.html` (`aria-pressed="false"`), según `specs/003-lodging-category/contracts/catalog-alojamientos.md`

**Checkpoint**: El chip existe; aún no hay cards de alojamiento (no publicar así a producción)

---

## Phase 3: User Story 1 - Filtrar alojamientos en el catálogo (Priority: P1) 🎯 MVP

**Goal**: Chip Alojamientos muestra exactamente Laguito y Torices, mismo estilo de card; Todas incluye esas dos

**Independent Test**: Quickstart pasos 1–5 (filtros). Sin depender de WhatsApp más allá de que el botón exista como en las demás cards

### Implementation for User Story 1

- [x] T003 [US1] Añadir `article.service-card` `data-experience-id="apartamento-laguito"` `data-category="alojamientos"` en `#catalog-grid` de `index.html`: imagen `assets/apartamento-laguito.jpeg`, `alt` descriptivo (apartamento El Laguito), `h3` y párrafo del data-model, `fade-in-scroll`
- [x] T004 [US1] Añadir la card `apartamento-torices` en `index.html` con `assets/apartamento-torices.jpeg`, `alt` (apartamento Torices), copy autorizado (2 hab., 5 personas, equipamiento), misma plantilla que T003
- [x] T005 [US1] Actualizar el subtítulo de `.section-header` en `#experiences` (`index.html`) para mencionar alojamientos junto a city tours, traslados, barcos e islas y destinos; conservar el `h2`
- [x] T006 [US1] Si los seis chips se desbordan, ajustar wrap/gap de `.catalog-filters` en `style.css` sin rediseñar `.service-card` ni `.filter-chip` de marca; si ya envuelven bien, no cambiar CSS

**Checkpoint**: Filtro Alojamientos = 2 cards; otras categorías sin esas cards; Todas = 13

---

## Phase 4: User Story 2 - Consultar un alojamiento por WhatsApp (Priority: P1)

**Goal**: CTA de cada apartamento abre WhatsApp con el título de esa oferta

**Independent Test**: Quickstart paso 6

### Implementation for User Story 2

- [x] T007 [US2] En las dos cards de `index.html`, usar `a.card-btn` con `data-wa-title` igual al `h3` (`Apartamento Laguito` / `Apartamento Torices`), `target="_blank"` `rel="noopener noreferrer"` e icono WhatsApp como el resto del catálogo (el `href` lo pinta `initCatalog` en `script.js`)
- [x] T008 [US2] Confirmar en `script.js` que no hace falta código nuevo: el `forEach` de `.card-btn[data-wa-title]` cubre las cards nuevas; solo tocar `script.js` si un selector se rompe

**Checkpoint**: Mensaje `Hola, me interesa reservar: {title}.` para ambos inmuebles; sin formulario ni precios

---

## Phase 5: User Story 3 - Reconocer el catálogo unificado (Priority: P2)

**Goal**: Filtros y ofertas 001 intactos; sin menú “Apartamentos”

**Independent Test**: Quickstart pasos 5 y 7

### Implementation for User Story 3

- [x] T009 [US3] Verificar en `index.html` que nav no añade ítem Alojamientos; `#destinations` sigue y no activa `alojamientos`
- [x] T010 [US3] Verificar que las 11 cards previas conservan `data-experience-id` / `data-category` originales en `index.html`

**Checkpoint**: Catálogo unificado; Hero/FAQ/nav sin rediseño

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Quickstart y regresiones

- [x] T011 Recorrer [quickstart.md](./quickstart.md) en 375 / 768 / 1280: chips, 2+11 cards, WhatsApp, menú móvil
- [x] T012 Confirmar que `relatedSuggestions` en `script.js` no se modificó (apartamentos fuera del buscador del Hero)

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup**: T001 (fotos `.jpeg` ya en repo)
- **Foundational**: T002 chip (puede ir en el mismo edit que T003–T004, pero el chip no debe quedar sin cards al cerrar la feature)
- **US1**: T003–T006 tras T001–T002
- **US2**: T007–T008 tras markup de cards
- **US3**: T009–T010 puede solaparse con revisión de `index.html` al final de US1
- **Polish**: T011–T012 al cierre

### User Story Dependencies

- **US1 (P1)**: MVP — chip + 2 cards + intro
- **US2 (P1)**: CTA; en la práctica el markup de T003/T004 ya incluye el botón; T007 es checklist de atributos
- **US3 (P2)**: Conservación del catálogo 001

### Parallel Opportunities

- Poco paralelo: casi todo es `index.html`
- T006 (`style.css`) puede ir en paralelo a T007 si el markup de cards ya está
- T001 es verificación, no bloquea el markup si las rutas `.jpeg` son las acordadas

---

## Parallel Example: Setup

```bash
# Ya cumplido en el workspace:
# assets/apartamento-laguito.jpeg
# assets/apartamento-torices.jpeg
```

---

## Implementation Strategy

### MVP First (User Story 1)

1. T001–T002
2. T003–T005 (y T006 si hace falta)
3. Validar filtros
4. T007–T008 WhatsApp
5. Polish quickstart

### Incremental Delivery

Chip + cards (US1) ya es demostrable. US2 es el mismo CTA del catálogo. US3 es no-regresión.

---

## Notes

- IDs: `apartamento-laguito`, `apartamento-torices`; categoría `alojamientos`
- Copy: no inventar precios ni un tercer inmueble
- Siguiente: `/speckit-implement`
