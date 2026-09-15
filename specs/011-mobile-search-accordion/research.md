# Research: Acordeón del buscador en móvil

## Markup: botón + wrapper, no `<details>`

**Decision**: Un `button type="button"` (cabecera) y un wrapper `.search-composer` (tabs + formularios + errores). Clase `#hero-search.is-collapsed` para cerrado. MUST NOT reutilizar el `<details>` del FAQ.

**Rationale**: El resumen 007 es hermano; hay que ocultar la cabecera en `.is-quoted`. `<details>` no cubre bien “cerrado al cargar / abierto en Modificar / desaparece al cotizar” sin pelear con `hidden` del quote.

**Alternatives considered**: `<details>` nativo (FAQ ya lo usa; choca con 007). Solo CSS `:focus-within` (no cierra a propósito; no cumple cabecera fija).

## Breakpoint y escritorio

**Decision**: Acordeón solo en **`max-width: 767px`**, igual que 010. A **≥768px** la cabecera `display: none` y el compositor siempre visible; `is-collapsed` no oculta nada. Sin `matchMedia` obligatorio: el CSS ignora el colapso en ancho.

**Rationale**: Spec: tablet/escritorio en fila no usan acordeón. 010 ya cortó en 767.

**Alternatives considered**: JS al resize para quitar la clase (redundante si CSS manda).

## Estado inicial y Modificar

**Decision**: HTML inicial con `is-collapsed` y `aria-expanded="false"`. `renderQuote` añade `.is-quoted` (007) y CSS oculta cabecera + compositor. `hideQuote` (Modificar) quita `.is-quoted` y **`is-collapsed`** (abre). Toggle solo conmuta `is-collapsed` / `aria-expanded` si **no** está cotizado.

**Rationale**: FR-002 / FR-005. Los valores del form viven en el DOM (FR-006) aunque el cuerpo esté `display: none`.

**Alternatives considered**: `sessionStorage` (viola constitución I). Cerrar tras error (viola spec).

## Señal de estado

**Decision**: Chevron Unicons (`uil-angle-down` / rotar 180° cuando abierto) junto al texto fijo **Pedir cotización**. Estilo de **barra** (no naranja 50px) para no confundir con `.search-submit`.

**Rationale**: Clarificación: mismo texto + señal; el naranja envía.

**Alternatives considered**: Cambiar a “Cerrar” (rechazado). Cabecera naranja (parece submit).

## Animación

**Decision**: Abrir/cerrar **inmediato** (`display` / clase). MUST NOT librería ni `max-height` largo.

**Rationale**: Clarificación deferred; YAGNI; FAQ ya es instantáneo con details.

**Alternatives considered**: Transición de altura (frágil con ida-vuelta).
