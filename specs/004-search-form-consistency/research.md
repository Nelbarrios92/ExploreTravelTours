# Research: Consistencia UX del buscador

## 1. Un form vs dos forms

**Decision**: Conservar `#search-form-transporte` y `#search-form-hourly` y `setMode` actual (`hidden` / `is-active`).

**Rationale**: `initSearch` valida y pinta cotización por formulario. Fusionar DOM reescribe submit y origen=destino. El brief pide no tocar negocio.

**Alternatives considered**: Un solo form y campos `hidden` por modo — más limpio visualmente a costa de regresiones. Rechazado para esta iteración.

## 2. Etiquetas: flotantes vs estáticas

**Decision**: Abandonar el patrón flotante (`.field > span` absoluto). Markup: `<span class="field-label">` (o `<label>`) **antes** del control; el control sin `placeholder=" "` trampa.

**Rationale**: Spec FR-006. El flotante no cubre `<select>` ni date/time nativos (`:placeholder-shown`); Duración + “Selecciona” se solapan.

**Alternatives considered**: Arreglar flotante solo en select (`:valid` / clase `.is-filled`) — frágil y desigual vs text inputs.

## 3. CTA en la fila

**Decision**: Mover `.search-submit` **dentro** de `.search-fields` como último ítem. Grid desktop `repeat(5, minmax(0, 1fr)) auto`; el botón `align-self: end` a la altura del input (no de la etiqueta).

**Rationale**: Hoy el submit es hermano debajo; `width: 100%` en &lt;1280 y `width: auto` solo en el media 1280 — y aun así no está en el grid, así que “salta” o no alinea. Por horas y Transporte compartirán la misma plantilla de 6 celdas.

**Alternatives considered**: `position` absoluto del botón — se rompe con errores e ida-vuelta.

## 4. Franja Solo ida / Ida y vuelta (clarificación B)

**Decision**: Bloque `.search-chrome` con `min-height` igual en **ambos** forms. Transporte: radios existentes (`name="trip-type"`). Por horas: el mismo contenedor vacío (`aria-hidden="true"`).

**Rationale**: Spec clarificada. Evita salto de altura al cambiar de tab. No hay radio desactivado en Por horas.

**Alternatives considered**: Radios junto a tabs (opción C) — mezcla dos grupos de control. Fila solo en Transporte (A) — rechazada.

## 5. Fecha de regreso

**Decision**: Seguir con `.field-return` + `hidden` y JS actual. En grid, cuando visible, `grid-column: 1 / -2` (segunda fila) para no empujar el CTA fuera. El CTA permanece en la primera fila (`grid-row: 1` en desktop).

**Rationale**: Spec 001 + 004: segunda fila compacta; no seis+ controles en una línea.

**Alternatives considered**: Reservar siempre la celda de regreso vacía — más estable, más hueco; no pedido.

## 6. Tabs

**Decision**: `flex: 1 1 0`; `min-height` fijo; inactivo `background` gris claro, `color` pizarra, borde `#e2e8f0`; activo `--brand-blue` texto blanco. Sin `flex-grow` distinto por contenido.

**Rationale**: FR-005. Hoy el inactivo usa color `--brand-blue` sobre gris y compite con el activo.

## 7. Responsive

**Decision**:

| Ancho | `.search-fields` |
|-------|------------------|
| &lt;768px | 1 columna; submit `width: 100%` última fila |
| 768–1023 | 2 columnas; submit full width al final |
| 1024–1279 | 3 columnas; submit al final de la última fila o full width si no cabe |
| ≥1280 | 5 campos + CTA en una fila (solo ida / por horas) |

**Rationale**: FR-010. Evitar `repeat(5, 1fr)` demasiado pronto (overflow).

## 8. Sombras / superficie

**Decision**: Conservar panel blanco semitransparente; **reducir** `box-shadow` exagerada del pie (`0 -8px 40px`) a una sombra más corta y suave. No nuevos colores.

**Rationale**: Brief: evitar sombras exageradas; premium/limpio.

## 9. script.js

**Decision**: No cambiar mensajes, `buildWhatsAppUrl`, `relatedSuggestions` ni reglas de fecha. Solo tocar JS si `.field-return` deja de ser descendiente del form transporte.

**Rationale**: FR-013.
