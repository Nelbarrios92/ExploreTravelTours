# Tasks: Identidad tipográfica del Hero

**Input**: Design documents from `/specs/002-hero-brand-typography/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/, quickstart.md

**Tests**: No hay tareas de tests automatizados. El spec no las pide; la constitución exige verificación manual ([quickstart.md](./quickstart.md)).

**Organization**: Tareas agrupadas por user story (US1–US3). Producto solo en raíz.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Puede ir en paralelo (otro archivo, sin depender de una tarea incompleta)
- **[Story]**: US1, US2, US3 según spec.md
- Cada tarea incluye ruta de archivo

## Path Conventions

Producto: `index.html`, `style.css`. No tocar `script.js` salvo regresión. No crear `src/`, `frontend/` ni `package.json`. Contratos: `specs/002-hero-brand-typography/contracts/hero-typography.md`, `hero-copy.md`.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Registrar Fraunces sin aplicar aún la nueva jerarquía visual

- [x] T001 [P] Ampliar el `<link>` de Google Fonts en `index.html` para incluir Fraunces (pesos 400–600) junto a Montserrat y Playfair Display, con `display=swap`, según `specs/002-hero-brand-typography/contracts/hero-typography.md`
- [x] T002 [P] Añadir `--font-display: 'Fraunces', serif` en `:root` de `style.css` sin asignarlo todavía a ningún selector de sección

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Markup semántico del bloque izquierdo; todas las historias lo usan

**⚠️ CRITICAL**: No empezar user stories hasta completar esta fase

- [x] T003 Reestructurar `.hero-content` en `index.html`: identificador `<p class="hero-brand">Explore Travel Tours</p>` (no heading); regla `<hr class="hero-brand-rule" aria-hidden="true">` (o `span` equivalente); un solo `<h1 class="hero-title">` con el copy exacto y tres `span.hero-title-line` (`Tu viaje comienza` / `con la forma de` / `moverte.`); subtítulo del contrato de movilidad; CTA “Explorar servicios” hacia `#experiences`; conservar Instagram y `.hero-footer` intactos (`specs/002-hero-brand-typography/contracts/hero-copy.md`)

**Checkpoint**: El DOM del Hero ya distingue marca vs H1; el buscador y el resto de la página siguen igual; estilos nuevos aún no cierran la jerarquía

---

## Phase 3: User Story 1 - Percibir la marca como premium y contemporánea (Priority: P1) 🎯 MVP

**Goal**: “Explore Travel Tours” se lee como eyebrow contemporáneo (Fraunces), considerable pero subordinado al H1 Montserrat; sin versales forzadas y sin agrandar solo el título viejo

**Independent Test**: En desktop, un revisor identifica el mensaje de viaje como titular y el nombre como marca; Fraunces no aparece en otras secciones. Quickstart pasos 1–4 (parcial, sin exigir aún las tres líneas perfectas)

### Implementation for User Story 1

- [x] T004 [US1] Estilar `.hero-brand` en `style.css` con `font-family: var(--font-display)`, peso 400–600, `text-transform` normal, `clamp` de presencia intermedia (~45–70% del H1 en desktop), color blanco y text-shadow coherente con el overlay (`specs/002-hero-brand-typography/contracts/hero-typography.md`)
- [x] T005 [US1] Reasignar `.hero-title` en `style.css` a `var(--font-sans)`, peso 600–700, `clamp` **mayor** que `.hero-brand` (el máximo actual ~6.5rem deja de aplicarse al nombre), `line-height` ~1.05–1.15
- [x] T006 [US1] Confirmar en `style.css` que `--font-display` no se usa fuera de `.hero-brand` y que `--font-serif` (Playfair) sigue en títulos de sección (p. ej. `.section-header h2`)

**Checkpoint**: El nombre ya no es el H1 enorme de Montserrat; tiene carácter propio y el mensaje domina

---

## Phase 4: User Story 2 - Leer una composición editorial clara en escritorio (Priority: P1)

**Goal**: Desktop editorial: marca → regla → H1 en ~tres líneas → subtítulo subordinado; bloque izquierda; foto/vehículo a la derecha; sin sobrecarga

**Independent Test**: Captura ~1280×800: tres líneas del H1, regla sobria, contenido a la izquierda, buscador flush al pie, sujeto de la foto visible. Quickstart pasos 1–5

### Implementation for User Story 2

- [x] T007 [US2] En `style.css`, a `min-width: 1024px`, hacer que `.hero-title-line` sea `display: block` (o mostrar `br.hero-title-break`) para las tres frases del contrato; mantener `.hero-content` alineado a la izquierda y `max-width` ~640px
- [x] T008 [US2] Estilar `.hero-brand-rule` en `style.css`: 1px, blanco ~0.55–0.75 opacidad, ancho ≤ identificador, márgenes rítmicos en `rem`/`clamp`, sin degradado ni sombra extra
- [x] T009 [US2] Ajustar `.hero-subtitle` en `style.css` para que quede claramente menor que el H1 (escala cercana a la actual ~1–1.5rem) y no compita con marca ni titular
- [x] T010 [US2] Verificar en `index.html` que no se añadieron iconos, bullets de beneficios ni efectos nuevos en el Hero; el CTA conserva clases existentes (`.lets-go-btn`)

**Checkpoint**: Composición desktop del brief; buscador y foto no desplazados

---

## Phase 5: User Story 3 - Conservar jerarquía y legibilidad en tablet y móvil (Priority: P2)

**Goal**: Misma jerarquía (H1 > marca > subtítulo) en 768 y 375; marca proporcional; H1 sin tres líneas forzadas si dañan la lectura

**Independent Test**: 768px y 375px: nombre 1–2 líneas, H1 refluido, contraste, sin overflow-x. Quickstart pasos 7–8

### Implementation for User Story 3

- [x] T011 [US3] En `style.css`, bajo `1024px`, anular saltos forzados de `.hero-title-line` / `br` para wrap natural del H1
- [x] T012 [US3] Ajustar `clamp` y márgenes de `.hero-brand`, `.hero-title` y `.hero-subtitle` dentro del `@media` existente (~768px / menú móvil) en `style.css` para reducción proporcional, sin `font-size` mágico de una sola resolución
- [x] T013 [US3] Comprobar que `.hero-section` en móvil sigue pudiendo crecer (`height: auto; min-height: 100vh` actual) y que el bloque de marca no tapa de forma permanente el buscador ni provoca `overflow-x` en `body`

**Checkpoint**: Desktop US2 intacto; tablet/móvil legibles

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Contraste, regresiones y validación del quickstart

- [x] T014 Si el texto nuevo pierde contraste, ajustar solo `.hero-overlay` o text-shadow del bloque izquierdo en `style.css` (no rediseñar foto ni `.swoosh-path`)
- [ ] T015 Recorrer [quickstart.md](./quickstart.md) en 375 / 768 / 1280: un `h1`, copy del contrato, navbar/WhatsApp/Instagram, catálogo Playfair, buscador flush
- [x] T016 Confirmar que `script.js` no requirió cambios; si el markup rompió un selector, corregir el mínimo en `script.js` sin nueva lógica

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: Sin dependencias; T001 y T002 en paralelo
- **Foundational (Phase 2)**: Depende de Setup — BLOQUEA user stories
- **US1 (Phase 3)**: Depende de T003
- **US2 (Phase 4)**: Depende de US1 (mismos selectores; la composición asume tamaños de marca/H1)
- **US3 (Phase 5)**: Depende de US2 (salta sobre la composición desktop)
- **Polish**: Depende de US1–US3 deseadas

### User Story Dependencies

- **User Story 1 (P1)**: Tras Phase 2. MVP de percepción de marca
- **User Story 2 (P1)**: Tras US1. Integra regla y tres líneas
- **User Story 3 (P2)**: Tras US2. Responsive sobre la misma jerarquía

### Within Each User Story

- Markup fundacional antes de CSS de historia
- Tokens de fuente antes de aplicar `.hero-brand`
- Desktop (US2) antes de anular saltos en móvil (US3)

### Parallel Opportunities

- T001 (`index.html` fonts) y T002 (`style.css` token) en paralelo
- Tras T003, el trabajo es secuencial en `style.css` (mismo archivo): no paralelizar T004–T013 entre sí
- T010 es verificación de markup; puede hacerse en cuanto T003+T007 existan, no en paralelo con ediciones conflictivas de `index.html`

---

## Parallel Example: Setup

```bash
# Distintos archivos:
Task: "Ampliar Google Fonts (Fraunces) en index.html"
Task: "Añadir --font-display en style.css :root"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Phase 1: Fraunces + token
2. Phase 2: Markup semántico y copy
3. Phase 3: Estilos de marca vs H1
4. **STOP**: Validar percepción (nombre contemporáneo, H1 dominante)
5. Demo al cliente si basta para SC-001

### Incremental Delivery

1. Setup + Foundational → DOM correcto
2. US1 → identidad tipográfica (MVP)
3. US2 → composición editorial desktop
4. US3 → tablet/móvil
5. Polish → quickstart completo

### Parallel Team Strategy

Un solo implementador: `index.html` / `style.css` no se prestan a dos personas a la vez. Secuencia T001–T016.

---

## Notes

- [P] solo cuando el archivo no choca
- Sin suite de tests; cierre = quickstart en navegador
- No rediseñar buscador, catálogo, FAQ ni adornos
- Constitución v1.1.0: `--font-display` solo en el identificador
- Siguiente: `/speckit-implement`
